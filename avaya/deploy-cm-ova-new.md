# Playbook Name: deploy-cm-ova-new.yml

## Playbook Metadata:
##### version:
* 0.1: Initial release documentation

|Fields|Info|
|---|---|
|peer_review|TBD|
|author|[Tish Johnson](mailto:ljjohnson@convergeone.com?subject=deploy-cm-ova-new-ansible-playbook)
|creation_date|01/11/20|
|tested_ansible_release|2.7.2|

####  Description:
This playbook was designed to deploy an Avaya simplex CM server on VMware.

# Instructions:
## How to use the playbook:
Place this playbook on the server where Ansible is installed.

### Playbook Requirements:
- [x] Ansible 2.x
- [x] VMware 6.x
- [x] Logins to VMware with write permissions

#### Minimum command syntax required to run this playbook:

 See the testing information below for more info
 `ansible-playbook deploy-cm-ova-new.yml -i playbook_name -e "vmware_user=vmware_username" -e "target=vcenter_host"  -e "target_esxi=esxi_host"

### Variables for the playbook:
|Variable name|Description of the Variable|
|---|---|
|targets|Which are the hosts in the inventory to run the command against, i.e the vcenter server(s)|
|target_esxi|Is the ESXi host to target in vCenter|
|vmware_user|The user on VMware with permissions to login to vCenter and create new VMs from OVAs|


### Testing the playbook:
Below is a sample setup to test the ability to use the playbook.

Create a file on your Ansible server named ansible_host.

Inside ansible_host file add the following lines:
```
[vcenter]
1.1.1.50

```
Where 1.1.1.50 is replaced with your specific vcenter host IP.

For testing purposes it is highly advisable to setup a separate user login with the proper permissions to run commands in VMware

Run the following to execute

`ansible-playbook rdeploy-cm-ova-new.yml -i ansible_host -e "vmware_user=tjohnson@vsphere.local" -e "target=vcenter"  -e "target_esxi=1.1.1.51" `

**Note:** The command above uses the flags -e to set the vcenter user (vmware_user) which is tjohnson@vsphere.local. The  target_esxi for the ESXi IP address, and target field is the vcenter IP or name defined in the inventory file. Password will be

To be successful with deploying a CM the properities in the playbook do need to be set. Below is the properties that need to be edited in the playbook. Since this is the same as deploying the OVA manually, this is not included in the readme.

```
        properties:
          ip0: "1.1.1.52"
          netmask0: "255.255.255.0"
          ip1: "1.1.1.62"
          netmask1: "255.255.255.0"
          gateway: "1.1.1.1"
          hostname: "{{ hostName }}.{{ domain }}"
          weblmip: "1.1.1.5"
          dns: ""
          EASG_enable: "1"
          cm_login: "abccm"
          cm_password: "toor"
          ntpservers: "1.1.1.6"
```

### Output expected:
A deployed CM Simplex OVA :)
