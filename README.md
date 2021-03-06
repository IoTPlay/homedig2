# homedig2 v.0.21 - the Homie aligned version.

A framework that creates a 'digital twin' representation of a home, and reduces the complexities of hand-crafting your own home automation solution (on Node-RED). This version has been upgraded to work with the [MQTT open source Homie](https://homieiot.github.io) standard, which was born from the frustration of interoperability, and service discovery in the open source home automation community.

## A. The purpose of homedig2 & the Homie standard.

The Purpose of `homedig2` is to make a non-homie standard IoT devices comply to homie compliant settings of the messages, in order to have a *digital twin* stored for your house's device & attribute states, for standardised reporting, and interaction with other platforms, like message-based apps.    

The `homedig2` platform, or `dig2` for short, standardizes the messages from your home non-homie comliant devices, stores all the messages into a `digital twin` of the attribute states, and interacts with other platforms.    

One platform built into dig2 is [HomeBridge](https://homebridge.io), an opensource platform for projecting your house onto [Apple's Home](https://www.apple.com/ca/ios/home/) application. 

## B. Why we built it, and how it works.

In the link below we cover the reasons, where the solution fits, the framework needs, its building blocks, architecture, the purpose of using the Homie standard - the problem it tries to solve, and the solution, how this solution will change edge processing, see the readme file [docs/1_homedig2_why.md](docs/1_homedig2_why.md). 

See building blocks interaction diagram below, and a discussion document on it [docs/1_homedig2_how.md](docs/1_homedig2_how.md).   

![Interaction Diagram](https://github.com/IoTPlay/homedig2/blob/master/docs/images/dig2_InteractionDiagram.png)   


## C. Setting up the initiating files.

For understanding Homie, and Apple's HomeKit integration with open source [HomeBridge](https://homebridge.io), see previous section. Go to the help on the iitiating **homedig2** settings files, go to [Setting up Homie](docs/2a_Setup_Homie.md) and [Setting up HomeBridge](docs/2b_Setup_HomeBridge.md). 

## D. Deployment of the Solution.   

The solution is deployed as several docker containers. For details see [docs/3_Deployment.md](docs/3_Deployment.md).   

## E. Standard Screens.

The great thing of using a standard like Homie for the incoming info from devices, is that standard reports vcan now be created for all information. See some examples [docs/6_dig2_AppScreens](docs/4_dig2_AppScreens.md). 

## F. The Code.
The code is not published yet, it is a Node-RED flow, implemented as a broker between devices and other platforms. We will still publish the Node-RED flows.

## G. Maintenance Status
.
1. Maintainer. Jéan Roux, <jean@iotplay.org>. Find a Trello board with the dev pipeline. [Trello IoTP dig2 Invite](https://trello.com/invite/b/yC1CnUMK/f45c720766ca0d44e7c28e3c00375494/iotp-dig2).

1. Issues are tracked in this GitHub repo, but a summary listed in [docs/7a_Issues.md](docs/7a_Issues.md). For release notes, see [docs/7b_ReleaseNotes.md](docs/7b_ReleaseNotes.md).

1. Future releases will include:   
    a. **dig2Msgr** using Telegram not completed yet. We have draft system working here.   
    b. **Rules Engine** not completed yet. Previous versions had working models.

## H. Credits

- The fantastic community at https://discourse.nodered.org for all the help.

- For the ideas and subflow on having a syslog front-end, from Chris in Berlin https://github.com/Christian-Me/node-red-contrib-home/tree/master/Node-RED/syslog




