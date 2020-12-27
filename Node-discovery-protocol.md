---
name: Node Discovery Protocol
category: 
---

In a nutshell:
* Aimed at discovering _RLPx nodes_ to connect to
* UDP-based RPC protocol ([kademlia](https://en.wikipedia.org/wiki/Kademlia)-like)
* Defines 4 packet types: _ping_, _pong_, _findnode_ and _neighbors_

See details at either:
* [devp2p](https://github.com/vaporyco/devp2p) repository's [node discovery protocol](https://github.com/vaporyco/devp2p/blob/master/rlpx.md) page
* [go-vapory](https://github.com/vaporyco/go-vapory) repository's [node discovery protocol](https://github.com/vaporyco/go-vapory/wiki/RLPx-----Node-Discovery-Protocol) page