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

Some DAT projects:

[Fritter](dat://fritter.hashbase.io) is a prototype Twitter clone on DAT. No image support.

![](https://i.imgur.com/jupjifV.png)

[Rotonde](https://louis.center/p2p-social-networking/) is a social network built on DAT.

Used by a small community. Supports sharing images.

![](https://louis.center/p2p-social-networking/library.png)

Services like [Hashbase](https://hashbase.io/pricing) exist where you can pin DAT content for a fee.

### Scuttlebutt

Clients discover each other a LAN with multicast UDP and "gossip" the social network's data with other people they follow. Projects like [MinBase](https://github.com/evbogue/minbase) could form the basis for a simple and minimal server run by each rpi. [Patchwork](https://github.com/ssbc/patchwork) is a solid, themable client. All backpacks could, when they have internet access, join a specific [pub server](https://github.com/ssbc/scuttlebot/wiki/Pub-Servers) so that they know to sync with each other.

A major con would be that to be recognized as a unique "person" on Scuttlebutt, you'd need to run a client--i.e., if everyone whose phones are connected to a backpack uses its scuttlebutt instance, everyone is "posting" as the same identity. Not sure this is actually a problem for our use-case though...

![](https://github.com/ssbc/patchwork/raw/master/screenshot.jpg)

#### Raspberry Pi Installation

Currently no ARM7 binaries exist for an easy installation of Patchwork/SSB--there's an [issue
for that](https://github.com/ssbc/patchwork/issues/745).

There's also issues running electron apps with the newest version of
electron--[this thread](https://github.com/electron/electron/issues/10468) was
helpful in finding an electron version that actually worked.

Here's the install process:

```
# add github.com to known_hosts
ssh-keyscan github.com

# upgrade node and npm
sudo apt-get remove nodejs
sudo apt update
sudo apt full-upgrade -y
curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
sudo apt install -y nodejs
npm install -g npm

# increase swapfile size for compiling patchwork
sudo vi /etc/dphys-swapfile

# in the file above, uncomment the CONF_SWAPSIZE and make it read:
CONF_SWAPSIZE=1024

# modify package.json to use an older version of electron
vim package.json

# edit the "electron" entry in the "devDependencies" section to read
"electron": "~1.7.9"

# install patchwork
git clone https://github.com/ssbc/patchwork
cd patchwork
npm install
npm start
```

After a long time, patchwork should appear on screen. Unfortunately, it looks
like the CPU usage on my RPI 2 is pretty unusable. Connecting to a pub and
syncing messages, which usually takes a few seconds on a laptop, took 15+
minutes on the RPI.

Additionally, after digging into the source to see how feasible a "headless"
mode might be, where clients might be able to connect to a website and post
on behalf of the backpack, it looks like the code is pretty reliant on being
an electron-first app, instead of a hybrid app layering native functionality
on top of an HTML-first app.

I also saw that a more minimal SSB client called
[minbase](https://github.com/evbogue/minbase) was linked to from on the
patchwork github, so I tried installing that:

```
cd ~
git clone https://github.com/evbogue/minbase.git
cd minbase
npm install
npm run build
npm start
```

Unfortunately there were errors:

```
Error [ERR_HTTP_HEADERS_SENT]: Cannot set headers after they are sent to the client
    at validateHeader (_http_outgoing.js:503:11)
    at ServerResponse.setHeader (_http_outgoing.js:510:3)
    at /home/pi/Downloads/minbase/node_modules/decent-ssb/plugins/ws/json-api.js:23:11
```

I posted an [issue in their tracker](https://github.com/evbogue/minbase/issues/5).

So for now, SSB on rpi with an easy client is a no go.

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
