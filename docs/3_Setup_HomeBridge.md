Back to [README](../README.md) at root of the Repo. 


# For HomeBridge : Understanding the Settings of dig2  


**About the folder structure - MyHome, and others** .   

1. This document can be viewed under the dig2 client, but also at the location: `/opt/iotplay/<3cld>_dig2/projects/Prod/Docs` where <3cld> defaults to `myh` for `my home`, but can be replaced by 3 letters which identifies the client, for cases where more than one client is hosted on the same host.    

1. In this document where the pre-letters `myh` to a folder is used, this rule applies.

1. [HomeBridge](https://homebridge.io) comes preinstalled with dig2 in this version. (We maybe latero n make it a seperately installable product, for those not on Apple). **homeBridge** requirs a seperately installed broker running on Docker, accessable by the host this is running on.

## Setting up the dig2 settings files


### Folders Locations
- `/opt/iotplay/myh_dig2/projects/Prod` : The folder where dig2 Node-RED flows will install, instance Production.
- `/opt/iotplay/myh_dig2/iotp.conf`     : The settings for the house <myh>. 

### The File names  

- Settings files for `Homie`. To assist with configuring your Home in the homie standard.
    - `homieClientSetup.yml`: For setting up your IoT devices - in cases where self-discovery standards are not complied to by the device, and even if it does, you can create etra meaning per the homie standard in this file.
    - `homieTransforms.yml`: Transforms mqtt messages from non-homie appliances to the *homie* standard.

- Settings files for `homeBridge`. 

* * * 

### The Settings Files 

#### 1. Setting up your dig2 twin with <homieClientSetup.yml>

A yaml file, with which to create all the attributes in the `dig2 digital twin` about your devices. Each line is transferred into an MQTT message, and sent into the `dig2Homie` engine, to build the digital twin. This is a once-off event, or as you want to make changes.

Actioning the changes you made to this file, is done from the **Setup* screen, * 

``` yaml
---

# -------- Additional home Details ----------------------------------   
homieClientSetup:

  # Device Names <$name>---------------------------------------------    
    homie/ESP62/$name:                  Sprinkler System & Outside Air

  # Devices Mac Addresses <$mac>-------------------------------------
    homie/ESP62/$mac:                   "18:fe:34:cf:54:26"

  # Devices IP Addressses <$localip>---------------------------------
    homie/ESP62/$localip:                 192.168.1.42

  # Device Implementations <$implementation>-------------------------
    homie/ESP62/$implementation:         ESP_Easy

  # Node Names <$name>-----------------------------------------------
    homie/ESP62/Air/$name:               Kitchen Quad Air

  # Attribute Properties: Unit <$unit>------------------------------- 
    homie/ESP62/Air/Temperature/$unit:   "°C"
    homie/ESP62/Air/Humidity/$unit:      "%"
    homie/ESP62/Leg1/Relay/$unit:        "on/off"

  # Attribute Properties: settable? <$settable>----------------------
    homie/ESP71/Light/Switch/$settable:  true

  # Attribute Properties: Names of Thing Property <$name>------------
    homie/ESP62/Leg1/Relay/$name:        Sprinkler Leg-1

  # How to talk back to Devices with MQTT <$mqttToDevice> -----------
    homie/ESP71/Light/Switch/$mqttToDevice:    espeasy/ESP71/gpio/12

```


#### 2. homieTransforms.yml 

A yaml file, which transforms incoming MQTT messages from devices, and transforms them to make them [homie standard](https://homieiot.github.io) compliant.

``` yaml

---

transformToHomieTopic: # fromDevice
# instructions: If payload_from must go as-is to payload_to, do not map, else map in equal length array.
# example:
#      payload_from: [true,false]
#      payload_to  : [ready,lost]

    - shellies/shelly1-058DDF/online:
        payload_from: [true,false]
        payload_to  : [ready,lost]
        mqtt_to     : homie/shelly1-058DDF/$state

    - "Paradox/Zone/TV-Room_PIR":
        payload_from: [CLOSED,OPEN]
        payload_to  : [false,true]
        mqtt_to     : "homie/Paradox/Zone/TV-Room_PIR"

transformHomeBridgeToDevice: #after converted by function with same name...

    - homie/ESP62/Leg1/Relay/set: 
        payload_from: [1,0]
        payload_to  : ["event,L1","event,allsprinkleroff"]
        mqtt_to     : espeasy/ESP62/cmd

    - homie/shelly1-24D051/relay/Light/set: 
        payload_from: [true,false]
        payload_to  : ["on","off"]
        mqtt_to     : shellies/shelly1-24D051/relay/0/command

#----- Known do not use ----------
    - home/OpenMQTTGateway/version:
        mqtt_to     : homie/ziotp/knowndoNotUse

transformJSONtoHomie:
# jsonInEx means: Example incoming json
    - home/OpenMQTTGateway/SYStoMQTT:
        jsonInEx    : {"uptime":7472,"freeMem":42560,"rssi":-42,"SSID":"TheStorm","modules":"SRFB"}
        mqtt_to     : [
                        homie/OpenMQTTGateway/$stats/uptime,
                        homie/OpenMQTTGateway/$stats/signal,
                        homie/OpenMQTTGateway/$stats/freeheap,
                        ]
        json_in     : [
                        uptime,
                        rssi,
                        freeMem
                        ]

# ----- TODO -----------
notMappedYet:
    -  home/OpenMQTTGateway/version: (must go to /$fw/version)

# ==================================================
transformDeviceToHomeBridge:
# not working, one msg should be able to go to 2 msg's, thus rather take msg's to ESP rules.
#    - espeasy/ESP62/Leg1/Relay:
#        payload_from: ["0","1"]
#        payload_to  : [{"name":"ESP62.Leg1.Relay","characteristic":"InUse","value":0},{"name":"ESP62.Leg1.Relay","characteristic":"InUse","value":1}]
#        mqtt_to     : homebridge/to/set

# ========= from HomeBridge to Device ==============

```

* * * 

## Initiating, Changing your dig2Twin

After you made changes to your setup files, the steps to get the dig2Twin to accept them. Changes are made from the Setup screen.   


![Setup Screen](images/dig_2setup.png)   


