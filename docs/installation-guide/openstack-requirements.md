# OpenStack Requirements
KYPO Platform requires several OpenStack resources and components, that can be installed or configured only by the OpenStack administrator.

## OpenStack Version

KYPO Cyber Range Platform is tested with Open Stack releases from Train to Yoga, but it is possible it will also work on newer releases.

## OpenStack Services
KYPO Platform requires the following OpenStack services:

* Nova with SPICE or VNC console support
* Neutron with user-defined internal networks and floating IPs (provider networks are not supported)
* Keystone with Application Credentials

For every instance of KYPO Cyber Range Platform you also need two floating IP addreses from Open Stack public pool to access the platform.

Floating IP addreses need to be unrestricted on any firewalls.

For OpenStack deployment, it is recommended to use open source project [Kolla Ansible](https://github.com/openstack/kolla-ansible), which supports all KYPO requirements.

### MUNI-KYPO Images

More images can be found in the [MUNI-KYPO-IMAGES](https://gitlab.ics.muni.cz/muni-kypo-images) GitLab group. These images, each stored in its own repository, were created specifically for the needs of KYPO-CRP and their use is strongly recommended. Once an image is uploaded to the OpenStack project, it can be used in the `topology.yml` file of the sandbox definition. 

!!!note
    In the `topology.yml`, it is necessary to specify a `mgmt_user` along with each used image. This can be found in the `README.md` of the image, in the section _Image for QEMU/OpenStack_.
