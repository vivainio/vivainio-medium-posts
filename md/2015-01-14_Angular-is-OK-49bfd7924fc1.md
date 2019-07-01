# Angular is OK

As far as adoption goes, Angular is the most popular JavaScript Single Page Application framework (few will contest that).

![](https://cdn-images-1.medium.com/max/800/1*FzR73ujQAMSj3BOiyc0jlA.png)

As far as adoption goes, Angular is the most popular JavaScript Single Page Application framework (few will contest that).

It’s not perfect, but it’s not particularly worse than other offerings in the field. The fact that various bloggers have graced the world with their insight on how bad Angular is does not automatically mean they are right; people have been known to be Wrong on the Internet in the past, and blogging is cheap (this being one such example).

Some key points that are worth mentioning:

1.  **Angular does not lock you into anything**. You can minimize dependency injection and get your singleton handles any way you deem fit (window.foo, anyone?). You can use AMD/Browserify/ES6 module system instead of Angular module system to partition your code (by slapping everything in a single angular.module(“app”)). You can use the quirky jQuery tree plugin (or the lightning-fast table) you inherited from the guy that left last month by putting it into directive (that allows raw DOM manipulation unlimited by digest cycle). Angular (unlike e.g. Ember or even Backbone) has no opinion how you deal with web apis. And so on.
2.  **There is no perfect framework yet,** but you need to pick something**.** If you are in the business of building a web app, there is no choice that will last you five years without some degree of migration. Angular 1 is the most conservative choice available right now, with skill (and likely code, to some extent) portability to Angular 2 (which is guaranteed to become successful due to community dynamics). If winds were to change and React eventually became the dominant framework, it’s unlikely to be the React of today, but rather some future iteration of it — likewise, a future iteration of Angular would likely have Virtual DOM and other architectural features of the frameworks at that time. Competition will be good and healthy.
3.  **Marketable skillset.** If you are an employer, a way to keep your employees happy is to let them build skills that are valuable to the employees themselves. Being able to hack Angular well is an asset that increases the demand of the employee in the marker, so your developers won’t feel they are sacrificing their youth on a dead-end framework their architect picked (or worse, implemented) after reading a sales pitch on Reddit. Even if you feel like the framework is too hard here and there (Angular has some rough, complex edges), it’s good to know all that efforts to tackle the beast is not going to waste.
4.  **It’s not that enterprisey.** Angular tends to use some terminology that bears unfortunate connotations from Enterprise Java or European Union (Dependency Injection, Directive, Isolate Scope…), but the actual experience is as agile as anything. The fact that you write a lot of HTML doesn't mean you are somehow hiding the logic, you are merely skipping the mundane scaffolding work you would need to keep DOM and JavaScript models in sync.

It is unfortunate Angular 1 is not smaller, faster and better than it is, but it’s the “IBM” that won’t get you fired in a year or so — and you won’t need to keep answering to “why not Angular then” for everyone that hears you are using FooBarFramework 0.12.2.

By [Ville M. Vainio](https://medium.com/@vivainio) on [January 14, 2015](https://medium.com/p/49bfd7924fc1).

[Canonical link](https://medium.com/@vivainio/angular-is-ok-49bfd7924fc1)

Exported from [Medium](https://medium.com) on July 1, 2019.