# ES6, the unnecessary standard?

About necessity of standardizing the current ES6, accompanied by whining about the ES6 modules proposal.

With the inflammatory (some would say flamebait) headline out of the way — I used to be excited about ES6, but the excitement has been wearing thin lately, especially now that the spec is starting to stabilize.

#### **Reason 1: too late?**

ES6 is not in final form in several non-evergreen browsers (including the still popular IE9). You will not be able to use direct on-the-browser ES6 for years, and since you will need to use transpiler anyway, you can get more functionality using another transpiler like TypeScript, AtScript or JSX (for FB’s Flow support)

#### **Reason 2: too little?**

No types. By the time ES6 is acceptable to be used without transpiler, we will have a widespread agreement on how types should work, and provisional transpilers for ES7. People currently transpiling from ES6 (read: people ahead of the curve and willing to use transpilers in the first place) will be updating to the ES7 transpilers, leaving the newly stabilized ES6 browser support in the dust.

#### **Reason 3: modules**

(TLDR: I don’t like the idea of shoving asynchronous loading in a programming language spec, browserify seems cool.)

JS needs support for more modular application development. The mundane reason for this is that developers generally like to put features into different namespaces, files and directories — for this, **browserify** already exists and provides an (apparently) rather elegant solution. Functions get a namespace, developers get control what is exported and projects are nicely decomposed into separate files and directories.

Using Browserify means you need a build step to concatenate your Javascript. If you are doing a production build, you will be concatenating your Javascript anyway.

[ES6 modules](http://www.2ality.com/2014/09/es6-modules-final.html), on the other hand, leave the domain of pure programming language design, and in addition to static representation specify a “module loader api” to asynchronously fetch the modules. This is not unlike what RequireJS is doing. However, it’s unclear whether asynchronous module loading is widely needed — it only helps gigantic applications where you want to split the application in separate parts that are lazily loaded while the initial phase of application is “booting up”, AND your concatenation logic is sophisticated enough to do the splitting.

If you really are building application big enough to need lazy loading, you’d rather want explicit control to state when another big part of application gets loaded, and this responsibility resides more naturally in your framework of choice. E.g. in a fictional future version of Angular that supported lazy loading, this could be done by router that ‘resolves’ the lazily loaded part before instantiating a view, relevant controllers and services. Or you could just use RequireJS infrastructure for parts of your application.

Deployment of Javascript is complicated enough as it is. An OS runtime may naturally defer reading a DLL from disk before a function in that DLL gets referenced, but it would be very unorthodox to specify a logic how it should start fetching said DLLs from network transparently. If you need that, you write the networking code and invoke dynamic library loader explicitly (dlopen(), System.load(), …)

Update: I was informed by Allen Wirfs-Brock that module loader pipeline has been moved out of ES6 to separate specification during October. For reference, see [1](https://github.com/tc39/tc39-notes/blob/master/es6/2014-09/sept-25.md#loader-pipeline), [2](https://github.com/tc39/tc39-notes/blob/master/es6/2014-11/nov-18.md) and [3](http://wiki.ecmascript.org/doku.php?id=harmony:specification_drafts#october_14_2014_draft_rev_28).

#### **ES6: the good parts**

ES6 has lots of uncontroversial good parts — fat arrow and destructuring to name a few. Yes, this is a short chapter, but you already know about all the good stuff.

#### **What should happen next?**

*   Finalize a stripped down standard as ES6 quickly. This would include only the simplest things in the standard proposal, but it most definitely has to include fat arrow ;-).
*   Switch gears and start focusing on ES7, with type annotations, async/await and other features that warrant a new full-blown standard. Do not let the current lackluster standard proposal become the new stagnation point for the web development for years to come.
*   Specify “lightweight” ES6.x “standards” that transpilers will use as the specification. Don’t even attempt to build in-browser support for these, just let people on the cutting edge keep using their transpiler of choice.

#### Why did you write this drivel?

The quality standard for webdev blogging has been very low lately, so why not? More seriously, I was wondering why there is very little criticism of ES6 out there, and in absence of popular bandwagon to jump on, I took a jab. Through the process of writing, I almost ended up with “heck, I want the full ES6 anyway”, but not quite.

Update: I’m happy that this has sparked some discussion on twitter and elsewhere, e.g. “[ES6, a necessary response](https://medium.com/@webprolific/es6-a-necessary-response-3eafbdfed919)” by Lars Kappert.

By [Ville M. Vainio](https://medium.com/@vivainio) on [November 26, 2014](https://medium.com/p/7158b8c344a0).

[Canonical link](https://medium.com/@vivainio/es6-the-unnecessary-standard-7158b8c344a0)

Exported from [Medium](https://medium.com) on July 1, 2019.