It is possible to add docker containers to hosts in the topology of the sandbox definition. The trainees can then directly connect to these containers. This is done as part of networking ansible, and the only prerequisite is the existence of the `containers.yml` file in the topology. The structure of this file, along with the container functionality, is explained in an example [sandbox definition](https://gitlab.ics.muni.cz/muni-kypo-crp/prototypes-and-examples/sandbox-definitions/general-testing-definition/-/tree/test-docker-containers).

The definition contains a host `deb`, with two docker containers running on it (`home-docker` and `home-docker2`). These containers are specified in a file `containers.yml`. 

```
containers:
  - name: home-docker
    image: debian
  - name: home-docker2
    dockerfile: home-docker2/

container_mappings:
  - container: home-docker
    host: deb
    port: 2222
  - container: home-docker2
    host: deb
    port: 2223
```

### Containers

`containers` specify Docker containers' names and whether they are created from an *image* (as in `home-docker`) or a custom *Dockerfile* (`home-docker2`). In the case of a Dockerfile, a path to the Dockerfile in the repository has to be specified. Container *names* have to be unique, and either an *image* or a *dockerfile* have to be specified.

!!! note
    When using an image, a [default Dockerfile](https://gitlab.ics.muni.cz/muni-kypo-crp/backend-python/kypo-sandbox-service/-/blob/develop/kypo/sandbox_ansible_app/lib/templates/Dockerfile.j2) is used. It installs an *OpenSSH server* on the container. This is necessary so that the trainees can connect. When using a custom Dockerfile, you also have to include the installation of the OpenSSH server (see [here](https://gitlab.ics.muni.cz/muni-kypo-crp/prototypes-and-examples/sandbox-definitions/general-testing-definition/-/blob/test-docker-containers/home-docker2/Dockerfile#L3)).

### Container Mappings

`container_mappings` specify which containers will be set up on which hosts. Multiple containers can run on a single host (as seen in the example), and one container can be run on multiple different hosts. However, one container cannot run on a single host multiple times. Each container mapping consists of the container `name`, `host` (which will run the container), and a `port` of a host that is used to tunnel ssh from the container through the host and to the trainee. Two containers cannot share a single port on one host.

!!! warning "Docker requirements"
    An installation of docker and docker-compose, which enable this functionality, requires at least `Python 3.4` on the docker host. Image `debian-9-x86_64`, for instance, is not able to run the containers, and it is recommended to use `debian-11-x86_64` instead. Docker containers also require more resources, so using a reasonable flavor is recommended (`csirtmu.medium4x8` was tested to run two containers on a single machine)

!!! note
    Currently, there is no indication of which hosts have running containers on the KYPO CRP frontend. You have to use the training definition to inform trainees on which host in the topology the containers are running (if that is important to the training).

## User access

The running docker containers can be accessed with ssh, using the *user ssh config* that can be downloaded for each sandbox. If containers.yml is present in the sandbox definition, the ssh config is expanded with entries for each docker container so that the containers are easily accessible with ssh, just like any other host.

Connecting to the containers from the KYPO CRP using Spice console or Guacamole access is not supported.

!!! note
    Docker hosts do **not** have to be user accessible to allow the user access to the containers.

!!! warning
    Do not reboot hosts which run the docker containers.

## Troubleshooting

The docker containers are set up and started in **networking ansible**. If there are tasks in user ansible (performed on the host which runs these docker containers) that **require a reboot** of the system (such as a role [disable-qxl](https://gitlab.ics.muni.cz/muni-kypo/ansible-roles/disable-qxl/-/blob/master/tasks/disable-qxl.yml#L17)), the containers will be stopped and not ready once the sandbox allocation is over. To prevent this and still allow a reboot, add the following play to the end of playbook.yml in your sandbox definition, as it will start the containers again.

```
- name: Prepare docker enabled machines
  hosts:
    - docker_hosts
  become: yes
  tasks:
    - name: Build docker containers
      community.docker.docker_compose:
        project_src: "/home/kypo-user/containers/"
```