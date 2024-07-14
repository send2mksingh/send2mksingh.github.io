---
 layout: post
 title: OpenStack Default Resouce Quota Limits
---


In OpenStack, the default quotas and maximum limits for various resources such as instances, vCPUs, RAM, and others can vary depending on the configuration set by the OpenStack administrators. These quotas are designed to control resource usage and ensure fair sharing among users.

### Default Quotas

The default quotas are typically configured in the `nova.conf` file on the controller node. Here are the common default quotas for various resources in OpenStack:

- **Instances (cores)**: 10 instances per project
- **vCPUs**: 20 vCPUs per project
- **RAM**: 50 GB per project
- **Floating IPs**: 10 floating IPs per project
- **Security Groups**: 10 security groups per project
- **Volumes**: 10 volumes per project
- **Volume Storage**: 1 TB per project

### Maximum Quotas

The maximum quotas can be configured by the OpenStack administrators based on the capacity and policies of the OpenStack deployment. There isn't a predefined "maximum limit" for quotas in OpenStack itself; it depends on the resources available and the limits set by the cloud provider.

### Viewing and Modifying Quotas

#### Viewing Quotas

You can view the quotas for a project using the OpenStack CLI:

```sh
openstack quota show <project-id>
```

For example:

```sh
openstack quota show my_project
```

#### Modifying Quotas

Administrators can modify quotas using the OpenStack CLI. For example, to change the quota for instances for a project:

```sh
openstack quota set --instances <number> <project-id>
```

For example:

```sh
openstack quota set --instances 50 my_project
```

Similarly, other quotas can be adjusted using the corresponding parameters (`--ram`, `--cores`, `--volumes`, etc.).

### Example Command to Set Quotas

To set the following quotas for a project:
- Instances: 100
- vCPUs: 200
- RAM: 500 GB

You can use:

```sh
openstack quota set --instances 100 --cores 200 --ram 512000 <project-id>
```

For example:

```sh
openstack quota set --instances 100 --cores 200 --ram 512000 my_project
```

### Checking Current Quotas

To check the current quotas and their usage for a project, use:

```sh
openstack quota show <project-id>
```

For example:

```sh
openstack quota show my_project
```

This will display the current quotas and their usage for instances, vCPUs, RAM, floating IPs, security groups, volumes, and more.

### Summary

The default quotas in OpenStack typically provide a balanced initial allocation of resources, but these can be adjusted by administrators to meet the specific needs and capacity of the OpenStack deployment. There is no predefined "maximum limit" for quotas, as it depends on the infrastructure and policies of the cloud provider.