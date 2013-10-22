---
layout: default
title: "WNoDeS v. 2.2.0 release notes"
release_date: "20.09.2013"
rfcs:
   - id: WNODES-308
     title: (Component Bait)Fixed - Typo error in handling the ping command
   - id: WNODES-270
     title: (Component Bait)Fixed - Bait logs declares need of VM creation when considering real jobs (Mixed mode HV)
   - id: WNODES-344
     title: (Component Bait)Fixed - Wrong message error when the BATCH_SYSTEM_FILE variable is LSF and the LSF_PROFILE variable is commented or missing.
   - id: WNODES-343
     title: (Component Bait)Fixed - Jobs are nod deleted at the stop of hypervisor service
   - id: WNODES-297
     title: (Component Manager)Verify if the NS hostname is correct
   - id: WNODES-338
     title: (Component Manager)Fixed - Wnodes_manager -s "*" does not show jobid information
   - id: WNODES-310
     title: (Component Manager)Fixed - vmResources show CPU and MEM inverted in case of BATCH_REAL
   - id: WNODES-304
     title: (Component Manager)Fixed - Wnodes_manager with option -s and bait down
   - id: WNODES-312
     title: (Component Manager)Fixed - Identified two worng behaviour in bhost and bjobs in obtaining the correct entry
   - id: WNODES-271
     title: (Component Manager)Fixed -  wnodes_manager inconsistent behaviour
   - id: WNODES-268
     title: (Component Manager)Fixed -  wnodes_manager -s "*" hangs
   - id: WNODES-331
     title: (Component Site Specific)Fixed - Add wnodes_utils dependency in site-specific
   - id: WNODES-307
     title: (Component Site Specific)Fixed - Error in handling Variable_list
   - id: WNODES-330
     title: (Component Utils)Fixed - Add python-demjson dependency for OS 5
   - id: WNODES-312
     title: (Component Utils)Fixed - Identified two worng behaviour in bhost and bjobs in obtaining the correct entry
   - id: WNODES-307
     title: (Component Utils)Fixed - Error in handling Variable_list
   - id: WNODES-304
     title: (Component Utils)Fixed - Wnodes_manager with option -s and bait down
   - id: WNODES-306
     title: (Component Hypervisor)Fixed - hv wrong behaviour with a wrong conf file
   - id: WNODES-300
     title: (Component Hypervisor)Fixed - hexception raised when the hypervisor stop
   - id: WNODES-298
     title: (Component Hypervisor)Fixed - Hypervisor network down
   - id: WNODES-285
     title: (Component Nameserverisor)Fixed - Verify the check of hostname available on the hypervisor site
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
     title: Fixed - Wnodes_manager -S "*" behaves incosistently with respect to -s "*"
   - id: WNODES-249
     title: Fixed - Permanent hypervisor removal
   - id: WNODES-220
     title: Replace commands with subprocess
---

## WNoDeS v. 2.2.0

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

