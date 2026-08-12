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

## 1.1.4

In Sunstone - press on the username and then go to **Profile Settings**.

<img src="./../assets/ca-images/module1_lab1/s6.png">

    
## 1.1.5

In the Settings navigate to **Security**.

<img src="./../assets/ca-images/module1_lab1/s7.png">

    
## 1.1.6

Locate the **SSH private key** and press the **Edit** button. 

<img src="./../assets/ca-images/module1_lab1/s8.png">

## 1.1.7

Paste the certificate contents and click anywhere outside of the field to save it.

<img src="./../assets/ca-images/module1_lab1/s9.png">
   
The private key should be saved now.

# Congratulations, you've completed the assignment!
{: .no_toc}