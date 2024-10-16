# OpenStack Requirements
CyberRangeCZ Platform requires several OpenStack resources and components, that can be installed or configured only by the OpenStack administrator.

## OpenStack Version

CyberRangeCZ Platform is tested with Open Stack releases from Train to Yoga, but it is possible it will also work on newer releases.

## OpenStack Services
CyberRangeCZ Platform requires the following OpenStack services:

* Neutron with user-defined internal networks and floating IPs (provider networks are not supported)
* Keystone with Application Credentials

For every instance of CyberRangeCZ Platform you also need two floating IP addreses from Open Stack public pool to access the platform.

Floating IP addreses need to be unrestricted on any firewalls.

For OpenStack deployment, it is recommended to use open source project [Kolla Ansible](https://github.com/openstack/kolla-ansible), which supports all CyberRangeCZ Platform requirements.
