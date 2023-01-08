## Introduction

To configure a swicth we use a serial cable from the serial port of one computer and plug it in the console port of the switch. Specifically, in GENIAL lab we need to connect it tothe cabine that connects all computers and from there connect the pc number in the main cabinet to one of the other cabinets (France, Russia, Finland or Sweden).

### Connecting to the switch : 

To connect to the switch console, we use PuTTy (SSH, Serial and Telnet client), we then get access to the switch console in user mode. We might need to enter a password to get to this mode. 

We can write `?` to get a list of commands available in user mode ordered alphabetically. To enter the "All-previlege mode" we can write `enable` or `en` for short, this might ask us for a password a second time. We can also use tab key to autocomplete a command, *spacebar* to all output and *enter* to 

### Reloading the switch :

In order to reload the switch we need to :
- Delete the vlan database
- Erase the startup-config
- Reboot the switch software (reload) -> this operation can take some time, between 10 to 20 minutes.
  
  ```
  Switch# enable
  Switch# delete flash:vlan.dat
  Switch# erase startup-config
  ```
In both steps we just press enter every time (to select the default options). Now we enter into the terminal config mode (global config) so that we reload the switch software : 

``` 
Switch# conf ter
Switch (conf) # reload 
```
In the reload command, press 'n' or 'no' when it asks : "System configuration has been modified, do you want to save it". This command will take sometime to reload.

### Renaming the switch

We can also rename a switch using the hostname command like this in terminal config mode : `host S1` to change it's name to S1. 

### Saving a configuration:

To save a configuration, we copy the config from RAM of the switch (the current configuration) called `running-config` and copy it in the hard drive (NVRAM) of the switch in a special file named `startup-config`, the command is :

Switch# copy running-config startup-config




