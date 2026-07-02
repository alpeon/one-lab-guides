---
layout: default
title: Lab 1 - Datastores
parent: Module 5 - Storage
---
# Module 5 - Lab 1 : Datastores
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

total 20K
drwxr-x--- 5 oneadmin oneadmin 4.0K Jul 21 07:16 .
drwxr-x--- 9 oneadmin oneadmin 4.0K Jul 22 19:39 ..
drwxr-xr-x 2 oneadmin oneadmin 4.0K Jul 21 07:16 .isofiles
drwxr-xr-x 2 oneadmin oneadmin 4.0K Jul 21 07:04 1
drwxr-xr-x 2 oneadmin oneadmin 4.0K Jul 21 07:04 2
```


## 5.1.2

Note that your output might have it other way around!

From the Node 1's Command Line list the Node 2's directories. 

```console
ssh lab-X-node2 'ls -lah ~/datastores/'
total 8.0K
drwxr-x--- 2 oneadmin oneadmin 4.0K Jul 21 07:11 .
drwxr-x--- 7 oneadmin oneadmin 4.0K Jul 22 10:07 ..
```

Perform the same on Node 3.

```console
ssh lab-X-node3 'ls -lah ~/datastores/'

total 12K
drwxr-x--- 3 oneadmin oneadmin 4.0K Jul 21 07:16 .
drwxr-x--- 6 oneadmin oneadmin 4.0K Jul 21 07:11 ..
drwxrwxr-x 2 oneadmin oneadmin 4.0K Jul 21 08:02 0
```

# Answer these questions
{: .note}
> Why is the Frontend Node missing the directory with ID 0 ?

> Why only one Virtualization Node has the directory with ID 0?


# Congratulations, you've completed the assignment!
{: .no_toc}