# Multi Node Network

An example of creating multiple L2 networks, one on each of the nodes. Each network contains
2 network namespaces (containers), connected via a bridge, and have different subnets. The
containers are connected via static routing rules set on each of the nodes.

![Diagram](./diagram.jpg)

Create the 2 VMs (3-multi-node-1 and 3-multi-node-2):

```
vagrant up
```

SSH to each node (VM) in turn, and run the setup script to create the network namespaces connected via a bridge:

```
vagrant ssh 3-multi-node-[12]
cd /vagrant
./setup.sh
```

To test the connectivity between the containers within and node, and across nodes, run the following:

```
./test.sh
```

To teardown the network:

```
./teardown.sh
```

To test the entire flow, i.e. setup - run the tests - teardown, from your machine, run the following:

```
make
```

# FAQ

## how to test the connectivity?

on 3-multi-node-1

```shell
ping 172.16.1.2
```

on 3-multi-node-2

```shell
sudo tcpdump -ni veth10 icmp
```
