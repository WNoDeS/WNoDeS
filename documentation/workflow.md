---
layout: page
title: "WNoDeS Workflow"
description: ""
---

{% include JB/setup %}
**This page contains information that may not apply to the latest release and it will be soon updated**

Real and Virtual WN can coexist together. The bait host is a virtual machine, acting as a batch job attractor. Batch jobs dispatched
on the bait are immediately suspended. The HyperVisor (HV) instantiates the VM using the requested virtual image. Job execution is
migrated on the VM.

![How WNoDeS works](https://web2.infn.it/wnodes/images/stories/WNoD/wnod_high_level.png) 
Figure 1 - How WNoDeS works.

### WNoDeS process flow.

The process flow for a batch job that needs to be dispatched from the LRMS to a computing resource is described in Figure 3.  A job is received by the LRMS, through whatever method is supposed (e.g., local or Grid job submission). At this point the following steps are followed:

* step 0: The LRMS dispatches the job for execution to a bait VWN.
* step 1: The bait VWN receives the job. A job starter script stops the job, gets the jobs requirements (e.g., required RAM), and sends a notification message to a process called wnodes_bait running on the bait, signaling there is a new job to process.
* step 2: The process wnodes_bait running on the bait asks a process called  running on the KVM VMM (on the same physical node) to provide a VM for job execution.
* step 3: The process wnodes_hypervisor running on the KVM VMM creates or recycles a VM for job execution, and notifies wnodes_bait when the VM is ready.
* step 4: wnodes_bait migrates the job to the VM provided by wnodes_hypervisor.
* step 5: The job goes through a second job starter script on the VWN, which notifies wnodes_bait on the bait that the job has started. The job then runs normally on the VWN.
* step 6: When the job finishes, a post-execution script on the VWN notifies wnodes_bait on the bait.
* step 7: wnodes_bait on the bait closes the VWN and goes back to waiting for a new job.

![ The WNoDeS process flow.](https://web2.infn.it/wnodes/images/stories/WNoD/wnod_process_flow.png) 
Figure 2 - The WNoDeS process flow.