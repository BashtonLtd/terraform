---
layout: "aws"
page_title: "AWS: aws_instance"
sidebar_current: "docs-aws-resource-instance"
description: |-
  Provides an EC2 instance resource. This allows instances to be created, updated, and deleted. Instances also support provisioning.
---

# aws\_instance

Provides an EC2 instance resource. This allows instances to be created, updated,
and deleted. Instances also support [provisioning](/docs/provisioners/index.html).

## Example Usage

```
# Create a new instance of the ami-1234 on an m1.small node with an AWS Tag naming it "HelloWorld"
resource "aws_instance" "web" {
    ami = "ami-1234"
    instance_type = "m1.small"
    tags {
        Name = "HelloWorld"
    }
}
```

## Argument Reference

The following arguments are supported:

* `ami` - (Required) The AMI to use for the instance.
* `availability_zone` - (Optional) The AZ to start the instance in.
* `ebs_optimized` - (Optional) If true, the launched EC2 instance will be
     EBS-optimized.
* `instance_type` - (Required) The type of instance to start
* `key_name` - (Optional) The key name to use for the instance.
* `security_groups` - (Optional) A list of security group IDs or names to associate with.
   If you are within a non-default VPC, you'll need to use the security group ID. Otherwise,
   for EC2 and the default VPC, use the security group name.
* `subnet_id` - (Optional) The VPC Subnet ID to launch in.
* `associate_public_ip_address` - (Optional) Associate a public ip address with an instance in a VPC.
* `private_ip` - (Optional) Private IP address to associate with the
     instance in a VPC.
* `source_dest_check` - (Optional) Controls if traffic is routed to the instance when
  the destination address does not match the instance. Used for NAT or VPNs. Defaults true.
* `user_data` - (Optional) The user data to provide when launching the instance.
* `iam_instance_profile` - (Optional) The IAM Instance Profile to
  launch the instance with.
* `tags` - (Optional) A mapping of tags to assign to the resource.
* `block_device` - (Optional) A list of block devices to add. Their keys are documented below.
* `root_block_device` - (Optional) Customize details about the root block
  device of the instance. Available keys are documented below.

Each `block_device` supports the following:

* `device_name` - The name of the device to mount.
* `virtual_name` - (Optional) The virtual device name.
* `snapshot_id` - (Optional) The Snapshot ID to mount.
* `volume_type` - (Optional) The type of volume. Can be standard, gp2, or io1. Defaults to standard.
* `volume_size` - (Optional) The size of the volume in gigabytes.
* `iops` - (Optional) The amount of provisioned IOPS. Setting this implies a
    volume_type of "io1".
* `delete_on_termination` - (Optional) Should the volume be destroyed on instance termination (defaults true).
* `encrypted` - (Optional) Should encryption be enabled (defaults false).

The `root_block_device` mapping supports the following:

* `device_name` - The name of the root device on the target instance. Must
  match the root device as defined in the AMI. Defaults to "/dev/sda1", which
  is the typical root volume for Linux instances.
* `volume_type` - (Optional) The type of volume. Can be standard, gp2, or io1. Defaults to standard.
* `volume_size` - (Optional) The size of the volume in gigabytes.
* `iops` - (Optional) The amount of provisioned IOPS. Setting this implies a
    volume_type of "io1".
* `delete_on_termination` - (Optional) Should the volume be destroyed on instance termination (defaults true).

## Attributes Reference

The following attributes are exported:

* `id` - The instance ID.
* `availability_zone` - The availability zone of the instance.
* `key_name` - The key name of the instance
* `private_dns` - The Private DNS name of the instance
* `private_ip` - The private IP address.
* `public_dns` - The public DNS name of the instance
* `public_ip` - The public IP address.
* `security_groups` - The associated security groups.
* `subnet_id` - The VPC subnet ID.
