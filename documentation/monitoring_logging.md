---
layout: page
title: "Monitoring and Logging"
description: ""
---

Since VWNs are an integral part of the LRMS cluster, no changes are actually necessary for what regards monitoring of resources and logging: monitoring tools will boot be able to perceive any difference between a real Worker Node and a Virtual Worker Node. Also, logging will not be affected by WNoDeS, because the LRMS itself will not see any difference between a job running on a real Worker Node and a job running on a Virtual Worker Node.