# Using Stencil components in AngularJS application

Since StencilJS is just #UsingThePlatform (Web Components), I imagined it should be as easy (or easier) to integrate to an existing…

![](https://cdn-images-1.medium.com/max/800/1*TneQm8Qa4gqNi1LabVMxZw.jpeg)

Since [StencilJS](https://stenciljs.com/) is just #UsingThePlatform (Web Components), I imagined it should be as easy (or easier) to integrate to an existing AngularJS (a.k.a Angular 1.x) app as one of those “jquery plugin” style direct DOM access libraries with imperative API. I tried that yesterday, and wasn’t disappointed.

**Why would I want this?**

Some reasons for being interested in this are:

1.  Improving the performance bottlenecks in your AngularJS application. Stencil components sit alone outside the digest cycle, so anything happening inside them doesn’t impact the outer Angular application. Also, every time you press a damn keyboard button in your <input> fields doesn’t cause the digest cycle to evaluate everything in your Stencil component.
2.  Some complex things (that heavily alter the DOM structure beyond what ng-if’s etc. do) are easier in JSX, and don’t require PhD in AngularJS compiler trickery.
3.  Creating complex components in Stencil makes them transferable to Angular 2/4/5 or whatever, when you decide to take the plunge of porting to a trendier framework.

**How it works**

1.  You include the component assets with a <script> tag (this is important — don’t bundle the Stencil side, you need to have that script tag).
2.  You slap the components in your template normally.
3.  To change the props, you either set them imperatively on the HTMLElement or, for simple string properties, use angular {{ value }} binding.
4.  To listen to events, bind the DOM Event listeners in you angular $postLink() method.

**Example**

I used the StencilJS starter application to create a minimal component that showcases a few things: complex non-string object (‘strings’), simple string (‘simplestring’), and an event (‘onListClick’):

I’m then using this component (descriptively known as ‘<my-name>’) in AngularJS template like so:

The only “special” things here are

1.  being able to use {{$ctrl.message}} to assign values to the component directly in the template and
2.  “Transclusion”, i.e. StencilJS “slots” working in the last my-name instantiation on line 19.

Our Stencil component emits DOM Custom Events when clicking on list items; to listen to them in your AngularJS component you hook up some event listeners in $postLink() method (if you don’t know about $postLink() method, it’s one of the new component lifecycle methods in Angular 1.5):

When a complex object changes, you can’t just use {{ }} binding for obvious reasons. You need to explicitly dig up the HTMLElement for the component and assign value to this. You can use querySelector (or injected $element) to get a handle to the element:

Note how I didn’t just Array.push() the new value in the object. To trigger the change for complex object, you need to create a new object by Object.assign, Array.concat or whatever strikes your fancy and assign that.

For more ergonomics, you may want to introduce “props” directive in your AngularJS application:

With this, you can set the properties of the component directly in html by doing:

(source: see this [plunkr](http://plnkr.co/edit/7gvw0cqICfYZFAPi6bcG?p=info) and [github](https://github.com/angular/angular.js/issues/16235) issue)

The full example is [here](https://github.com/vivainio/stencil-ng1-demo) in all its messy, unproductized glory.

Caveat: Stencil is not widely used in production yet (as of 17.9. 2017). Observe usual caution when evaluating this approach.

By [Ville M. Vainio](https://medium.com/@vivainio) on [September 17, 2017](https://medium.com/p/2f09287c151).

[Canonical link](https://medium.com/@vivainio/using-stenciljs-components-in-angular-1-application-2f09287c151)

Exported from [Medium](https://medium.com) on July 1, 2019.