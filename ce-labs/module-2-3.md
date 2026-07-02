---
layout: default
title: Lab 3 - Quota
parent: Module 2 - Advanced User Administration
---
# Module 2 - Lab 3 : Quota
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
- Create a VM Quota for the "users" group.
- Create a new User and instantiate VMs.

# Create a VM Quota for the "users" group.

    
## 2.3.1

Navigate to **System -> Groups**. 

<img src="./../assets/ca-images/module2_lab3/s1.png" class="img_80_percent">

    
## 2.3.2

Select the **users** group from the list.

<img src="./../assets/ca-images/module2_lab3/s2.png" class="img_80_percent">

    
## 2.3.3

In the infotab of the group switch to the **Quota** tab.

<img src="./../assets/ca-images/module2_lab3/s3.png" class="img_80_percent">

    
## 2.3.4

Set the **Type** to **VM Quota**.

Set the **Cluster ID** to **@Global**.

Set the **identifier** to **Virtual Machines**.

Set the **Value** to **3**.

And Apply the settings.

<img src="./../assets/ca-images/module2_lab3/s4.png" class="img_70_percent">

    
## 2.3.5

Make sure that the Quota has been applied.

<img src="./../assets/ca-images/module2_lab3/s5.png" class="img_80_percent">


# Create a new User and instantiate VMs.

    
## 2.3.6

Switch to the Frontend Node's Command Line and create a new user. 

```console
oneuser create 'jvalentine' 'Pa$$w0rd' --group 1
ID: 3
```

Instantiate 4 VMs from the "Alpine Linux 3.21" VM Template on behalf of the newly created user. 

```console
onetemplate instantiate 0 -m 4 --user jvalentine
Password:
VM ID: 0
VM ID: 1
VM ID: 2
[one.template.instantiate] User [3] : group [1] limit of 3 reached for VMS quota in VM.
```

You can confirm that Quota has been applied. Terminate the running VMs.

```console
onevm terminate --hard 0..2
onevm list
ID USER     GROUP    NAME     STAT  CPU     MEM HOST        TIME
```

    
# Congratulations, you've completed the assignment!