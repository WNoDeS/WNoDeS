---
layout: default
title: "WNoDeS Hypervisor v. 2.2.0-1 release notes"
release_date: "12.10.2013"
rfcs:
   - id: WNODES-356
     title: Fixed - File system mount on vm fails
   - id: WNODES-346
     title: Fixed - /tmp/wnodes/repo negli hv creata con 644 anziche 755
   - id: WNODES-336
     title: Change the way the info is exchanged between services
---

## WNoDeS Hypervisor v. 2.2.0-1

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

