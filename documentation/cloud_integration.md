---
layout: page
title: "Cloud Integration"
description: ""
---
{% include JB/setup %}

## Clouds and Grids: A Very Short Introduction

While Grid interfaces are widely used by large user communities, Cloud computing offers significant advantages for many uses (among them, pay-asyou-go models, simplified access). Ideally, though, one would like to adopt Cloud services so that:

* Resources are shared between access interfaces (Grid, Cloud, or else).
* Scalability is ensured.
* Existing services and agreements are not required to change.
* Resource center policies and know-how are honored.
* New services can attract both existing and new customers.

These are both key challenges and opportunities for existing Grid infrastructures.

Some of the typical new service requests. Customer-definable software environments. This is a feature that finds several uses in "traditional" Grids as well. Setting up dynamic pools of virtual servers (e.g., user interfaces, or worker nodes for parallel interactive analysis). More generally, flexibly allocating hardware resources through complex advance-reservation requests. Instantiating pre-packaged, ready-to-go services. Truly distributed, on-demand, Cloud storage. Not everybody "speaks Grid": providing access to distributed, traditional Grid infrastructures as if they were not Grids, also to non-traditional users, like Public Administrations, or to the private sector.

The key problem is one of integration between several access interfaces (Grid, Cloud, or else).

Grids and Clouds (abstracting from the concept of "a Grid job", which one should regard as an implementation detail) basically target the use of resources. The two terms come from different grounds, but really they are just different interfaces to access resources.
Users may actually benefit joining an existing infrastructure, rather than building (or "buying") a new one. This may actually not be a user’s choice. Sharing of data and resources across Grid/Cloud interfaces should be encouraged. Leveraging on multi-year investments and know-how on Grids to incrementally evolve and build new services is a strategic decision. Grids like EGEE are production infrastructures, serving the scientific needs of many (big and small) research communities.


The question is then how you do integrate Grids and Clouds.

## Intergrating Cloud Services

WNoDeS delivers access to Cloud services through the Open Cloud Computing Interface, implementing a subset of the OCCI API, using X.509 authentication and exposing a REST interface.

![WNoDeS evolution](https://web2.infn.it/wnodes/images/stories/WNoD/wnodes_evolution.png "Figure 3 - WNoDeS evolution.") 

Figure 3 - WNoDeS evolution.

The WNoDeS authentication gateway is described in Figure 4.

![WNoDeS evolution](https://web2.infn.it/wnodes/images/stories/WNoD/wnodes_authn.png "Figure 4 - WNoDeS authentication gateway.")

Figure 4 - WNoDeS authentication gateway.

The WNoDeS Cloud RESTful web service is accessible via a basic alphastage Web application (see demo). 

Missing video..

At the moment, upon a VM deployment request a "dummy job" is sent to the LRMS, and from there to a bait; eventually the dummy job runs on the allocated
Cloud VM. This has some disadvantages (like having the Cloud VM to be part of the LRMS cluster). The next WNoDeS version will support Cloud VM instantiations so that:

* A Cloud VM is totally oblivious of the LRMS.
* Control of the Cloud VMs is fully distributed, and consistency is ensured by the baits.

In case of Cloud allocations, only wallclock time is considered for accounting purposes.

Apart from the new architecture for instantiation of Cloud VMs, the following enhancements are targeted for the first WNoDeS public release (3Q10):

* Support for private/public ssh keys (using libguestfs to change VM images on the fly).
* Support for the OCCI commands deploy, start, stop, restart.
* VM image selection (only a pre-defined image is currently available.)
* VOMS and authentication gateway integration.
* Network parameter: requested subnet (public, private.)
* Network parameter: requested throughput.
* Virtual storage (details still to be worked out for this item.)

