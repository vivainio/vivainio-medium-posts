# Quick note on the implementation of “maybe” (and maybe of relevance to the topic in general):

This:

Quick note on the implementation of “maybe” (and maybe of relevance to the topic in general):

This:

> if (value === null || value === undefined)

Can be more idiomatically expressed by:

> if (value == null)

I agree on just doing ‘truthy’ checks instead of more explicit checking though, mainly on the basis of being less messy and checks being almost always made against objects, not primitive types.

Somehow, I have ended up using “null” for “value missing”, possibly because undefined ends up there because of programming errors. This may be an unnecessary safeguard, and TS should make errors where undefined’s show up rarer. If TSC source code does not need nulls, I probably need to reconsider this habit ;).

By [Ville M. Vainio](https://medium.com/@vivainio) on [March 11, 2016](https://medium.com/p/f0a00bf501e8).

[Canonical link](https://medium.com/@vivainio/quick-note-on-the-implementation-of-maybe-and-maybe-of-relevance-to-the-topic-in-general-f0a00bf501e8)

Exported from [Medium](https://medium.com) on July 1, 2019.