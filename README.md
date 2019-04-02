# iotp_dig2

A digital Twin framework for running IoT devices.

## What is it?
IoTPlay's 'Digital Twin' for running the full life-cycle of a framework for the life-cycle of managing IoT devices The implementation is on Node-Red, with extensive use of Docker, the author runs this on Raspberry Pi's.

## Maintainer
Jéan Roux, <jean@iotplay.org>

## Why?

**YAIOTF ?** Yet another IoT Framework? What else were my options?
What problems did I have that I wanted to solve?

## Inspiration

    a. Running a Home Automation system for 3 yrs, and discovering the issues of implementing, and maintaining the system.  
    b. Amazon Web Services IoT Framework.  
    c. SAP's Leonardo IoT framework
    d. Efforts by different parties to standardize, like (homie)[https://homieiot.github.io]
    e. The inner workings of MQTT.

## Building Blocks

### Docker Containers of iotp_dig2

|#| Container Name|docker?| Ver    | Some Details
|-|---------------|-------|--------|--------------
|a|iotp_dig2      |y      | v0.0.7 |Required, 'almost' a generic framework. The registry, broker, shadow, rules engine.
|b|iotp_dig2Msgr  |y      | v0.0.1 |A subscribe-based messenger and bot with which to interact with the IoT shadow.
|c|iotp_coachdb   |y      | -      | a No-SQL db underlying the events, if history of the events are required for further analysis.
|d|iotp_HomeKit   |y      | v0.0.9 |Less of a framework to run Apple's HomeKit.
|e|iotp_mqtt      |y      | v1.0.0 |A broker.
|f|menu_ansible   |not yet| v0.0.5 |A menu system with which to drive Ansible, which which the management of the system is done.

### a. Building Block: iotp_dig2

```
1. Application Settings:   
    a. Registry
    b. Rules
    b. Settings
2. In-Memory Settings Lists
    a. Things Registry
    b. Things Shadow  
    c. Others
3. A Broker
4. A Rules engine
5. An IoT thing event generation tool for testing.
```

### Installation Pre-Requisites

|#|Pre-Req | Containers|a|b|c|d|e
|-|--------|-----------|
|a|Ansible |           |y|y|y|y|y
|b|Docker  |           |y|y|y|y|y
|c|github
|d|Telegram
