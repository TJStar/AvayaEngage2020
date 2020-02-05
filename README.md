# Ansible_Playbooks

## Purpose:
This is an inital repo to store created ansible playbooks created to complete specific tasks not a part of a larger project.

### Usage:
* Push your playbook and a markdown file to repo
* Include in your markdown file with how to use your playbook (an example is nice), any other longer descriptions and output if an output is expected.
* Update this Readme's table with your playbook name, a brief one line description, and link to the playbook's markdown file.

## Playbooks in the repo:

|Playbook Name|Brief Description|Readme for Playbook|
|---|---|---|
|snmpCheck|This playbook was designed to check if Windows SNMP is configured|[snmpCheck](win/snmpCheck.md)|
|snmpInstall|This playbook was designed to install and configure Windows SNMP |[snmpInstall](win/snmpInstall.md)|[snmpInstall](win/snmpInstall.yml)|
|CM release|Pulls the Avaya release data from the CM |[CM Release](avaya/cmrelease.md)|[CM Release](avaya/cmrelease.yml)|
|deploy-cm-ova|Deploys a simplex CM server |[deploy-cm-ova](avaya/deploy-cm-ova.md)|[deploy-cm-ova](avaya/deploy-cm-ova.yml)|
