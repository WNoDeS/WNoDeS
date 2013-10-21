---
layout: page
title : Grid Integration       
header : Post Archive
description: ""
---
{% include JB/setup %}

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

[R1] Cecchi Marco, et all., "The gLite Workload Management System, Advances in Grid and Pervasive Computing", the 4th International Conference, GPC 2009, Geneva, Switzerland, May 4-8, Proceedings, Lecture Note in Computer Science, 5529, 256--268, 2009.

[\[R2\] Fabrizio Pacini, "Job Description Language JDL Attributes Specification"] (https://edms.cern.ch/document/590869/120EGEE-JRA1-TEC-590869-JDL-Attributes-v0-4)

[\[R3\] http://www.cs.wisc.edu/condor/classad] (http://www.cs.wisc.edu/condor/classad)

[\[R4\] http://www.cs.wisc.edu/condor ] (http://www.cs.wisc.edu/condor)

[\[R5\] Sergio Andreozzi, et all., "Glue Specification v. 20" http://www.ogf.org/documents/GFD.147.pdf] (http://www.ogf.org/documents/GFD.147.pdf)
