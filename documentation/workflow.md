---
layout: page
title: "WNoDeS Workflow"
description: ""
---

{% include JB/setup %}
Standard Worker Node (WN) and Virtual Worker Node (VWN) can coexist together.
The Bait (wnodes\_bait) is a process acting as a batch job attractor.
Jobs requiring to be executed over non-virtual machine (if the mixed mode is enabled) are handled as a standard job of batch system.
The worker node resources are dynamically modified in order to reflect the real availability of the host, which needs to keep in consideration the resources allocated for the execution of the Virtual Machines (VM).
The other jobs dispatched on the Bait are immediately suspended.
The Hypervisor (HV) instantiates the VM by using the requested virtual image and the job execution is migrated on the VM.

### WNoDeS process flow for batch

![How WNoDeS works]({{site.baseurl}}/images/wnodes_high_level.png) 
_Figure 1 - How WNoDeS works._
Figure 2 describes the process flow for a batch job that needs to be dispatched from the Batch System to a virtual computing resource - known as virtual job.
A job is received by the Batch System, through whatever method is supposed (e.g., local or Grid job submission). At this point the following steps are followed:


1. the Batch System dispatches the job to be executed on a WN under the WNoDeS control containing HV and Bait services;
2. the WN receives the job. A pre-execution script stops the job, gets the job's requirements (e.g., required RAM);
3. the pre-execution script sends a notification message to a process called Bait running on the WN, advising on a new job to process;
4. the process Bait running on the WN evaluates if the job needs to run on and asks the HV if the job's requirements are available;
5. the HV contacts the central  Nameserver (NS) service to obtain a lease hostname for the VM
6. the HV creates a VM for job execution using the KVM stack;
7. the HV notifies Bait when the VM is ready;
8. the Bait migrates the job to the VM provided by the HV;
9. the job goes through a second pre-execution script on the VM, which notifies the Bait that the job has started;
10. when the job finishes, a post-execution script on the VM notifies the Bait;
11. the Bait delivers the VM and waits for a new job.

![ The WNoDeS process flow.]({{site.baseurl}}/images/wnodes_architecture.png) 
_Figure 2 - The WNoDeS process flow._
