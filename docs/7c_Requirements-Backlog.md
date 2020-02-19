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
