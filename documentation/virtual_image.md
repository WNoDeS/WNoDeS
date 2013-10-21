---
layout: page
title: "Virtual Image"
description: ""
---

{% include JB/setup %}

#### Selection
Virtual images may be selected through a number of methods. In general, if the LRMS is able to distinguish different jobs, it is then possible to associate these jobs to different virtual images. Examples of methods normally used to differentiate among jobs are:

* the queue the job is submitted to;
* the Unix group ID of the user submitting the job;
* the Unix user ID of the user submitting the job;
* the LRMS group of nodes the job is submitted to.

It is important to note that all methods for image selection require approval and action by the local system administrator. The is an explicit requirement of the WNoDeS architecture, i.e., the local resource provider must retain full control of how its resources are selected and used.

In fact, any method where a decision algorithm can be implemented in a LRMS pre-execution script should work with the WNoDeS architecture. This is what made it straightforward to extend WNoDeS to support virtual image selection through Grid job submission. It is only necessary that the LRMS be aware of the appropriate Grid information through (for example) environment variables, passed to the LRMS by the Grid Computing Element. This information can then be used by the LRMS and, hence, by WNoDeS, to select the image to run.

#### Loading
An important part of the image selection process is to determine from which location will the virtual image be loaded. While attractive from an implementation point of view, the idea of loading master virtual images from shared storage every time a job is received is often not feasible due to scalability concerns: the load on the network and on the shared storage itself might in that case rapidly become unmanageable. A rough estimate of the network bandwidth needed to support such a solution can be easily given: if we assume that in a farm 100 VWNs may start jobs approximately at the same time (a conservative estimate for a heavily used farm made of O(10^3) nodes), with an average size for the virtual images of about 2 GigaBytes, then one can expect a request due to the download of virtual images from shared storage of about 100 x 2 = 200 GigaBytes. If the storage subsystem were connected to the network with an aggregate bandwidth of about 20 Gigabit/seconds, then it would take at least about

    200 x 8
    ------- = 80
    20

seconds just to copy a virtual image from shared storage to the local disk of a VWN. This estimate is fairly optimistic, because if neglects any interference due to other network traffic and assumes there are no bottlenecks due e.g., to I/O subsystem inefficiencies.

The method used by WNoDeS to load virtual image makes therefore use of three main concepts:

1. Read-only images (master copies) for each type of supported virtual images available on shared storage. It is not necessary to assume anything about the actual type and location of this shared storage: the read-only images could be available either locally or remotely. The only requirement of the current WNoDeS implementations is that the images are accessible through a normal copy command. At the INFN Tier-1, our shared fileSystem is [IBM GPFS](http://www-03.ibm.com/systems/software/gpfs/), so our own read-only virtual images are shared on a GPFS fileSystem.
2. Virtual image local caching. Virtual images are stored on the KVM VMM partition of each physical box. The first time a job is run on a pristine node part of a WNoDeS cluster, the VMM will not have any locally available virtual images, and will therefore resort to loading a read-only master image from shared storage. If a second job requesting the same image arrives to the bait while the copy of the master images is ongoing, the job will be put on hold until the copy is completed; once the image has been fully copied, all jobs waiting for it on the bait will be allowed to run. Upon termination of a VWN job, the read-only image will be retained on local storage for re-use by another job requiring the same image.
3. KVM snapshots. A VWN will be started using the locally available read-only image as a base. Modifications to this image, though, will be written to KVM snapshots. This means that only differences to the read-only image will need to be written to local disk.

Initially, then, the WNoDeS cluster will beed to download master copies of the virtual images from shared storage; once running, though, the network traffic due to the copying of virtual images will be normally negligible, thanks to local caching, KVM snapshots make it possible to store several read-only images onto the VMM partition: assuming an average size of virtual images of about 2 Gigabit, storing 10 different virtual images requires about 20 Gigabit of local storage, i.e. an amount of space easily satisfied by modern hard disks.

Relying on master copied brings about the problem of updating them, e.g. in case of an OS upgrade. This is currently solved in the following way:

* The master copy is addressed by the KVM VMM through a soft-link. The soft-link point to the current copy.
* When the master copy needs to be changed, the new image is copied to the shared storage, and the soft-link is updated to point to the new copy.
* A management command is issued to the KVM VMMs (to one VMM at a time, or to a group of VMMs, or to all VMMs) to invalidated the local copy of the virtual image. When a new job requiring the affected virtual image needs to be started, the VMM will proceed to download the new master copy from the shared storage. With large farm clusters, it is often best to phase-in the deployment of updates to avoid high loads on the network and on the storage subsystem; this statement is not specific to WNoDeS, being just good practice in any large scale software deployment.

Installation procedures are therefore dramatically simplified with WNoDeS, because what is necessary is just to keep master copies for the virtual images up to date. The WNoDeS system will then take care of the actual deployment o the images to the cluster.