# Our deps are concatenated by a gulp script at build time.

If you use several “micro libraries” from npm, this approach is not applicable and you are indeed stuck at using CJS. As a semi-joke, I…

Our deps are concatenated by a gulp script at build time. See this boilerplate: [https://github.com/enaukkarinen/modest-tsc-ng1-boilerplate/blob/master/gulp/tasks/vendor.js](https://github.com/enaukkarinen/modest-tsc-ng1-boilerplate/blob/master/gulp/tasks/vendor.js)

If you use several “micro libraries” from npm, this approach is not applicable and you are indeed stuck at using CJS. As a semi-joke, I actually created a library for that: [https://github.com/vivainio/decjs](https://github.com/vivainio/decjs)

By [Ville M. Vainio](https://medium.com/@vivainio) on [December 4, 2016](https://medium.com/p/7ada46ea7c56).

[Canonical link](https://medium.com/@vivainio/our-deps-are-concatenated-by-a-gulp-script-at-build-time-7ada46ea7c56)

Exported from [Medium](https://medium.com) on July 1, 2019.