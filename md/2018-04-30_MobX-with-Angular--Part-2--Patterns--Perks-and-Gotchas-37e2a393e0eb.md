# MobX with Angular, Part 2: Patterns, Perks and Gotchas

This is the second installation of the critically acclaimed “MobX with Angular” series. If you came here googling for “ngrx alternatives…

![State management shouldn’t be rocket science](https://cdn-images-1.medium.com/max/800/1*NxzzwQj3ffG0jugGdFrP2w.jpeg)
State management shouldn’t be rocket science

This is the second installation of the critically acclaimed “MobX with Angular” series. If you came here googling for “ngrx alternatives sweet jesus make it stop”, you are in the right place. You probably want to read [part 1](https://medium.com/@vivainio/mobx-with-angular-the-prelude-1c0dcfb43fe6) for the basics (or any generic React-oriented MobX tutorial if you don’t particularly like my writing).

On to the non-basics. We are creating a big Angular application with a largish, geographically distributed team at [Basware](https://www.basware.com/), and have established this as a pretty workable design (for the purposes of discussion I’m using the classical Blog Post feature as the example):

*   The single source of truth is the Store, _posts.store.ts_ (class _PostsStore_). It contains the @observable properties, and all the @action’s that modify the state.
*   There are many Stores. You could have _AuthorsStore_, _SettingsStore_ etc.
*   Components don’t access (i.e. inject) the Store directly. Instead, they use a facade called _PostsService_, in _posts.service.ts_.
*   Http requests are done by _PostsApiService_, in _posts.api.ts_. This is the only place that knows what url’s are used. This is also a good place to put a breakpoint when wondering why on earth that one request was sent three times.

#### The Facade

_PostsService_ is responsible for exposing parts of the Store to the components. That is, it’s what your _post-reader.component.ts_ injects to do stuff.

If there is asynchronous http work to do, _PostsService_ calls to _posts.api.ts_ service (_PostsApiService_) that sends the request. _PostsService_ then captures the response and updates the state accordingly (usually calling an action in Store). Here’s an example flow:

1.  User clicks a post. Component calls _postsService.documentChanged(id)_ which is a hint that we want the data for that document.
2.  _PostService_ notices that we don’t have that document in store. It triggers the fetch knowing it’s needed soon.
3.  _PostsReaderComponent_ is observing _postService.getPost(id)_. It keeps returning _undefined_ (or _null_ if you are so inclined) for now. A busy spinner is spinning.
4.  _PostService_ finally receives the post content. It calls the action _store.setPost(id, { content: “blah blah”})_
5.  The observer of _getPost(id)_ is woken up now that the data changed, and it can place the content in a component instance variable. This dismisses the spinner and reveals the glorious post content.

It’s worth mentioning that MobX itself has support for async workflows, through [async actions and flow()](https://mobx.js.org/best/actions.html). We are not using those because

*   we want to stick with relatively tried-and-true async patterns familiar from AngularJS 1.x days
*   generators don’t work great (read: hardly at all) with current crop of debuggers and source maps
*   async is not exactly rocket science. Every action on the store is a dumb, instant “commit”.

#### createTransformer()

You noticed the _postService.getPost(id)_ above. It will probably look for the content in an observable _Map<string, PostData>_. You can call it in autorun body just fine, but there is actually a better and faster way.

Usually, MobX recommends doing most calculations in _@computed_ properties instead of complex _autorun_ bodies when you can:

*   It’s faster. When a computed property is observed, it is “hot”. That is, when the data or other computed properties are modified, the computed values are pushed out and memoized. Just calling the computed property will get you the memoized value. If there are many components observing the same data in autoruns, they will be recalculated every time the data changes. With computed properties, the calculation is run only once. This means you can safely call them without worrying about performance under the hood.
*   They are a cleaner programming pattern. When you see something is computed, you know it’s just a pure projection of underlying state. And, you know you should be observing that state in the top level autorun() somewhere. Non-computed things could be doing anything else. You’ll probably implement your state by having a whole tree of projections refining and improving the state to fit your particular consumption needs.

Now that I convinced you of their merits, here comes the Gotcha 1: **you can’t pass arguments to computed functions**. They are just getters with no arguments. You could just have “_currentPostId_” in store, and give data for that current post in the computed getters. But, this won’t work if you have multiple posts being observed at the same time (say, you have a two pane post reader showing different posts at the same time).

This is where [createTransformer() in mobx-utils](https://mobx.js.org/refguide/create-transformer.html) steps in (if you understood none of the official description, read on). Here we create a _getPostAndAuthorData_ (in _PostsService_ class body) that reads stuff from two different transformers (projections):

The call to _getPostAndAuthorData_() discovers the internal computation by looking it up by the _postId_. You can only pass one primitive argument to the transformation, but I know that you, Dear Reader, will usually be using a string _documentId_ or somesuch. If you would need something more complex, eat it up and use _autorun_() instead.

#### Component code

In the end, you’ve got to be observing the data in autorun, otherwise it’ll all be for naught. For our application, we have made a utility to

1.  Create a list of autoruns.
2.  Dispose them in ngOnDestroy().

It’s used like this:

The strings in there are names of the observables, so [mobx-devtools](https://chrome.google.com/webstore/detail/mobx-developer-tools/pfgnfdagidkfgccljigdamigbcnndkod?hl=en) Chrome plugin (that also works with Angular) shows them nicely. You can grab the utilities (_startObservers_, _addComponentDisposer_ and _stopObserving_) from [Github](https://github.com/vivainio/angularpack/blob/master/src/mobtool.ts). The first argument to _startObservers_() is optional; if you pass the component _ChangeDetectorRef_ there, triggering any of the listed observers will also run change detection on that component. This is usually needed for OnPush components.

Why not shove everything in one autorun? The basic idea is to segregate them so that only the part that depends on a particular change is run when needed.

Natural place to “start observing” is _ngOnInit_(), since that is only run once per component, and the components input attributes have settled by the time it runs. You can delay the initialization of observables by MobX _when()_ function that retuns a promise that resolves when the observed expression returns true:

#### There is no such thing as free lunch

With all this magic and rainbows, there’s got to be a price to pay, right? Well, there is, and sooner you know the better:

*   Decorators like @observable and @computed can’t currently (as of Angular 5) be used in components because AoT compiler chokes up on them. _createTransformer_(), on the other hand, can be used, and can be handy for some marginal refinement you want to do at the edges. MobX 4 provides an alternative syntax using _declare(),_ which won’t trigger this problem.
*   The observable data in stores is injected with MobX specific metadata, and the attributes of objects are transformed to getters/setters. This means you need to click individual properties in the debugger to investigate them.
*   Observable arrays look bad in the debugger. You will see hundreds of items per array, and need to click through the items to even see the length. Upcoming MobX 5 will fix this (by using ES6 proxies).
*   Some JavaScript libraries can when fail dealing with observable data structures. E.g. lodash _\_.flatMap_ (which is lodash version of _smooshMap()_) just fails to deliver with an observable array. To be fair, that’s the only bad lodash function that I know of, so no need to throw out lodash quite yet.

The last three problems above can be avoided by using toJS() in your computeds/transformers/autoruns — so you won’t see the guts of observable data structures at the edges. You can also log stuff to console through toJS():

All that being said, the debugger experience with MobX is very good. If you set a breakpoint in autorun or computed property, you see precisely what triggered the change from the call stack — and the call stack fits on the screen, as opposed to anything involving RxJS observables.

#### Should you still be using RxJS?

A good rule of thumb is: not as much as you did.

*   For dumb components that don’t want to take dependency to any kind of store, pass immutable objects as inputs, and reassign the value to trigger component update (for OnPush components).
*   Sometimes you have scenarios where component needs notification for events (as opposed to changing state as pure function of data in store — something you should do most of the time). Creating a _BehaviorSubject<SomeSpecialEvent>_ in a service provided at component level is fine for that. The alternative of passing _@Output_ events through every level can get cumbersome. Real life example: we are broadcasting events from ag-grid through a _BehaviorSubject_ for the components above.
*   Methods in your http api services (e.g. _PostsApiService_) usually start the _HttpClient_ observable and _map()_ it a bit to mungle the data. If the logic gets complex enough to not be readily readable using RxJS (e.g. once you go beyond trivial _map()_), you shouldn’t be shy to run _.toPromise()_ on the observable and use async/await. Your pull request reviewers will thank you for it.

By [Ville M. Vainio](https://medium.com/@vivainio) on [April 30, 2018](https://medium.com/p/37e2a393e0eb).

[Canonical link](https://medium.com/@vivainio/mobx-with-angular-part-2-patterns-perks-and-gotchas-37e2a393e0eb)

Exported from [Medium](https://medium.com) on July 1, 2019.