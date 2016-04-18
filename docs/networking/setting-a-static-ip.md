Disable the auto-magic ```network daemon```

```
adrian@openindiana-hipster:~$ sudo svcadm disable physical:nwam
```

Define in your IP/hostname ```/etc/hosts```, if not already, an entry for this host. For example:

```
192.168.1.22 hostname hostname.local localhost loghost 
# Subsittude 192.168.1.22 for YOUR IP
```

Enable the default physical service with ```svcadm``` and configure the ```interface```:

```
adrian@openindiana-hipster:~$ sudo svcadm enable physical:default
```

Configure interface with ipadm:

```
adrian@openindiana-hipster:~$ sudo ipadm create-addr -T static -a local=192.168.1.22/24 bge0/v4static
```

If you do not know what the interface name is (bge0 in this case); then type in

```
adrian@openindiana-hipster:~$ dladm show-link
```

or:

```
adrian@openindiana-hipster:~$ kstat -c net | grep net 

# look for hme0, bge0, e1000g0 or soemthing that resembles the driver in use.
```

Add gateway
```
adrian@openindiana-hipster:~$ sudo route -p add default 192.168.1.121
```

or

```
adrian@openindiana-hipster:~$ sudo nano /etc/defaultrouter 

# Enter in your gateways IP
```

Set DNS server(s)

```
adrian@openindiana-hipster:~$ sudo nano /etc/resolv.conf 
# Enter in the DNS server IP(s)
nameserver 192.168.1.121
```

or

```

adrian@openindiana-hipster:~$ sudo echo 'nameserver 192.168.1.121' >> /etc/resolv.conf

```

Set the workgroup

```
adrian@openindiana-hipster:~$ sudo smbadm join -w workgroupname
```
Restart

Note: IF you cannot ping an external IP(e.g. google.com) run this command and try again.

```
adrian@openindiana-hipster:~$ sudo cp /etc/nsswitch.dns /etc/nsswitch.conf
```

credit for these docs go to [/u/127b](https://www.reddit.com/user/127b)
