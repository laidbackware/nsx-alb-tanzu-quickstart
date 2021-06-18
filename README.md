# NSX-ALB Tanzu Quickstart
Ansible Role to deploy a minimum viable NSX Advanced Load Balancer (Avi) solution for VMware Tanzu.</br/>
These roles are not for building production deployments and is in no way associated with VMware.

## Dependencies
This has been tested on a Linux system and should also work on Mac.</br/>
Tested against Ansible 2.11.
```
pip install avisdk --upgrade
ansible-galaxy collection install vmware.alb:21.1.1-beta3
```
The Relevant OVA is required. This can be accessed via the [Tanzu Kubernetes Grid download page](https://my.vmware.com/en/group/vmware/downloads/info/slug/infrastructure_operations_management/vmware_tanzu_kubernetes_grid/1_x).

## Instructions
First you must export the necessary environment variables.
```
# The default password is show on the ova download page.
export AVI_DEFAULT_PW='####'
# This is a public key within your environment.
export SSH_PUBLIC_KEY='####'
# This is the vCenter which will host the controller VM.
export VCENTER_PASSWORD='####'
# This is the vCenter where you Avi Service Engines will be deployed.
export CLOUD_VCENTER_PASSWORD='####'
```
Next update the var-exmaple.yaml
