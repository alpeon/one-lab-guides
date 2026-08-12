---
layout: default
title: Lab 1 - VM Templates
parent: Module 8 - VM Templates & VMs
---
# Module 8 - Lab 1 : VM Templates 

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
- Adjust the Alpine Linux 3.21 VM Template.
- Create a VM Template for the DB Server.
- Adjust Permissions for VM Templates and Images.


# Adjust the Alpine Linux 3.21 VM Template.
    
## 8.1.1

From the Dashboard press **VM Templates** shortcut button to access the VM Template management screen.

<img src="./../assets/ca-images/module8_lab1/s1.png">

    
## 8.1.2

Select the **Alpine Linux 3.XX** VM Template and press the rename button.

<img src="./../assets/ca-images/module8_lab1/s2.png">

    
## 8.1.3

Name it as **alpine-app-server** and press anywhere outside of the text box.

<img src="./../assets/ca-images/module8_lab1/s3.png">

## 8.1.4

While the template remains selected - press the **Update** button.

<img src="./../assets/ca-images/module8_lab1/s4.png">
    
## 8.1.5

Change the **Memory** value from **256** to **2048** and proceed ot the **Next** step of the wizard.

<img src="./../assets/ca-images/module8_lab1/s5.png">


## 8.1.6

Navigate to the **Network** section and press the **Attach NIC** button. 

<img src="./../assets/ca-images/module8_lab1/s6.png">

    
## 8.1.7

Toggle the **SSH connection** switch under the **Guacamole Connections** section.

<img src="./../assets/ca-images/module8_lab1/s7.png">

    
## 8.1.8

On the next page select the **routable-vnet** network then proceed through other pages without changes and save changes.

<img src="./../assets/ca-images/module8_lab1/s8.png">

    
## 8.1.9

You should end up having the **NIC0: routable-vnet** attached with the **SSH** label.

<img src="./../assets/ca-images/module8_lab1/s9.png">

## 8.1.10

**Attach another vNIC**

Perform this task on your own without any guidance!

{: .warning}
> This time place it into the **isolated-vnet** virtual network and **without any Guacamole setting enabled**.

You should end up with two vNICs in two vNETs.

<img src="./../assets/ca-images/module8_lab1/s10.png">
    
## 8.1.11

Switch to the **Context** tab.

<img src="./../assets/ca-images/module8_lab1/s11.png">

## 8.1.12

Add the following code to the **Start script** field and proceed to the next page.

```console
source /root/bin/activate
cd /root/app/app
python3 -u app.py &

cloudflared tunnel --url http://127.0.0.1:5000 > /var/log/cfd.log 2>&1 &
sleep 60
export CFD=$(grep -o -e 'https.*trycloudflare.com' /var/log/cfd.log)
onegate vm update $VMID --data CFD_URL=$CFD
```
<img src="./../assets/ca-images/module8_lab1/s12.png">
    
## 8.1.13

Toggle the **Add OneGate token** switch.

<img src="./../assets/ca-images/module8_lab1/s13.png">

## 8.1.14

Scroll down to the **User inputs** section and create a new input.

Name: **DB_HOST**

Type: **Text**

Either keep "Description" empty or anything you like.

**Set the default value to 127.0.0.1**

Toggle the **Mandatory** switch.

Press **+ Add**

<img src="./../assets/ca-images/module8_lab1/s14.png">

## 8.1.15

Add another one

Name: **APP_DATABASE**

Type: **Text**

Either keep "Description" empty or anything you like.

Default value: **app**

Toggle the **Mandatory** switch.

Press **+ Add**

<img src="./../assets/ca-images/module8_lab1/s15.png">
    
## 8.1.16

Add another one

Name: **DB_USER**

Type: **Text**

Either keep "Description" empty or anything you like.

Default value: **appuser**

Toggle the **Mandatory** switch.

Press **+ Add**

<img src="./../assets/ca-images/module8_lab1/s16.png">
    
## 8.1.17

Add another one

Name: **DB_USER_PASSWORD**

Type: **Password**

Either keep "Description" empty or anything you like.

Toggle the **Mandatory** switch.

Press **+ Add**

<img src="./../assets/ca-images/module8_lab1/s17.png">
    
## 8.1.18

Finally add the **optional** **TIMEZONE** input.

Name: **TIMEZONE**

Type: **Text**

Either keep "Description" empty or anything you like.

Default value: **UTC**

Keep  **Mandatory** switch un-toggled.

Press **+ Add**

<img src="./../assets/ca-images/module8_lab1/s18.png">
    
## 8.1.19

You should have 5 variables in the list.

<img src="./../assets/ca-images/module8_lab1/s19.png">

## 8.1.20

Navigate further down and expand the **Context Custom Variables** section.

Set the Variable name **SET_HOSTNAME** and map it to the **$NAME** value and press the **+** button.

<img src="./../assets/ca-images/module8_lab1/s20.png">

## 8.1.21

Now press the **Save** button.

## Create a VM Template for the DB Server.

## 8.1.22

Select the **alpine-app-server** VM Template and press the **Clone** button. 

<img src="./../assets/ca-images/module8_lab1/s22.png">
    
## 8.1.23

Change the name to **alpine-db-server** and confirm the cloning. 

Make sure that the checkbox remains empty!

<img src="./../assets/ca-images/module8_lab1/s23.png">

    
## 8.1.24

Select the **alpine-db-server** and press the **Update** button.

<img src="./../assets/ca-images/module8_lab1/s24.png">

    
## 8.1.25

Scroll down and set the **CPU** to 2. Then proceed to the next configuration screen.

<img src="./../assets/ca-images/module8_lab1/s25.png">


## 8.1.26

Under the storage section locate the currenly attached disk and press the **three dots** button. 

Select the **Edit** from there.

<img src="./../assets/ca-images/module8_lab1/s26.png">


## 8.1.27

Select the **Alpine Linux DB Server** image and then the **Save** button. 

<img src="./../assets/ca-images/module8_lab1/s27.png">


## 8.1.28

Then switch to the **Network** tab, locate the NIC that is attached to the **routable-vnet** networks and detach it. 

<img src="./../assets/ca-images/module8_lab1/s28.png">

## 8.1.29

Confirm the detachment.

<img src="./../assets/ca-images/module8_lab1/s29.png">

## 8.1.30

Switch to **Context** tab and change the **Start script**.

```console
rc-service mariadb start
```

<img src="./../assets/ca-images/module8_lab1/s30.png">

## 8.1.31

Remove all **User inputs** but **TIMEZONE** and **Save** the template.

<img src="./../assets/ca-images/module8_lab1/s31.png">

# Adjust Permissions for VM Templates and Images.

## 8.1.32

Go to Node 1's Command Line and execute the onetemplate command.

```console
onetemplate list
```

Write down the IDs of all VM Templates you have and execute the **onetemplate** one more time to share them with others.

```
onetemplate chmod <LOWEST ID>...<HIGHEST ID> 644
```

    
## 8.1.33

Use the **oneimage** command to list all images.

```console
oneimage list

```
Write down the IDs of all Images you have and execute the **oneimage** one more time to share them with others.

```console
oneimage chmod <LOWEST ID>...<HIGHEST ID> 644
```

# Congratulations, you've completed the assignment!
{: .no_toc}