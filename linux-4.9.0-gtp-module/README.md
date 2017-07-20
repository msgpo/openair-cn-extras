# GTP OVS Integration Off-Tree Build

## Usage

### gtp.ko

```
make
make install  # this overwrites the old gtp.ko

modprobe udp_tunnel
modprobe ip6_udp_tunnel
modprobe gtp
```

### ovs

```
git clone https://github.com/openvswitch/ovs.git
cd ovs
git am ../ovs-patches/datapath-gprs-tunneling
git am ../ovs-patches/userspace-gprs-tunneling
./boot.sh
./configure --with-linux=/lib/modules/`uname -r`/build
make -j`nproc`
# the following "include" the symbols from the gtp.ko
cat ../gtp-v4.9-backport/Module.symvers >> datapath/linux/Module.symvers
make
make modules_install  # this overwrites openvswitch.ko, vport.ko, vport-gtp.ko, etc.
make install
mkdir -p /usr/local/etc/openvswitch
mkdir -p /usr/local/var/run/openvswitch
ovsdb-tool create /usr/local/etc/openvswitch/conf.db vswitchd/vswitch.ovsschema
```

### Setup NAT

```
iptables -t nat -A POSTROUTING -o <uplink_iface> -j MASQUERADE
iptables -A FORWARD -i <internal_iface> -j ACCEPT
iptables -A FORWARD -o <internal_iface> -j ACCEPT
```
