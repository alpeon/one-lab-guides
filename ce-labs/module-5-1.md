---
layout: default
title: Lab 1 - Services
parent: Module 5 - Services
---
# Module 5 - Lab 1 : Services 
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
- Import the Service Template.
- Instantiate the Service Template.
- Scale the Service Role.
- Run the Test Application.
- Destroy the running Service. 
    

# Import the Service Template.
    
## 5.1.1

Navigate to **Storage -> Apps**.

<img src="./../assets/ca-images/module5_lab1/s1.png" class="img_80_percent">

    
## 5.1.2

Enter **OneKE** in the search and in the **Filter** drop-down set **Type** to **Service Template**.

<img src="./../assets/ca-images/module5_lab1/s2.png" class="img_70_percent">

    
## 5.1.3

Locate the **Service OneKE 1.31** and press **Import**.

<img src="./../assets/ca-images/module5_lab1/s3.png" class="img_80_percent">

    
## 5.1.4

You can change the **Name** and **VM Template** name if you wish, however it's better to keep it as is.

<img src="./../assets/ca-images/module5_lab1/s4.png" class="img_80_percent">

    
## 5.1.5

Select the **default** datastore and press **Finish**.

<img src="./../assets/ca-images/module5_lab1/s5.png" class="img_80_percent">


# Instantiate the Service Template.


## 5.1.6

From the Frontend Node's Command Line run the **oneflow-template** command.

```console
oneflow-template instantiate Service\ OneKE\ 1.31
```

Leave most of the variables as is (simply press Enter or Return everytime there's a prompt) aside form the ones mentioned below.

Make sure to map correctly the Virtual Networks. Public - **evpn0** and Private - **evpn1**.

```console
...
    * (ONEAPP_K8S_LONGHORN_ENABLED) Enable Longhorn
    Press enter for default (NO). YES
...
* (ONEAPP_K8S_TRAEFIK_ENABLED) Enable Traefik
    Press enter for default (NO). YES
...
There are some networks that require user input. Use the string <<EDITOR>> to launch an editor (e.g. for multi-line inputs)
* (Public) Public
    TYPE Existing(1), Create(2), Reserve(3). Press enter for default. 1
    VN ID. 0
* (Private) Private
    TYPE Existing(1), Create(2), Reserve(3). Press enter for default. 1
    VN ID. 1
ID: 1
```

    
## 5.1.7

Wait until the service is in the state **RUNNING**.

```console
oneflow list
    ID USER     GROUP    NAME                                                                                                                                                                                          STARTTIME STAT
1 oneadmin oneadmin Service OneKE 1.31    08/03 19:47:24 RUNNING
```


## 5.1.8

Export the kubectl configuration file from the master node to verify that k8s is running.

```console
oneadmin@apetrovs-one-frontend:~$ onevm list --filter NAME~master
ID USER     GROUP    NAME                                               STAT  CPU     MEM HOST                TIME
1 oneadmin oneadmin master_0_(service_1)                                runn    2      3G 163.172.138.109     0d 00h20

onevm show <id> -j | jq -r '.VM.USER_TEMPLATE.ONEKE_KUBECONFIG|@base64d' | install -m u=rw,go= -D /dev/fd/0 ~/.kube/config
```

You should end up being able to run the **kubectl get nodes** command and have an output similar to the one below.

```console
kubectl get nodes
NAME                  STATUS   ROLES                       AGE   VERSION
oneke-ip-172-18-2-2   Ready    control-plane,etcd,master   20m   v1.31.3+rke2r1
oneke-ip-172-18-2-3   Ready    <none>                      18m   v1.31.3+rke2r1
```

    
# Scale the Service Role.

## 5.1.9

Once Service is up and running - it's time to scale the **storage** role. Currently **storage** role is running with cardinality to 0. Scale it to 1!

```console
oneflow scale Service\ OneKE\ 1.31 storage 1
```

Your service should transition to the **SCALING** state. 

```console
oneflow list
ID USER     GROUP    NAME                               STARTTIME STAT
1 oneadmin oneadmin Service OneKE 1.31                  08/03 19:47:24 SCALING
```

Wait until the transition to the **COOLDOWN** state.

```console
oneflow list
    ID USER     GROUP    NAME                                                                                                                                                                                          STARTTIME STAT
1 oneadmin oneadmin Service OneKE 1.31                  08/03 19:47:24 COOLDOWN
```

    
## 5.1.10

Run the **kubectl** command to verify that the new node has been added.

```console
kubectl get nodes
NAME                  STATUS   ROLES                       AGE     VERSION
oneke-ip-172-18-2-2   Ready    control-plane,etcd,master   28m     v1.31.3+rke2r1
oneke-ip-172-18-2-3   Ready    <none>                      27m     v1.31.3+rke2r1
oneke-ip-172-18-2-4   Ready    <none>                      2m38s   v1.31.3+rke2r1 
```

Clone the git repository.

```console
export REPO='https://github.com/OpenNebula/one-training-files.git'
rm -rf ~/Files
git clone --no-checkout $REPO  ~/Files
cd ~/Files
git sparse-checkout init --cone
git sparse-checkout set OneKE
git checkout
cd OneKE
ls -lh
total 8.0K
drwxrwxr-x 2 oneadmin oneadmin 4.0K Aug  3 20:22 test-app
-rw-rw-r-- 1 oneadmin oneadmin  943 Aug  3 20:22 test-app.tar
```

    
# Run the Test App.

    
## 5.1.11

Create the deployment. 

```console
kubectl apply -f test-app
deployment.apps/mariadb created
persistentvolumeclaim/mariadb-data created
service/mariadb created
deployment.apps/test-app created
ingressroute.traefik.io/test-app-ingress created
service/test-app-service created
```

Extract the Public (eth0) IP of the VNF VM.

```console
onevm show <vm id> -j | jq -r '.VM.TEMPLATE.CONTEXT.ETH0_IP'
172.17.2.200
```
    
## 5.1.12

It's time to test the Application. 

Try to create the database.

```console
curl 172.17.2.200/create-db
{"message":"Table 'data' created successfully"}
```

Add some dummy data a few times.

```console
curl 172.17.2.200/insert-dummy
{"message":"Dummy data inserted successfully"}
curl 172.17.2.200/insert-dummy
{"message":"Dummy data inserted successfully"}
```

And read data from the database. 

```console
curl 172.17.2.200/get-data
[{"data1":"2025-08-03 20:38:34","data2":"98","id":1},{"data1":"2025-08-03 20:38:35","data2":"73","id":2}]
```

    
## 5.1.13

Destroy the running Service.

```console
oneflow delete Service\ OneKE\ 1.31
```
 
# Congratulations, you've completed the assignment!
{: .no_toc}