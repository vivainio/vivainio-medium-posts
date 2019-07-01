# I think you are being a bit unfair to tsc — for apps where you don’t need code splitting, it does…

I think you are being a bit unfair to tsc — for apps where you don’t need code splitting, it does the exact job of bundling (i.e. creating a concatenated file with modules wrapped in either AMD or SystemJS module wrappers). The only thing you need to add is the runtime loader for the module system (we are using Almond).

By [Ville M. Vainio](https://medium.com/@vivainio) on [February 22, 2018](https://medium.com/p/32c63e5656a0).

[Canonical link](https://medium.com/@vivainio/i-think-you-are-being-a-bit-unfair-to-tsc-for-apps-where-you-dont-need-code-splitting-it-does-32c63e5656a0)

Exported from [Medium](https://medium.com) on July 1, 2019.