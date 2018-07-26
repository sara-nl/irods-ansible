# iRODS 4.1.10 Formation Playbooks

## System Requirements:
- CentOS7.x
- Internet Connection
- Ansible account configured (ansible/ansiRods)

## Operator Requirements:
- IP addresses of machines in formation
- Access to ansible account on machine
- This ansible playbook

## Overview
The most important file to operate this is the "hosts" file. This file contains all of the definitions and options used during machine setup. An exampe looks like this:
```
145.100.58.13 setup=1 svrType="icat"
145.100.58.19 setup=1 svrType="resc" rescICAT="145.100.58.13"
145.100.58.20 setup=1 svrType="icat"
145.100.58.243 setup=1 svrType="resc" rescICAT="145.100.58.20"
145.100.58.68 setup=1 svrType="resc" rescICAT="145.100.58.20"
```

The only truly required variables are listed above, they are:
- setup
- svrType
- rescICAT

If setup is set to 1, it will install and configure irods for you using predefined variables. 

If setup is set to 1, a server type (svrType) must be defined. Available options are:
- "icat"
- "resc"

And lastly, if the server is a Resoruce server defined above, you must point to an iCAT with this variable:
- rescICAT

## Instructions
1. Cone the repository
```
git clone https://git.ia.surfsara.nl/data-management-services/ansible
cd ansible
```
2. Configure your host file with the correct information
```
vi hosts
```
3. Run the playbook
```
ansible-playbook -i hosts build.yml
```

----
### Additional Information
It is worth noting that there are in fact several variables, all customizeable if listed in the same line as the appliciable host. 

These variables are all defined here, as well as in the hosts file itself:


**Variable** | **Purpose** 
----|----
 ansible_user=admincentos | #User to SSH as into machine
 fwd=0 | #0 is iptables, 1 is Firewalld
 serviceable=0 | #proudction level machine or no (for LDAP and such)
 setup=0 | #Setup iRODS? 0=N, 1=Y
 dbName="ICAT" | #Database Name
 dbAcnt="irods" | #Database Username
 dbPwd="irods" | #Database Password
 svrType="icat" | #iRODS Server Type
 svcAcnt="irods" | #serviceaccount
 iAcnt="rods" | #rods admin account
 iPwd="rods" | #rods admin password
 iZone="tempZone" | #irods zone
 iDBsvr="127.0.0.1" | #iRODS Database Server
 iDBname="{{dbName}}" | #iRODS Database Name
 iDBacnt="{{dbAcnt}}" | #iRODS Database Username
 iDBpwd="{{dbPwd}}" | #iRODS Database Password
 rescICAT="1.1.1.1" | #iCAT Server IP/FQDN
