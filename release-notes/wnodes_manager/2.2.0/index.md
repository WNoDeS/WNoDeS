---
layout: default
title: "WNoDeS Manager v. 2.2.0 release notes"
release_date: "20.09.2013"
rfcs:
   - id: WNODES-338
     title: Fixed - Wnodes_manager \-s "*" does not show jobid information
   - id: WNODES-312
     title: Fixed - Identified two worng behaviour in bhost and bjobs in obtaining the correct entry
   - id: WNODES-310
     title: Fixed - vmResources show CPU and MEM inverted in case of BATCH_REAL
   - id: WNODES-304
     title: Fixed - wnodes_manager with option -s and bait down
   - id: WNODES-297
     title: Verify if the NS hostname is correct
   - id: WNODES-271
     title: Fixed - wnodes_manager inconsistent behaviour
   - id: WNODES-268
     title: Fixed - wnodes_manager -s "*" hangs
   - id: WNODES-336
     title: Change the way the info is exchanged between services
   - id: WNODES-335
     title: Change LICENSE from EUPL to Apache 2.0
   - id: WNODES-332
     title: Verify BuildRequires dependencies in the all spec files
   - id: WNODES-325
     title: Fixed - Review WNoDeS documentation
   - id: WNODES-305
     title: Fixed - Ns inconsistent behaviour
   - id: WNODES-284
     title: Fixed - Service wnodes_hypervisor start on "nonempty" nodes
   - id: WNODES-277
     title: Fixed - wnodes-manager -X
   - id: WNODES-275
     title: Fixed - wodes_manager -S "*" behaves incosistently with respect to -s "*"
   - id: WNODES-249
     title: Fixed - Permanent hypervisor removal
   - id: WNODES-220
     title: Replace commands.* with subprocess
---

## WNoDeS Manager v. 2.2.0

Released on **{{ page.release_date }}** with [WNoDeS v. 2.2.0]({{ site.baseurl }}/release-notes/WNoDeS-v2.2.0.html).

### Description

This release provides several bug fixes.

### Bug fixes

{% include list-rfcs.liquid %}

### Installation and configuration

You can find information about upgrade, clean installation and configuration of WNoDeS services in the [System Admininistration Guide][wnodes-sysadmin-guide] of the [Documentation][wnodes-documentation] section.

### Known issues

None at the moment

[wnodes-documentation]: {{site.baseurl}}/documentation.html
[wnodes-sysadmin-guide]: {{site.baseurl}}/documentation/sysadmin-guide/2.2.0

