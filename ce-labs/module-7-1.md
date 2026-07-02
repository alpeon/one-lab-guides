---
layout: default
title: Lab 1 - OpenNebula Cloud API
parent: Module 7 - OpenNebula Cloud API
---
# Module 7 - Lab 1 : OpenNebula Cloud API 
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
- Install the python bindings.
- Download the script and adjust it.
- Run the script and verify the execution.


# Install the python bindings.


## 7.1.1

Create the virtual environment and install the **pyone** bindings.
```console
cd ~
mkdir oca
python3 -m venv oca
cd oca
source bin/activate
pip install pyone
``` 

# Download and adjust the script.

## 7.1.2

```console
export REPO='https://github.com/OpenNebula/one-training-files.git'
git clone --no-checkout $REPO
cd one-training-files
git sparse-checkout init --cone
git sparse-checkout set OCA
git checkout
cd OCA
ls -lh
total 8.0K
-rw-rw-r-- 1 oneadmin oneadmin 2.7K Aug  4 13:09 ascii.py
-rw-rw-r-- 1 oneadmin oneadmin 1.7K Aug  4 13:09 oca.py
```


## 7.1.3

Adjust the **oca.py** script! 

Locate a few **\<\<CHANGE ME\>\>** objects in the script and substitute these with the values - **2633**, **evpn0** and **AlmaLinux 9**.

# Run the script and verify the execution.

## 7.1.4

Execute the script and provide the credentials in-line.

```console
python3 oca.py 'oneadmin' '<PASSWORD>' '127.0.0.1'
```

Verify that the VM has been deployed and now running.

```console
ID USER     GROUP    NAME                    STAT  CPU     MEM HOST                  TIME
10 oneadmin oneadmin AlmaLinux 9-10         runn    1    768M 163.172.138.109       0d 00h02
```

Run **onevm show** and verify the persistence of START_SCRIPT and the IP Address to make sure the VM Template was altered.

```console
onevm show 10
...
VM NICS
ID NETWORK              BRIDGE       IP              MAC               PCI_ID
0 evpn0                onebr.20     172.17.2.200    02:00:ac:11:02:c8
...
CONTEXT=[
...
START_SCRIPT_BASE64="ZWNobyAkKGRhdGUpID4+IC9yb290L2RhdGUudHh0Cg=="
...
]
```
{: .note}
> Try to connect to the VM using the SSH. Can you tell why it fails? Send a private message with the answer to your trainer.

# Congratulations, you've completed the assignment!
{: .no_toc}