# Playbook Name: deploy-cm-ova-new.yml

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
- [x] VMware 6.x
- [x] Logins to VMware with write permissions

#### Minimum command syntax required to run this playbook:

 `ansible-playbook -e targets=inventory_hostname `

### Variables for the playbook:
|Variable name|Description of the Variable|
|---|---|
|targets|Which are the hosts in the inventory to run the command against, i.e the CM server(s)|


### Testing the playbook:
Below is a sample setup to test the ability to use the playbook.

Create a file on your Ansible server named ansible_host.

Inside ansible_host file add the following lines:
```
[abccm]
1.1.1.7

[abccm:vars]
ansible_port=22
ansible_connection=ssh
ansible_ssh_common_args='-o StrictHostKeyChecking=no UserKnownHostsFile=/dev/null'
```
Where 1.1.1.7 is replaced with your specific Windows host IP.

Verify the Linux server responds to Ansible commands.
`ansible windows -i ansible_host -m ping -u cust -k`

**Note:** The command above uses the flags -u to set the user, cust in this case, and -k to prompt for the password.

For testing purposes it is highly advisable to setup a separate user login with the proper permissions to run commands in VMware

Run the following to execute

`ansible-playbook -e targets=abccm -i ansible_host -u cust  -k release.yml`

**Note:** The an error maybe experienced when the task check SNMP community string is ran because the SNMP community string public may not be defined.

### Output expected:
A deployed CM Simplex OVA :)

```
