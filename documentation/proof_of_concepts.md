---
layout: page
title: "Proof of concepts"
description: ""
---


### DVN

The extensive use of virtualization technologies in cloud environments has created the need for a new network access layer residing on hosts connecting the various Virtual Machines.
In fact, virtualized deployment environments impose requirements on networking for which traditional models are not well suited.
For example, hundreds of users issuing cloud requests for which full access (i.e., including root privileges) to VMs are requested, typically require the definition of network separation at layer through the use of virtual LANs.
However, in large computing centers, due for example to the number of installed network switches, to their characteristics, or to their heterogeneity, the dynamic (or even static) definition of many VLANs is often impractical or simply not possible.

WNoDeS DVN [1] is a solution to the problem of dynamic virtual networking based on the use of the Generic Routing Encapsulation Protocol.
GRE is used to encapsulate VM traffic so that the configuration of the physical network switches doesn't have to change.
This solution can be used to tackle problems such as dynamic network isolation and mobility of VMs across hosts.

* Reduce the network broadcast domain.
* Grant different network access polices to every virtual machine.

VLANs provide network isolation, particularly requested for cloud computing, where users get root access to virtual machine.

### VIP

WNoDeS Virtual Interactive Pool [2] is an on-demand provisioning of virtual user interfaces for local users out of a common resource pool.
Based on a CLI, it can be easily used by computing centre users seeking for additional, unused resources.
Provides customized computing resources for interactive usage like, for example, software development or physics analysis.
The provisioned virtual resource matches user requirements for RAM, CPU, bandwidth and shared file systems to be mounted.
A caching mechanism is available, to reduce system provisioning time.



**References**

[1] Salomoni D., Caberletti M., ["A Dynamic Virtual Networks Solution for Cloud Computing"](http://www.computer.org/csdl/proceedings/sccompanion/2012/4956/00/4956a526-abs.html), Proceedings of the 2nd International Workshop on Network-aware Data Management, November 11, 2012, Salt Lake City, Utah, USA

[2] Grandi C., Italiano A., Salomoni D., Calabrese Melcarne A.K, ["Virtual pools for interactive analysis and software development through an integrated Cloud environment"](http://web2.infn.it/wnodes/download/CHEP10-Grandi-VIP-101019.pdf), CHEP 2010, Taipei

