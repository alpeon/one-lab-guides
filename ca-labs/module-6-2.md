---
layout: default
title: Lab 2 - Virtual Network Usage
parent: Module 6 - Virtual Networks
---
# Module 5 - Lab 2 : Security Groups
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
- Create a Security Group.
- Attach the Security Group to the Isolated Virtual Network.


# Create a Security Group.

## 6.2.1

Navigate to **Networks -> Security Groups**. 

<img src="./../assets/ca-images/module6_lab2/s1.png">

    
## 6.2.2

Press the **Create Security Group** button to add a new **Security group**.

<img src="./../assets/ca-images/module6_lab2/s2.png">

    
## 6.2.3

Name it as **App Group**. 

<img src="./../assets/ca-images/module6_lab2/s3.png">

    
## 6.2.4

Add a new **Outbound** Rule with the settings as seen below.

<img src="./../assets/ca-images/module6_lab2/s4.png">

    
## 6.2.5

Add another Rule. This time it's the **Inbound** rule to allow MySQL **3306/tcp** traffic from **isolated**.

<img src="./../assets/ca-images/module6_lab2/s5.png">

    
## 6.2.6

Add another **Inbound** rule. This time allow traffic targeting the port **22/tcp** from **Any Network**.

<img src="./../assets/ca-images/module6_lab2/s6.png">

    
## 6.2.7

Add another **Inbound** rule. This time allow traffic to **5000/tcp** from the **isolated** network.

<img src="./../assets/ca-images/module6_lab2/s7.png">

## 6.2.8

Verify that you have the rules added and press **Finish** to add the **Security Group**.

<img src="./../assets/ca-images/module6_lab2/s8.png">

## 6.2.9

Enable **Other** users to **Use** the newly created Security Group.

<img src="./../assets/ca-images/module6_lab2/s9.png">

# Attach the Security Group to the Isolated Virtual Network.

## 6.2.10

Select the **isolated-vnet** Virtual Network and go to the **Security groups** tab. 

<img src="./../assets/ca-images/module6_lab2/s10.png">

## 6.2.11

Press the **Select Security Group** button.

<img src="./../assets/ca-images/module6_lab2/s11.png">

## 6.2.12

Add the **App Group** and then press **Continue**.

<img src="./../assets/ca-images/module6_lab2/s12.png">

## 6.2.13

You should end up having only the **App Group** security group attached to the **isolated-vnet** virtual network.

<img src="./../assets/ca-images/module6_lab2/s12.png">
    
### Congratulations, you've completed the assignment!
{: .no_toc}