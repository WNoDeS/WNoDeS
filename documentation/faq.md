---
layout: page
title: "FAQ"
description: "FAQ"
group: faq
dropdown: project
---
{% include JB/setup %}

#### How are users supposed to specify an image tag into the JDL file?
An attribute of the Glue1.3 specification is used to allow job submissions to a specific virtual machine (VM). The attribute ApplicationSoftwareRunTimeEnvironment was chosen. This choice potentially leads to name clashes since this attribute originally meant to describe a list of software packages installed on the hosts. In order to limit this issue, a naming convention for virtual images has been adopted,  prepending the value of this attribute with a known string.

#### Do you plan to use other batch systems, like SluRM, along with the ones (Torque/Maui e LSF) already supported?
Yes, we have plans to support more batch systems. If you have specific requests, please contact us with details.

#### Which component is responsible to check resources availability?
Globally, a dedicated WNoDeS component called “Nameserver” allocates VMs to the systems where WNoDeS is installed. On individual systems where WNoDeS is installed, a component called "bait" checks local resource availability.

#### How can a VO acquire extra resources if it is has already reached its maximum limit?
In order to add extra resources the cluster administrator should change the priority in the batch system configuration for the specific VO. WNoDeS uses batch system policies to schedule jobs and VMs.
How is the VM started?

A WNoDeS component called “Hypervisor” automatically creates and starts VMs on demand, i.e. when the need for a VM arises.

#### Can an experiment require a custom VM?
Generally speaking, a formal agreement must be found with the WNoDeS administrator, who can create the new image or accept the one provided by the experiment.
 
