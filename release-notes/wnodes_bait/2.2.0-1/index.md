---
layout: default
title: "WNoDeS Bait v. 2.2.0-1 release notes"
release_date: "12.10.2013"
rfcs:
   - id: WNODES-344
     title: Fixed - Wrong message error when the BATCH_SYSTEM_FILE variable is LSF and the LSF_PROFILE variable is commented or missing.
   - id: WNODES-343
     title: Fixed - Jobs are nod deleted at the stop of hypervisor service
   - id: WNODES-336
     title: Change the way the info is exchanged between services
---

## WNoDeS Bait v. 2.2.0-1

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

