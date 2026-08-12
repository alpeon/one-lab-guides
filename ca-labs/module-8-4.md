---
layout: default
title: Lab 4 - VM Operations
parent: Module 8 - VM Templates & VMs
---
# Module 8 - Lab 4 : VM Operations

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
- Resize a VM.
- Migrate a VM.
- Perform the Recover - Recreate & Restore actions.
- Save a VM as a VM Template.

# Resize a VM.
    
## 8.4.1

Connect to Node 1 using SSH and execute the onevm list command.

```console
onevm list
```

```console
ID USER     GROUP    NAME                       STAT  CPU     MEM HOST                      TIME
3 oneadmin oneadmin alpine-app-server-3        runn    1      2G lab-2109-node2        0d 01h12
2 oneadmin oneadmin alpine-db-server-2         runn    2      2G lab-2109-node3        0d 01h29
```

Poweroff the database VM.

```console
onevm poweroff <VM ID>
```

Wait until the VM is powered down. Use the onevm command to check the state of VMs.

```console
ID USER     GROUP    NAME                       STAT  CPU     MEM HOST                     TIME
3 oneadmin oneadmin alpine-app-server-3        runn    1      2G lab-2109-node2       0d 01h16
2 oneadmin oneadmin alpine-db-server-2         poff    2      2G lab-2109-node3       0d 01h33
```

## 8.4.2

Once VM is down - execute the resize command and set the CPU value to 1.

```console
onevm resize <VM ID> --cpu 1
```

The resize procedure shouldn't take long. Power on the VM once done.

```console
onevm resume <VM ID>
```

And wait until the VM is back running.

```console
onevm resume <VM ID>
```

# Migrate a VM.

## 8.4.3

Navigate to Sunstone.

Select the **alpine-db-server** VM.

<img src="./../assets/ca-images/module8_lab4/s3.png">
    
## 8.4.4

Note the host the VM is currently running and from the list select the **Migrate** action.

<img src="./../assets/ca-images/module8_lab4/s4.png">
    
## 8.4.5

Select another host in the same cluster and proceed to **Advanced Option**.

<img src="./../assets/ca-images/module8_lab4/s5.png">
    
## 8.4.6

Keep it on the same datastore and press **Finish**. 

<img src="./../assets/ca-images/module8_lab4/s6.png">
   
## 8.4.7

The VM will enter the **Save migrate** state and then will cycle through other migration-related states.

<img src="./../assets/ca-images/module8_lab4/s7.png">

## 8.4.8

Wait until the VM is back to **Running** state.

<img src="./../assets/ca-images/module8_lab4/s8.png">

# Perform the Backup, Recover - Recreate & Restore actions.
    
## 8.4.9

Firstly let's recreate the VM from scratch.

Select **Recover** from the VM actions menu.

<img src="./../assets/ca-images/module8_lab4/s9.png">

## 8.4.10

Select the **Recreate** operations from the recover menu and press **Continue**. 

<img src="./../assets/ca-images/module8_lab4/s10.png">

    
## 8.4.11

Wait until the VM is back to the **Running** state.

<img src="./../assets/ca-images/module8_lab4/s11.png">

    
## 8.4.12

Visit the application's page once again and press the **Read the Travel Log**.  

<img src="./../assets/ca-images/module8_lab4/s12.png">

    
## 8.4.13

You must receive an error. With this we can confirm that the VM was recreated from scratch and now is missing the data table. 

<img src="./../assets/ca-images/module8_lab4/s13.png">

    
## 8.4.14

Press the button to create the database table. 

<img src="./../assets/ca-images/module8_lab4/s14.png">

    
## 8.4.15

In case of success - return back to the main page.

<img src="./../assets/ca-images/module8_lab4/s15.png">

    
## 8.4.16

Go back to Sunstone and visit the *alpine-db-server's** **Snapshot** page. 

Press the **Create snapshot** button. 

<img src="./../assets/ca-images/module8_lab4/s16.png">
    
## 8.4.17

Give your snapshot a name and start the snapshot creation.

<img src="./../assets/ca-images/module8_lab4/s17.png">

## 8.4.18

The VM will enter the **Hotplug snapshot** state. 

<img src="./../assets/ca-images/module8_lab4/s18.png">
    
## 8.4.19

Wait until the VM is back **Running**.

<img src="./../assets/ca-images/module8_lab4/s19.png">

    
## 8.4.20

Go back to the test app and press the middle button to create a record in the database.

<img src="./../assets/ca-images/module8_lab4/s20.png">

    
## 8.4.21

Execute the log action a few times to create more records. 

<img src="./../assets/ca-images/module8_lab4/s21.png">

## 8.4.22

Then return to the main page.

<img src="./../assets/ca-images/module8_lab4/s22.png">

## 8.4.23

Query the database for the data.

<img src="./../assets/ca-images/module8_lab4/s23.png">

## 8.4.24

Verify that the data table isn't empty.

<img src="./../assets/ca-images/module8_lab4/s24.png">

## 8.4.25

Return to Sunstone and revert back from the snapshot. 

<img src="./../assets/ca-images/module8_lab4/s25.png">

## 8.4.26

Confirm the action.

<img src="./../assets/ca-images/module8_lab4/s26.png">

## 8.4.27

Wait for VM to return back to the **Running** state.

<img src="./../assets/ca-images/module8_lab4/s27.png">

## 8.4.28

Request the data once again.

<img src="./../assets/ca-images/module8_lab4/s28.png">

## 8.4.29

The output supposed to be without any records.

<img src="./../assets/ca-images/module8_lab4/s29.png">

# Save a VM as a VM Template.

## 8.4.30

Poweroff the **alpine-db-server** by selecting the **Poweroff** action from the **VM State** dop-down menu.

<img src="./../assets/ca-images/module8_lab4/s30.png">

## 8.4.31

Once the VM is in **poweroff** state - press the **Save as Template** button. 

<img src="./../assets/ca-images/module8_lab4/s31.png">

## 8.4.32

Name it the way to idenitfy that with this VM template the data table already exists.

<img src="./../assets/ca-images/module8_lab4/s32.png">

## 8.4.33

The VM will enter the **Hotplug save as power off** state.

<img src="./../assets/ca-images/module8_lab4/s33.png">

## 8.4.34

Check the **Images** page and verify that the new image has been created (or in the process of creation).

<img src="./../assets/ca-images/module8_lab4/s34.png">

## 8.4.35

As the last step - verify that the VM Template also exists and is ready to be deployed.

<img src="./../assets/ca-images/module8_lab4/s35.png">

# Congratulations, you've completed the assignment!
{: .no_toc}