* * *
Back to [README](../README.md) at root of the Repo. 
* * *
 

# Next Release to RouxHome Prod:

### Working On:

- NEXT:

- BUSY with:

    - Config / Test Homie sprinklers:
        - passing characteristic:inUse to homeBridge from Device - https://github.com/cflurin/homebridge-mqtt/issues/85 
            - via translator transformRules.yml 


### Backlog Todo's

- **backlog**: 
    - clean up sheet old "Broker" - remove & deprecate old stuff
    - Can firmware be brought in? ($fw/name / $fw/version)
    - not all Paradox eyes are firing ?
    - Incoming messages to enable (they have been blocked out in do not use translate file)
        - home/OpenMQTTGateway/version
    - Alarm - separate view to show history of alarm that was on.

- **Older**:
    - Upgrade to Homie 4.0 translator - see example from ESP_Easy under ../images/homie_4_mqtt msgs.png
    - When receiving json on val, show properly in Shadow, and Events. (ie. "val"{"CurrentDoorState":0, "TargetDoorState":0})
    - Broadcast ESP_Easy to get ea's IP to query for Homie.
    - Translate into dig2 protocol & store into dig2.Shadow:
        - [**dig2.Broker**] Translate _broker mgt._ events from RF Gateway to dig2.iotp protocol  
        - [**dig2.Broker**] Translate _trigger_ events from RF Gateway to dig2.iotp protocol
    - Add timestamp to /LWT/ or $state?
    - Transform ~ offline to lost. But what is online?
        ```
        - home/OpenMQTTGateway/LWT:
            mqtt_to     : homie/OpenMQTTGateway/$state
        ```
    - Broker - `State Machine` : from any actuation (homekit & other!), operate the garage door - make a state machine from this. Dynamic State Machine for Garage Gate.
    - **Fix**:
        - Format html of uptime report to #.##
        - Shadow time update - all the same?
    - Write (started allready) a startup script named **Test-System-Components** to check for all required settings:
        ```
        { cfg_lists: [sevMapRulesFields, notify, severity, actionTypeArr, homieAttributes_v301,
            homeKitServices], cfg_vars: "list of vars", homieCDev: [transformToHomieTopic, transformJSONtoHomie], homieShw}
        ```

- **Nice to Have**:
  - only refresh the dashboard when someone is logged in?
  - A mqtt channel where all errors are sent, with [from module, error description, severity, data that caused error]; then a db where the errors get published to, with a f/e to that db.
  - Admin screen - button to re-run homieClientSetup / delete the homieShadow
  - add an thing_approved flag - as new ones announce themselves to homieShadow - and gets included into the 'db', then only show on reports not approved.
  - create my own announce mqtt message for homie for ESP's

### Dev 25 Jan '20
- Moved /data/projects/Prod/code yaml settings files to /data/project/iotp.conf as a configuration settings folder, to get it out from underneath Git, so that changes can be made to settings without cloning the project fro bitbucket git.
- 4 x delete buttons on screen Setup Variables and 4 x Load buttons to relaod...
- Changed current screen **Setup** to **Setup_Help**

### 03 Jan '20
- Added have completed darksky api mechanism to check the rain - how much did, it, and how much going to.
- NOT COMPLETED.

### Dev 24 Sep'19
- Added transform rules device to homeBridge
- Added homeBridge translator & setup file
- Added homeBridge to homie .../set directive --> to device /cmd for ESP and /command for shelly
- Broker: from homeKit --> homie --> devices
    - done(homeKit rules in mqtt setup files: `homekitServices`), add - re **codeX** per prev model, shall we do unique code in mqtt settings?  
- a Broker for ~ `from HomeKit to a MQTT queue, back to Homie`:
    ```
    topic: "iotpHomeKit/command/Lig-10"
    payload: {"On":false}
    ```
- homie **Settable & set** using the ESP_Easy homie plug-in:
    - `homie/kitchen-light/light/power/set ← "true"` , then:
    - `homie/kitchen-light/light/power → "true"`
    - for ESPEasy - use the homie controller: https://espeasy.readthedocs.io/en/latest/Controller/C014.html?highlight=mqtt
    - flash **ESP_Easy with homie Controller** first, then the Set will work.
- Tested all lights from homeBridge
- homeBridge docker ansible install

### Dev 23 Jul'19
- Tested State machine simulations
- cleaned up Web interface
- changed alarm from 1/0 to false/true
- `Thing Status` dashboard node (rest still in DEPRECATED)- remove old, but have we got all to new? - yes.

### Dev 22 Jul'19 (late at night)
- added shellies announce to homie for ip, mac, state. still to be done = fw.
- added error reporting, tracking db still to be built on Broker.
- test & adjust non ESP & homie standards mqtt in messages & brokering. Added in file `tf_to_HomieRules.yml` a section to not use incoming messages, pointing to:
`mqtt_to     : homie/iotp/knowndoNotUse`

