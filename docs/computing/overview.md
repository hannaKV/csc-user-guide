# Overview

Puhti and Mahti are CSC's supercomputers. Puhti has been available for CSC users since
2 September 2019 and Mahti has been available since 26 August 2020.

Puhti contains CPU nodes with a range a memory sizes as well as a large GPU partition (Puhti AI), while
Mahti contains homogeneous CPU nodes and is meant for larger jobs (minimum 128 CPU-cores). Mahti also contains a GPU partition from 2021 (Mahti AI) with latest generation Nvidia GPUs.
See [specifications](available-systems.md) for details on the systems.

CSC supercomputers use the Linux operating system and we recommend that you are familiar with basics of [Linux command line usage](../support/tutorials/env-guide/overview.md) before starting.

## Accessing Puhti and Mahti

To be able to use CSC's supercomputers, you need to have a CSC user account that belongs to
a computing project that has access to the respective supercomputer. CSC user
accounts and projects are managed in [my.csc.fi](https://my.csc.fi) portal. 
Further instructions are provided in the [Accounts section](../accounts/index.md) of this user guide.

## Connecting to the supercomputers

Connect using a ssh client:

```
ssh yourcscusername@puhti.csc.fi
```
or
```
ssh yourcscusername@mahti.csc.fi
```


This will connect you to one of the login nodes. If you need to connect
to a specific login node, use the command:

```
ssh yourcscusername@puhti-login<number 1-2>.csc.fi
```
or
```
ssh yourcscusername@mahti-login<number 1-2>.csc.fi
```

Where **yourcscusername** is the username you get from CSC.

For more details, see the [connecting](connecting.md) page. 


## Usage policy

### Login nodes
When you login to CSC supercomputers, you end up to one of the login nodes of the cluster.
These login nodes are shared by all users and they are **not** intended for heavy computing.

The login nodes should be used only for:

 * compiling
 * managing batch jobs
 * moving data
 * **light** pre- and postprocessing

Here **light** means **one-core-jobs** that finish in **minutes** and require **a few GiB** of memory at maximum.
All the other tasks are to be done in compute nodes either as normal [batch jobs](running/getting-started.md)
or as [interactive batch jobs](running/interactive-usage.md).
Programs not adhering to these rules will be terminated without warning.

!!! warning "Important"
    The login nodes are not meant for long or heavy processes.

### GPU nodes

Puhti-AI's V100 GPUs should only be used for the following workloads:

 * Machine Learning (ML) / Artificial Intelligence (AI) workloads
 * Code development for porting codes GPUs 
 * HPC applications benefitting greatly from GPUs, or even only supporting GPUs. This means that the code should be at least **2x** as fast on one V100 GPU compared to one Puhti node. Please confirm this for your use case and keep the log files and corresponding SLURM jobids in case we ask for them later.


Mahti-AI's A100 GPUs should only be used for the following workloads:

 * ML/AI workloads
 * Code development for porting codes GPUs 
 * HPC applications that can use the new hardware features in A100 (tensor cores). This means that the code should be at least **3x** as fast on one A100 GPU compared to one Mahti node. Please confirm this for your use case and keep the log files and corresponding SLURM jobids in case we ask for them later.



The rationale for this policy is:

 * The majority of compute resources are CPU based. Hence it is likely that you (and everyone) will
actually also get results faster due to less queuing if your code can use both CPUs and GPUs.
 * Puhti-AI and Mahti-AI have been specifically funded to be used in
machine learning (ML) and artificial intelligence (AI) related
research. A significant part of these resources must be available for
this use.
 *  ML/AI workloads often use libraries and frameworks specifically optimized for GPUs. Typically, a ML/AI workflow will be many times faster if run on a GPU, compared to running e.g. using a full node of CPUs. Typically, the benefit for GPU optimized other HPC workloads is smaller, although sometimes still faster than with a full CPU node.
 * The significant improvement of the A100 GPU cards in Mahti-AI over V100 in Puhti-AI are the tensor cores. There are many ML/AI workloads
that can make use of them resulting in large speedups, whereas non-AI/ML workloads often don't. Optimal usage of this resource requires ability to utilize the tensor cores. 




### Scalability

Don't allocate more resources to your job that it can use
efficiently. This needs to be verified for each new code and job type
(different input) by a scaling test. The policy is that the job should
be **at least 1.5 times faster** when you double the resources
(cores). [Instructions for performing a scalability
test](../../support/tutorials/cmdline-handson/#scaling-test-for-an-mpi-parallel-job).
Please also consider [other important factors related to performance.](performance.md)



## Projects and quotas

Working in Puhti is based on projects. The computing and storage resources are allocated to projects and when you start a batch job, you must always define the project that the job belongs to.

Projects are managed with [MyCSC portal](https://my.csc.fi), were you can add services, resources and users to your CSC projects.

In Puhti, you can check your currently active Puhti-projects with command:

```text
csc-projects
```
This command shows information for all your CSC projects that have access to Puhti. You can select just one project to be reported with option `-p` . For example:
```bash
[kkayttaj@puhti ~]$ csc-projects -p project_2012345
-----------------------------------------------------------------
Project: project_2012345	Owner: Kalle Käyttäjä
Title: "Ortotopology modeling"
Start: 2015-12-17 End: 2022-03-16 Status: open
Budget:   1174188  Used   1115284 Remain:      58904
Latest resource grant: 2019-03-04
-----------------------------------------------------------------
```
The command reports the owner of the project, title, start and end dates. In addition the command prints out the budgeting information for the project: how many billing units have been granted to your project, how much has been used and how much still remain. 

The [disk areas](disk.md) of your Puhti projects can be checked with command:
```text
csc-workspaces
```

## Using Puhti and Mahti


* [Systems](available-systems.md): What computational resources are available
* [Connecting](connecting.md): How to connect to  CSC supercomputers 
* [Disk areas](disk.md): What places are there for storing data on CSC supercomputers 
* [Modules](modules.md): How to find the programs you need
* [Applications](../apps/index.md): Application specific instructions.
* [Running jobs](running/getting-started.md): How to run programs on the supercomputers 
* Using compilers and building your applications:
    * [Puhti](compiling-puhti.md)
    * [Mahti](compiling-mahti.md)
* [Debugging applications](debugging.md): How to debug your applications
* [Performance analysis](performance.md): How to understand the performance of your applications
