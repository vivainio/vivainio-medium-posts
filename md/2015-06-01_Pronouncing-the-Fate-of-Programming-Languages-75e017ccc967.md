# Pronouncing the Fate of Programming Languages

I read way too much reddit and felt like writing down predictions on what will happen with various programming languages on the radar right…

I read way too much reddit and felt like writing down predictions on what will happen with various programming languages on the radar right now. This is a bizarre mixture of of wishful thinking, personal delusion and realism; and as expected for the subject matter, not without a pinch of good old-fashioned trolling.

### Java

Will continue to be hated by the masses, and will lag behind other programming languages by 5–10 years in features. Despite this, it will be widely used because it’s a fast, managed (safe) runtime that runs on Linux.

There is also good money to be made in Java consulting, so if you appreciate the Good Life with a degree of tolerance for professional garbage shoveling, Java offers tons of opportunities.

### C#

Recent open sourcing and cross platform push will make it viable for “hot” startups in 2016. It will still lag behing Java, but it’s also moving much faster in terms of new feature development, so “cool kids” may discover it sooner rather than later (probably around the time Linux will become the first class deployment target and OSX a good development environment). It’s growing several modern features (tuple unpacking etc) and, unlike Java, already has a good array of nowadays-expected enablers like LINQ and local type inference.

### Scala

Will slow down — it’s a in many ways “best in class” on JVM, but also considered too complex and various companies (like Linkedin) have been backpedaling on it. It’s also said to be significantly slower than Java (when written in the community-preferred functional style), and even Stroustrup has been taking jabs at how slow the compiler is.

### Clojure

Will slow down. Lisp syntax is a showstopper for many programmers (not just junior developers), and lack of static typing will become a contraindication in larger projects. Like Ruby and Python, you will get “somewhere” quite fast, but scaling a dynamically typed macro-heavy code will become a mess. The selling points like immutable data or concurrency libraries are available elsewhere.

The language has energetic and vocal community, so it will keep popping up with some regularity. This should not be seen as indicative of its long-term mainstream appeal.

ClojureScript could be a promising exempt to this — the macro system could prove to be a good productivity boost for next generation javascript framework creation.

### Haskell

Will continue to go nowhere. Unfamiliar runtime behavior (laziness), severe restrictions for “normal programming” (like local mutable variables and loops) and impenetrable academic jargon will keep it as a research language. Also, the M-word.

### Node

Will continue it’s fast ascent. It has found good adoption regardless of it’s flaws (single threaded runtime, widely-disliked programming language and “callback hell”), but as the runtime and the programming language are being improved more rapidly (TypeScript, SoundScript, IO.js “takeover”, etc) it will be hard to stop — also, as far as dynamic languages go, it will be hard to rationalize Clojure over Node in greenfield (non-JVM) projects.

### Python

Will retain it’s popularity, but won’t grow much. It already does very well the job it’s being used for, but its raw runtime performance will continue to lag behing the present competition (and runtime performance is the new hotness). “Batteries included” and simplicity will continue to find new fans. New gradual typing enchancements in Python 3 could breath new life to it in larger team efforts, but the (real or perceived) performance problems will make it a harder sell for new projects.

### Ruby

Will decline. Hayday of Rails is over with new focus on REST(ish) api’s, so server side rendering (the forte’ of Rails) is already seen be a legacy technology. Ruby has several “killer applications” on the web development side, but, unlike Python, doesn’t have a strong foothold in scientific computing or system scripting. Like Python, it’s in the slower end of the language spectrum.

### Perl

Is dead.

### Go

Will continue it’s good growth. Programming language theorists abhor the weak type system (no generics), but it has “somehow sufficient” static type system, acceptable performance, well thought out standard library, good community and big deployment benefits (just drop the statically linked executable on your server), so it will become a well-liked language for command line apps and focused microservices (yes, the other M-word).

### F#

I actually have no idea how well F# will fare, but I like the language a lot so wanted to add it to the list ;-). Due to new cross-platform drive for .NET, it has become newly viable; it also has several advanced features (like global type inference, dead-easy generics, appealing syntax and a strong type system) while remaining usable as a “normal” imperative programming language. It also benefits from good tooling support (read: visual studio), but unfortunately you are still stuck with Windows for best experience.

If you are a fan of dynamic languages and gravitate towards functional style (think short functions; list comprehensions; arrays, tuples and dicts instead of classes; generators), you can find yourself quite cozy with F#.

### Visual Basic

Will continue to be used for applications that are not deemed worth porting to better-liked programming languages

### Erlang

Is still being used, for reasons known only to Erlang users. Has a fancy runtime that can deal with restarting dead lightweight processes, but is locked to a bizarre programming language from the 70's for incomprehensible reasons.

### C++

Will be used for AAA game development until ca. 2024. C++11 took some steps to make it more palatable to modern programming tastes (auto, lambdas), but the language itself has just grown too big and hard for new generation of programmers.

### C

Will be replaced by Rust once developers realize how unsafe and vulnerable their C applications are. High Priesthood of programmers, IOW kernel developers, will stick to it forever.

### PHP

Enough has been said about PHP. It won’t go away even if you don’t pay attention to it, but if you keep your skills sharp you should be able to avoid PHP-related jobs even in current economy.

### Objective-C

Will be phased out in favor of Swift once Cook finally & unilaterally pulls the plug.

### Rust

Will grow as a safer alternative C and, to some extent, C++. Most programmers don’t need full control of memory allocation (maximization of stack usage, using heap as little as possble) and absolutely predictable performance, but Rust delivers this along with a lot of modern conveniences (pattern matching, destructuring) and an NPM-like package ecosystem through creates.io.

### Dart

Offers no tangible benefits over TypeScript (especially after the introduction of Google’s “SoundScript” (repeat after me, it’s not called “SaneScript” anymore as a manner of professional courtesy), and the development will be gradually ramped down to “community effort”

### TypeScript

Will continue to be shunned by ES6-purists for emotional reasons, but in the meantime it will be successfully used in big projects to get real work done. Will disappear once ES20XX gain a type system that is exactly as implemented in TypeScript. Once browsers grow ES7 support, they will ignore the type annotations so a transpiler (as opposed to development time type checker) won’t be needed anymore.

### OCaml

Had a chance to be the “Go” language several years ago, but it didn’t pan out. Legacy lives on in F# and Rust.

By [Ville M. Vainio](https://medium.com/@vivainio) on [June 1, 2015](https://medium.com/p/75e017ccc967).

[Canonical link](https://medium.com/@vivainio/pronouncing-the-fate-of-programming-languages-75e017ccc967)

Exported from [Medium](https://medium.com) on July 1, 2019.