---
layout: page
title: "System administration guide"
description: ""
---

### WNoDeS components

WNoDeS is characterized by the following components:   
bait, hypervisor, manager, nameserver and site-specific.


INSERIRE FIGURA    


**Bait** is the host resource manager responsible for verifying  that there are resources to execute both real jobs and virtual jobs, requiring the instantiation of the virtual machine when necessary, and executing the job on the suitable resource;   
*Hypervisor* is mainly the interface to the virtualization system responsible for instantiating virtual machines where the virtual job will be executed.
However, if the mixed mode feature is enabled, it is also able to run real job;   
**Nameserver, Manager** can be considered as the information management.
The nameserver is a sort of catalogue responsible for keeping trace of all the virtual machines currently running for each hypervisor, and all the virtual machine images stored in the configured repository
 (see [Section](INSERIRE LINK)). The **Manager** is a Command Line Interface (CLI) that is responsible for the configuration of the repository of the virtual machine images.
 It provides a set of options to handle images, VLANs, hostnames, bait and hypervisor configuration files.
 Furthermore, it supports a set of options that manage bait and hypervisor status.
 
#### Overview of WNoDeS Deployments
WNoDeS can be differently deployed on a given site in relation to its needs.
However, both physical and virtual machines need to be prepared.  
Figure 2 shows the WNoDeS deployment with the mixed mode enabled.
In this case the **wnodes\_bait** service is installed and configured on the same host of the **wnodes\_hypervisor** service.   

![Example of deployment]({{site.baseurl}}/images/example_of_deployment.png)
_Figure 2 - Example of deployment_

<!--

COMMENTED.. TO VERIFY

### Quick Start Guide

This guide gives the steps to be followed when installing the WNoDeS services in a given deployment.



#### Torque/Maui Batch System With Mixed Mode Enabled

Let us installing the WNoDeS services with mixed moded enabled and Torque/Maui as Batch System.
Prepare at least two MAC-Addresses (e.g., MAC-1, MAC-2) and associated hostnames (e.g., test-1.cnaf.infn.it, test-2.cnaf.infn.it) for virtual machines, and configure a Torque/Maui server (also with a CE when necessary).

##### Step 1
Create and setting a **qwnodes** queue on the Torque server ([more details]())

Edit a file called for example **wnodes\_queue\_command** in order to create and set a **qwnodes** queue. Below an example is shown.

    cat /root/wnodes_queue_command
    create queue qwnodes
    set queue qwnodes queue_type = Execution
    set queue qwnodes Priority = 1000000
    set queue qwnodes max_running = 80
    set queue qwnodes resources_max.cput = 100:00:00
    set queue qwnodes resources_max.walltime = 100:00:00
    set queue qwnodes resources_default.neednodes = wnodes
    set queue qwnodes enabled = True
    set queue qwnodes started = True


Run the **qmgr** command with the file specified above as input

    qmgr <  /root/wnodes_queue_command


whose output is specified below:

    Max open servers: 9
    create queue qwnodes
    set queue qwnodes queue_type = Execution
    set queue qwnodes Priority = 1000000
    set queue qwnodes max_running = 80
    set queue qwnodes resources_max.cput = 100:00:00
    set queue qwnodes resources_max.walltime = 100:00:00
    set queue qwnodes resources_default.neednodes = wnodes
    set queue qwnodes enabled = True
    set queue qwnodes started = True

##### Step 2
Modify Torque configuration ([more details](modifytorque)}   
Configure the Torque server to allow job management from the **wnodes\_preexec** service on the **wnodes\_bait**

    qmgr -c "set server managers +=root@<hostname>.<domain>"

where **<hostname>** is the hostname of the real machine where the **wnodes\_bait** service runs. For each hostname where the **wnodes\_bait** service runs executes the above command.

Configure the Torque server to allow real job to use only the other queues   

    qmgr -c "set queue demo resources_default.neednodes = lcgpro"

##### Step 3
Add in the nodes configuration file the new nodes that WNoDeS will use to instantiate virtual machines ([more details](nodetorque)). Below an example is shown.

-->

### Installation Prerequisites

#### Operating System

All WNoDeS components are certified to work on Scientific Linux SL5 x86\_64 and SL6 x86\_64 with EPEL as repository for external dependencies.

#### DNS

Full access to the DNS configuration is needed in order to add each virtual machine hostname, which is used to instantiate a virtual resource. Host resolution will be used by DHCP to provide ip address to the virtual resource.   
The hostname for the **wnodes\_bait** service should contain 'bait' in case of Mixed Mode disabled.

