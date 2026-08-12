---
layout: default
title: Lab 1 - Explore Datastore Directories
parent: Module 5 - Storage
---
# Module 5 - Lab 1 : Explore Datastore Directories
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

- Inspect the datastores directory on every Host.

## 5.1.1

From the Node 1's Command Line list the contents of datastores directory.

```console
ls -lah ~/datastores/
```

```console
total 16K
drwxr-xr-x 2 oneadmin oneadmin 4.0K Aug 10 06:31 1
drwxrwxrwx 2 oneadmin oneadmin 4.0K Aug 10 06:57 100
drwxrwxrwx 2 oneadmin oneadmin 4.0K Aug 10 06:57 101
drwxr-xr-x 2 oneadmin oneadmin 4.0K Aug 10 06:31 2
```


## 5.1.2

Note that your output might have it other way around!

From the Node 1's Command Line list the Node 2's directories. 

```console
ssh lab-X-node2 'ls -lah ~/datastores/'
```

```console
total 16K
drwxr-x--- 4 oneadmin oneadmin 4.0K Aug 10 06:58 .
drwxr-x--- 5 oneadmin oneadmin 4.0K Aug 10 08:39 ..
drwxrwxrwx 2 oneadmin oneadmin 4.0K Aug 10 06:57 100
drwxrwxrwx 2 oneadmin oneadmin 4.0K Aug 10 06:57 101
```

Perform the same on Node 3.

```console
ssh lab-X-node3 'ls -lah ~/datastores/'
```

```console
total 16K
drwxr-x--- 4 oneadmin oneadmin 4.0K Aug 10 06:58 .
drwxr-x--- 5 oneadmin oneadmin 4.0K Aug 10 06:36 ..
drwxrwxrwx 2 oneadmin oneadmin 4.0K Aug 10 06:57 100
drwxrwxrwx 2 oneadmin oneadmin 4.0K Aug 10 06:57 101
```

## 5.1.3

Now let's inspect the fstab file.

```console
ssh lab-X-node3 'cat /etc/fstab'
```

```console
LABEL=cloudimg-rootfs	/	 ext4	discard,commit=30,errors=remount-ro	0 1
LABEL=BOOT	/boot	ext4	defaults	0 2
LABEL=UEFI	/boot/efi	vfat	umask=0077	0 1
lab-X-node1:/system /var/lib/one/datastores/100 nfs4 defaults,_netdev,nfsvers=4.2 0 0
lab-X-node1:/images /var/lib/one/datastores/101 nfs4 defaults,_netdev,nfsvers=4.2 0 0
```

As you can see in the output the directories 100 & 101 both are served via NFS4 protocol.

{: .warning}
> Also it's worth mentioning that in this lab environment frontend servers as the NFS server, however in real-life scenario you will have a dedicated Storage system for this!

# Answer the question
{: .note}
> Why hypervisor nodes are missing directories 1 & 2 ?

# Congratulations, you've completed the assignment!
{: .no_toc}