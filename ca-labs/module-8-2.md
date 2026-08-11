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
- Instantiate the alpine-app-server
- Install application software
- Terminate the VM to save changes

# Instantiate the ubuntu-application VM
    
## 8.2.1

Go to the Node 1's Command Line and use **onetemplate** to deploy the **alpine-app-server** VM.

For now you can enter any values once prompted!

```console
onetemplate instantiate alpine-app-server
```

You would need to enter some parameters. Leave all on their respective defaults as it doesn't matter at the moment.

```console
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
VM ID: 0
```
    
## 8.2.2

Wait until the VM is in the **runn** state.

```console
onevm list
```

```console
ID USER     GROUP    NAME                  STAT  CPU     MEM HOST                 TIME
0 oneadmin oneadmin alpine-app-server-0    runn    1      2G lab-2108-node3       0d 00h00
```

## 8.2.3

Use the **onevm** command to get the IP address of a VM from the routable network. Make sure to use your VM ID and VNET ID.

```console
onevnet show <VNET ID> -j | jq -r '.VNET.AR_POOL.AR.LEASES.LEASE | select(.VM == "<VM ID>") | .IP'
```

Note that your output might be different!

```console
192.168.0.100
```

Connect to the VM using the SSH.

```console
ssh root@<IP ADDR>
```

You must see the console prompt similar to the one below!

```console
root@alpine-app-server-0>
```
    
## 8.2.3

Clone the git repository.

```console
apk add git
export REPO='https://github.com/OpenNebula/one-training-files.git'
rm -rf ~/Files
git clone --no-checkout $REPO  ~/Files
cd ~/Files
git sparse-checkout init --cone
git sparse-checkout set VMs
git checkout
cd VMs
ls -lh
```
The directory must contain the following files.

```console
total 5K
-rw-r--r--    1 root     root         901 Aug 11 14:44 prep_all.sh
-rw-r--r--    1 root     root         483 Aug 11 14:44 prep_alpine_app.sh
-rw-r--r--    1 root     root         218 Aug 11 14:44 prep_app.sh
-rw-r--r--    1 root     root         359 Aug 11 14:44 prep_clfd.sh
-rw-r--r--    1 root     root         708 Aug 11 14:44 prep_db.sh
```

    
## 8.2.4

Execute the **prep_alpine_app.sh** script.

```console
bash prep_alpine_app.sh
```

Once finished - verify that app files are present.

```console
cd ~
ls lh app/
```

You supposed to have set of files that includes **app.py** and directory such as **templates**.

```console
total 10K
-rw-r--r--    1 root     root         368 Aug 11 14:45 Dockerfile
drwxr-xr-x    2 root     root        1.0K Aug 11 14:45 app
-rw-r--r--    1 root     root        3.5K Aug 11 14:45 app.py
-rw-r--r--    1 root     root         466 Aug 11 14:45 docker-compose.yaml
drwxr-xr-x    3 root     root        1.0K Aug 11 14:45 old
-rw-r--r--    1 root     root         139 Aug 11 14:45 requirements.txt
drwxr-xr-x    2 root     root        1.0K Aug 11 14:45 templates
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
exit
```
   
## 8.2.6

Terminate the VM to save changes.

```console
onevm terminate <VM ID>
```

## 8.2.7

Execute the **oneimage** command.

```console
oneimage list
```

Locate the Alpine Linux 3.XX image ID.

```console
  ID USER     GROUP    NAME                      DATASTORE     SIZE TYPE PER STAT RVMS
   2 oneadmin oneadmin shared                    vfs             1M FS    No rdy     0
   1 oneadmin oneadmin Alpine Linux DB Server    nfs-img         5G OS    No rdy     0
   0 oneadmin oneadmin Alpine Linux 3.21         nfs-img       512M OS   Yes rdy     0
```

Change the **Alpine Linux 3.XX** image persistencty

```console
oneimage nonpersistent <IMAGE ID>
oneimage show <IMAGE ID>
```

Verify that the image is no longer persistent.

```console
MAGE 0 INFORMATION
ID             : 0
NAME           : Alpine Linux 3.21
...
PERSISTENT     : No
...
```

# Congratulations, you've completed the assignment!
{: .no_toc}