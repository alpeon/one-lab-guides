---
layout: default
title: Lab 2 - Building a Custom VM
parent: Module 8 - VM Templates & VMs
---
# Module 8 - Lab 2 : Building a Custom VM

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
- Instantiate the ubuntu-application VM
- Install application software
- Terminate the VM to save changes
    

# Instantiate the ubuntu-application VM
    
## 8.2.1

Go to the Node 1's Command Line and use **onetemplate** to deploy the **ubuntu-application** VM.

For now you can enter any values once prompted!

```console
onetemplate instantiate ubuntu-application

There are some parameters that require user input. Use the string <<EDITOR>> to launch an editor (e.g. for multi-line inputs)
* (DB_HOST) 
    Press enter for default (127.0.0.1). 
* (APP_DATABASE) 
    Press enter for default (app). 
* (DB_USER) 
    Press enter for default (appuser). 
* (DB_PASSWORD) 
    Password: 
* (TIMEZONE) 
    Press enter for default (UTC).
VM ID: 1
```
    
## 8.2.2

Wait until the VM is in the **runn** state.

```console
onevm list

ID USER     GROUP    NAME                  STAT  CPU     MEM HOST                 TIME
0 oneadmin oneadmin ubuntu-application-0   runn    1      2G lab-2022-node3   0d 00h01
```

## 8.2.3

Use the **onevm** command to get the IP address of a VM from the routable network. Make sure to use your VM ID and VNET ID.

```console
onevnet show <VNET ID> -j | jq -r '.VNET.AR_POOL.AR.LEASES.LEASE | select(.VM == "<VM ID>") | .IP'

192.168.0.100
```

Connect to the VM using the SSH.

```console
ssh root@<IP ADDR>

root@ubuntu-application-0>
```
    
## 8.2.3

Clone the git repository.

```console
export REPO='https://github.com/OpenNebula/one-training-files.git'
rm -rf ~/Files
git clone --no-checkout $REPO  ~/Files
cd ~/Files
git sparse-checkout init --cone
git sparse-checkout set VMs
git checkout
cd VMs
ls -lh

total 4K
-rw-r--r--    1 root     root         894 Apr 13 20:05 prep_all.sh
-rw-r--r--    1 root     root         180 Apr 13 20:05 prep_app.sh
-rw-r--r--    1 root     root         359 Apr 13 20:05 prep_clfd.sh
-rw-r--r--    1 root     root         708 Apr 13 20:05 prep_db.sh
```

    
## 8.2.4

Execute the **prep_app.sh** script.

```console
bash prep_app.sh

...
```

Now execute the prep_clfd.sh script.

```console
bash prep_clfd.sh
```
    
## 8.2.5

Execute the clouflared command to verify that the app has been installed.

```console
cloudflared --help

NAME:
cloudflared - Cloudflare's command-line tool and agent

USAGE:
cloudflared [global options] [command] [command options]
...
```

Exit from the VM's console.

```console
# exit
```

    
## 8.2.6

Terminate the VM to save changes.

```console
onevm terminate <VM ID>
```

# Congratulations, you've completed the assignment!
{: .no_toc}