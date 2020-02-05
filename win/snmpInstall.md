# Playbook Name: snmpInstall.yml

## Playbook Metadata:
##### version:
* 1.1: Cleans up the log file created
* 1.0: Working logging of the output
* 0.5: Corrected all of the commands to pull the correct SNMP data
* 0.1: Initial release

|Fields|Info|
|---|---|
|peer_review|TBD|
|author|[Tish Johnson](mailto:ljjohnson@convergeone.com?subject=snmpCheck-ansible-playbook)
|creation_date|05/11/19|
|tested_ansible_release|2.7.2|

####  Description:
This playbook was designed to check the install status of the SNMP windows module, check the SNMP community name,and check the configured Windows SNMP managers. The intent was to use this playbook to check the snmp_install.yml playbook.

# Instructions:
## How to use the playbook:
Place this playbook on the server where Ansible is installed.

### Playbook Requirements:
- [x] Ansible 2.x
- [x] WinRM enabled on the Windows servers - [More about setting up Windows hosts for Ansible](https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html#winrm-setup)
- [x] pywinrm - [More about WinRM and Ansible here](https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html?highlight=ansible_connection)
- [x] A user with the ability to run powershell commands and read the registry  

#### Minimum command syntax required to run this playbook:

 `ansible-playbook -e targets=inventory_hostname -e community_name=SNMPcommunity snmp_check.yml`

### Variables for the playbook:
|Variable name|Description of the Variable|
|---|---|
|targets|Which are the hosts in the inventory to run the command against.|
|community_name|The SNMP community name to set for the Windows server|

### Testing the playbook:
Below is a sample setup to test the ability to use the playbook.

Create a file on your Ansible server named ansible_host.

Inside ansible_host file add the following lines:
```
[windows]
1.1.1.5

[windows:vars]
ansible_port=5986
ansible_connection=winrm
ansible_winrm_transport=ntlm
ansible_winrm_server_cert_validation=ignore
```
Where 1.1.1.5 is replaced with your specific Windows host IP.

Verify the Windows server responds to Ansible commands.
`ansible windows -i ansible_host -m win_ping -u Administrator -k`

**Note:** The command above uses the flags -u to set the user, Administrator in this case, and -k to prompt for the password.

For testing purposes Administrator can be used however it is highly advisable to setup a non Administrator user with the proper permissions to run Ansible commands from.

Expected output should be similar to
```
1.1.1.5 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
Once basic windows connectivity is established run the following.

`ansible-playbook -e targets=windows -e community_name=public -i ansible_host -u Administrator  -k snmpCheck.yml`

**Note:** The an error maybe experienced when the task check SNMP community string is ran because the SNMP community string public may not be defined.

### Output expected:
A file is created is named stored in the /tmp folder. The filename is dynamic is created in the form of <targets>-<playbook name>-<date>.log

As an example if, the target is windows and the date is 06/13/2019. The full location of the file would be /tmp/windows-snmpCheck-2019-06-13.log

If more than one target is specified, like the inventory hostname windows has 5 child servers all 5 servers will be in the same output file and each server's data will be in between the BEGIN SNMP Settings and END SNMP Settings blocks of data.

Example Output:
```
############             SNMP Check              ############


 Start Time: 2019-06-13T04:42:39Z Central Standard Time


 #### BEGIN SNMP Settings for 1.1.1.78 ####
task_name Check if SNMP Installed
...
"
"- ''
- 'Display Name                                            Name                   '
- '------------                                            ----                   '
- '        [X] SNMP Tools                                  RSAT-SNMP              '
- '[X] SNMP Service                                        SNMP-Service           '
- '    [X] SNMP WMI Provider                               SNMP-WMI-Provider      '
- ''
- ''
"
task_name Check SNMP Manager
"'1':
    raw_value: 1.1.1.3
    type: REG_SZ
    value: 1.1.1.3
'2':
    raw_value: 1.1.5.3
    type: REG_SZ
    value: 1.1.5.3
    task_name Check SNMP community name
    "public:
        raw_value: 4
        type: REG_DWORD
        value: 4
    "
    task_name Check SNMP Trap
    "'1':
        raw_value: 1.1.1.3
        type: REG_SZ
        value: 1.1.1.3
    '2':
        raw_value: 1.1.5.3
        type: REG_SZ
        value: 1.1.5.3
    "
    #### END SNMP Settings for 1.1.1.78 ####

```
