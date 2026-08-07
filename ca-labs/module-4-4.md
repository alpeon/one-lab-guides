---
layout: default
title: Lab 3 - Host Management
parent: Module 4 - Hosts
---
# Module 4 - Lab 3: Host Management
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
- Change the State of a Host with ID 0.

### Change the State of a Host with ID 0.

## 4.3.1

From the Node 1's Command Line execute the **disable** subcommand to Disable the Host with ID 0.

```console
onehost disable 0
```

List the hosts.

```console
onehost list

ID NAME             CLUSTER    TVM      ALLOCATED_CPU      ALLOCATED_MEM STAT
3 lab-2022-node3   default      0       0 / 200 (0%)     0K / 3.8G (0%) on
2 lab-2022-node2   default      0       0 / 200 (0%)     0K / 3.8G (0%) on
1 35.159.249.245   default      1     50 / 200 (25%)  512M / 3.8G (13%) on
0 18.153.100.94    default      0       0 / 200 (0%)     0K / 3.8G (0%) dsbl
```
## 4.3.2

Tail the log file and locate messages that are similar to the highlighted below.

Note that date/time in your output is going to be different.

```console
tail -n10 /var/log/one/monitor.log

Thu Apr 16 09:24:11 2026 [Z0][HMM][I]: Successfully monitored VM: 0
Thu Apr 16 09:24:19 2026 [Z0][HMM][I]: Successfully monitored host: 1
Thu Apr 16 09:24:19 2026 [Z0][HMM][I]: Successfully monitored host: 0
Thu Apr 16 09:24:34 2026 [Z0][HMM][I]: Successfully monitored VM: 0
Thu Apr 16 09:24:34 2026 [Z0][HMM][I]: Successfully monitored host: 2
Thu Apr 16 09:24:41 2026 [Z0][HMM][I]: Successfully monitored VM: 0
Thu Apr 16 09:25:04 2026 [Z0][HMM][I]: Successfully monitored VM: 0
Thu Apr 16 09:25:05 2026 [Z0][HMM][D]: Updated Host 0, state DISABLED
Thu Apr 16 09:25:12 2026 [Z0][HMM][I]: Successfully monitored VM: 0
Thu Apr 16 09:25:18 2026 [Z0][HMM][I]: Successfully monitored host: 3
```

# Congratulations, you've completed the assignment!
{: .no_toc}