# Only if your third party library expects Webpack or Browserify.

Only if your third party library expects Webpack or Browserify. Usually they don’t, e.g. there is an UMD bundle in dist/ folder that you just concatenate to your lib.js. We have them concatenated AFTER almond.js, so they are just made available in Window object.

By [Ville M. Vainio](https://medium.com/@vivainio) on [November 27, 2016](https://medium.com/p/929dc305c384).

[Canonical link](https://medium.com/@vivainio/only-if-your-third-party-library-expects-webpack-or-browserify-929dc305c384)

Exported from [Medium](https://medium.com) on July 1, 2019.