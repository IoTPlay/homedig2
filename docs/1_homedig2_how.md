* * *
Back to [README](../README.md) at root of the Repo. 
* * *
 

# homedig2 v.0.21 - the Homie aligned version

## A. How the system works

See below an interaction diagram, which represents the Nore-RED flows and how the components interacts with one another.  

![Interaction Diagram](../images/dig2_interactionDiagram.png)    


|No  | Description |
|----|-------------|
|A1a | Mqtt msg, in more-or-less homie format from homie compliant devices, or esp_easy |
|A1b | Mqtt msg, not in homie format, even with json inbound msg’s, on it’s own mqtt topic
|A1c | For some device/node events, an inbound msg in homeBridge json format, to drive complex interactions between homeBridge and property. (how does dig2 storage get updated?)
|2a  | Non-homie compliant msgs, then gets transformed to homie format first
|2b  | Homie compliant msgs are packed into an internal dig2 msg which then either creates or updates the homie Shadow on NR global context.
|3   | NR msg to update the Dashboard (future V. – add an http endpoint for reporting to other tools)
|4a  | Event 2b) that cr/upd the homie Shadow, also triggers a homeBridge understood msg, if cfg_vars.eventsToHomeKit is set.
|4b  | Devices that talks directly to homebridge/to/set goes directly to homeBridge server, such devices has to send a 2nd msg to also update the homie Shadow.
|B1  | Apple Home events – translated back to devices messages, device resp to report changes state of a property back to homedig2.
|E1,2,3| Yaml files which configures the homedig2 system.
|C&D | Not implemented yet. Rules engine requires changes to homieShw – to also store the previous state.



### B. Advise for Edge Processing
To be completed. Here we add how to setup in ESPEasy & others for dig2 to work.

<details>
    <summary>Expand for the assitance on configuring ESPEasy Rules, others.</summary>

#### ESPEasy:
  
  - For instance, to pubish to mqtt from ESP Rules:   

    ```
    on GateClosed#Status=1.00 do    // door closed
      CurrentDoorState,1
      Publish homebridge/to/set,{"name":"ESP66.Gate1.relay","service_name":"Garage Door","characteristic":"CurrentDoorState","value":1}
    endon

    ```

#### Other?

</details>



* * *
Back to [README](../README.md) at root of the Repo. 
* * *
 