#### DHCP

Full access to the DHCP configuration is needed in order to configure the mapping from MAC address to hostname for each hostname that is used to instantiate virtual machine.

#### KVM

KVM needs to be installed on all the nodes where the hypervisor service runs.

#### Repository Distribution

A dedicated repository for the virtual machine images needs to be configured.
It could be a Web Server or a shared file system such as the common NFS, Lustre and GPFS.
In the former, a http repository needs to be configured.

#### Image

Use **virtio** driver to define the image.

#### Batch System
The batch system either LSF or Torque/Maui needs to be installed and configured.    
In case of PBS, the Computing Elements, worker nodes and submission nodes are configured to allow **ssh** connection without requiring password: each worker node could login without password to the Computing Element and among worker nodes.
It is suggested to put the same **ssh** host keys in all the nodes (i.e., both bait and worker node) in order to easy the managing of the host list.


### Installation Recommendations

#### Nameserver

The **wnodes\_nameserver** service can be installed on any machine that is not used as **hypervisor**. It can be both virtual or physical. **This service contains the configurations of hypervisor and bait.**

Please use the following package:

    wnodes_nameserver

Log files are produced under **/var/log/wnodes/nameserver**.
Standard error and standard output files are produced under **/tmp**.

#### Manager


The **wnodes\_manager** CLI can be installed on any machine or laptop.

Please use the following package:

    wnodes_manager


#### Hypervisor

The **wnodes\_hypervisor** service can be installed on any machine, where the virtualization technology is enabled.
As detailed in (see [Section](INSERIRE LINK)), the behaviour of the **wnodes\_hypervisor** service depend on the mixed mode feature:

* If the feature is not enabled, then the **wnodes\_hypervisor** service will instantiate a virtual machine that contains the **wnodes\_bait** service. Therefore, the image of that virtual machine needs to be created with the bait software and added to the WNoDeS repository before starting the **wnodes\_hypervisor** service.
* If the feature is enabled, the **wnodes\_hypervisor** service will be able to execute jobs.

Please use the following package:

    wnodes_hypervisor

Log files are produced under **/var/log/wnodes/hypervisor**.
Standard error and standard output files are produced under **/tmp**.


#### Bait

As detailed in (see [Section](INSERIRE LINK)), the installation and configuration of the **wnodes\_bait** service depend on the mixed mode feature:

* If the feature is not enabled, then the **wnodes\_bait** service will run on a virtual machine that is automatically instantiated by the **wnodes\_hypervisor** service.
* If the feature is enabled, the **wnodes\_bait** service will run on the same machine where the **wnodes\_hypervisor** service runs.

Please use the following package:

    wnodes_bait

Log files are produced under **/var/log/wnodes/bait**.
Standard error and standard output files are produced under **/tmp**.


#### Site specific

The **wnodes\_site\_specific** component contains, among other things, the **wnodes\_preexec** script that sends a request to the **wnodes\_bait** service in order to instantiate a virtual machine that can be used to execute a job.

The **wnodes\_preexec** script and its configuration file need to be present on the machines where jobs are executed.
In case of a shared FS, the **wnodes\_preexec** script and its configuration file can be copied in a common area: otherwise, you need to install them in all the machines specifying the same configuration file.

Please use the following package:

    wnodes_site_specific

Debug Log file is produced under **/tmp** with the name **<user>\_debug\_px\_wnodes**, where **<user>** is who has submitted the job.


### Nameserver Configuration

The **wnodes\_nameserver** configuration files that need to be edited are:

* MAC list file
* wnodes hypervisor file
* wnodes bait file

#### WNoDeS nameserver MAC list file

The **/etc/wnodes/nameserver/mac\_list.ini** file has an INI format in which each section corresponds to a given VLAN and the content of each section shows details of the specified VLAN.
The file contains the following information:

    [<VLAN_NAME>]
    network_type = OPEN
    bait_host = <fully bait hostname>^00:16:3e:01:00:16;...
    vm_host = <fully virtual image hostname>^00:16:3e:01:00:16;...

where **<VLAN\_NAME>** is the section that expresses the name of the VLAN, whose value can be a set of integer numbers or the **DEFAULT\_VLAN** string,
which is chosen when the virtual image hostnames belong to the same VLAN of the **wnodes\_hypervisor** hostname.
The section contains the following options:

`network_type` can have the OPEN value or the CLOSE value (see Table~\ref{tab:mac});

