---
layout: page
title: "FAQ"
description: "FAQ"
group: faq
---
{% include JB/setup %}

#### Image tag into the JDL file
Q: How are users supposed to specify an image tag into the JDL file?
An attribute of the Glue1.3 specification is used to allow job submissions to a specific virtual machine (VM). The attribute ApplicationSoftwareRunTimeEnvironment was chosen. This choice potentially leads to name clashes since this attribute originally meant to describe a list of software packages installed on the hosts. In order to limit this issue, a naming convention for virtual images has been adopted,  prepending the value of this attribute with a known string.

#### Other batch systems
Q: Do you plan to use other batch systems?
Like SluRM, along with the ones (Torque/Maui e LSF) already supported?
Yes, we have plans to support more batch systems. If you have specific requests, please contact us with details.

#### Resources availability
Q: Which component is responsible to check resources availability?
Globally, a dedicated WNoDeS component called “Nameserver” allocates VMs to the systems where WNoDeS is installed. On individual systems where WNoDeS is installed, a component called "bait" checks local resource availability.

#### Extra resources
Q: How can a Virtual Organization acquire extra resources, if it is has already reached its maximum limit)
In order to add extra resources the cluster administrator should change the priority in the batch system configuration for the specific VO. WNoDeS uses batch system policies to schedule jobs and VMs.

#### Virtual machine start
Q: How is the Virtual Machine started?
A WNoDeS component called “Hypervisor” automatically creates and starts VMs on demand, i.e. when the need for a VM arises.

#### Custom virtual machine
Q: Can an experiment require a custom Virtual Machine?
Generally speaking, a formal agreement must be found with the WNoDeS administrator, who can create the new image or accept the one provided by the experiment.

#### WNoDeS intallation
Q: Where is WNoDeS installed?
WNoDeS is installed at [INFN CNAF](https://www.cnaf.infn.it/) since 2008. Recently it has also installed at [INFN Laboratori Nazionali di Legnaro](http://www.lnl.infn.it/).

## Mixed Mode FAQ

#### What is WNoDeS mixed mode?
WNoDeS mixed mode (in short: mixed mode) is a configuration mode that lets WNoDeS to send batch jobs on a physical system and, at the same time, to instantiate virtual machines (VMs) on the same system. These VMs can be used to also run batch jobs or to support Cloud services.

#### Why is mixed mode useful?
With mixed mode, you can install WNoDeS on an existing farm without first deciding which nodes will support virtualization and which not.
Whith mixed mode enabled, any node of a farm may act as a traditional, "real" node (running only traditional batch jobs), as a pure hypervisor (running only VMs), or as a node capable of running, at the same time, both jobs on the physical hardware (without thus incurring penalties typical of virtual infrastructures), and jobs or cloud services on VMs (thus exploiting capabilities offered by virtual environments).

Therefore, mixed mode greatly enhances the flexibility of the configuration of a farm and lets system administrators progressively integrated WNoDeS into existing data centers.

#### When should I turn mixed mode on?
If you have for example jobs that require full performance from, for example, the I/O subsystem, without incurring the penalties brought about by virtualization, you can turn mixed mode on and configure WNoDeS so that these jobs are sent to a physical system rather than to a VM.

Or, if you have jobs that need to access hardware that is not easily amenable to being virtualized like, for example, GPGPUs, with mixed mode you can configure WNoDeS so that such jobs are only sent to a physical system.

In both cases above you can configure WNoDeS so that on the same systems where the jobs mentioned are running you can also have VMs handling other types of requests supported by WNoDeS like, for example, other types of jobs, or cloud instantiations.

#### When should I not turn mixed mode on?
With mixed mode, each physical system where WNoDeS is installed has to be part of the LRMS cluster. This may have some side effects:

1. you will give jobs the possibility to run on the physical system. This means that the physical system has to be properly configured to run these jobs, for example in terms of programs installed that will be required by the jobs. From a security point of view, the jobs will run in user space like any job in a traditional farm.
2. since the physical system will be part of the LRMS cluster, it may use up LRMS licenses proportionally to the number of physical cores. Then, if the same system is also used to create VMs that will batch jobs as well, each of these VMs may use up LRMS licenses proportionally to the number of cores of the VMs. In the worst case, with mixed mode enabled a system with N cores may use up to 2xN LRMS licenses. With commercial LRMS', this may in some cases be a limitation.

If you want to disallow batch jobs access to the physical systems, and want to use these system just as pure hypervisors to manage VMs, do not enable mixed mode. Without mixed mode it is not necessary (nor recommended) to have the physical systems as part of the LRMS cluster. Without mixed mode, you could put physical system for example on private, management networks, without any direct access to jobs, Cloud instances, or the Internet.