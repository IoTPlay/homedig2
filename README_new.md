# Readme for the New dig2 based on Homie


|#|mqtt_in                     | Store as global context                     |
|-|--------------------------- |---------------------------------------------|
|1| espeasy/ESP70/Light/Switch | homie/ESP70/$nodes/Light/$properties/Switch |


## Storing in a JSON object & array structure
|#|mqtt_in                     | Array1 | Obj1 | Array2 | Obj2  | Array3   |Obj3   |
|-|--------------------------- |--------|------|--------|-------|----------|-------|
| |                            |        |      |$nodes  |       |$properties|      |
|1|espeasy/ESP70/LWT           | ESP70  | X    | X      | $state| X        |X      |
|1|espeasy/ESP70/System/Uptime | ESP70  | X    | X      | $stats| X        |uptime |  
|2|espeasy/ESP70/Light/Switch  | ESP70  | X    | Light  | X     | Switch   |X      |
|3|espeasy/ESP70/Air/Humidity  | ESP70  | X    | Air    | X     | Humidity |X      |
