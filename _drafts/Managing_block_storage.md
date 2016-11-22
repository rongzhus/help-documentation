---
layout: page
title: Managing Block Storage
author: Ying Tang
dateAdded: November 21, 2016
tags: [cinder, block storage]
featured: true
weight: 4
---

You might have heard that IBM Bluemix Private Cloud offers several different storage models, each with the performance and scale to address our customers’ unique requirements. If you have workloads such as expandable file systems and data management systems hosted on your Bluemix Private Cloud, block storage may be a good fit for your environment-specific use case. This post explains how to get started with our block storage model.

### OpenStack Cinder

Block storage is stand-alone persistent storage that you can attach to and detach from your virtual servers. With block storage, your data persists beyond the lifecycle of the virtual server. For example, if your virtual server stops unexpectedly, your data stored in block storage remains safe and intact, so that you retain peace of mind that your stored data is safeguarded.

Because Bluemix Private Cloud is powered by OpenStack, we can offer OpenStack Cinder as the block storage option to our clients. Cinder gives developers the ability to manage their block volumes using both the OpenStack Horizon dashboard UI and standardized OpenStack APIs.

Because storage needs may vary, Cinder supports multiple backends: its scheduler can locate the right volume types with certain flexibility. Cinder block storage is configured to use Ceph clusters, by default.

### How Ceph works with Bluemix Private Cloud

With the power of Ceph, Bluemix Private Cloud provides a block storage option with increased capacity, exceptional performance, and lower cost. According to your specific workload requirements, our clients can also customize the following node types for their Ceph clusters:

 * An SSD-only option with SSD-only OSD disks and co-located Ceph Journal has the optimal I/O performance. It suits your storage workload expecting high IOPS.
 
 * A hybrid option with SATA OSD disks and SSD-based Ceph Journal has good IO performance and lower cost, and fits into medium IOPS workloads.
 
 * A multi-tier option with a mixture of SSD-only and hybrid nodes is ideal for large-scale environments.

After your block storage is configured with the proper multiple backend and multi-tier options, creating a Cinder volume is just a few quick steps away! You can easily use the Horizon dashboard or the Cinder client.
Creating a Cinder volume using OpenStack API

To create a volume using the OpenStack client, run the following Cinder command:

```
$  cinder create <size> --display-name <name> --volume-type <type> \
--image-id <imageid> --availablity-zone <az>
```

The following commands show examples of how you can customize your newly-created volume for your Bluemix Private Cloud.

```
    <size>: The size of the volume in gibibytes (GiB).
    <name>: The name of the volume.
    <type>: CEPH_HYBRID for the hybrid option or CEPH_SSD for the SSD-only option. You can also use the cinder type-list command to get a list of available volume types.
    <imageid>: Optionally, specify the ID of the image that you want to use for your volume. You can use the nova image-list command to list the existing images.
    <az>: Optionally, specify the availability zone in which you want to create the volume. You can use the cinder availability-zone-list command to get a list of availability zones.
```

**Creating a Cinder volume with Horizon**

You can also create a block storage volume using Horizon, the OpenStack dashboard. You can get started with the following steps:

    Log into the Horizon dashboard.
    
    Under the Project section, select Compute, then click Volumes. If you have existing volumes, you can view a list of your volumes and their details (such as name, description, size, and status), from the dashboard UI.

Click Create Volume on the upper right portion of the Horizon dashboard. The Create Volume dialog is displayed.

**Create a volume using Horizon**

Provide the following details about the volume:

    Volume Name: Type the name of your volume.
    Description: Type a description of your volume.
    Volume Source: No source, empty volume or Image. If you choose an empty volume, an empty volume does not contain a file system or a partition table. If you choose the image option, a new field for Use image as a source displays and you can select the image from the list.
    Type: Select CEPH_HYBRID if you want the hybrid option or CEPH_SSD for the SSD-only option.
    Size (GiB): Select the size of the volume in gibibytes(GiB), for example, 1.
    Availability Zone: Choose the availability zone. For example, Nova.

Simply click Create Volume when complete. You’re now able to attach your Cinder volume to your virtual server. It’s also just as easy to detach and re-attach your block volume to another Virtual Server requiring persistent storage, and you can rest assured that your data will remain safe.
Learn more

After creating and attaching your Cinder volumes to Virtual Servers, you can easily adjust and expand their volume sizes as your capacity requirements grow. To learn more about Cinder, check out our documentation.