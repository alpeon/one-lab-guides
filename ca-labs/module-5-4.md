---
layout: default
title: Lab 4 - Image Management
parent: Module 5 - Storage
---
## Module 5 - Lab 4 : Image Management
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
- Download an Image from the Marketplace.
- Import an Image from the URL.
- Create a VirtioFS image. 
- Change the Persitency of an Image.


# Download Images from the Marketplace.

    
## 5.4.1

Navigate to **Storage -> Apps** to access the list of available Images from all  Marketplaces. 

<img src="./../assets/ca-images/module5_lab4/s1.png">

    
## 5.4.2

In the search bar enter **Alpine Linux 3.21** and locate the **Alpine Linux 3.21** image. 

Please select the **correct architecture**!

<img src="./../assets/ca-images/module5_lab4/s2.png">

    
## 5.4.3

Press the Import button.

<img src="./../assets/ca-images/module5_lab4/s3.png">

    
## 5.4.4

Keep the names as is, then proceed to the next page of the wizard.

<img src="./../assets/ca-images/module5_lab4/s4.png">

    
## 5.4.5

From the datastores select the **shared image datastore** one and press **Finish**.

<img src="./../assets/ca-images/module5_lab4/s5.png">

# Import an Image from the URL.
    
## 5.4.6

Navigate to the **Storage -> Images**.

<img src="./../assets/ca-images/module5_lab4/s6.png">

    
## 5.4.7

Press **Create Image** to start the wizard.

<img src="./../assets/ca-images/module5_lab4/s7.png">

    
## 5.4.8

Name image as **Alpine Linux DB Server**.

Set the URL to the one provided by your instructor.

<img src="./../assets/ca-images/module5_lab4/s8.png">

    
## 5.4.9

Select the shared image datastore and proceed to the next screen.

<img src="./../assets/ca-images/module5_lab4/s9.png">

    
## 5.4.10

Set the **BUS** to **Virtio**.

<img src="./../assets/ca-images/module5_lab4/s10.png">


## 5.4.11

Keep the **Custom Atributes**  empty and press **Finish**

<img src="./../assets/ca-images/module5_lab4/s11.png">


# Create a VirtioFS Image. 
    
## 5.4.12

Press the **Create Image** buton once again.

<img src="./../assets/ca-images/module5_lab4/s12.png">

## 5.4.13

Name it the way you wish. 

Set **Type** to **Filesystem** and **Path** to **/var/tmp/one/share**.

<img src="./../assets/ca-images/module5_lab4/s13.png">

## 5.4.14

This time due to being the **virtiosfs** type - place it on the **virtiofs-compatible** datastore. 

<img src="./../assets/ca-images/module5_lab4/s14.png">

## 5.4.15

Keep this page as is and proceed to the next page. 

<img src="./../assets/ca-images/module5_lab4/s15.png">

## 5.4.16

Keep this page as is and finish the process.

<img src="./../assets/ca-images/module5_lab4/s16.png">

## 5.4.17

If everything is correct - your shared virtiofs image must be in the **Ready** state!

<img src="./../assets/ca-images/module5_lab4/s17.png">

# Share Images and Change the Persitency of an Image.
    
## 5.4.18

Select both Alpine-based Images.

<img src="./../assets/ca-images/module5_lab4/s18.png">

## 5.4.19

Then press the **Persistent** button.
    
<img src="./../assets/ca-images/module5_lab4/s19.png">

## 5.4.20

After that confirm the mode change.
    
<img src="./../assets/ca-images/module5_lab4/s20.png">

## 5.4.21 

You should end up with three images, two of them must be **Persistent**. 

<img src="./../assets/ca-images/module5_lab4/s21.png">
    
# Congratulations, you've completed the assignment!
{: .no_toc}