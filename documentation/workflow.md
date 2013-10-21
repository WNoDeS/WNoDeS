---
layout: page
title: "WNoDeS Workflow"
description: ""
---

{% include JB/setup %}

Real and Virtual WN can coexist together. The bait host is a virtual machine, acting as a batch job attractor. Batch jobs dispatched
on the bait are immediately suspended. The HyperVisor (HV) instantiates the VM using the requested virtual image. Job execution is
migrated on the VM.

![How WNoDeS works](https://web2.infn.it/wnodes/images/stories/WNoD/wnod_high_level.png) 
Figure 2 - How WNoDeS works.