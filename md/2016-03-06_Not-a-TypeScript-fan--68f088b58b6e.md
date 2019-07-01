# Not a TypeScript fan?

Ongoing theme in TypeScript community is that once you switch to TypeScript, you don’t want to go back (to Babel or whatever). I bumped…

Ongoing theme in TypeScript community is that once you switch to TypeScript, you don’t want to go back (to Babel or whatever). I bumped into a [post listing some of the reasons](https://medium.com/@amcdnl/why-i-m-not-a-typescript-fan-c5057d76aaa4) why you may prefer to steer clear of TypeScript, which is as good a reason as any to debunk some of the popular myths and misunderstandings around the topic.

This post turned out to be longer than what I usually want to write, apologies for that. I sneaked in some items I have been willing to blog about anyway, now that the opportunity presented itself.

#### “Not da standard”

> I’d be will to bet in 3 years JavaScript will still be around without a doubt but I can’t say the latter for TypeScript.

I used to have that concern before Angular 2 adopted TypeScript. Lots of folks wanted to jump on the TypeScript bandwagon much earlier, but it needed “non-Microsoft validation” to close the deal. Technical superiority is of limited value unless you have community confidence to back it up.

If you are making a “3 year bet” on a project, you have all the more reasons to start hardening your project with types. At that scope, you are eventually going to have a bad time maintaining and growing with an untyped mess.

#### “You know its gonna happen…”

> Its inevitable that types are going to land in JavaScript sooner than later. To be honest, I’m surprised with all the ❤ JavaScript has gotten lately its not stage-0 by now. As soon as those land, things like TypeScript will be obsolete and technical debt to remove.

My money is on types not landing in ES standard. Here’s why:

*   Types are not a single feature that can just “land”. Modern type systems are advanced constructs that need a lot of time to build out, let alone standardize.
*   JavaScript is first and foremost a runtime that specifies how code will run in the browser. Runtime needs to be standardized, because it needs to behave compatibly on different browsers. Compile time doesn’t need to be standardized; it’s nice to have a standard for marketing reasons, but if you have a cross platform open source implementation there is no reason you couldn’t just use that implementation as is.
*   Type system would just be dead weight (i.e. extra complexity) for other compile-to-js languages that implement their own, sometimes very sophisticated type systems. Think Elm, PureScript, FunScript, Kotlin, ScalaScript, ClojureScript etc. Shoehorning a “lesser” type system system to JavaScript would limit innovation in this area.
*   Standardizing something slows everything down, and doesn’t guarantee a payback. Just follow the Node discussions around ES6 modules for proof.
*   Obligatory “appeal to authority” fallacy: Brendan Eich recently said he doesn’t see it happening, at least in the runtime.

If I turn out to be completely wrong about this bet, and JavaScript indeed standardizes a degree of type system, it will be handled by a future version of TypeScript: just use the newly standardized constructs in the areas where they apply, and keep the more advanced type checking in TypeScript.

#### “Its been around and gotten no ❤”

> TypeScript has been since 2012!!! I believe the only reason its gotten popular lately is because of Angular2. I think thats kinda a red flag in my book but thats just me talking…

People that most benefit from TypeScript are those from conservative shops that build big products. They are the kind that tend to wait for proofs.

If you take a look at current TypeScript tooling, it is receiving lots of love. Or Google trends:

![](https://cdn-images-1.medium.com/max/800/1*Ci8Hx6zF3RvKugW-hso09Q.png)

#### “Not Community Driven”

> I don’t see a lot of community involvement driving the spec / grammar / language like I do with even experimental features I see in ES\*. I could be looking in the wrong places but shouldn’t they be looking to the community and only building that instead of implementing C# in JavaScript?!

Easily accessible place to follow what is going to happen is the [TypeScript roadmap](https://github.com/Microsoft/TypeScript/wiki/Roadmap). You can click through the links and participate in the discussions. Senior developers hang around Gitter and read your questions and feedback, should the need arise.

You will likely have a much better chance on having an impact on a project that is “freely” implementing stuff than a language standardization process.

TypeScript is necessarily a more conservative project than “I’ll whip up my own Babel plugin and publish on npm”, and as a user of this technology I hope they keep it that way.

#### “A square in a circle hole”

> Adding typing into a non-typed language is always gonna be a hard mission to accomplish. TypeScript feels like it put types first and then JavaScript came in. That makes it really odd when you try to do things that have always been in JavaScript or are even new that don’t fit that paradigm.

TypeScript runs just plain JavaScript, and it has a type system that adds checks on top of that. You can do all the things that have always been in JavaScript (if you can’t file a bug ;). It may not have been easy task, but the design they have chosen has been proven in action over and over again.

#### “TypeScript Definitions”

> TypeScript requires definitions for all the files you are using in your application. Makes sense right? It needs to know about everything and those types so it can compile stuff for you. But what if you use a library that isn’t written in TypeScript which is most libraries.

TypeScript doesn’t need definition files for anything. You can use any marginal module you find on npm, just without types. If you are OK with using Babel in the first place, you are OK with having no type information available for parts of your application. Missing type information at the edges doesn’t “pollute” the rest of your application.

#### “What about FlowType?”

> Given my strong opinion above you would probably think, ya he’s gonna hate that too but actually I don’t. I feel like FlowType puts JavaScript FIRST and types just lay on top. It feels way more natural to me when I’m using it.

This is a subjective feeling. Biggest differences between Flow and TypeScript (and future trajectories of these projects) are probably between quality and scope of the tooling. I don’t know how well resourced (or widely used) Flow project is, but I have been spying on what TypeScript team is doing by skimming the discussions in github tickets, and it has so far been very easy for me to throw my vote of confidence in that direction.

#### Links

If you are not bored quite yet, you can check my [earlier blog post](https://medium.com/@vivainio/typescript-is-pretty-good-d8fecf80ea0c#.193mvxkug) in the same theme.

By [Ville M. Vainio](https://medium.com/@vivainio) on [March 6, 2016](https://medium.com/p/68f088b58b6e).

[Canonical link](https://medium.com/@vivainio/not-a-typescript-fan-68f088b58b6e)

Exported from [Medium](https://medium.com) on July 1, 2019.