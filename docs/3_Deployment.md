
* * *
Back to [README](../README.md) at root of the Repo. 
* * *

# How to Deploy the homedig2 solution?  

## Docker Images   

The solution is deployed using several docker containers, some as a joint service. Our's is deployed on a RaspberryPi 3B+, as at writing of this document, we use the following images on http://hub.docker.com :

|# | For ...     | Image                    | More Info     |
|--|-------------|--------------------------|---------------|
|1 | mqtt server | eclipse-mosquitto:latest | mqtt          |
|2 | homeBridge  | oznu/homebridge          | opensource Apple HomeKit server |
|3 | Node-RED    | nodered/node-red         | it's obvious ... 8-) |

## 3 x Docker Containers using Node-RED image   
We fire-up three instances of Node-RED using Docker Services:

|#| Docker Container | Purpose   |
|-|------------------|-----------|
|1| home_dig2base    | The base homedig2 system, as per the [interaction diagram](1_homedig2_how.md). 
|2| home_dig2test    | All the events to test all aspect of the base system.
|3| home_dig2custom  | All the non-generic stuff, in our case we have a sprinkler system here.

## How we install & maintain the solution   
We use the opensource version of [Ansible](http://ansible.com) to configure and setup the full system. IoTPlay have published a zsh-based menu script (new on macOS Catalina - replaced bash) to envoke the ansible playbooks - which configures the full system. 

<details>
  <summary> See the menu we use to configure & manage the full system - expand this view... </summary>   

```
==== MENU SYSTEM: 12) IoTPlay-Digital Twin (homedig2_v021)---, with inv_limit:[Prod_rhome], menu host: [rh02.home.lan] ===============
0 : Passphrase for the ssh id_rsa
1 : MENU: Change to menu (1) - Home (homedig2 v021)
2 : Edit the inventory_limit variable, inv_limit:[Prod_rhome]
3 : 
4 : Mosquitto: PREP in files /opt/iotplay/rhm_mqtt
5 : Mosquitto: DEPLOY Mosquitto
6 : Mosquitto: REMOVE for RouxHome
7 : 
8 : HomeBridge   : BUILD & DEPLOY oznu
9 : HomeBridge   : Stop
10 : HomeBridge   : DEPLOY oznu
11 : Homebridge   : rh02.home.lan:8080 (login: admin/admin), 2) edit Config - add mqtt platform, 3) add plugin Homebridge Mqtt, 4) restart server
12 : 
13 : homedig2: Copy iotp Settings to Host
14 : Docker Services: Start Node-RED homedig2 (base, test, custom)
15 : Docker Services: Remove Services
16 : 
17 : 
18 : 
19 : 
20 : Web: Open Node-RED homedig2 BASE   UI    sites on rh02.home.lan:1890
21 : Web: Open Node-RED homedig2 BASE   Admin sites on rh02.home.lan:1890
22 : Web: Open Node-RED homedig2 TEST   Admin sites on rh02.home.lan:1891
23 : Web: Open Node-RED homedig2 CUSTOM Admin sites on rh02.home.lan:1892
24 : 
25 : 
26 : PREP: Setup~ Create folders, Copy iotp_conf, Start Docker Services, Edit Node-RED settings.js, Restart Docker
27 : PREP: Create Folders .../iotplay/homedig2base/data/projects/   (to copy secret keys)
28 : PREP: Create Folders .../iotplay/homedig2test/data/projects/   (to copy secret keys)
29 : PREP: Create Folders .../iotplay/homedig2custom/data/projects/ (to copy secret keys)
30 : PREP: Clone NR projects from bitbucket from within Node-RED admin clients, in sites opened, (add on pallette: node-red-dashboard)
----------------------------------------------------------------------
..cmdline 1 = <1..x> - for the action.
----------------------------------------------------------------------

```
</details>

## Pre-requisites  
Some pre-req's to running a successful system:
- Setup your home's config files, see [2a_Setup_Homie.md](2a_Setup_Homie.md), and [2_Setup_HomeBridge.md](2_Setup_HomeBridge.md).
- Clone the 2x Node-RED code (not yet published!) - of homedig2, namely the BASE, and TEST sets. The 3rd one will be your custom code.

## Sample Ansible Playbooks    

Find an extract from an Ansible playbook which uses **docker_compose** command, to build the 3 Node-RED containers & the service. It uses several variables, contact us if you need explanations on them (we carry for instance install locations in an Ansible variables file, and the image to pull, etc.).   
<details>  
<summary>Expland here for Ansible playbook for the Docker Service...</summary>  

``` yaml
---
hosts: all

  tasks:

  # --(4ai)  ---- arm    ~ Docker Compose of Multiple Services | tags: dockerservices / setup -----
    - name: 4a. Docker Compose Start Services (base, test, custom) # docker_service was deprecated
      docker_compose:
        project_name: home #Short for Rouxhome, the prefix to the Services
        definition:
          version: '3'
          services:
          # --------- dig2base ---------------------------------------------------
            dig2base: # homedig2
              hostname: home_dig2base
              image: "{{image.nodered}}" # "{{image.nodered}}:{{archtag}}"
              environment:
                - NODE_ENV=PROD
                - TZ="Africa/Johannesburg"
                #- NODE_ENV_VER=0.1.33
              ports:
                - "1890:1880"
              expose:
                - 1880
              volumes:
                - '{{folder.apps}}/{{ clientVars.name }}base/data:/data' 
                # Does not work on Mac:
                # - /etc/localtime:/etc/localtime:ro
                # - /etc/timezone:/etc/timezone:ro
              #depends_on:
              #  - mqtt
              restart: always
          # --------- dig2test ---------------------------------------------------
            dig2test: 
              hostname: home_dig2test
              image: "{{image.nodered}}" # "{{image.nodered}}:{{archtag}}"
              environment:
                - NODE_ENV=PROD
                - TZ="Africa/Johannesburg"
                #- NODE_ENV_VER=0.1.33
              ports:
                - "1891:1880"
              expose:
                - 1880
              volumes:
                - '{{folder.apps}}/{{ clientVars.name }}test/data:/data' 
              #depends_on:
              #  - mqtt
              restart: always
          # --------- custom -----------------------------------------------------
            dig2custom: 
              hostname: home_dig2custom
              image: "{{image.nodered}}" # "{{image.nodered}}:{{archtag}}"
              environment:
                - NODE_ENV=PROD
                - TZ="Africa/Johannesburg"
                #- NODE_ENV_VER=0.1.33
              ports:
                - "1892:1880"
              volumes:
                - '{{folder.apps}}/{{ clientVars.name }}custom/data:/data' 
              #depends_on:
              #  - mqtt
              restart: always
      when: ansible_architecture == 'armv6l' or ansible_architecture == 'armv7l'
      #when: ansible_architecture == "x86_64"        
      tags:
        - dockerservices
        - setup
```   

</details>

If anyone wants to seriously use the Ansible playbooks & the menu structure to get homedig2 up and running, contact us.    


* * *
Back to [README](../README.md) at root of the Repo. 
* * *