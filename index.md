---
layout: page
title: WNoDeS
base_url: "./"
---

The Worker Nodes on Demand Service (WNoDeS) is an INFN-developed architecture that makes possible to dynamically allocate virtual resources out of a common resource pool.

WNoDeS realizes a Cloud over Grid approach which is quite original in the European Grid Infrastructure (EGI) ecosystem of software products and tools.

Other approaches in the field of Grid and Cloud integration are quite different from the WNoDeS one:

* Grid of Clouds - which is the approach being pursued by the EGI project with a dedicated work package.
It has the objective of creating a federation of various Cloud sites, running different software stacks, which need to interoperate publishing resource discovery information and accounting/monitoring data to the central EGI services.
Solutions for a central images marketplace, for an unified Authentication and Authorization and for a cloud brokering system are also under investigation.
* Grid over Cloud - which implies the creation of Grid sites on top of a Cloud infrastructure though landscape deployment of virtual resources.
The provided Grid infrastructure can exploit the dynamic nature of the Clouds, provisioning resources according to the real needs of the users.

The WNoDeS focus is on Everything as a Service, where Everything may be hardware, software, data, platform, infrastructure.

WNoDeS dynamically provides virtualized and customized computing resources on demand.
Virtualized resources can be used to run applications software, interactive analysis, software development, services.
It allows to integrate the Grid and Cloud paradigms exploiting the same physical resources.

It is built around a tight integration with a LRMS (a "batch system") and is running in production at the INFN Tier-1 Computing Center. Its main characteristics are:

* Full integration with existing computing resource scheduling, policing, monitoring and accounting workflow.
* On-demand virtual resource provisioning and VLAN support to dynamically isolate Virtual Machines depending on service type / customer requests.
* Support for users to select and access WNoDeS-based resources through Grid, Cloud interfaces, or also through direct job submissions.


WNoDeS lets local, Grid and cloud computing converge upon Dynamically Provided Virtualized Resources.
