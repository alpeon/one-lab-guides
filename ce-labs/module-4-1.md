---
layout: default
title: Lab 1 - OneApps
parent: Module 4 - OneApps
---
# Module 4 - Lab 1 : OneApps 
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
- Clone the repositories.
- Configure and Build the VM appliance.
- Upload an Image and Instantiate the VM.
    

# The majority of commands in this section must be executed as root!


# Clone the repositories.


## 4.1.1

Clone the OneApps repository.

```console
cd ~
git clone https://github.com/OpenNebula/one-apps/
Cloning into 'one-apps'...
remote: Enumerating objects: 9027, done.
remote: Counting objects: 100% (947/947), done.
remote: Compressing objects: 100% (311/311), done.
remote: Total 9027 (delta 806), reused 645 (delta 635), pack-reused 8080 (from 3)
Receiving objects: 100% (9027/9027), 22.54 MiB | 41.07 MiB/s, done.
Resolving deltas: 100% (4819/4819), done.
```

    
## 4.1.2

Clone the repository with files.


```console
export REPO='https://github.com/OpenNebula/one-training-files.git'
rm -rf ~/Files
git clone --no-checkout $REPO  ~/Files
cd ~/Files
git sparse-checkout init --cone
git sparse-checkout set OneApps
git checkout
cd OneApps
ls -lh
total 12K
drwxr-xr-x 3 root root 4.0K Aug  4 10:13 appliances
drwxr-xr-x 3 root root 4.0K Aug  4 10:13 packer
drwxr-xr-x 2 root root 4.0K Aug  4 10:13 templates
```

# Configure and Build the VM appliance.


## 4.1.3

Navigate to the **one-apps** git repository and create duplicate the Wordpress service.

```console
cd ~/one-apps/packer
cp -R service_Wordpress service_FlaskApp
```

Change directory to FlaskApp and use sed to substitute paths and names.

```console
cd service_FlaskApp/
mv Wordpress.pkr.hcl FlaskApp.pkr.hcl
sed -i 's/Wordpress/FlaskApp/g' *.pkr.hcl
sed -i 's/Wordpress/FlaskApp/g' gen_context
sed -i 's/alma8.qcow2/ubuntu2204.qcow2/g' *.pkr.hcl
```

    
## 4.1.6

Add two scripts from Files.

```console
cp ~/Files/OneApps/packer/ubuntu/*.sh ~/one-apps/packer/ubuntu/
```

Create the **FlaskApp** dir under the **appliances** and copy the shell script from Files.

```console
mkdir -p ~/one-apps/appliances/FlaskApp
cp ~/Files/OneApps/appliances/FlaskApp/*.sh ~/one-apps/appliances/FlaskApp/
```

    
## 4.1.7

Edit the **Makefile.config**.

```console
vi ~/one-apps/Makefile.config
```

Append it with the new service.

```console
SERVICES_AMD64 := service_Wordpress service_VRouter service_OneKE service_OneKEa capone \
                service_Harbor service_SlurmController service_SlurmWorker service_MinIO \
                service_Vllm service_Capi service_FabricManager service_OneKS service_example \
                service_Nim service_FlaskApp
```

Run the builder from the one-apps directory and wait until the appliance .qcow2 image can be found inside the **export** directory.

```console
cd ~/one-apps
make ubuntu2204 service_FlaskApp
...
==> Builds finished. The artifacts of successful builds are:
--> null.null: Did not export anything. This is the null builder
--> qemu.FlaskApp: VM files in directory: build/service_FlaskApp
--> qemu.FlaskApp: VM files in directory: build/service_FlaskApp
[INFO] Packer service_FlaskApp done
```


# Upload an Image and Instantiate the VM.

    
## 4.1.8

Copy the service Image to the **/var/tmp/one** directory and change the ownership.

```console
cp export/service_FlaskApp.qcow2 /var/tmp/one/
chown oneadmin:oneadmin /var/tmp/one/service_FlaskApp.qcow2
```

Import the appliance.

```console
oneimage create -d 1 --name 'Service FlaskApp' --path /var/tmp/one/service_FlaskApp.qcow2
ID: 0
```


## 4.1.9

As root edit the Virtual Machine template.

```console
vi ~/Files/OneApps/templates/vm.tmpl
```

Map it to the Image ID from the previous step.

```console
DISK=[
    IMAGE="Service FlaskApp",
    IMAGE_ID="<YOUR IMAGE ID>",
    IMAGE_UNAME="oneadmin",
    SIZE="10240",
    TARGET="vda" ]
```

Copy the template and adjust permissions.

```console
cp ~/Files/OneApps/templates/vm.tmpl /var/lib/one/
chown oneadmin:oneadmin /var/lib/one/vm.tmpl
sudo -i -u oneadmin
onetemplate create vm.tmpl
ID: 1
```

    
## 4.1.10

As the **root** user perform the restart of the frr service.

```console
systemctl restart frr
```

Instantate the VM

```console
onetemplate instantiate <template id>
There are some parameters that require user input. Use the string <<EDITOR>> to launch an editor (e.g. for multi-line inputs)
* (APP_DATABASE)
    Press enter for default (appdb).
* (DB_USER)
    Press enter for default (appuser).
* (DB_USER_PASSWORD)
    Password:
VM ID: 1
```


## 4.1.11

Test the application.

```console
vmip=$(onevm show <vm id> -j | jq -r '.VM.TEMPLATE.CONTEXT.ETH0_IP')
curl $vmip:5000/create-db
{"message":"Table 'data' created successfully"}

curl $vmip:5000/insert-dummy
{"message":"Dummy data inserted successfully"}

curl $vmip:5000/insert-dummy
{"message":"Dummy data inserted successfully"}

curl $vmip:5000/get-data
[{"data1":"2025-08-04 10:02:30","data2":"30","id":1},{"data1":"2025-08-04 10:02:32","data2":"24","id":2}]
```
    
# Congratulations, you've completed the assignment!
{: .no_toc}