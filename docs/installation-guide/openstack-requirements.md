# OpenStack Requirements
KYPO Platform requires several OpenStack resources and components, that can be installed or configured only by OpenStack administrator.

## OpenStack Services
Kypo Platform requires the following OpenStack services:

* Nova with SPICE console support
* Neutron with user-defined internal networks and floating IPs (provider networks are not supported)
* Keystone with Application Credentials
* Heat

Floating IPs need to be unrestricted on any firewalls.

## OpenStack Resources

### Flavors
All flavors used by KYPO Platform can be customized in its configuration. It is recommended to create the following flavor with a command (OpenStack admin only):
```
openstack flavor create --ram 2048 --disk 20 --vcpus 1 csirtmu.tiny1x2
```

### Images
KYPO Platform requires images of supported Operating Systems. They can be customized in KYPO Platform configuration or created with following commands (with **public** argument OpenStack admin only):

* **ubuntu-bionic-x86_64**
```
wget https://cloud-images.ubuntu.com/bionic/current/bionic-server-cloudimg-amd64.img -P /tmp/
openstack image create --disk-format qcow2 --container-format bare --public --property \
os_type=linux --file /tmp/bionic-server-cloudimg-amd64.img ubuntu-bionic-x86_64
```
* **ubuntu-focal-x86_64**
```
wget https://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-amd64.img -P /tmp/
openstack image create --disk-format qcow2 --container-format bare --public --property \
os_type=linux --file /tmp/focal-server-cloudimg-amd64.img ubuntu-focal-x86_64
```

* **debian-9-x86_64**
```
wget http://cdimage.debian.org/cdimage/openstack/current-9/debian-9-openstack-amd64.qcow2 -P /tmp/
openstack image create --disk-format qcow2 --container-format bare --public --property \
os_type=linux --file /tmp/debian-9-openstack-amd64.qcow2 debian-9-x86_64
```
