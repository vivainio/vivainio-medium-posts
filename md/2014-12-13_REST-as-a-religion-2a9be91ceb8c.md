# REST as a religion

You don’t need to rewrite everything to comply with REST philosophy.

It is widely understood that developers don’t typically know what REST means.

However, developers know what kind of web api’s people like:

*   Dynamically typed API schema (informally specified, non-machine-checked JSON)
*   Nice URL’s
*   Discoverability (API can be deduced from following the links in browser and sniffing the network requests)
*   Ease of use. You can use the API without buying in to a fat library that can somehow extract the meaning from cryptic protocol (see: SOAP)

REST got lucky in that people didn’t know what it means, so they ended up calling their preferred approach RESTful. Only after it was established that “REST is great”, discussion was steered towards “this is not REST, you should write your API this way instead”.

Food for thought: if you have a large RPC based system (implemented in e.g. SOAP), it may be better use of your money to investigate whether you can reap some of these benefits without buying into the whole REST philosophy. If you want more flexibility in your metadata, try relaying the metadata as JSON within the existing RPC structure, instead of rewriting the whole system as RESTful service. Even if you use a legacy statically specified protocol like SOAP, you don’t have an obligation to cripple all your message passing by overspecifying it.

(This is relevant to ongoing discussion about X-road service bus being triaged in Finland).

By [Ville M. Vainio](https://medium.com/@vivainio) on [December 13, 2014](https://medium.com/p/2a9be91ceb8c).

[Canonical link](https://medium.com/@vivainio/rest-as-a-religion-2a9be91ceb8c)

Exported from [Medium](https://medium.com) on July 1, 2019.