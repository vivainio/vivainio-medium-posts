# AngularConnect 2016 retrospective

I went to AngularConnect 2016 (thank to my employer Basware for sponsoring the trip), and am writing up some takeaways now that I still…

![](https://cdn-images-1.medium.com/max/800/1*jeZF8j0yQRGZf9mu2i7TSg.jpeg)

I went to AngularConnect 2016 (thank to my employer [Basware](http://www.basware.com/about-us/careers) for sponsoring the trip), and am writing up some takeaways now that I still remember (something about) them, from the topic-specific sessions I attended.

### “Mini workshop: New Data Architecture” by Gerard Sans

Recap of the basics, followed by tips on integrating Redux to an ng2 app. Fun detail: friendly reference to Redux as a “snob architecture” (immutable state), which rings true to some folks. GraphQL queries were also demoed.

### “The Angular 2 Compiler” by Tobias Bosch

About the AoT compiler. Apparently an occasional internal nickname for the compiler was “Tobiler”, due to Tobias’ big influence on it. Tobias walked through 3 iterations on how the compiler was made incrementally better performing. The talk also included a JS performance tip on benefiting from “hidden classes” when a variable always has the same object (as in the final version of the AoT compiler).

Tobias seemed quite happy to showcase his baby (= compiler) in the talk.

### “Building Progressive Web Apps and Hybrid Apps with Ionic” by Adam Bradley and Brandy Carney

Ionic is often understood as a framework for making native apps on Phonegap. Adam and Brandy demoed how easy it is to turn such an app to a progressive web app instead, switching to offline mode in chrome. Benefits of PWA’s over native apps were highlighted (search engine discovery, offline etc).

PWA’s could be an advantage for Ionic over React Native / NativeScript, so it was an interesting talk to catch.

### “Redux with AngularJS” by Pavithra Kodmad

The only Angular 1 talk I watched (which is a bit of a shame, would have wanted to see Pete & the guys gloating about the good job they did with 1.5). Pavithra inherited an Angular 1 app that had grown messy, and wanted to clean it up with Redux. She showed how to integrate Redux using ng-redux project, how store changes were automatically applied in $scope etc.

### “Optimizing Angular 2 Apps” by Martin Probst

Aka “the revenge of Closure Compiler” (ok, Martin didn’t actually use that term). Martin used to be known as “guy that hates code” at Google due to his obsession with deleting and optimizing away unnecessary code. Showed a handy tool to analyze where the bloat comes in your application binary ([source-map-explorer](https://www.npmjs.com/package/source-map-explorer)). Safe optimization strategies (like tree shaking) were described.

The really intriguing stuff, though, was the possibly upcoming ability to do property name shortening during minification. Closure Compiler can do that if you have sufficient type info (in JSDoc type annotations, generated with [tsickle](https://github.com/angular/tsickle) tool from typescript source code). This is still a bit of a dangerous endeavour, but hopefully they can make it safer. This is an upcoming nice bonus if you are flying with TS (or have JSDoc annotated libs). Maybe time to also reconsider using Closure as your go-to minifier.

There was some overlapping themes with this and with Tobias’ talk, but you want to watch both from the web to get the full picture.

### “Why I am betting my future on Angular 2” by Shai Reznik

Shai did some of his usual standup comedy’ish stuff, but ended up with a serious twist on why he is betting on Angular 2 (community stuff etc).

### Tuesday evening party

![](https://cdn-images-1.medium.com/max/800/1*gp5jrJ2GRmm4C-22WIxi_A.jpeg)

80’s theme disco (Human League ”Don’t you want me”, that kind of stuff). People enjoyed their time goofing around with costumes, throwing Frisbee etc.

I’m Finnish, and a programmer, so the time frame allocated for beer consumption was not fully sufficient to facilitate a safe space needed for relaxed fun & merriment, but it was a good evening nevertheless.

### “Angular CLI” by Stephen Fluin

Stephen described various nice things about the CLI. Frankly, I already forgot a lot of it, but an interesting new (for me) detail was how the CLI conceives the project as a full tree (“AST”-ish) and can do advanced heuristics based on that, instead of blindly doing dumb regexp replacements around.

### “The Angular Router” by Victor Savkin

Victor showed off the final version of the router. Lazy loading got lots of stage time, and how angular-cli tooling will help with that. Webpack can cut the whole bundle in separate route-specific modules, that are then transparently loaded by the router. Useful pattern will be to load and show the initial bundle quickly, then to preload the later bundles while the user already using the app.

Victor’s router book was available as a free download through Tuesday, so hopefully you managed to catch a copy while it lasted.

### “Look Deeply Into Your App with Augury” by Igor Kamenetsky

Igor explained some of the background and did a live demo of the debugger. Browsing the component tree, live-updating the attributes in the elements, dependency visualization and troubleshooting etc. Also covered on how Augury has evolved from early versions, and some nice tidbits of the implementation (frontend is a normal ng2 app running as chrome plugin, codebase is quite small at 5k LoC etc). I’m very much looking forward to having difficult problems to debug with this one ;).

### “How fast can web-apps be?” by Tim Ruffles

This was actually a quite funny, “motivational” talk to watch if you caught some of the SPA framework fat-shaming going around on Twitter recently. Discourse was compared to a server-rendered forum ([https://forum.dlang.org](https://forum.dlang.org)) when used on phones. Interesting observations thrown around:

*   Blocking (non-async) script tags fethcing data from several different CDN’s is a bad idea (multiple DNS lookups).
*   Consumers spend on average 200EUR on their Android phones. The phones are not bad, but apps like Discourse perform very badly on them.
*   Even in good networks, phones can expect big latencies because the radio is usually turned off to conserve power, and needs to be powered up for the new request.
*   Being able to stream most of content in initial request increases the perf a lot. This means inline critical styles, inline images (i.e. content directly in src), etc. The story doesn’t tell how to do this in modern SPA’s most easily, but I bet we’ll hear more about that later.
*   Even the most horrible phone you can still buy (40 eur or something, can’t remember) can play cut the rope, but can’t load up Discourse at all.
*   Web apps are often bad, and we should feel bad for giving a negative impression on consumers (leading to consumer preference for native apps, which is not great if you are a web dev).

### “Angular 2 Forms” by Kara Erickson

Kara is the author of the Angular 2 forms API. She showed the ropes around the forms, and contrasted template driven forms (ok for simple stuff) and reactive forms (better for more complex stuff, bigger initial development time but simpler and more predictable in long term). Kara seemed to gather some kind of cult following in the conference due to her incredible typing speed and editor (WebStorm) acuity.

### “Connect your Angular app to any existing backend with GraphQL” by Uri Goldstein

GraphQL was on table a lot, and it’s great to see it making inroads. Uri (not URI, \*eh\*) works with the Apollo GraphQL client, which is like Relay without React lock-in. Uri showed fast patterns on maintaining network-fetched application data with GraphQL, hooking it up to his demo Angular 2 application. He played around with the GraphiQL interactive query authoring tool, and it seemed like a breeze.

### “Universal Tooling” by Jeff Whelpley

Jeff (of AngularAir & Universal fame) was going through the still-unreleased features in Angular-CLI to enable building universal apps. Apparently they are also looking to enable testing straight in Node, without having to boot up Karma. Jeff also announced the “[AngularNation](https://angularnation.org/)” community effort, which will grow to be a website where feedback and discussion on Angular 2 can happen. There will be curation, and some stuff could be cherry picked as feature requests to Angular 2 project itself. Right now it’s just a Medium blog though.

### General takeaways

*   The conference was a confident tour-de-force for Angular 2. It’s good and shipping. There was no React whataboutism or “it will be very hard to port my Angular 1 app” in the air.
*   Performance and optimization was a recurrent theme. Closure Compiler deserves a fresh look.
*   GraphQL is actually happening. Couldn’t be happier about this; if you know me, you’ll know that I’m no fan of the REST/HATEOAS/Roy Fielding trainwreck for web API’s. Doing the server side was not covered.
*   RxJS story is not complete yet. They will be working on that.
*   Exra from the sponsor booths: ag-Grid is a real company now, with paid developers, marketing and clients (esp. in finance shops). This is good news for those of us not completely happy with the other grids in the market.
*   Kara is a fast typist.
*   Further evolution of Angular 1 will be all about easing the porting to Angular 2. We could see stuff like backporting the Http service etc.

By [Ville M. Vainio](https://medium.com/@vivainio) on [October 1, 2016](https://medium.com/p/96bfc790c7fa).

[Canonical link](https://medium.com/@vivainio/angularconnect-2016-retrospective-96bfc790c7fa)

Exported from [Medium](https://medium.com) on July 1, 2019.