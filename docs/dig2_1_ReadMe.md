# Settings files to Setup your dig2 home's Devices & Things.

The Purpose of `iotpdig2` is to make a non-homie standard comply to homie compliant settings of the messages, in order to have a *digital twin* stored for your house's device & attribute states, for standardised reporting, and interaction with other platforms, like message-based apps.    

The `iotpdig2` platform, or `dig2` for short, stanrdizes the messages from your home non-homie comliant devices, stores all the messages as a `digital twin`, and interacts with other platforms.    

One platform built into dig2 is [HomeBridge](https://homebridge.io), an opensource platform for projecting your house onto [Apple's Home](https://www.apple.com/ca/ios/home/) application.   
 

## What does the settings do and Why?

### The Problem

- We were looking for a standard way to bring IoT information to a platform, such that this standard can be used to standardise reporting, and interaction with other platforms. After building the first version of this, which my house ran for more than 7 months, I found the [MQTT open source Homie](https://homieiot.github.io) standard, "An MQTT Convention for IoT/M2M", which was exactly what I wanted. Now I did not have to think out about how to ove my standard forward, but could collaborate with others.

- However, after trying for 6 months beginning of 2019 to convert my current fleet of devices [Shelly](https://shelly.cloud), and ESP8266's flashed with [ESPEasy](https://espeasy.readthedocs.io/en/latest/), and a few others like my alarm, etc, I realised that the move to homie standards-based messages fro mdevices are not going to convert fast. 

### The Solution    


1. The homie standard, now at version 4, structures the messages that flows from the devices through mqtt to homie standards-based brokers. Dig2 (for digital twin) attempts to be one, not all the homie 4.0 standards have been implemented.   

1. I realised I need a mechansism to receive any form of mqtt message, and have a broker that can convert the message to a homie compliant format. Then use this message to store it in Node-RED context memory, or to go further and stick it into for instance couchDB. From here - reporting can be standardised, plus interactions with other systems, like the iotplay messager - based on Telegram and others.   
