# Playbook Name: g450-annc-download.yml

## Playbook Metadata:
##### version:
* 0.1: Initial release documentation

|Fields|Info|
|---|---|
|peer_review|TBD|
|author|[Tish Johnson](mailto:ljjohnson@convergeone.com?subject=release-ansible-playbook)
|creation_date|01/11/20|
|tested_ansible_release|2.7.2|

####  Description:
This playbook was designed to check the install status of the SNMP windows module, check the SNMP community name,and check the configured Windows SNMP managers. The intent was to use this playbook to check the snmp_install.yml playbook.

# Instructions:
## How to use the playbook:
Place this playbook on the server where Ansible is installed.

### Playbook Requirements:
- [x] Ansible 2.x
- [x] G450 with SSH enable
- [x] G450 login

#### Minimum command syntax required to run this playbook:

 `ansible-playbook playbook_name`

### Variables for the playbook:
|Variable name|Description of the Variable|
|---|---|
|playbook_name|Name of the playbook|


### Testing the playbook:
Below is a sample setup to test the ability to use the playbook.

**Note:** Creation of an inventory file, i.e ansible_host file, is not required to run this playbook


For testing purposes cust can be used however it is highly advisable to setup a non privilege login with the proper permissions to run Ansible commands from.



**Note:** The command above uses the flags -u to set the user, cust in this case, and -k to prompt for the password.

### Output expected:
The output is all the announcement downloaded on the server running ansible.
