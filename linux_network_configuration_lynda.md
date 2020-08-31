# Linux Network Configuration

Notes compilation from the corresponding course on Lynda.com.

## Setup

- Two VMs, CentOS and Ubuntu are setup on NATNetwork. By default VirtualBox creates different VMs on separate networks with same IP address. When you put the VMs on the same network (i.e. NATNetwork, they will be on the same network with incremental IP addresses)

## Networking tools

Here are some basic networking tools available

### ip / iproute

This is a replacement for ifconfig. Can be uses the same way as `ifconfig` to get IP address information as below:

```bash
# show ip addresses for all network interfaces
# the inet line will show the ip address and the subnet
# it will also show whether the ip address is static or dynamically assigned
ip addr

# show only ipv4 interfaces related info. This excludes all ip v6 interfaces
ip -4 addr

# show only ipv6 interfaces related info. This excludes all ip v4 interfaces
ip -6 addr
```

Let's dissect one of the lines from the result of above commands:

`3: wlp4s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000`

Here,

- wlp4s0 indicates it's a Wireless (wl) interface, on pci bus 4 (p4) and slot 0 (s0)
- UP keyword indicates that the network adapter is available to handle the data.
- LOWER_UP means the interface is connected to network and can talk to other devices. This has one to one correspondance with "state UP" on the same line. If you unplug the cable, for example, the UP will stay UP, but LOWER_UP will go away and the state will go to state down
- In order to completely disable the interface, you can use `ip` command with `link` manipulation options, as below:

```bash

# bring the wireless network interface down completely
# when this is issued, UP and LOWER_UP will both be gone and the state will be down
ip link set wlp4s0 down
```

You can also use ethtool command to get more information about an interface

```bash
ethtool wkp4s0
```

### NetworkManager

- You can query the status, start, stop NetworkManager as follows:

```bash

# Check if network manager is running
sudo systemctl status NetworkManager

# Start network manager
sudo systemctl start NetworkManager

# restart network for any changes to take effect (e.g. when you configured an interface to not be managed)
sudo systemctl restart network
```

- In order for NetworkManager to make changes to a connection, it has to be managed by NetoworkManager. You can check the devices managed by NetworkManager as follows:

```bash
# List NetworkManager managed devices
nmcli device
```

- You can tell NetworkManager to not manage an interface by editing the corresponding configuration that NetworkManager looks at. On Ubuntu, this configuration is at `/etc/NetworkManager/NetworkManager.conf`
- You can open UI for NetworkManager using `nm-connection-editor`
- You can also use `nmcli` i.e. network manager command line interface to manipulate network manager configuration
