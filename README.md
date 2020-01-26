# iotp_dig2 v.0.2 - the Homie aligned version

A framework which creates a 'digital twin' representation of a home, and reduces the complexities of running the full solution. This version have been upgraded to work with the [MQTT open source Homie](https://homieiot.github.io) standard.

## A. The purpose of iotpdig2 & the Homie standard

The Purpose of `iotpdig2` is to make a non-homie standard comply to homie compliant settings of the messages, in order to have a *digital twin* stored for your house's device & attribute states, for standardised reporting, and interaction with other platforms, like message-based apps.    

The `iotpdig2` platform, or `dig2` for short, stanrdizes the messages from your home non-homie comliant devices, stores all the messages as a `digital twin`, and interacts with other platforms.    

One platform built into dig2 is [HomeBridge](https://homebridge.io), an opensource platform for projecting your house onto [Apple's Home](https://www.apple.com/ca/ios/home/) application. 

## B. Why we built it

For the reasons, where it fits, the framework needs, its building blocks, architecture, the putpose of using the Homie standard - problerm and solution, how this will change edge processing, see the readme file [docs/1_iotpdig2_why.md](docs/1_iotpdig2_why.md). 

## C. Setting up the initiating files.

For understanding Homie, and Apple's HomeKit integration with open source [HomeBridge](https://homebridge.io), see previous section. Go to the help on the iitiating **iotpdig2** settings files, go to [Setting up Homie](docs/2_Setup_Homie.md) and [Setting up HomeBridge](docs/3_Setup_HomeBridge.md). 

## D. The Code
The code is not published yet, it is a Node-RED flow, implemented as a broker between devices and other platforms. We will still publish the Node-RED flows.

## E. Maintenance Status

### E1. Maintainer
Jéan Roux, <jean@iotplay.org>. Find a Trello board with the dev pipeline. [Trello IoTP dig2 Invite](https://trello.com/invite/b/yC1CnUMK/f45c720766ca0d44e7c28e3c00375494/iotp-dig2).

### E2. Big-ticket items & Outstanding for Next releases

For release notes, see [docs/5_ReleaseNotes/md](docs/5_ReleaseNotes/md). 

1. Completed from previous release:

    * **Self-Discovery of Devices & Things**. Completed this release. ~ "We will use the Homie mqtt self-discovery standard. [Homie - An MQTT Convention for IoT/M2M](https://homieiot.github.io). "

    * **Registry yaml** - in HomeKit - the `service` must be an array of required services, not just one service. Homie standars solves this !

    * Make it **Multi Client** so that the same framework can be hosted centrally for different clients? Solved.

2. **dig2Msgr** using Telegram not completed yet.

3. **Rules Engine** not completed yet.



