We can see spanning tree informations through the following command : 

```
sh spanning-tree
```

We can run this on multiple switches to know which one is the root. The root bridge is the one having the lowest bridge ID using this formula :

Bridge ID = Bridge Priority Number + Sys Extension + Lowest MAC Address

Note that by default, a spanning tree instance will be created for each VLAN.

We can also see the different events for the spanning tree through this command : 

```
debug spanning-tree events
```

This command will show three event : listening, learning, forwarding.
