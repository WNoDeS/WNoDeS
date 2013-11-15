---
layout: page
title : Supported Requests
description: ""
---
{% include JB/setup %}

WNoDeS is able to support users' requests by handling the following request types as shown in Figure:

* Web-based resource request through which users are able to submit cloud requests by using a IGI portal that also handles IaaS Cloud resources. In this case users need to belong to a VO and have a valid certificate in order to access the correspondent cloud portlet and request the instantiation of virtual machines.
* WNoDeS CLI-based cloud resource request: users submit cloud requests by using a simple CLI that allows users to instantiate cloud resources and to get information about the state of the provided machines. In this case users need to belong to a VO and have a valid certificate.
* Local or Grid virtual job: users are able to submit computational jobs by using batch CLI or grid CLI. These jobs will be executed on virtual machines that have been transparently instantiated by the WNoDeS core with the mixed mode feature turned on. In this case users just need to belong to the pool of users authorized to access the farm resources.
* Local or Grid real job: users are able to submit computational jobs by using batch CLI or grid CLI. These jobs will be executed on physical machines that have been transparently allocated by the WNoDeS core with the mixed mode feature turned on. In this case users just need to belong to the pool of users authorized to access the farm resources.

![WNoDeS Framework]({{site.baseurl}}/images/supported_requests_new.png)