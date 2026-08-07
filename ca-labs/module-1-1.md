---
layout: default
title: Lab 1 - Frontend Node
parent: Module 1 - Architecture and Deployment
---

# Module 1 - Lab 1 : Introduction and Architecture
{: .no_toc}

## Table of Contents
{: .no_toc}

<details markdown="block">
  <summary>
    Expand to access the In-page navigation
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Objective(-s):

- Login to the Sunstone UI as oneadmin.
- Enroll the Private Key.

# Install the opennebula-form package and inspect the running systemd services.

## 1.1.1

Connect to Node 1's using your Frontend FQDN (lab-X.opennebula.academy) with a **gateway** user. 

Look at the OpenNebula services:

```console
systemctl | grep opennebula
    opennebula-fireedge.service            loaded    active running   OpenNebula FireEdge Server
    opennebula-flow.service                loaded    active running   OpenNebula Flow Service
    opennebula-form.service                loaded    active running   OpenNebula Form Service
    opennebula-gate.service                loaded    active running   OpenNebula Gate Service
    opennebula-guacd.service               loaded    active running   OpenNebula Guacamole Server
    opennebula-hem.service                 loaded    active running   OpenNebula Hook Execution Service
    opennebula-ssh-agent.service           loaded    active running   OpenNebula SSH agent
    opennebula.service                     loaded    active running   OpenNebula Cloud Controller Daemon
    opennebula-showback.timer              loaded    active waiting   OpenNebula's periodic showback calculation
    opennebula-ssh-socks-cleaner.timer     loaded    active waiting   OpenNebula SSH persistent connection cleaner
```

## 1.1.2

Open the <a href="https://lab-X.opennebula.academy/fireedge/sunstone/" target="_blank">Sunstone UI</a> and login using the credentials (substitute X with your Lab ID and hit enter).

<img src="./../assets/ca-images/module1_lab1/s2.png">


## 1.1.3

Return to Node 1's console.

From the Node 1 (Frontend) server establish the ssh connection to the Node 2 (as oneadmin user).

```console
oneadmin@lab-X-node1:~ssh lab-X-node2
Warning: Permanently added 'lab-2022-node2' (ED25519) to the list of known hosts.
Welcome to Ubuntu 24.04.2 LTS (GNU/Linux 6.8.0-1030-aws x86_64)
....
```

```console
oneadmin@lab-X-node2:~dpkg -l | grep opennebula
ii  opennebula-common         7.2.0-1    all          Common OpenNebula package shared by various components (Community Edition)
ii  opennebula-common-onecfg  7.2.0-1    all          Helpers for OpenNebula onecfg (Community Edition)
ii  opennebula-node-kvm       7.2.0-1    all          Services for OpenNebula KVM node (Community Edition)
ii  opennebula-rubygems       7.2.0-1    amd64        Ruby dependencies for OpenNebula (Community Edition)  
```

## 1.1.4

Let's look at running services on the Node 2.

```console
systemctl | grep opennebula
```

You shouldn't have any opennebula services on Nodes 2 & 3, however you must have **libvirt** running on both nodes.

```console
systemctl | grep libvirt
libvirt-guests.service    		loaded    active     exited    libvirt guests suspend/resume service
libvirtd.service          		loaded    active     running   libvirt legacy monolithic daemon
virtlockd.service         		loaded    active     running   libvirt locking daemon
virtlogd.service          		loaded    active     running   libvirt logging daemon
libvirtd-admin.socket     		loaded    active     running   libvirt legacy monolithic daemon admin socket
libvirtd-ro.socket        		loaded    active     running   libvirt legacy monolithic daemon read-only socket
libvirtd.socket           		loaded    active     running   libvirt legacy monolithic daemon socket
virtlockd-admin.socket    		loaded    active     running   libvirt locking daemon admin socket
virtlockd.socket          		loaded    active     running   libvirt locking daemon socket
virtlogd-admin.socket     		loaded    active     running   libvirt logging daemon admin socket
virtlogd.socket           		loaded    active     running   libvirt logging daemon socket
virt-guest-shutdown.target		loaded    active     active    libvirt guests shutdown target
```

exit to the Node 1 once done.

```console
exit
```

## 1.1.5

On Node 1 make sure you are logged in as oneadmin and execute the **cat** command.

```console
cat ~/.ssh/id_rsa
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
NhAAAAAwEAAQAAAYEA1o6N1Y/9Q5KZyIRJySPeG8OcVe7LzA2iy8IAioke3bBs1NpNVDmk

...
uqcjK6Uh/CAbOycfXu7RHDuoeQVtJ81Gdc52Q5y2RhWzeLt1sJoM0Et9qSLxbeLK0hoNs/
RjkqlibWhxOiqwBxBEAyR3PrdbtRtmIVzMZlfhEJ3rBwQoaGLjiyvHILrsPSVT2C6SaPnZ
YzSoldmKW6cmHjAAAAF29uZWFkbWluQGxhYi0yMDIyLW5vZGUxAQID
-----END OPENSSH PRIVATE KEY-----
```

Copy the entire key - you are going to need it in the future steps

## 1.1.6

In Sunstone - press on the username and then go to **Profile Settings**.

<img src="./../assets/ca-images/module1_lab1/s6.png">


    
## 1.1.7

In the Settings navigate to **Security**.

<img src="./../assets/ca-images/module1_lab1/s7.png">

    
## 1.1.8

Locate the **SSH private key** and press the **Edit** button. 

<img src="./../assets/ca-images/module1_lab1/s8.png">

## 1.1.9

Paste the certificate contents and click anywhere outside of the field to save it.

<img src="./../assets/ca-images/module1_lab1/s9.png">
   
The private key should be saved now.

# Congratulations, you've completed the assignment!
{: .no_toc}