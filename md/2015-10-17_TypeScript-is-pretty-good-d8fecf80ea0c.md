# TypeScript is pretty good

TLDR: A column about how TypeScript is pretty good, compared to ES6.

TLDR: A column about how TypeScript is pretty good, compared to ES6.

It’s gradually becoming clear to wider community that you should be transpiling; while ES5 still has a loyal cult following, it mostly consists of people that erased their pasts and extinguished all critical thought once they accepted Crockford in their hearts.

Everyone knows ES6 is great; one thing ES6 (currently in form of Babel, mostly) doesn’t give you is checking that your program is valid — something we old people used to call “compilation” and “type system”. If you instantiate a class Foo on line 12, ES6 forgets that your variable had a method “bar()” by the time it reaches line 13. Let alone importing another module and knowing what is in there, despite the fact that you explicitly export the members you want to expose even in ES6 specification.

Lint tools can do halfway guesses on what is valid, but they are generally more useful in warning you about wrong kind of quotes (apparently single quotes are the way to go these days, contrary to the way our Fathers wrote their strings) and missing a newline at the end of file. It’s like parsing xml trees with regexps — it seems to do something sensible sometimes, but you know it ain’t right.

TypeScript advocates are often embarrassingly humble and polite; you will never catch them boasting how they are several years ahead of ES6 spec in technical sophistication (zero static understanding of the program, vs. something C#, Java, let alone FP programmers have been pampered with for years). They will point out that ES6 is great step forward, and in passing note that “you can get some help from the tooling if you try this typescript thing”. As in “huffing solvents is a pretty decent approach to altering your mood, but you should probably take a sip of beer to check it out, you might like it”.

Rational engineer is (or has been) rightly skeptical about TypeScript for the following reasons:

*   Will it catch on? Will our codebase be marginalized if we choose this transpiler?
*   What if we hit unexpected hurdles when using it? What if there are bad design choices that we will suffer from once we go for it?

At some point, I was wondering whether TypeScript could attract the community momentum that CoffeeScript had. We may laugh at that now, but it was a real concern back in 2012 when TypeScript launched. As TypeScript closely aligned with ES6 around 1.5 release (alpha in spring 2015), this concern evaporated, not to mention the new “validation” of Angular 2 switching over to TypeScript from their traceur-based AtScript contraption. The act of transpilation itself has been widely accepted in 2014/2015, short of the few usual luddites (and possibly your boss, at which point you should probably refresh your CV and look around a bit).

As for the second bullet point — does it really work?

Obviously, gradual typing means you can add types gradually; the parts of the application that are not “ready” (read: clean enough or well understood enough) can be left untyped without compiler whining about it. What I have seen is that once you tighten the types, you won’t be hitting unanticipated problems; usually, what you get is previously undetected bugs in your application being smoked out. Or, if you hit a bug in your type definition file, you cast to “any”, file a bug in DefinitelyTyped and move on.

Basically, TypeScript type system is well thought out. It’s not at the level of usual 18 year olds uploading their hobby projects to npm **at all**. It’s one of those paid projects where people’s livelihood depends on the stable releases being stable, with paid Quality Assurance and paid people doing code reviews.

Can TypeScript compete against Flow (the type inference engine from Facebook?). Let’s assume for the sake of argument that Flow was anywhere near ready:

*   Flow’s selling point is using global type inference instead of explicitly declaring your types. No other programming language goes this far; Hindley-Milner (or similar) type inference is used in several functional programming languages as an **adjunct** to explicit type definitions; you have type definitions at key points of your API, after which inference can do educated analysis of the functions referring to your API.
*   TypeScript is hosted in Node; Flow is an unix-only Ocaml application that is optimized to do wide analysis of Facebook code base. You may or may not be working at Facebook, but usually you are not.

There is also one irrational (yet important) argument against TypeScript that needs to be addressed: TypeScript is Microsoft, Microsoft is Windows, and Windows is horrible (also: Microsoft hates you, everything that is good in life and will sue you once you hit their searchlights).

TypeScript, being built on Node, is obviously cross platform, but Microsoft is investing heavily in Visual Studio Code that gives the best-in-class TypeScript experience (better than the Windows-only Visual Studio proper). Their recent developer push has been to release their best engineering achievements (CoreCLR etc.) under the MIT license. It’s highly likely they have your best interest in their minds in 2015 and further.

You could do much worse than making the bet on TypeScript.

Edit: it would be unfair to call TypeScript always the best choice. If you are a “gun for hire”, you may not have any say on the transpiler to use; also, if you are typically doing quick and small projects, the maintainability and refactoring benefits may not be at the center of your decisions.

By [Ville M. Vainio](https://medium.com/@vivainio) on [October 17, 2015](https://medium.com/p/d8fecf80ea0c).

[Canonical link](https://medium.com/@vivainio/typescript-is-pretty-good-d8fecf80ea0c)

Exported from [Medium](https://medium.com) on July 1, 2019.