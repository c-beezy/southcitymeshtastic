# Concept of Operations

This will try to explain the the whats, whys, and hows of this project with more specifity than the READMEs but less wonkiness than the technical docs.

## Basic Principles

The network we are building (ZSNet) will be a [LoRa-based](https://en.wikipedia.org/wiki/LoRa) [mesh network](https://en.wikipedia.org/wiki/Mesh_networking) made with cheap devices running [Meshtastic](https://meshtastic.org/docs/introduction/). We (the ZSNet network owners/admins) will build, configure, and deploy these devices around town to expand the mesh network so that they can talk to each other and as many people as possible.

We will configure our devices to work in the same frequency slot as the default Meshtastic configuration so that it interoperates with everyone running Meshtastic handheld devices in their default configuation. ZSNet will be a public service, and this maximizes the number of people who can see and use it.

The mesh nodes we deploy should be build to withstand outdoor conditions in Missouri. This means baking in the sun, plenty of rain, plenty of ice, along with some high winds and hail. Sturdy waterproof enclosures are a must.

We want ZSNet to remain operational during emergencies, which means they must be indefinitely self-powered. Right now, this means they should be solar-powered with a generous battery backup. The nodes should have enough reserve power to survive at least a week of no power, to account for snow/ice covering a solar panel, or wind/hail damaging the panel.

## Mesh Concepts:

We want the mesh to be as good as possible as cheaply as possible. LoRa will go 10 miles or so with line-of-site, but like any UHF radio, terrain and foliage will quickly attenuate the signal below the noise floor. This means putting devices outside, as high up in the air as possible so they get maximum coverage. We want our nodes on top of flat roofs on geographic high points, or better yet on towers if at all possible. (I will personally pay anyone a hundred bucks if they can get a node on the roof of the bank building at Grand & Gravois).  There are some good free radio analysis tools availble for calculating line-of-sight coverage distances for installations available:

- [RF Line of Sight](https://www.scadacore.com/tools/rf-path/rf-line-of-sight/)
- [Path Profiler](https://www.heywhatsthat.com/profiler.html)
- [Path Profiler for multiple radios](https://www.scadacore.com/tools/rf-path/rf-line-of-sight-for-multiple-radios/)
  
The initial sites for our nodes will probably necessarily be "on top of the houses of people willing to build nodes" but since its as yet undetermined who will build nodes, no projected mesh map is available at this time.

Meshtastic networks are self-organizing and self-healing once nodes are given an initial config, so our ongoing maintenance work should be limited to making sure they are still charging properly. The goal is for the node telemetry and health to be available via the LoRa mesh, over an encrypted channel and admin function, so the only time we need to physically touch the node is to update firmware or perform a hardware repair (which will hopefully be a relatively rare occurence)

Since we are going to be configuring our nodes on the [default frequency slot](https://meshtastic.org/docs/overview/radio-settings/#north-america-frequency-bands) for Meshtastic, our nodes should automatically mesh with any other Meshtastic nodes. This will extend our network as well as theirs, making all boats float with the rising tide.

## Mesh Channels, public and private.

In Meshtastic, the concept of a [Channel](https://meshtastic.org/docs/configuration/radio/channels/) exists somewhere between a digital radio talkgroup and a chat channel. It is defined not by frequency but by name and encryption key. Meshtastic nodes will happily forward any and all packets they receive regardless of whether they can be decrypted locally. This means that any device on a given frequency slot can work with any other device on that frequency slot, but only the end-user devices that have the pre-shared key for a given channel can decode them.

The upshot of this is that it allows ZSNet nodes to serve the public for whatever they want to do with Meshtastic, while simultaneously also enables ZSNet (and more generally all Meshtastic) users to configure their own chat channels with their own keys for more private communications.

## Mesh Management

Meshtastic allows for remote management of mesh nodes via the LoRa mesh, with commands authenticated via public-key encryption. All Meshtastic nodes generate a unique key pair.  Nodes that will be managed remotely can be given a list of public keys for Meshtastic devices that are allowed to send remote commands to it. This security is augmented by using a private pre-shared key for the "Primary" channel of nodes on our network, to keep administrative and telemetry data out of the public datastream. This security model is by no means perfect, but with some good planning the risks can be mitigated to acceptable limits.

