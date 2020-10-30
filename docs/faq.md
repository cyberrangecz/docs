#FAQ

Here you can find the **Frequently asked questions** and answers regarding the **KYPO platform**. If the questions answered on this page are not sufficient as solutions for your problem, be sure to contact us on *support@kypo.cz*.

## Deployment
###  1. **Q:** Placeholder
**A: placeholder**

## Sandboxes
### 1. **Q:** Can I connect to the VMs in my sandbox via ssh?
**A: Yes!** Detailed instructions can be found in [Sandbox SSH Access](./operation-guide/sandboxes/sandbox-ssh-access.md). 

### 2. **Q:** Are there any remote management tools on the sandbox machines? SSH, RDP, or WinRM? How are they set up? Is it possible to use them for my scenario?

**A: Yes!** Sandbox machines must have these tools to provision sandbox. On UN*X machines there is an SSH and on Windows there is WinRM. These tools are configured by image developers and KYPO does not change their configuration. But their configuration can be changed in Sandbox Provisioning. Be careful not to cut the path to the machine. 

### 3. **Q:** Is it possible to restrict SSH only for the management network after Sandbox Networking or turn it off completely?
**A: Yes!** SSH user acceess is led through the networks defined in the sandbox topology definition, so trainee could access the machine only via web console. Management network can be completely blocked in [Sandbox Provisioning](../operation-guide/sandboxes/sandbox-provisioning), but you (as organizer) won't be able to access machines and won't help your students.


## Trainings
### 1. **Q:** Placeholder
**A: placeholder**
