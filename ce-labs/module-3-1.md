---
layout: default
title: Lab 1 - Scheduling
parent: Module 3 - Scheduling
---
# Module 3 - Lab 1 : Scheduling
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
- Configure the OneDRS policy.
- Configure Undercommitment & Overcommitment.
- Deploy VMs and verify the OneDRS policy.
    

# Configure the OneDRS policy.

    
## 3.1.1

As **oneadmin** login to the Sunstone and navigate to **Infrastructure -> Clusters**.

<img src="./../assets/ca-images/module3_lab1/s1.png" class="img_80_percent">

    
## 3.1.2

Select the **default** cluster and expand the infotab.

<img src="./../assets/ca-images/module3_lab1/s2.png" class="img_80_percent">

    
## 3.1.3

Switch to **OneDRS** tab.

<img src="./../assets/ca-images/module3_lab1/s3.png" class="img_80_percent">

    
## 3.1.4

Press **Enable OneDRS** to start the DRS policy wizard. 

<img src="./../assets/ca-images/module3_lab1/s4.png" class="img_80_percent">

    
## 3.1.5

Set the **Policy** to **Balance** and **Accept** the settings.

<img src="./../assets/ca-images/module3_lab1/s5.png" class="img_80_percent">

    
## 3.1.6

Make sure your policy is looks like the following one.

<img src="./../assets/ca-images/module3_lab1/s6.png" class="img_80_percent">


# Configure Undercommitment & Overcommitment.

    
## 3.1.7

Navigate to **Infrastructure -> Hosts**.

<img src="./../assets/ca-images/module3_lab1/s7.png" class="img_80_percent">

    
## 3.1.8

Select one host and expand the infotab.

<img src="./../assets/ca-images/module3_lab1/s8.png" class="img_80_percent">

    
## 3.1.9

Under **Capacity** locate the **Allocated CPU** and press the edit button.

<img src="./../assets/ca-images/module3_lab1/s9.png" class="img_80_percent">

    
## 3.1.10

Set the value to **200**.

<img src="./../assets/ca-images/module3_lab1/s10.png" class="img_80_percent">

    
## 3.1.11

Perform the same action with another host but set the value to 800.

<img src="./../assets/ca-images/module3_lab1/s11.png" class="img_80_percent">

    
## 3.1.12

You should end up with one host that's **undercommited** and one **overcommited**.

<img src="./../assets/ca-images/module3_lab1/s12.png" class="img_80_percent">


# Deploy VMs and verify the OneDRS policy.

    
## 3.1.13

From the Frontend Node's Command Line disable the undercommited host.

```console
onehost disable 1
```

Instantiate 15 VMs from the **Custom AL 3.21** VM Template.

```console
onetemplate instantiate 1 -m 15
VM ID: 7
VM ID: 8
VM ID: 9
VM ID: 10
VM ID: 11
VM ID: 12
...
...
VM ID: 21
```
    
## 3.1.14

Wait until all VMs are in the running state and go enable the previously disabled host.

```console
onehost enable 1
```

# Deploy VMs and verify the OneDRS policy.


## 3.1.15

Return to **OneDRS** settings on the **default** cluster and press **Optimize**.

<img src="./../assets/ca-images/module3_lab1/s15.png" class="img_80_percent">

    
## 3.1.16

Once the plan is in place - press **Apply** to execute it!

<img src="./../assets/ca-images/module3_lab1/s16.png" class="img_80_percent">

    
## 3.1.17

Wait until all VMs that are subject of this plan are in the **DONE** state.

<img src="./../assets/ca-images/module3_lab1/s17.png" class="img_80_percent">

    
## 3.1.18

Go to **Infrastructure -> Hosts** and check the CPU metrics.

<img src="./../assets/ca-images/module3_lab1/s18.png" class="img_80_percent">


# Remove all running VMs.
    
# Congratulations, you've completed the assignment!
{: .no_toc}