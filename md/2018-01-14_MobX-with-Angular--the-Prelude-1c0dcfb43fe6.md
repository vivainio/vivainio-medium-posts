# MobX with Angular: the Prelude

This is Part 1 of the in-progress article series. Part 2 with more advanced concepts is also available.

![Conan experimenting with NGRX](https://cdn-images-1.medium.com/max/800/1*A9D1M7Uv3FprLXa3QAHN3A.jpeg)
Conan experimenting with NGRX

This is Part 1 of the in-progress article series. [Part 2](https://medium.com/@vivainio/mobx-with-angular-part-2-patterns-perks-and-gotchas-37e2a393e0eb) with more advanced concepts is also available.

I hit a degree of analysis paralysis on writing an “all in one” blog post about using MobX on Angular (2+) at Basware, but it ended up being a bit heavy reading. Instead of that I’m doing a series of shorter, hopefully harder-hitting posts. (_Narrator: this one ended up being neither short, nor hard-hitting_)

Aim is not to teach you MobX, but rather to generate some appetite for the productivity wins you can reach with it — and maybe help you debug some of your personal misconceptions faster (I also had some in the beginning).

#### The Store

MobX is not really built around “Stores”. You can have your state spread over however widely you want (e.g. dozens of different Angular services or ES6 classes if you are so inclined). Simple state is always easier to track, but there is no need to cargo cult a single God-object to hold everything. The mechanics of MobX will work regardless of how you split your state.

#### Observables

There is probably a small subset of state that actually needs to change. These are marked by @observable decorator, and they are usually primitives, arrays, objects and ES6 Maps. Note that, for better or worse, you must use ES6 Maps instead of objects to represent dictionaries (as MobX can’t detect keys being added to objects). “Changing the state” means writing to these fields (mutating, reassigning, whatever).

#### Computed properties

@computed decorator marks an ES6 property getter that uses some of the observables defined above to calculate derivable parts of the state. If you have observable’s called “foo”, “bar” and “baz”, you can use computed properties to produce e.g. { foo, bar } object if both are defined, or null otherwise. You need that new unique object to trigger OnPush change detection, among other things. If “baz” property changed, your computed property comfortably sits as the old value, without unwanted triggers of OnPush change detection.

#### Autorun

This is where the actual magic happens.

Autorun is a function that:

1.  You probably have in your _ngOnInit_(). Class constructor is too early (e.g. Angular ChangeDetectorRef is not available there).
2.  Is run once in the beginning. MobX records what properties (observable’s and computed’s) from MobX stores it accesses, and remembers its dependencies.
3.  Is run again when any of your dependencies change.
4.  Remains “hot” until you unsubscribe from it. autorun() returns a callable disposer that you will call in your _ngOnDestroy_ for the component.

What’s in your autorun() in a typical Angular application? You can have code that:

*   Copies values from store to your local component variables that are used from the template.
*   Runs patchValue() on a Reactive Form within the component.
*   Does some last minute tuneups for the data to make it easier to access from the template.
*   Calls ChangeDetectorRef.detectChanges() to force Angular to check changes in case you are within a ChangeDetectionStrategy.OnPush component (and didn’t trigger any Input to change).

A single component can have many autorun() blocks. The smaller and more granular the blocks, the more specific you can be about how often they fire.

Autoruns are not limited to components though! Services can have their own autorun’s observing the state, possibly initiating HTTP requests when interesting data is available in stores, and commit interesting responses back to the stores when they return.

#### Don’t you need a new library for this?

Not really. Core MobX works fine with Angular, with the scheme mentioned above.

We have a few convenience functions to help with disposing autoruns, like this:

You call startObserving(this, () => …) in _ngOnInit_(), and stopObserving(this) in _ngOnDestroy_. There will be a new blog post with some more productized helpers later on.

There is also [https://github.com/mobxjs/mobx-angular](https://github.com/mobxjs/mobx-angular) project that detaches a component completely from normal Angular change detection. It can work for your needs, but I posit that you may not need it, and operating directly with the (already simple) core MobX API can help when debugging problems in your own logic (e.g. “why did this not change? I better set a breakpoint in my autorun!”)

#### How about Rx Observables?

We started out by piping stuff from MobX as Rx observables to our components, as described here: [https://netbasal.com/managing-state-in-angular-with-mobx-51191803e14f](https://netbasal.com/managing-state-in-angular-with-mobx-51191803e14f)

Still, I was left wondering “y tho”. If you are just using autorun(), you avoid that unnecessary wrapper, and remove need to use async pipes. You just assign new immutable references (that you got from @computed getters or autoruns) to your component variables and their change detectors kick in.

MobX itself, despite its simplicity and ease of use, is a sophisticated reactive system on its own right. It just gives you the same power you get with Rx with a cheaper price tag (no need to do combineLatest(), switchMap() etc. to express a fundamentally simple computation).

#### How about NGRX?

Bright eyed and bushy tailed, we started out with NGRX; it has a very good industry buy-in, is based on React community darling Redux, and is being pushed by a cadre of Angular community hotshots. So it’s going to be the default conservative choice, right? Right?

It was a traumatizing experience for me personally. There was **one directory with 5 files** to represent something that was 5 lines with MobX — basically an array.

I wanted to give it a week to sink in, but I think I managed 2 days of zero productivity before calling off the experiment. Now, I have done some horrible things in my past (Symbian C++, raw GObject macro programming, 4GL’s, Perl…), but it’s 2018, I’m not getting any younger, and frontend development should be a bit fun and playful — experimenting with different state schemas and so on should be natural, energizing part of the work.

#### Call to action

So a degree of “Question authority” is in order here. If we see MobX as the better mousetrap for Angular, we should drive that point more consistently. We should start writing developer tools that illustrate the data flow on the screen. Barring everything else, we can at least make some noise in the blogs.

By [Ville M. Vainio](https://medium.com/@vivainio) on [January 14, 2018](https://medium.com/p/1c0dcfb43fe6).

[Canonical link](https://medium.com/@vivainio/mobx-with-angular-the-prelude-1c0dcfb43fe6)

Exported from [Medium](https://medium.com) on July 1, 2019.