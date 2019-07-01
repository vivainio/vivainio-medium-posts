# Node considered harmful (on Windows)

TLDR: you need to do use Node, but you probably won’t be happy with the experience if you are on Windows.

TLDR: you need to do use Node, but you probably won’t be happy with the experience if you are on Windows.

Node.js is what you need to use to get a modern frontend development toolchain (Gulp, transpilers, etc). If your development weapon of choice is Windows, it’s good to be prepared in advance for some pain.

### Maximum path length

Windows file system has maximum path length of 260 characters. Node module system is implemented with utter disregard for this, so you will quite easily end up with a path that is too long by require’ing some popular modules (like karma-jasmine-jquery).

Node itself has support for longer paths, because they convert them to UNC paths (\\\\?\\C:\\foo.txt) internally, but pretty much everything that runs on windows doesn’t support these. This means you can’t remove that directory with PowerShell “rm” command, yet alone the cmd.exe equivalent. To work around this, I recommend running [rimraf](https://github.com/isaacs/rimraf) a few times (because as it happens, Windows likes to lock files every now and again causing rimraf to fail).

Needless to say you can’t check files like this into git (e.g. if you want to maintain local versioning for your node\_modules tree). Even C# APIS to delete directory fail unless you use the UNC apis. The intuitive answer would be to “just use UNC apis, then” — but those don’t work with many tools, including those from Microsoft.

Worse, Node community feels the path-length-happy module system is a [feature, not a bug in Node](https://github.com/joyent/node/issues/6960#issuecomment-46704998) — so don’t hold your breath on any urgency to fix this non-bug.

For zipping and unzipping these trees, I recommend 7zip (which is also OSS). Info-zip’s zip doesn’t work.

### NPM

NPM has it’s share of detractors, but on Windows it feels particularly fragile. It’s not unusual to wedge up your npm cache to a state where you have to delete it.

### Module ABI

Node project publicly claims to retain the ABI for 0.10 series. However, I found that at least in my project, using node-sass (that uses libsass) broke between 0.10.32, 0.10.33 and 0.10.36. If you opt to distribute pre-built node\_modules directories, ensure the environments you are running with standardize on some version of Node.

### What are some good alternatives?

There are no viable alternatives for front end tooling, if you wish to stay on the frontlines of web development. Even Microsoft implemented their TypeScript transpiler on top of Node. This is unlikely to change as long as majority of front end developers are developing on Macs, deploying on Linux, and coding in JavaScript.

Since Microsoft is a big contributor to Windows port of Node, they likely need to fix this themselves. Maybe in the context of the io.js fork, Microsoft can have the leverage to change how the module system fundamentally operates — e.g. by providing “symbolic” module links that can refer up the tree to a specific version of the module. For production deployments, node could implement something like python’s zipimport or Java’s JAR files — which allow you to provice modules in a .zip file.

By [Ville M. Vainio](https://medium.com/@vivainio) on [January 30, 2015](https://medium.com/p/ccdc3a947979).

[Canonical link](https://medium.com/@vivainio/node-considered-harmful-on-windows-ccdc3a947979)

Exported from [Medium](https://medium.com) on July 1, 2019.