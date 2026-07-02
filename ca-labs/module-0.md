---
layout: default
title: Module 0 - Getting familiar with the Lab Environment 
parent: Certified Administrator
---
# Module 0 - Lab 0: Getting familiar with the Lab Environment
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

# FQDNs & Credentials

Your lab consists of 3 nodes:

| Node Name     | Username (SSH) | Password | Comment |
|----------------- | -------- | --------- | --------- |
| lab-**X**-node1     | gateway | Assigned by the instructor | Frontend Node ( Node 1)  | 
| lab-**X**-node2    | gateway 		| Assigned by the instructor | Node 2 |
| lab-**X**-node3 | gateway | Assigned by the instructor |  Node 3 |
| N/A			| backup-admin	| Assigned by the instructor | Backup Server for Rsync |

where **X** is your unique lab number issued by the instructor.

# Access the Web GUI

The 1st Node is hosting the Frontend services including the Web GUI (Sunstone).

You need to access Sunstone using the following URL:

https://lab-X.opennebula.academy/fireedge/sunstone/

where **X** is your unique lab number issued by the instructor.


# Access the Frontend node using SSH

Certain activities in this lab guide will require you to use CLI tools or access Node 2 & Node 3.

Use SSH from your personal device to the Frontend server. Don't forget to substitute X with your unique number assigned by the instructor.

Credentials are available on <a href="#/1/1" target="_blank">FQDNs & Credentials</a> page.

```console
ssh gateway@lab-X.opennebula.academy
gateway@lab-X.opennebula.academy's password:

gateway@lab-X-node1:~
```

# Inspect hosts file

/etc/hosts file contains records pointing to other hosts

```console
cat /etc/hosts
127.0.0.1 localhost

# The following lines are desirable for IPv6 capable hosts
::1 ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts
10.0.46.213 lab-X-node1
10.0.46.216 lab-X-node2
10.0.46.218 lab-X-node3
```

# oneadmin account

You are going to use **oneadmin** account to perform all OpenNebula-related activities.

```console
sudo -i -u oneadmin
[sudo] password for gateway: 
oneadmin@lab-X-node1:~$
```