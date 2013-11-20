---
layout: page
title: "Architectural framework"
description: ""
---
{% include JB/setup %}

WNoDeS realizes a Cloud-over-Grid approach which is quite original in the European Grid Infrastructure (EGI) ecosystem of software products and tools.

It allows to integrate the Grid and Cloud paradigms exploiting the same physical resources.
Other approaches in the field of Grid and Cloud integration are quite different from the WNoDeS one, we can identify:

* Grid of Clouds: which is the approach being pursued by the EGI project with a dedicated work package.
It has the objective of creating a federation of various Cloud sites, running different software stacks, which need to interoperate publishing resource discovery information and accounting/monitoring data to the central EGI services.
Solutions for a central images marketplace, for an unified Authentication and Authorization and for a cloud brokering system are also under investigation.

* Grid over Cloud: which implies the creation of Grid sites on top of a Cloud infrastructure though landscape deployment of virtual resources.
The provided Grid infrastructure can exploit the dynamic nature of the Clouds, provisioning resources according to the real needs of the users.
An example of this approach is given in [1] where the “Grid as a Service” tool is used as a PaaS infrastructure to create new Grid Sites, add computational resources to existing Grid Sites and modify the resources aggregation scheme, e.g., site queues.
Also the StratusLab project [2] provides Grid services using the StratusLab IaaS system.

A Cloud over Grid approach, similar to the one adopted by WNoDeS can be found in the CLEVER [3] middleware developed by the University of Messina, Italy.
In this section we will analyse with some details the architecture and main features of the WNoDeS system.


![WNoDeS Framework]({{site.baseurl}}/images/wnodes_framework.png  )
WNoDeS Framework. The grey boxes identify the non-WNoDeS software components such as the Batch CLI, Batch Server and Linux KVM components, whilst the white boxes show the WNoDeS software components.


The WNoDeS framework can be conceptually divided into five main layers as shown in Figure:

5. the Access Layer that represents the access point of users at the framework;
4. the Cloud Layer that handles the Cloud part of the framework;
3. the Information Management Layer that characterize the WNoDeS core; 
2. the Business Logic Layer that characterize the WNoDeS core; 
1. the Virtual Resources Layer that handles the instantiated virtual machines related to grid, batch and cloud requests.

Each layer has characterized by some WNoDeS components and has specific tasks.
The whole logic can be explained by using a bottom up approach.

At the lowest level, the Virtual Resources Layer, there is the site-specific component, which is designed to be run on the virtual machine itself to make it able to interact with the rest of the WNoDeS system.

At the Business Logic Layer level there are the bait, hypervisor and site-specific components.
The bait is the WNoDeS interface to the batch system, and its duty is to translate requests for job execution into requests for virtual machine creation and then move the actual job to the newly created virtual machine, and does this with the help of another instance of the site-specific component, which redirects batch system requests to the bait itself.
The hypervisor is the component that actually deals with the low-level detail of the virtual machine management (such as creation, configuration, and destruction) and works on top of an existing virtualization technology that is the Linux KVM.
The site-specific is the component that allows the site administrator to personalize users’ requests by considering the image characteristics.

Above that there is the Information Management Layer, which contains the nameserver and manager components.
The nameserver component keeps track of the set of virtual machines allocated to WNoDeS and assigns them to the hypervisor component when a new one is needed.
It keeps track of the configurations for the bait and hypervisor.
The manager is a Command Line Interface (CLI) component that is used by a system administrator to send commands to specific parts of the WNoDeS infrastructure for the network configuration, the image settings, the virtual machine hostnames, and the bait and hypervisor configurations.

The fourth level is the so-called Cloud Layer.
At this level there are the interfaces used to request direct instantiation of a virtual machine, which would be directly accessible to the user, rather than being used to generate virtual machines to run batch system jobs.
Two such interfaces are provided: the Cloud Service, which is a HTTP REST binding of OCCI 1.1 4, and a proprietary protocol implemented by Cachemanager Service.
The cloud component receives users’ requests and sends them to the Cachemanager Service: each request has a unique identifier that user can adopt to verify the virtual machine state.
The cachemanager component handles the provisioning of virtual machines.

Finally, there is the Access Layer, which provides a cloud CLI component that can send commands to the Cloud Layer through the OCCI interface.
The same component is used by the [IGI portal] (https://portal.italiangrid.it/) to provide cloud resources via a Web interface.
At this level it is also available a CLI to submit grid or local requests.
For what concerns the authentication and authorization, in case of cloud or grid requests the user needs to belong to a virtual organization [4] and have a valid X.509 certificate [5], whilst in case of batch requests the user needs to belong to the pool of users that is authorized to submit jobs by the batch system.
There are two common flows throughout this architecture:

1. Grid/Batch access: through jobs sent by the batch system to a WNoDeS-controlled farm or sub-farm;
2. Cloud access: through direct user requests to allocate specific virtual machines for their use.

The former flow is the following: when a new job arrives to a WNoDeS-controlled worker node, the site-specific component first redirects the request to the bait service.
The bait will then send a new request to the hypervisor to allocate a new virtual machine, and when the allocation is completed redirects the job to the new virtual machine.
After the job execution ends, the site-specific component handles the destruction of the virtual machine after the job results have been sent back.
In the latter case the user sends a request for a virtual machine creation, specifying parameters like memory, CPUs and disk and most importantly the user’s SSH public key, to the OCCI interface or directly to the cachemanager service.
Such a request then gets translated into a job for a virtual machine with the parameters specified and a sleep command as payload and sent to the batch system; when this request reaches the bait component, the virtual machine allocation request is forwarded to the hypervisor.
The cachemanager monitors this process, and as soon as the VM allocation is completed, copies the user’s SSH public key into it and reports the name of the VM to the user, which can the login into it.
The virtual machine is then destroyed when the sleep job ends or when the user explicitly requests it destruction, whichever happens first.

**References**

[1] Barone, G.B., Bifulco, R., Boccia, V., Bottalico, D., Canonico, R. and Carracciuolo, L. GaaS: Customized Grids in the Clouds. Proceedings of Euro-Par 2012, Lecture Notes in Computer Science N. 7640, 577-586, 2013.

[2] Loomis, C., Airaj, M., Begin, M., Floros, E., Kenny, S., and O’Callaghan, D. StratusLab Cloud Distribution. In: Petcu, D., Vazquez-Poletti, J. (eds.) Chapter 10 in European Research Activities in Cloud Computing, 260-282, Cambridge Scholars Publishing, 2012.

[3] Tusa F., Paone M., Villari M., and Puliafito A. CLEVER: A Cloud Cross-Computing Platform Leveraging GRID Resources. Proceedings of the IEEE Internatonal Conference on Utility and Cloud Computing, 390-396, IEEE Computer Society, 2011.

[4] Foster,I., Kesselman,C. and Tuecke,S. The Anatomy of the Grid: Enabling Scalable Virtual Organizations. International Journal of High Performance Computing Applications, 15, 200-222, 2001.

[5] Housley, R., Polk, W., Ford, W., and Solo, D. In- ternet X.509 Public Key Infrastructure, Certificate and Certificate Revocation List (CRL) Profile, 2002. [http://www.ietf.org/rfc/rfc3280.txt] (http://www.ietf.org/rfc/rfc3280.txt)
