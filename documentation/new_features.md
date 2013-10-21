---
layout: page
title: "New Features"
description: ""
---

<div class="row-fluid marketing">
<div class="row">
<div class="span3">
</div>
<div class="span9">
</div>
</div>
<div class="row">
<div class="span3">

#### VLAN support

</div>
<div class="span9">
Different virtual machines running on the same hypervisor can belong to different VLAN.

* Reduce the network broadcast domain.
* Grant different network access polices to every virtual machine. VLANs provide network isolation, particularly requested for cloud computing, where users get root access to virtual machine.
</div>
</div>
<div class="row">
<div class="span3">

#### Virtio

</div>
<div class="span9">

[Virtio] (http://www.linux-kvm.org/page/Virtio) enables Virtual Machine to get high performance network and disk operations.

* Virtio driver currently used only for virtual machine running SL5 OS.
* Improve performance when using GPFS fileSystem. Poor network performance is a major issue for GPFS cluster consistency.
</div>
</div>
<div class="row">
<div class="span3">

#### Libguestfs

</div>
<div class="span9">

[Libguestfs] (http://libguestfs.org) is a library for accessing and modifying virtual machine (VM) disk images. Amongst the things this is good for: making batch configuration changes to guests, viewing and editing files inside guests. We currently use it for:

* Edit/create local files.
* Redirect SysLog to the right dom0.
* Enable kernel modules.

In general it could be used to apply site specific configuration.
</div>
</div>
</div>

