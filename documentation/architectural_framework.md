---
layout: page
title: "Overall architectural framework"
description: ""
---
{% include JB/setup %}


Users can easily access virtualized and customized computing resources through three interfaces: the local and Grid interfaces are used for batch jobs submission, whilest the cloud interface (OCCI) lets users instantiate a Virtual Machine for interactive usage. LRMS is still the key component. It is robust, flexible, scalable and can manage thousands of nodes concurrently. WNoDeS dynamically instantiates virtual resources on demand.

Figure 1 summarises the WNoDeS architecture whose key points are: On-demand virtual service provisioning; Flexible, integrated scheduling policies; Multiple access interfaces; Multiple authentication methods; Integrated access to existing (e.g., Grid) infrastructures; Access to external resources.

![WNoDeS architecture](https://web2.infn.it/wnodes/images/stories/WNoD/wnodes_architecture.png) 

Figure 1 - WNoDeS architecture.

The Open Cloud Computing Interface (OCCI) API is being developed within the Open Grid Forum to access "Infrastructure as a Service" (IaaS) based Clouds. It is a slim RESTful based API, allowing users to access and manage (computing, storage, network) resources using a Uniform Resource Identifier (URI).