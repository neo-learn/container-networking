# Single Node Network

An example of creating a single L2 network on one node, containing
2 network namespaces (containers), connected via a bridge.

![Diagram](./diagram.jpg)

Create the VM (container-networking):

```
vagrant up
```

SSH to the node (VM) and run the setup script to create the network namespaces connected via bridge:

```
vagrant ssh container-networking-[12]
cd /vagrant
./setup.sh
```

To test the connectivity between the containers within the node, run the following:

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

## FAQ

### can't access internet on container?

on the host node

```shell

sysctl -w net.ipv4.ip_forward=1

sudo iptables -t nat -n -L
sudo iptables -t nat -A POSTROUTING -s 172.16.0.1/24 -o enp0s3 -j MASQUERADE
```

on the container node

```shell
sudo ip netns exec con1 bash
ping 8.8.8.8
```
