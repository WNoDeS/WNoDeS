---
layout: page
title: WNoDeS
base_url: "./"
---
The Worker Nodes on Demand Service (WNoDeS) is an INFN-developed architecture that makes possible to dynamically allocate virtual resources out of a common resource pool.

WNoDeS integrates the Grid and Cloud paradigms exploiting the same physical resources.
It is built around a tight integration with a Local Resource Management System (a batch system) and is running in production at the INFN Tier-1 Computing Center. Its main characteristics are:

* Full integration with existing computing resources, scheduling, policing, monitoring and accounting workflow.
* On-demand virtual resource provisioning and VLAN support to dynamically isolate Virtual Machines depending on service type and customer requests.
* Support for users to select and access WNoDeS-based resources through Grid, Cloud interfaces, or also through direct job submissions.

WNoDeS realizes a Cloud over Grid approach.
Other approaches in the field of Grid and Cloud integration are quite different from the WNoDeS one:

* Grid of Clouds - which is the approach being pursued by the EGI project with a dedicated work package.
It has the objective of creating a federation of various Cloud sites, running different software stacks, which need to interoperate publishing resource discovery information and accounting/monitoring data to the central EGI services.
Solutions for a central images marketplace, for a unified Authentication and Authorization and for a cloud brokering system are also under investigation.
* Grid over Cloud - which implies the creation of Grid sites on top of a Cloud infrastructure though landscape deployment of virtual resources.
The provided Grid infrastructure can exploit the dynamic nature of the Clouds, provisioning resources according to the real needs of the users.



WNoDeS lets local, Grid and cloud computing converge upon Dynamically Provided Virtualized Resources.
