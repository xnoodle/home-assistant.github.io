---
layout: page
title: "Broadlink RM Switch"
description: "Instructions how to have Broadlink RM switches."
date: 2016-11-22 22:41
sidebar: true
comments: false
sharing: true
footer: true
logo: broadlink.png
ha_category: Switch
ha_release: 0.35
---

This `Broadlink` switch platform allow to you control Broadlink RM2 Pro and RM mini IR+RF [devices](http://www.ibroadlink.com/rm/).

To enable it, add the following lines to your `configuration.yaml`:

```yaml
# Example configuration.yaml entry
switch:
  platform: broadlink
  host: IP_ADDRESS
  mac: 'MAC_ADDRESS'
  switches:
    reciever:
      command_on: 'switch_packet on'
      command_off: 'switch_packet off'
```

Configuration variables:
- **host** (*Required*): The hostname/IP address to connect to.
- **mac** (*Required*):  Device mac address.
- **timeout** (*Optional*): Timeout in seconds for the connection to the device
- **switches** (*Optional*): The array that contains all switches.
  - **identifier** (*Required*): Name of the command switch as slug. Multiple entries are possible.
    - **friendly_name** (*Optional*): The name used to display the switch in the frontend.
    - **command_on** (*Required*): Base64 encoded packet from RM device to take for on.
    - **command_off** (*Required*): Base64 encoded packet from RM device to take for off.



How to obtain IR/RF packets?

Choose Call Service from the Developer Tools. Choose the service broadlink/learn_command from the list of Available services:  and hit CALL SERVICE. Press the button on your remote with in 20 seconds. The packet will be printed in the log and as a persistent notification.


Example config:

```yaml
- platform: broadlink
  host: 192.168.1.2
  mac: 'B4:43:0D:CC:0F:58'
  timeout: 15
# Will work on most Phillips tvs:
    tv:
      friendly_name: "Phillips Tv"
      command_on: 'JgAcAB0dHB44HhweGx4cHR06HB0cHhwdHB8bHhwADQUAAAAAAAAAAAAAAAA='
      command_off: 'JgAaABweOR4bHhwdHB4dHRw6HhsdHR0dOTocAA0FAAAAAAAAAAAAAAAAAAA='
      
# Will work on most LG tvs
    tv_lg:
      friendly_name: "LG Tv"
      command_on: 'JgBYAAABIJISExETETcSEhISEhQQFBETETcROBESEjcRNhM1EjcTNRMTERISNxEUERMSExE2EjYSNhM2EhIROBE3ETcREhITEgAFGwABH0oSAAwzAAEfShEADQU='
      command_off: 'JgBYAAABIJISExETETcSEhISEhQQFBETETcROBESEjcRNhM1EjcTNRMTERISNxEUERMSExE2EjYSNhM2EhIROBE3ETcREhITEgAFGwABH0oSAAwzAAEfShEADQU='

    tv_lg_HDMI1_HDMI2:
      friendly_name: "LG Tv"
      command_on: 'JgBIAAABIZMRExITEjYSExMRERURExEUEDkRNxEUEjYSNhM3ETcSNxITETgSNhI2ExMQExE4ETYSNxIUERMSExE4ETcRFBETEQANBQ=='
      command_off: 'JgBQAAABJJMSEhISETgSEhITEBMSEhMSETcSNxMREjcSNxI3EjcSOBETERITNhM2EhITERM2EzcRNxI3ExISEhI3EjcRExETEgAFLQABJEoRAA0FAAAAAAAAAAA='
      
    tv_lg_HDMI3:
      friendly_name: "LG Tv"
      command_on: 'JgBIAAABIZMSFBISETgRExEUERQQFBETEjcTNhMSETgRNxE3EjcROBM2ERMSFBE4ERMSNxM2EjUSFBE2ETgRExM2ExITEhATEwANBQ=='

    tv_lg_AV1_AV2:
      friendly_name: "LG Tv"
      command_on: 'JgBIAAABIpQPFBITETgSEw8UEhQSEhEVDzgSOBAUETgQOQ84EjgRNxITETgSExA5EDgREhI3EhMROBMSEDkQFBETEjYTEhE4EQANBQ=='
      command_off: 'JgBIAAABH5YPFBETETgUERAUEBURFBATETgROBEUETcSNxE4ETcSOBISEBUQFREUEjUSFBA5ETcRNxE4ETkQOBAUEjcRFRAUEQANBQ=='
``` 
