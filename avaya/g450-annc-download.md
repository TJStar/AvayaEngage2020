# Playbook Name: g450-annc-download.yml

## Playbook Metadata:
##### version:
* 0.1: Initial release documentation

|Fields|Info|
|---|---|
|peer_review|TBD|
|author|[Tish Johnson](mailto:ljjohnson@convergeone.com?subject=g450-annc-download-ansible-playbook)
|creation_date|01/11/20|
|tested_ansible_release|2.7.2|

####  Description:
This playbook was designed to download all announcements from a g450.

# Instructions:
## How to use the playbook:
Place this playbook on the server where Ansible is installed.

### Playbook Requirements:
- [x] Ansible 2.x
- [x] G450 with SSH enable
- [x] G450 login
- [x] Server with SFTP and login with write access

#### Minimum command syntax required to run this playbook:

 `ansible-playbook playbook_name`

### Variables for the playbook:
|Variable name|Description of the Variable|
|---|---|
|playbook_name|Name of the playbook|


### Testing the playbook:
Run the playbook with the command:

 `ansible-playbook g450-annc-download.yml`

However, before running set the following variables. 

         g450_user: root
         g450_pass: toor
         g450_host: 1.1.1.14
         annc_bkup_host: 1.1.1.8
         annc_bkup_login: hostUser
         annc_bkup_pwd: hostPwd
         g450_ftp_login: ftpUser
         g450_ftp_pwd: ftpPassword
         annc_file: []
         annc_dir: /tmp/{{ lookup('pipe', 'date +%Y_%m%d_%H%M') }}

|Variable name|Description of the Variable|
|---|---|
|g450_user|G450 Login with read permissions|
|g450_pass|G450 password|
|g450_host|G450 IP|
|annc_bkup_host|Backup server IP or FQDN|
|annc_bkup_login|Backup server username|
|annc_bkup_pwd|Backup server password|
|g450_ftp_login|FTP login to the G450|
|g450_ftp_pwd|FTP password to the G450|
|annc_dir|Where to save the announcements|

**Note:** You should really save your password in an Ansible vault. However, that was out of scope for this playbook at the time.

### Output expected:
The output is all the announcement downloaded on the server specified.
