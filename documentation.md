---
layout: page
title: "Documentation"
description: ""
---
{% include JB/setup %}


The Worker Nodes on Demands Service (WNoDeS) is a software INFN is developing. It is built around a tight integration with a LRMS (a "batch system") and is running in production at the INFN Tier-1 Computing Center. Its main characteristics are:

* Full integration with existing computing resource scheduling, policing, monitoring and accounting workflow.
* On-demand virtual resource provisioning and VLAN support to dynamically isolate Virtual Machines depending on service type / customer requests.
* Support for users to select and access WNoDeS-based resources through Grid, Cloud interfaces, or also through direct job submissions.

The WNoDeS focus is on Everything as a Service, where Everything may be hardware, software, data, platform, infrastructure.

WNoDeS dynamically provides virtualized and customized computing resources on demand. Virtualized resources can be used to run applications software, interactive analysis, software development, services and so on. In a few words, WNoDeS lets local, Grid and cloud computing converge upon Dynamically Provided Virtualized Resources.

* [Overall architectural framework]({{site.baseurl}}/documentation/architectural_framework.html)
* [WNoDeS workflow]({{site.baseurl}}/documentation/workflow.html)
* [WNoDeS Process Flow]({{site.baseurl}}/documentation/process_flow.html)
* [Virtual Image Selection and Loading]({{site.baseurl}}/documentation/virtual_image.html)
* [Monitoring and Logging]({{site.baseurl}}/documentation/monitoring_logging.html)
* [Deployment Experience]({{site.baseurl}}/documentation/deployment_experience.html)
* [Current Status]({{site.baseurl}}/documentation/current_status.html)
* [New Features]({{site.baseurl}}/documentation/new_features.html)