### Dev 22 Jul'19 (on Plane from Amsterdam)
- Fixed Cannot report to Dashboard this input - `device/node/property/attribute`   
- fixed: espeasy/ESP62/Air/Temperature/$name "Outside Temp" - `"TypeError: Cannot read property 'getDate' of undefined"`   
- adding error handling to reporting tool.
- Send empty string to Shados dashboard if empty
- homieClientSetup file under /code to setup the system, according to homie standards.
- Thing Shadow html - scroll only last x entries  
- deleted older homie broker functions:   
    - Cr/Upd Homie.Twin (arrays)   
    - Update homie Shadow old with homie obj   
- partially: homeKit rules in mqtt setup files: `homekitServices`
- moved DEPRECATED to its tab.
- clean up sheet "Twin" - remove & deprecate old stuff
- upgraded Twin Test-System-Components, moved 2ndto 4th start of Twin to DEPRECATED, moved remaining Startup to Setup sheet
- moved homie test battery from sheet ESP toTest homie

### DEV: 20 Jul '19 (on plane back from Canada)
- espeasy/ESP66/Air/$name "Environmental DHT22"
- espeasy/ESP66/Air/Temperature/$name "Outside Temp"


### Dev: 10 Jul '19 (on plane to Vancouver)
- Completed:
  - homie Test Data (ESP62)
  - homie Dashboard - can display Thing Shadow by cycling through homieShw global context

### Dev: 29 May:
- client_devices.yml
  - Ready array transformToHomieTopic, and transform incoming to outgoing topic and values for incoming topics:
    - home/OpenMQTTGateway
    - Paradox/
    - shellies/
  - filter out incoming shellies/announce topic (TODO - a list for filtering out.)
  - incoming stats from for instance home/OpenMQTTGateway is a json object with several indicators

### Dev: 21 May'19
- Build homieCDev `Homie client Devices` - translation of such incoming messages to homie txObj format
- Flow Broker-Homie:
    - '2|device-stats'    : homie/ESP70/$stats/uptime -> 6654             // done
    - '1|device'          : homie/ESP70/$state -> "ready".                // done

### Dev: 09 May 22:43
- Split Twin 1st stat in cfg's and reg.
- Added cfg_lists homieAttributes v301
- Added homieDeviceConvert file, code/client_devices.yml

### Dev: 09 May 00:10
- Changed ESP's:
    - espeasy/ESP70/LWT --> homie/ESP70/$state
    - espeasy/ESP70/System/Uptime --? espeasy/ESP70/$stats/uptime
        - multiplied minutes with 60 for homie compliance
- Changed 'Update homie Shadow' to new way.
    - new variables, when an Attribute, does not use the ID.  
- Changed global homie shadow.

### Dev: 29 Apr 01:12
- if arr is not empty, check if deviceId is present, if so, add $state, if not, add deviceId, and $state, 1st on Test Homie.
- espeasy/ESP66/System/Uptime
    - get Uptime espeasy in homie to work
    - one homie conversion
- homie_example.yml as test batch for how homie json would look like.
not done:
- new deviceId/$state function (not required as retained on ea deviceID will run 1st?)

### Dev: 22 Apr 20:15
- Testing tool - homie_example.yml external file with correct structure
- Successful added homie/ESP66/$state -> ready from espeasy/ESP66/LWT if object/array is empty

### Dev 22 Apr 19 01:05
- espeasy brough to homie
- Paradox messages in.
- homie-like discovery & Shadow.

### Dev: 17 Apr 23:35
- Added cfg_vars.eventsToDig2Twin false / true. // for controlling if events should be sent to dig2Twin, in Broker.
    - Events from Shellies, ESPEasy, iotpDig2 controlled with cfg_vars.eventsToDig2Twin.
- Added eventsToDig2Twin control from dig2Iotp events stream to HomeKit in Broker.

### Dev to Bitbucket 14 Apr 19 15:36 gmt+2:
- When receiving json from ESP: ie. "val"{"CurrentDoorState":0, "TargetDoorState":0}, process & send to HomeKit
  - timestamp x 1000 received from %unixtime%
- removed `gat-1a` from Registry, not required anymore, and Change node for that.

### Dev to Bitbucket 14 Apr 19 01:52 gmt+2
- Added ESPEasy LWT
- Implemented Homie for ESP_Easy, by reading the /json endpoint (not for Tasks yet)
- Prepared msg from RF gateway into a json formatted message, ready for translation into dig2 iotp protocol?
  - [**dig2.Broker**] Translate _broker mgt._ events from RF Gateway to dig2.iotp protocol  
  - [**dig2.Broker**] Translate _trigger_ events from RF Gateway to dig2.iotp protocol

- Naming convention of Flows & flow descriptions
- Formatting changes to flows

### To Bitbucket @ 2019.04.12 22h50:

- [dig2.Broker]: home/OpenMQTTGateway/ - seperate uptime. LWT, version, /SRFBtoMQTT into own msg's.
- [dig2.Broker]: Added Broker mqtt in: home/OpenMQTTGateway/#
- [dig2.Registry]: Added OpenMQTTGateway to Registry
- [dig2.Broker]: iotp msg --> HomeKit: filter out HomeKit = N/A
- [dig2.Twin]: - Event Date on Web, TX problem. : Solutions was JSONata [z] , +0200, could be an issue if used in another TZ.

* * *
Back to [README](../README.md) at root of the Repo. 
* * *
 