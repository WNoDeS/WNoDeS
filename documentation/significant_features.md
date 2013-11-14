---
layout: page
title : Significant Features
header : Post Archive
description: ""
---
{% include JB/setup %}



### Mixed Mode Feature

The Mixed Mode [1] is one of the main functionalities of WNoDeS.
It was introduced to make it able to handle physical computing resources both as traditional member nodes of a batch system to execute jobs and as hypervisor node to instantiate virtual machines.
This way a physical node can host at the same time both traditional jobs, directly running in the real machine, and also virtual ones, running in a virtual node instantiated there by the hypervisor.
This feature is optional and allows a computing centre to optimize the usage of its resources by integrating real and virtual resources.
As in the WNoDeS deployment with mixed mode turned off, the instantiated virtual machines can be used to execute batch jobs, to perform analysis or to run applications.
Through this functionality it is possible to execute jobs having special resources need, such as GPU, or higher I/O requirements directly on the physical node, thus avoiding the slowdown introduced by the virtualization overhead.
Moreover, on the same physical node, provided it has enough memory, CPUs and disk, the mixed mode can also offer virtualized services for those users requiring them.
The mixed mode mechanism handles users' requests in collaboration with the batch system.
These can be traditional batch jobs requests, submitted locally or via grid: in this case by using the site-specific configuration file, the batch job can be executed either on the physical node or on the virtual machine.
There can be also cloud provisioning requests, submitted via the Cloud CLI or the IGI portal: in this case the provisioning will only be furnished by a virtual machine.
WNoDeS translates these users' requests into jobs that are handled by the batch system.
This Mixed mode has been available since WNoDeS 2.0.0-2 in the EMI-2 Matterhorn distribution [15] whilst the Cloud CLI that interacts with the WNoDeS cloud platform has been released since the version WNoDeS 3.0.0-1 in the EMI-3 Monte Bianco distribution [15].
Figure shows how the mixed mode turned on works: the job in queue to the batch system is sent to the bait service that verifies the state of the virtual machines contacting the hypervisor service.
In relation to the type of job and the site-specific configuration, the batch job will be executed on either virtual machine or physical one.
The cloud job will be always executed on the virtual machine.


![WNoDeS Framework]({{site.baseurl}}/images/mixed_mode_on_new.png )


### VLAN support

Different virtual machines running on the same hypervisor can belong to different VLAN.

* Reduce the network broadcast domain.
* Grant different network access polices to every virtual machine. VLANs provide network isolation, particularly requested for cloud computing, where users get root access to virtual machine. 





WNoDeS enables the possibility for Grid users to select at job submission time the virtual image that will be loaded on the Worker Node that will execute the job.

In the gLite middleware, in particular in the gLite Workload Management System (WMS) [R1], users can describe the characteristics of their jobs using a well-known formalism called Job Description Language (JDL) [R2]. The JDL is based on Classified Advertisements (ClassAds) [R3], developed within the Condor project [R4]. ClassAds basically consists of a list of (key, value) pairs that represent the various characteristics of a job (like input files, arguments, and executable) in terms of requirements, constraints and preferences  (such as physical and virtual memory, CPU, and Operating System). The attributes used for describing high-end resources come from a common schema, the GLUE Schema [R5], born from a joint effort to standardize and facilitate interoperation between various Grid infrastructures.

The GLUE Schema v1.3, which is currently used on the EGEE infrastructure, foresees the SubCluster entity to provide details of the mechines that offer execution environments to jobs. This entity refers to a homogeneous set of hosts with respect to a given set of attributes. One or more SubClusters are aggregated in a Cluster, which instead represents a heterogeneous set of resources. In our case, the SubCluster entity provides attributes for specifying the Operating System or processor and memory capabilities.

None of the attributes in SubCluster is suitable for describing something like the virtual image that a host is running. At the time of the definition of the GLUE Schema v.1.3, virtualization was not spread enough to raise use cases for the description of virtual resources in terms of images. While waiting for an evolution of the GLUE Schema that takes into account the recent advances in virtualization and the role of virtualization is playing in modern computing centers, we pragmatically decided to make the SubCluster entity fit to our goal. The attribute that we have choosen is ApplicatioNSoftwareRunTumeEnvironment, originally meant to describe a list of software packages installed on the hosts. Even if this choice could be considered semantically incorrect (also note that a virtual image should be ideally defined at the Cluster level) this attribute was, among what we could find in GLUE 1.3, quite suitable to be used for a proof of concept. The choice also potentially leads to name clashes, in the case a user, unaware of WNoDeS, used the name of a virtual machines for the purpose is normally used for. To limit the risks of that, we decided to use a naming convention for virtual images, prepending the string in ApplicationSoftwareRunTimeEnvironment with a known string. This makes very unlikely that the same name is used with another purpose in mind.

## Best description of the involved middleware

The gLite middleware allows submission to the Computing Element (CE) through the gLite WMS. With WMS version 3.1 and jobs submitted using the glite-wms-job-submit command on a gLite User Interface, the CERequirements JDL attribute can be used to specify requirements for the CE, as shown in the following example:

    CERequirements = "other.GlueCEPolicyMaxCPUTime >= 100 &&
                      other.GlueHostMainMemoryRAMSize > 2000";

To enable the virtual image selection, this attribute must contain the
GlueHostSoftwareApplicationRuntimeEnvironment string. WNoDeS uses a naming convention to understand which of the members of this attribute is requesting a virtual image.

    CeForwardParameters =  {"GlueHostSoftwareApplicationRuntimeEnvironment"};
    CeRequirements = "(Member(\"vm_etics_slc4\",
                              other.GlueHostApplicationSoftwareRuntimeEnvironment))

The requirement for the virtual image can be concatenated with other CE requirements. For example:

    CeRequirements = "other.GlueHostMainMemoryRAMSize > 16 &&
                     other.GlueHostProcessorClockSpeed >= 2800 &&
                     (Member(\"FDTD\", other.GlueHostApplicationSoftwareRuntimeEnvironment))";

requires the virtual image identified by FDTD to be used on a virtual machine with the specified memory and clock speed capabilities.

The WMS forwards user requirements to CREAM. CREAM then interacts with the underlying Local Resource Manager (LRMS) using a component called BLAH. BLAH is an abstraction layer that provides a uniform interface to different batch systems, among which LSF and PBS. BLAH manages the \verb#CERequirements# expression and sets environment variables that are eventually made available to the LRMS for consumption in scripts managing job submissions.
References

[1]

[\[2\] 