---
layout: page
title: "Use of Grid Resources through Cloud Interfaces"
description: ""
---
{% include JB/setup %}

Requirements for making Cloud Computing (namely IaaS) services available are seen with increasing frequency.
Europe has largely invested in Grid Computing in the last years, establishing an infrastructure that is now used by several thousands of scientists in full production.
Making IaaS services available **using the same resources that are used for providing Grid services** is then absolutely desirable.
To avoid static partitioning of resources between Grid and Cloud services, the two services should provide the same mechanisms for authorization.
In computing centers of the European Grid Infrastructures, fair resource sharing between Grid jobs is assured by Local Resource Management Systems (LRMS).
To avoid moving resources for those available for Grid jobs through the batch system, IaaS machines must be served via the same mechanism.

WNoDeS enables the creation of virtual worker nodes on demand, which can then be used to run Grid or Cloud services.
