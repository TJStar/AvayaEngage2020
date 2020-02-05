# Playbook Name: cmrelease.yml

## Playbook Metadata:
##### version:
* 0.1: Initial release documentation

|Fields|Info|
|---|---|
|peer_review|TBD|
|author|[Tish Johnson](mailto:ljjohnson@convergeone.com?subject=cmrelease-ansible-playbook)
|creation_date|01/11/20|
|tested_ansible_release|2.7.2|

####  Description:
This playbook was designed to grab the CM release from the CM server

# Instructions:
## How to use the playbook:
Place this playbook on the server where Ansible is installed.

### Playbook Requirements:
- [x] Ansible 2.x
- [x] A user with the ability to run commands in Avaya CM

#### Minimum command syntax required to run this playbook:

 `ansible-playbook -e targets=inventory_hostname -u user -k playbook_name`

### Variables for the playbook:
|Variable name|Description of the Variable|
|---|---|
|targets|Which are the hosts in the inventory to run the command against, i.e the CM server(s)|
|user|User name on the CM server that can run the command , i.e the CM server(s)|


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
Where 1.1.1.7 is replaced with your specific CM host IP.

Verify the Linux server responds to Ansible commands.
`ansible abccm -i ansible_host -m ping -u cust -k`

**Note:** The command above uses the flags -u to set the user, cust in this case, and -k to prompt for the password.

For testing purposes cust can be used however it is highly advisable to setup a non superuser login with the proper permissions to run Ansible commands from.

Expected output should be similar to
```
1.1.1.7 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
Once basic Linux connectivity is established run the following.

`ansible-playbook -e targets=abccm -i ansible_host -u cust  -k cmrelease.yml`


### Output expected:
A file is created is named stored in the /tmp folder. The filename is dynamic is created in the form of <targets>-<playbook name>-<date>.log

As an example if, the target is abccm and the date is 06/13/2019. The full location of the file would be /tmp/abccm-cmrelease-2019-06-13.log


