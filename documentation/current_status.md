---
layout: page
title: "Current WNoDeS Status"
description: ""
---

{% include JB/setup %}

WNoDeS is already deployed on the INFN Tier-1 production infrastructure. Selection of VM images works either statically or  dynamically, through standard local and Grid job submission commands. All the supported VOs run on WNoDeS. WNoDeS lets us still provide SLC4 support without allocating resources statically. Several virtual images available. They really provide a customized
virtual environment for different VOs.

Due to some delays, virtualized slots are still 1600. We hope to grow up to 2600 in a short term. More than 50% slots available
in the cluster will be virtualized.

Manage GPFS fileSystems on the VM is major issue: in terms of time spent to develop the right way to support it (thanks INFN Tier-1
storage group for all the support); in terms of time spent to have the fileSystem ready on the VM. Usually more than 100% of the time needed to get the machine ready to run the job.

