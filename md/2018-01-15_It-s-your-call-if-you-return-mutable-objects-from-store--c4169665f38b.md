# It’s your call if you return mutable objects from store.

If the object is not immutable (e.g. you dig up the same array reference), then you need to trigger manual change detection in an OnPush…

It’s your call if you return mutable objects from store. If your autorun, or a computed property gives you a new immutable object, it works fine.

If the object is not immutable (e.g. you dig up the same array reference), then you need to trigger manual change detection in an OnPush component. That’s pretty expected & explicit. (And that’s what async pipe does as well)

There are very little reasons not to have immutable objects though. MobX makes it very easy to do that.

By [Ville M. Vainio](https://medium.com/@vivainio) on [January 15, 2018](https://medium.com/p/c4169665f38b).

[Canonical link](https://medium.com/@vivainio/its-your-call-if-you-return-mutable-objects-from-store-c4169665f38b)

Exported from [Medium](https://medium.com) on July 1, 2019.