---
layout: default
title: Lab 1 - Hooks
parent: Module 6 - Hooks
---
# Module 6 - Lab 1 : Hooks 
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
- Download the hook script and create the Hook.
- Test the execution.
 

# Download the hook script and create the Hook.
     
## 6.1.1

Clone the repository with the hook script.

```console
export REPO='https://github.com/OpenNebula/one-training-files.git'
rm -rf ~/Files
git clone --no-checkout $REPO  ~/Files
cd ~/Files
git sparse-checkout init --cone
git sparse-checkout set Hooks
git checkout
cd Hooks
ls -lh
total 4.0K
-rw-rw-r-- 1 oneadmin oneadmin 818 Aug  4 12:10 report.py
```
 
    
## 6.1.2

Copy the script to the hooks directory and make it executable.

```console
cp report.py ~/remotes/hooks/
chmod +x ~/remotes/hooks/report.py
```
 

## 6.1.3

Create a file named **hook.cfg** with the following content.

```console
NAME      = "report"
TYPE      = STATE
RESOURCE  = "VM"
ON        = "CUSTOM"
STATE     = "PENDING"
LCM_STATE = "LCM_INIT"
COMMAND   = "report.py"
ARGUMENTS = "$TEMPLATE"
```

Use **onehook** command line to create a hook.

```console
onehook create hook.cfg
ID: 0
```
 

# Test the execution.
 
    
## 6.1.4

Instantiate **any** VM Template a few times.

```console
onetemplate instantiate Alpine\ Linux\ 3.21 -m 4
VM ID: 2
VM ID: 3
VM ID: 4
VM ID: 5
```
 
    
## 6.1.5

View the Hook Execution log.

```console
onehook log
HOOK    ID       TIMESTAMP    RC EXECUTION
    0     3     08/04 12:24     0 SUCCESS
    0     2     08/04 12:24     0 SUCCESS
    0     1     08/04 12:24     0 SUCCESS
    0     0     08/04 12:24     0 SUCCESS
``` 
    
## 6.1.6

Check the **report.txt** file for the contents.

```console
cat /tmp/report.txt
New VM data:
VM Name: Alpine Linux 3.21-6
VM ID: 2
Owner: oneadmin
*******************
New VM data:
VM Name: Alpine Linux 3.21-8
VM ID: 3
Owner: oneadmin
*******************
New VM data:
VM Name: Alpine Linux 3.21-7
VM ID: 4
Owner: oneadmin
*******************
New VM data:
VM Name: Alpine Linux 3.21-9
VM ID: 5
Owner: oneadmin
*******************
``` 
    
# Congratulations, you've completed the assignment!
{: .no_toc}
