# PowerShell as find.exe replacement

Or: how I learned to stop worrying and use a PowerShell feature.

Or: how I learned to stop worrying and use a PowerShell feature.

Are you one of those guys that keeps trying to run “find” on Windows, and seeing that it runs some ancient MS-DOS command that nobody has used since the 80's? Not one to brick your scripts by prepending Cygwin commands to your PATH, you cringe in despair and reach out for alternatives.

So, PowerShell has a suprisingly reasonable alternative.

(“PowerShell!”, you say, againg cringing in despair. But fear not!)

The alternative is “Get-ChildItem”, aliased as “dir” and “ls”. Henceforth I’ll just use “ls” since “Get-ChildItem” is pedantic to the extent of being insulting.

The thing you will try first is “ls _-<tab> <tab> Recurse_” (yes, not pressing Tab a lot is going to slant your view heavily against PowerShell).

The output, as you expected, is useless. It lists the directories in separate paragraphs like the old “dir /s” MS-DOS command:

![](https://cdn-images-1.medium.com/max/800/1*hQTnWCNI8kLJX9B8LeeOBQ.png)

The remedy is to use the “-name” parameter that outputs full path names:

![](https://cdn-images-1.medium.com/max/800/1*aEnN-fFvPRk8Ok7axrGaSQ.png)

So now you’ll want to get just the directories:

![](https://cdn-images-1.medium.com/max/800/1*f-bTMtCyfpp6xfMustaX8g.png)

Or files starting with \_\_:

![](https://cdn-images-1.medium.com/max/800/1*-rBlgoU1a89w5QVE5GsMzQ.png)

#### Pipes

“So what’s the deal? Everyone said PowerShell is all about piping objects?”, you say.

Well, if you omit the -Name argument you get those Objects. Happy now? These objects may be useful for some things, but you’ll want to use them to foreach stuff for all the files. For this purpose, these is the “_foreach”_ command and $\_.FullName:

![](https://cdn-images-1.medium.com/max/800/1*L94GzPePnPqGnUIaUd8gqQ.png)

This one runs “cat” on all the files. If you wanted to delete all the node\_modules directories to free up disk space, you would do:

![](https://cdn-images-1.medium.com/max/800/1*zm32NSrTc34TygJzzi7nIA.png)

Clearly, this will fail on Windows because of path length limitations, but at least it will have deleted some of the node\_modules directories.

Enjoy! And maybe use PowerShell.

Updating with new commands as I find them:

![Get-Command as “which” replacement](https://cdn-images-1.medium.com/max/800/1*pcFUE9qu6RBlcGFpJHqY2w.png)
Get-Command as “which” replacement

By [Ville M. Vainio](https://medium.com/@vivainio) on [October 18, 2017](https://medium.com/p/1d95498bc48e).

[Canonical link](https://medium.com/@vivainio/powershell-as-find-exe-replacement-1d95498bc48e)

Exported from [Medium](https://medium.com) on July 1, 2019.