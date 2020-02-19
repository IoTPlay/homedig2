* * *
Back to [README](../README.md) at root of the Repo. 
* * *
 

# ISSUES

This page describes Open Issues, Smaller improvements to be done, and further big-ticket items, and links to Closed Issues. Also see closed issues - [7b_releaseNotes.md](7b_releaseNotes.md) and [7c_Requirements-Backlog.md](7c_Requirements-Backlog.md) for more details brought from previous releases.   

## Open Issues  

| Summary                     | Details |
|-----------------------------|---------|
|2020.02.16 :                 |         |
|Shelly2 statusses to dig2shw | for New shelly2 - does not save the status of the property val in dig2shw |  
|Shelly app not updating dig2 | mqtt msg inbound for the device from homekit does come into dig2core, but when activating from shelly app, the inbound mqtt creates errors.
| Previous releases :         |         |
| status update homeBridge    | ESP_Easy rules does not for instance update the status on homeBridge - although homeBridge compliant mqtt message is sent.



## Smaller Improvements to be done    

|No| Summary  | Details |
|--|----------|---------|
|1.|**homedig2 to enable shelly CoaP** | Instead of using mqtt, which dis-enables that device's use on the http://my.shelly.cloud app; also provide a framework option to rather use the shelly CoaP capability, to both actuate and read statusses off the devices, instead of mqtt, (most components exists). |
|2.|**Reporting http endpoints** | Rather than only our own Dashboard - make the reports available as http endpoints, for the user to build reports in other tools. |


* * *   
## Big-ticket items & Improvements for future releases  

Big-ticket future building blocks like the **rules engine**, and the **homedigMsgr**, still to be refactored from previous releases.

## Closed Issues      

Moved to [5_ReleaseNotes](7b_ReleaseNotes.md).   