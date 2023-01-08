By default, Cisco's switch have a VLAN 1 as a default vlan. We use `show vlan` to show the list of vlans.
### Create VLANs
To create a VLAN : 
```
S1> enable
S1# conf t
S1 (config) vlan 10
(config-vlan) name Engineering
(config-vlan) exit
```

We can also create multiple vlans at once `vlan 10,20,30` 

We can assign IP address to each VLAN (we need to do this on each switch)

```
int vlan 10
(config-if) ip address <ip-adress> 255.255.255.0
```
It's recommended to give a default gateway IP address for the switch. 

### Using a VTP server and client:

Using a VTP server allow us to create VLANs and modify them on one swicth (the vtp server) and share that config to other switches (vtp clients).

**Server mode :**

```
S1(config)#vtp mode server 
Device mode already VTP SERVER. 
S1(config)#vtp domain Lab2 
Changing VTP domain name from NULL to Lab2 
S1(config)#vtp password cisco 
Setting device VLAN database password to cisco S1(config)
#end 
```
Then we create the VLANs on the switch that is in server mode, these VLANs will be replicated on other switches which are in VTP client mode.

**Access mode :**
```
S1(config)#vtp mode client 
Device mode already VTP Client. 
S1(config)#vtp domain Lab2 
Changing VTP domain name from NULL to Lab2 
S1(config)#vtp password cisco 
Setting device VLAN database password to cisco S1(config)
#end 
```

### Acces port configuration

For a normal access (switchport access) (interface gi0/0/0 as example) :

```
int gi0/0/0
(config-if) switchport mode access
(config-if) switchport access vlan <id>
(config-if) end
```
Of course, we need to run this command for each switch. 

### Trunk and native vlan :

A trunk is a link to connect two switches together that will transfer VLANs info between the switches. The link use a 802.1q standard. To configure a trunking port:

```
int gi0/0/5
(config-if) switchport mode trunk
(config-if) switchport trunk native vlan 99
```

In this case, untagged frames will belong to VLAN99 which is the native vlan. We need to reconfigure the trunk port on the 2nd switch.

### InterVLAN routing :

We can create subinterfaces for a port in the router, this way it can play the role of multiple ports, each subinterface will carry frames of a given vlan, we need to assign an IP address for each subinterface and 
then make them dot1q aware (so they use 802.1q encapsulation). 
```
int fa0/0.1
(conf-subif)encapsulation dot1q <vlan-id>
(conf-subif)no shut
(conf-subif)ip address <ip-address> 255.255.255.0
```

Note that the ip address must be in the same network as the vlan ip address. 




