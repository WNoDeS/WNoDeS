---
layout: page
title: "WNoDeS Workflow"
description: ""
---

{% include JB/setup %}
Standard Worker Node (WN) and Virtual Worker Node (VWN) can coexist together.
The bait (wnodes\_bait) is a process acting as a batch job attractor.
Jobs requiring to be executed over non-virtual machine (if the mixed mode is enabled,) has handled as a standard job of batch system with the only difference that the worker node resources are dynamically modified in order to reflect the real availability of the host. The host in fact need to keep in consideration the resources allocated for the execution of the VM.
The other jobs dispatched on the bait are immediately suspended.
The HyperVisor (HV) instantiates the Virtual Machines (VM) using the requested virtual image and the job execution is migrated on the VM.

### WNoDeS process flow for batch

![How WNoDeS works](https://web2.infn.it/wnodes/images/stories/WNoD/wnod_high_level.png) 
_Figure 1 - How WNoDeS works._

The process flow for a batch job that needs to be dispatched from the Batch System to a computing resource is described in Figure 2.
A job is received by the Batch System, through whatever method is supposed (e.g., local or Grid job submission). At this point the following steps are followed:

1. The Batch System dispatches the job for execution to a WN enabled as an HV. 
2. The WN receives the job. A job starter script stops the job, gets the jobs requirements (e.g., required RAM), and sends a notification message to a process called wnodes\_bait running on the HV, advising on a new job to process.
3. The process wnodes\_bait running on the HV evaluate if the job need to run on  asks a process called running on the KVM VMM (on the same physical node) to provide a VM for job execution.
4. The process wnodes\_hypervisor running on the HV creates a VM for job execution, and notifies wnodes\_bait when the VM is ready.
5. wnodes\_bait migrates the job to the VM provided by wnodes\_hypervisor.
6. The job goes through a second job starter script on the Virtual Worken Node (VWN), which notifies wnodes\_bait on the bait that the job has started. The job then runs normally on the VWN.
7. When the job finishes, a post-execution script on the VWN notifies wnodes\_bait on the bait.
8. wnodes\_bait on the bait closes the VWN and goes back to waiting for a new job.

![ The WNoDeS process flow.](https://web2.infn.it/wnodes/images/stories/WNoD/wnod_process_flow.png) 
_Figure 2 - The WNoDeS process flow._
