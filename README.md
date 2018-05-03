# decentralized-tech-research

| Project | Description | GitHub ⭐ |
| --- | --- | --- |
| [IPFS](https://ipfs.io/) | A global content-addressed DAG. Just immutable data, but a name service layer called IPNS lets you assign changable names to immutable content. | 12,708 |
| [DAT](https://datproject.org/) | Decentralized protocol for sharing data. The [Beaker](https://beakerbrowser.com/) browser can open links to [dat content](dat://beakerbrowser.com/docs/apis/dat.html). | 6,670 |
| [Scuttlebutt]() | Offline-first protocol and social network, with a few clients like [Patchwork](https://github.com/ssbc/patchwork). | 6,670 |
| [ShareDB](https://github.com/share/sharedb) | A real-time database for editing JSON docs concurrently. | 1,820 |
| [Mastodon](https://joinmastodon.org/) | Federated self-hosted microblogging | 13,226 |
| [Statebus](https://github.com/invisible-college/statebus) | Reactive JS framework reminiscent of [Meteor](https://www.meteor.com/) | 46 |

## the "quick take"

Based on an early look into what's out there, the easiest way to get **photos and simple message sharing** for offline devices with minimal setup would be:

to setup Patchwork on each device--and then instead of running the server through electron, we could run expose each backpack's instance as website accessible by anyone in the network.

## Projects

### IPFS

IPFS works like Bittorrent for files in a global namespace.

It's easy to [install](https://ipfs.io/docs/install/): a single binary or build from go source. A [Raspberry Pi installer](https://github.com/claudiobizzotto/ipfs-rpi) also exists.

IPFS is a low level tool for syncing data across devices. A survey of [awesome-ipfs](https://github.com/ipfs/awesome-ipfs), a list of things made on top of IPFS:

 * An early version of a message board called [ipfs-boards](https://github.com/fazo96/ipfs-boards) - here's an [example board](https://ipfs.io/ipfs/QmYT9EzvQY8zwtxQxUhPcphSGR4XtTRkT4MnXmQKPFamQ7/#/b/QmVfCR9XnqkiAa7BBR74WYKAzH9CdgbWYF5jdgVLjmfsXx/test-board-1) I made in ipfs-boards. Text-only. 

 * The [Yjs](http://y-js.org/) project has an IPFS "connector." Its [example page](http://y-js.org/#!/examples) has some nice demos of live decentralized editing.

### DAT

Tom MacWright has a [helpful blog post with a comparison between DAT and IPFS](https://macwright.org/2017/08/09/decentralize-ipfs.html).

It's also easy to install: via [Beaker](https://beakerbrowser.com/) knows how to open dat:// links to content on the DAT network.

[Fritter](dat://fritter.hashbase.io) is a prototype Twitter clone on DAT. No image support.

![](https://i.imgur.com/jupjifV.png)

[Rotonde](https://louis.center/p2p-social-networking/) is a social network built on DAT.

![](https://louis.center/p2p-social-networking/library.png)

### Scuttlebutt

Clients discover each other a LAN with multicast UDP and "gossip" the social network's data with other people they follow. Projects like [MinBase](https://github.com/evbogue/minbase) could form the basis for a simple and minimal server run by each rpi. All backpacks could, when they have internet access, join a specific [pub server](https://github.com/ssbc/scuttlebot/wiki/Pub-Servers) so that they know to sync with each other.

A major con would be that to be recognized as a unique "person" on Scuttlebutt, you'd need to run a client--i.e., if everyone whose phones are connected to a backpack uses its scuttlebutt instance, everyone is "posting" as the same identity. Not sure this is actually a problem for our use-case though...

### Mastodon

Decentralized microblogging with federation. Relies on DNS. Skinnable, each backpack could run an instance and know to find and federate with the other instances when they are on the internet. Supports photos and private messages.

### ShareDB

A low level library for making changes to a JSON document concurrently. Supports offline sync. A building block for bigger tools.

### Statebus

A small library for synchronizing state across webpages. Small opinionated framework for writing JS apps that can send and receive reactive state. Impressive but no real community around it (yet).

## upcoming offline-tech events

[Peer-to-Peer Web](https://peer-to-peer-web.com/) has a [Berlin hangout](https://peer-to-peer-web.com/berlin/2018-05-05) coming up.

## Local

Dhruv Mehrotra's [OtherNet](http://othernet.xyz) in Bedstuy and Bushwick.

[Hyperboria](https://docs.meshwith.me/) has resources on "meshlocals."

