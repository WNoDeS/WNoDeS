---
layout: page
title: "Deployment Experience"
description: ""
---

The WNoDeS system has been used at INFN Tier-1 to support about 1500 VWNs. Roughly 1 million jobs have been executed on the VWNs, without major problems. The deployment has been initially done to support the following use cases:

* A user community requiring very strict control over what is or is not installed on the systems.
* The migration to a new version of an Operating System.

For what regards the second use case, the INFN Tier-1 currently supports about 20 different user communities or Virtual Organizations. In the past, all these communities had agreed to have RedHat Enterprise Linux version 4 (RHEL4) or a compatible version (like Scientific Linux) as Operating System on the computing nodes. Recently, several large communities, mainly working on the Large Hadron Collider project [R6] have expressed the requirement  of a rapid upgrade to RedHat Enterprise Linux version 5 (RHEL5) or to a compatible version. Instead of partitioning the INFN Tier-1 cluster between a set node running RHEL4 and another one running RHEL5, we are installing WNoDeS in a phased way onto the INFN Tier-1 cluster. Each VWN will initially be able to run RHEL4 or RHEL5 and perhaps other images as well.  The actual image to be used is determined by the user community a job belongs to: for example, a job belonging to an user of one of the LHC communities may trigger the creation of a VWN running RHEL5, while a job belonging to a user of other communities may trigger the creation of a VWN running RHEL4. More fine-grained control is possible: since the determination of which image to run is contained in LRMS pre-execution scripts, all is needed to support more elaborate requirements is to write the appropriate commands in these scripts, differentiating users or communities based on variable which are available to the LRMS. It would thus be possible to have a community identified by a certain Unix group ID to run a certain virtual image; and a subset of the same community, identified perhaps by a set of specific users belonging to that community, to run a different virtual image.
