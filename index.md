---
layout: page
title: WNoDeS
base_url: "./"
---

During the last years INFN has worked in several European projects with the aim of establising a European Grid Infrastructure to serve scientists. Recently, Cloud Computing has emerged as an alternative pattern to Grid Computing. Though sometimes they are presented to be competitive, we believe that Grid and Cloud Computing serve different use cases and can work together in improving Distributed Computing Infrastructures (DCIs) offered to scientists in Europe.

These pages collect the work that is being carried on at INFN on the integration between Grid and Cloud services. We are mainly focusing efforts on the following two themes:
<div class="row-fluid marketing">
 <div class="row">
  <div class="span6">
#### Cloud Integration
WNoDeS delivers access to Cloud services through the Open Cloud Computing Interface, implementing a subset of the OCCI API, using X.509 authentication and exposing a REST interface.
[Read more]({{site.baseurl}}/documentation/cloud_integration.html)

#### Dynamic Provisioning of Virtual Worker Nodes
WNoDeS makes possible to run batch jobs on virtual worker nodes, i.e. on computing resources functionally identical to traditional servers, but running on virtual machines.
[Read more]({{site.baseurl}}/documentation/vwn_dynamic_provisioning.html)

  </div>
  <div class="span6">
#### Grid Integration
WNoDeS enables the possibility for Grid users to select at job submission time the virtual image that will be loaded on the Worker Node that will execute the job.
[Read more]({{site.baseurl}}/documentation/grid_integration.html)

#### Grid Resourses through Cloud (IaaS) interfaces
WNoDeS enables the creation of virtual worker nodes on demand, which can then be used to run Grid or Cloud services.
[Read more]({{site.baseurl}}/documentation/grid_resources_through_cloud_interfaces.html)
  </div>
 </div>
</div>