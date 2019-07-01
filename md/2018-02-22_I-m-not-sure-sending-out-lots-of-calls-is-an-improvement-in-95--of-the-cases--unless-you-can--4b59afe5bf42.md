# I’m not sure sending out lots of calls is an improvement in 95% of the cases (unless you can…

This can be true for trivial special case where http server sends out static files or something directly from cache. But most of the time…

I’m not sure sending out lots of calls is an improvement in 95% of the cases (unless you can progressively show the partial result set).

This can be true for trivial special case where http server sends out static files or something directly from cache. But most of the time it’s more efficient to reduce the database hits and back-and-forth with client and server. If you have a dependency A -> B -> C, you would be waiting for network latency 2 times instead of one. On a phone this can be waiting for your modem to turn on 2 times.

By [Ville M. Vainio](https://medium.com/@vivainio) on [February 22, 2018](https://medium.com/p/4b59afe5bf42).

[Canonical link](https://medium.com/@vivainio/im-not-sure-sending-out-lots-of-calls-is-an-improvement-in-95-of-the-cases-unless-you-can-4b59afe5bf42)

Exported from [Medium](https://medium.com) on July 1, 2019.