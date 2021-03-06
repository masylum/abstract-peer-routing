abstract-peer-routing
=====================

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](http://ipn.io) [![](https://img.shields.io/badge/freenode-%23ipfs-blue.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23ipfs)

> A test suite and interface you can use to implement a Peer Routing module for libp2p.

The primary goal of this module is to enable developers to pick and swap their Peer Routing module as they see fit for their libp2p installation, without having to go through shims or compatibility issues. This module and test suite were heavily inspired by abstract-blob-store and abstract-stream-muxer.

Publishing a test suite as a module lets multiple modules all ensure compatibility since they use the same test suite.

The API is presented with both Node.js and Go primitives, however, there is not actual limitations for it to be extended for any other language, pushing forward the cross compatibility and interop through diferent stacks.

# Modules that implement the interface

- https://github.com/diasdavid/node-ipfs-kad-router

# Badge

Include this badge in your readme if you make a module that is compatible with the abstract-record-store API. You can validate this by running the tests.

![](https://raw.githubusercontent.com/diasdavid/abstract-peer-routing/master/img/badge.png)

# How to use the battery of tests

## Node.js

```
var tape = require('tape')
var tests = require('abstract-peer-routing/tests')
var YourPeerRouter = require('../src')

var common = {
    setup: function (t, cb) {
      cb(null, YourPeerRouter)
    },
    teardown: function (t, cb) {
      cb()
    }
}

tests(tape, common)
```

## Go

> WIP

# API

A valid (read: that follows this abstraction) stream muxer, must implement the following API.

### Find peers 'responsible' or 'closest' to a given key

- `Node.js` peerRouting.findPeers(key, function (err, peersPriorityQueue) {})

In a peer to peer context, the concept of 'responsability' or 'closeness' for a given key translates to having a way to find deterministically or that at least there is a significant overlap between searches, the same group of peers when searching for the same given key.

This method will query the network (route it) and return a Priority Queue datastructe with a list of PeerInfo objects, ordered by 'closeness'.

key is a multihash
