# Migrating to Python 3 in 3 minutes or less

… on Windows.

![](https://cdn-images-1.medium.com/max/800/1*OtCdVpW-K8TGbcEloetFbw.jpeg)

… on Windows.

When you install Python 3, there will be a lancher called _c:\\Windows\\py.exe_. Barring weird stuff, this will be in your PATH. Stop using _python.exe_ and start calling that. You can call _py -2 myscript.py_ to use Python 2 instead, and _py -m pip <somepackage>_ to use pip for Python 3.

Use _futurize_ to port your code. “_futurize -w .”_ rewrites all files in current directory with fixed versions. Most importantly this adds _from \_\_future\_\_ import print\_function_ to your file. It’s directly in Anaconda distribution, or you can install it with _“py -m pip install future”_

By [Ville M. Vainio](https://medium.com/@vivainio) on [May 3, 2019](https://medium.com/p/11204364d969).

[Canonical link](https://medium.com/@vivainio/migrating-to-python-3-in-3-minutes-or-less-11204364d969)

Exported from [Medium](https://medium.com) on July 1, 2019.