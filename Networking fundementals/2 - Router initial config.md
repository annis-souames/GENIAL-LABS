To configure a router, it's the same commands as a switch. By default routers have most of their interfaces shutdown so we need to activate them. 

```
Router> show ip int brief
```

Will give us a brief summary of the available interfaces on the router. 

To configure an interface we need to be in terminal config mode: 

```
en
conf t
(conf) int gi0/0/0
(config-if) ip address <ip-address> 255.255.255.0
(config-if) no shut
```

Note that the subnet mask in a router interface cannot be 255.255.255.255. We can repeat the same procedure for each router interface or we can use a range command : 
`int range gi0/0/0-1`

Also note that the IP address used in the router interface (or native subinterface) should be used as a default gateway on the switch. 

We can copy router config like a switch using `copy running-config startup-config` 
