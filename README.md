# iRODS 4.1.10 Formation Playbooks

## System Requirements:
- CentOS7.x
- Internet Connection
- Ansible account configured (ansible/ansiRods)

## Operator Requirements:
- IP addresses of machines in formation
- Passwordless access to a sudo account on machines

## Overview
The most important file to operate this is the "hosts" file. This file contains all of the definitions and options used during machine setup. An example entry looks like this:
```
145.100.58.13
```
**NOTE:** Only one host machine per line.

However, we can configure multiple servers with some customized options. This example creates two machines, an iCAT and a Resource server:

```
145.100.58.13
145.100.58.14 svrType="resc" rescICAT="145.100.58.13"
```
**NOTE:** If creating a resource server, ***rescICAT*** must be defined as the iCAT to the resource server. It can be one built by this playbook.

These host files can have as many variables as you wish to customize, see below for a comprehensive table. 

## Instructions
1. Cone the repository
```
git clone https://git.ia.surfsara.nl/data-management-services/ansible
cd ansible/iRODS-4-X-X
```
2. Configure your host file with the correct information
```
vi hosts
```
3. Run the playbook
```
ansible-playbook -i hosts build.yml
```


**NOTE:** If the account requires a password for sudo commands, use the -K option as shown here:
```
ansible-playbook -i hosts build.yml -K
```
This -K flag tells ansible that you need to enter a password, and will be prompted to do so. It must be the same across all machines if used.

----
### Additional Information
It is worth noting that there are in fact several variables, all customizeable if listed in the same line as the appliciable host. 

The default values listed here are defined in the lower portion of the hosts file.

**Variable** | **Purpose** | **Input Options**
----|----|----
 ansible_user=admincentos | #User to SSH as into machine | "any quoted string"
 fwd=0 | #0 is iptables, 1 is Firewalld | 0 or 1
 serviceable=0 | #proudction level machine or no (for LDAP and such) | 0 or 1
 setup=1 | #Setup iRODS? 0=N, 1=Y | 0 or 1
 dbName="ICAT" | #Database Name | "any quoted string"
 dbAcnt="irods" | #Database Username | "any quoted string"
 dbPwd="irods" | #Database Password | "any quoted string"
 icatPkg="URL" | #URL to iRODS iCAT rpm | "Quoted URL to iCAT RPM"
 dbPluginPkg="URL" | #URL to iRODS database plugin | "Quoted URL to database plugin"
 rescPkg="URL" | #URL to iRODS Resource rpm | "Quoted URL to resource RPM" 
 svrType="icat" | #iRODS Server Type | "icat" or "resc"
 svcAcnt="irods" | #serviceaccount | "any quoted string"
 zoneKey="" | #Zone Key | "any quoted string"
 negKey="" | #Negotiation Key | "any quoted string"
 ctrlKey="" | #Control Plane Key | "any quoted string"
 iAcnt="rods" | #rods admin account | "any quoted string"
 iPwd="rods" | #rods admin password | "any quoted string"
 iZone="tempZone" | #irods zone | "any quoted string"
 iDBsvr="127.0.0.1" | #iRODS Database Server | "any quoted string"
 iDBname="{{dbName}}" | #iRODS Database Name | "any quoted string"
 iDBacnt="{{dbAcnt}}" | #iRODS Database Username | "any quoted string"
 iDBpwd="{{dbPwd}}" | #iRODS Database Password | "any quoted string"
 rescICAT="1.1.1.1" | #iCAT Server IP/FQDN | "any quoted string"
