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

## Network Forwarding

*(Since sandbox-service 4.0.0)*

Network forwarding (port mirroring) of a [topology definition](../user-guide-advanced/sandboxes/topology-definition.md#network_forwarding) is optional and turned off by default. Prepare the following before you set `network_forwarding_enabled` to `true` in the `application_configuration` of the sandbox-service configuration. Otherwise, a definition with `network_forwarding` is rejected.

* **Neutron TaaS**: the Neutron Tap-as-a-Service extension with the OVN driver. The platform mirrors the traffic with `tap_mirror` resources of type GRE.
* **Base resources**: deploy the `tf-module-openstack-base` module v1.3.0 or newer (see [Deployment of OpenStack base resources](https://github.com/cyberrangecz/devops-tf-deployment/blob/master/BASE.md)) with its `hypervisor_cidr` variable set to the narrowest CIDR covering the addresses from which the compute nodes send the mirrored GRE traffic. The following resources are used.
    * The security group `sandbox-mirror-sg`, which is new in v1.3.0. The module creates it only when `hypervisor_cidr` is set. It allows only GRE ingress from `hypervisor_cidr` and DHCP requests (UDP to port 67), which the ports on the destination network need for their addresses. The DHCP rule allows any destination address, because the DHCP server address depends on the sandbox subnet, so anything on the destination network can send UDP to port 67 of any address through the forwarding router. Every port of a topology on the destination network uses it.
    * The router `base-router-public`, which is the existing router of the platform and is not changed by v1.3.0. The platform takes the external network of the per-sandbox forwarding router from it.

    !!! warning
        Deploy the base resources before you turn network forwarding on. A missing `sandbox-mirror-sg` is not detected at import. Every sandbox build with forwarding fails until the group exists.
* **Quotas**: every sandbox with network forwarding needs additionally 1 router, 2 external IP addresses (the gateway of the router and the floating IP of the destination), and 1 port.
* **One deployment per project**: the tunnel IDs of the mirrors are derived from the sandbox ID and are unique in a project. Two CyberRangeCZ Platform deployments that share one OpenStack project cannot both use network forwarding.