`bait_host` is a list of values separated by ; whose value expresses hostname and mac address linked by the ^ symbol. **If the mixed mode feature is enabled, *bait\_host* can be empty;**

`vm_host` is a list of values separated by ; whose value expresses hostname and mac address linked by the ^ symbol.

All the hostnames must be defined in the DNS, while the mac addresses with the related IP addresses in the DHCP.

##### Description of Network Type Values

**OPEN**  It means that the related VLAN is able to access to the local network.

**CLOSE** It means that the related VLAN is able to access to the external network and disable to access to the local sub networks.
It is defined for the network isolation of the virtual machine in order to open to the network of virtual machine externally but not internally.
Typically virtual machine that is used to run jobs has the **network\_type** value set to OPEN.

#### WNoDeS hypervisor file

The **/etc/wnodes/nameserver/wnodes\_hv\_config.ini** file has an INI format. The file contains the following information:

    [HV_CONF]
    HV_PORT=8222
    BAIT_PORT=8111
    
    LOG_FILE_NAME=wnodes_hv.log
    
    MAX_LOG_FILE_SIZE=100000
    MAX_COUNT_LOG_FILE=5
    
    LOCAL_REPO_DIR=/etc/wnodes/repo
    
    BAIT_IMG_TAG=<image tag>
    BAIT_VM_RAM=800
    
    HOST_GROUP_<ALL>=
    ENABLED_VLAN_GROUP_<ALL>=DEFAULT_VLAN
    
    SSH_KEY_FILE=/etc/wnodes/hypervisor/.ssh/hv_id_rsa
    
    USE_LVM=YES
    VOLUME_GROUP=vg0
    
    SERVICE_NIC_IP=<IP NIC Service>
    SERVICE_NIC_IP_MASK=<MASK IP NIC Service>
    
    DNS_RANGE=<DNS RANGE 1,DNS RANGE 2>
    DNS_LEASE_TIME=5m

where **HV\_CONF** is the name of the section that contains the following options:

`HV_PORT` specifies the port of the \texttt{wnodes\_hypervisor} service;

`BAIT_PORT` specifies the port of the \texttt{wnodes\_bait} service;

`LOG_FILE_NAME` specifies the logging file name;

`MAX_LOG_FILE_SIZE` specifies the maximum size of the logging file name.
The size is expressed in Byte;

`MAX_COUNT_LOG_FILE` specifies the maximum number of rotations of the logging file name.
The value 5 means that after 5 rotations the first is removed;

`LOCAL_REPO_DIR` specifies the repository directory of images that the \texttt{wnodes\_hypervisor} service download;

`BAIT_IMG_TAG` specifies the tag name of the virtual machine associated to the bait.
The **wnodes\_hypervisor** service will get the image of the virtual machine related to the tag.
**The value of this option is only considered with mixed mode disabled**;

`BAIT_VM_RAM` specified the amount of RAM to allocate in the virtual machine where the **wnodes\_bait** service will run.
**The value of this option is only considered with mixed mode disabled.**
The following two options need to be specified in pair:

* `HOST_GROUP_<ALL>` specifies a set of regular expressions separated by ;. It represents  groups of hostnames that belong to given VLANs with <ALL> as its logical name;

* `ENABLED_VLAN_GROUP_<ALL>` specifies the enabled VLANs for the logical name that are associated to groups of hostnames. Please use **DEFAULT\_VLAN** to refer to the VLAN of the **wnodes\_hypervisor** service;

`SSH_KEY_FILE` is the location of the rsa key that is created by the **wnodes\_hypervisor** service during its start and saved there;

`USE_LVM` is a flag whose value can be yes or no. If it is yes, this means that the \texttt{wnodes\_hypervisor} service will define and create a file system to be associated to the virtual machine that will be instantiated.
LVM stands for logical volume;

`VOLUME_GROUP` specifies the name of the volume group to be set before creating the logical volume;

`SERVICE_NIC_IP` specifies the physical address of the **wnodes\_hypervisor** interface used to interact with the virtual machine;

`SERVICE_NIC_IP\_MASK` specifies the mask address of the **wnodes\_hypervisor** interface used to interact with the virtual machine;

`DNS_RANGE` specifies the range of the addresses that the DHCP server can assign to the virtual machine.
This option starts with DNS because the service used to change the DHCP is called **dnsmasq**;

`DNS_LEASE_TIME` specifies the time in which the address is not used.
After that the address is used for another virtual machine.







