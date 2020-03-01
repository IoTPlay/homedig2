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
|Action:                      | Capture the message before the homedig2 is set from Shelly2 - then look why the code overwrites this.
|Shelly app not updating dig2 | mqtt msg inbound for the device from homekit does come into dig2core, but when activating from shelly app, the inbound mqtt creates errors.
| Auto-change for Rpi vs x86  | in  /homedig2_v021/0.504_Prep-Server_NR.yml |
| Add security to end-points  | @ base_1 for /dig2/devices & nodepropvals
|                             |         |    
| Previous releases :         |         |
| status update homeBridge    | ESP_Easy rules does not for instance update the status on homeBridge - although homeBridge compliant mqtt message is sent.


## Closed Issues      

Moved to [5_ReleaseNotes](7b_ReleaseNotes.md).   