# NSX-ALB Tanzu Quickstart
This repo contains Ansible Roles to deploy a minimum viable NSX Advanced Load Balancer (Avi) solution for VMware Tanzu Kubernetes Grid on vSphere.<br/>
These Roles are not for building production deployments and this repo is in no way associated with VMware.

## Software Dependencies
This process has been tested on a Linux system and should also work on Mac.<br/>
Tested against Ansible 2.11 and Avi version 20.1.3.<br/>
Once you have Ansible installed, install the following:
```
pip install requests
ansible-galaxy collection install vmware.alb:21.1.1-beta4 --force
```
The 20.1.3 Avi OVA is required. This can be accessed via the [Tanzu Kubernetes Grid download page](https://my.vmware.com/en/group/vmware/downloads/info/slug/infrastructure_operations_management/vmware_tanzu_kubernetes_grid/1_x).

## Environment Dependencies
You will need a vSphere cluster under a vCenter running 6.7 or higher.<br/>
Avi Service Engines need to run in the same vSphere cluster as the Tanzu nodes and require 3 networks:
- Management - This will host the Service Engine management interfaces.
- VIP - This will host the Virtual Servers that TKG requests Avi to create.
- Backend - This is the network that contains Tanzu nodes.
The controller can be hosted in the management network if hosted within the same vCenter or it can be hosted elsewhere so long as there is network connectivity.

## Usage
To prevent committing secrets and your SSH public key into git, you must export the necessary environment variables. <br/>
If you prefer you can just skip this step and set the variables in the file in the next step.
```
# The default password is shown on the ova download page.
export AVI_DEFAULT_PW='####'
# This is a public key within your environment.
export SSH_PUBLIC_KEY='####'
# This is the vCenter which will host the controller VM.
export VCENTER_PASSWORD='####'
# This is the vCenter where your Avi Service Engines will be deployed.
export CLOUD_VCENTER_PASSWORD='####'
# This will be the password of the Avi Controller.
export CONTROLLER_PASSWORD='####'
```
Clone the example vars and fill in for your environment.<br/>
Make sure to leave any lookup functions in place if you want to pick up the secrets from environment variables.
```
cp var-exmaple.yaml my-vars.yml
vim my-vars.yml
```
Finally run the playbook using you new vars file.
```
ansible-playbook deploy.yml --extra-vars '@./my-vars.yml'
```

## Known issues
The initial UI setup wizard still needs to be completed due to the backup passphrase being missing.
