---
layout: default
title: Lab 2 - Security Groups
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

    
## 6.2.1

Navigate to **Networks -> Security Groups**. 

<img src="./../assets/ca-images/module6_lab2/s1.png">

    
## 6.2.2

Press the **Create** button to add a new **Security group**.

<img src="./../assets/ca-images/module6_lab2/s2.png">

    
## 6.2.3

Name it as **App Group**. 

<img src="./../assets/ca-images/module6_lab2/s3.png">

    
## 6.2.4

Add a new **Outbound** Rule with the settings as seen below.

<img src="./../assets/ca-images/module6_lab2/s4.png">

    
## 6.2.5

Add another Rule. This time it's the **Inbound** rule to allow MySQL TCP traffic from **isolated**.

<img src="./../assets/ca-images/module6_lab2/s5.png">

    
## 6.2.6

Add another **Inbound** rule. This time allow traffic targeting the port **22/tcp** from **Any Network**.

<img src="./../assets/ca-images/module6_lab2/s6.png">

    
## 6.2.7

Add another **Inbound** rule. This time allow traffic to 5000/tcp from the **isolated** network.

<img src="./../assets/ca-images/module6_lab2/s7.png">

#### 5.2.8

Verify that you have the rules added and press **Finish** to add the **Security Group**.

<img src="./../assets/ca-images/module6_lab2/s8.png">

## 6.2.9

Enable **Other** users to **Use** the newly created Security Group.

<img src="./../assets/ca-images/module6_lab2/s9.png">

    
## 6.2.10

Select the **isolated** Virtual Network and press the **Update** button. 

<img src="./../assets/ca-images/module6_lab2/s10.png">

    
## 6.2.11

Add the **App Group** and then remove the **default group**, then press **Finish**.

<img src="./../assets/ca-images/module6_lab2/s11.png">
    
### Congratulations, you've completed the assignment!
{: .no_toc}