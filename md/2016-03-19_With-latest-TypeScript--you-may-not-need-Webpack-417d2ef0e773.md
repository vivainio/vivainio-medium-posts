# With latest TypeScript, you may not need Webpack

(You won’t need Browserify either, but that’s not as catchy a headline)

![](https://cdn-images-1.medium.com/max/800/0*DFCZqJ3vRVQ1vzKi.jpg)

(You won’t need Browserify either, but that’s not as catchy a headline)

_Update for May 2018: many have pointed out that this approach won’t work if you have dependencies that are not provided as concateable UMD bundles. This is true. Look into modern options like ParcelJS if you need that._

In the olden days, when you bought a compiler for your PC, it came with a linker on the same box. With JavaScript, the two have been divorced. Somehow, we didn’t understand what the linking part should look like, so we ended up innovating on a bunch of creative solutions, much to the dismay of programmers just wanting to work on their app instead of build tooling.

TypeScript 1.8 brings the linker back to the compiler suite, as announced in [this deceptively downplayed feature section](https://github.com/Microsoft/TypeScript/wiki/What%27s-new-in-TypeScript#concatenate-amd-and-system-modules-with---outfile). Essentially, you point the compiler at your entry point TypeScript file (e.g. ‘app.ts’), and it emits a single bundled JS file after traversing all your imports.

The command you slap in your build script is essentially

$ tsc --watch -m system --outFile out.js app.ts

Don’t let “SystemJS” put you off — while SystemJS, like Webpack, is a baroque tool with in-browser transpilation, loader plugins and the works, none of that is at play here! The only parts used are _System.register()_ and _System.import()_ — _register()_ is the wrapper around your modules in the bundle, and _import()_ is what you’ll call to start your app (probably in index.html or equivalent).

There are some “hard”, somewhat overlapping benefits for TSC bundling:

*   Single component (TypeScript compiler) to track for problems and bug reports. If something like source maps break, you know it’s typescript instead of one the more fractured plugins/transformations floating around the web.
*   That single component comes from Microsoft, as opposed to various loaders/plugins maintained through part time/volunteer basis.
*   It’s faster. Testing with our app, TSC bundling was more than two times faster than Browserify + Tsify for a clean build.
*   You can launch it by just running an executable without external configuration, even from build.bat if you are so inclined. If you are interested in extra speed on Windows, you can even download ChakraCore-enabled tsc.exe from NuGet, drop it in place of the node-hosted “tsc” script and go to town.

As well as some softer ones:

*   SystemJS modules behave like ES6 modules. Imitating ES6 syntax with CJS (as in Webpack or Browserify) gives you “useful” semantic power that is not in ES6 spec; namely, imports are executed on the line they appear, as opposed to beginning of the module like they should.
*   System.register() is being standardized as a module bundling API. Don’t know the stage of it (or even how much it matters), but it can help future interoperability with third party modules.

Summary: do not multiply objects without necessity. Before setting up a majestic build pipeline funneling Typescript to Babel to Webpack, see if you can get your job done with a simpler, gentler approach.

_Disclaimer: it’s a new feature — suitability for your application may vary. Proceed with the usual caution and fear._

**Update**: some users have found SystemJS library too big for their needs. It’s 15kb when minified and gzipped; for small applications this may be too expensive. A lightweight alternative is to use the AMD module format (_tsc -m amd_) and A[lmond](https://github.com/requirejs/almond), which goes all the way down to 1kb when minified and zipped! While AMD is increasingly being perceived as a receding module format, it can still act as a light alternative to SystemJS, depending on your interop needs.

**Update**: Einari Naukkarinen has created a [minimal boilerplate project for an Angular 1 application](https://github.com/enaukkarinen/modest-tsc-ng1-boilerplate) using the described mechanism, with Almond module loader. This is the same mechanism we are currently using to bundle one of our larger SPA’s at [Basware](http://www.basware.com/about-us/careers).

By [Ville M. Vainio](https://medium.com/@vivainio) on [March 19, 2016](https://medium.com/p/417d2ef0e773).

[Canonical link](https://medium.com/@vivainio/with-latest-typescript-you-may-not-need-webpack-417d2ef0e773)

Exported from [Medium](https://medium.com) on July 1, 2019.