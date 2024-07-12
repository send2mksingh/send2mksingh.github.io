---
 layout: post
 title: OpenStack regular used commands
---

Providing a comprehensive list of all OpenStack commands with examples in a single response would be extensive, as OpenStack encompasses numerous services and functionalities. However, here are some essential OpenStack commands categorized by their common use cases, along with brief explanations and examples:

### Identity Service (Keystone)

1. **OpenStack CLI Authentication**
   - **Command**: 
     ```bash
     openstack auth login
     ```
   - **Use**: Authenticate to the OpenStack cloud.

2. **List Users**
   - **Command**: 
     ```bash
     openstack user list
     ```
   - **Use**: List all users in the OpenStack cloud.

### Compute Service (Nova)

1. **List Instances**
   - **Command**: 
     ```bash
     openstack server list
     ```
   - **Use**: List all instances (virtual machines) in the cloud.

2. **Create Instance**
   - **Command**: 
     ```bash
     openstack server create --flavor <flavor> --image <image> <instance-name>
     ```
   - **Use**: Create a new instance using a specific flavor and image.

### Networking Service (Neutron)

1. **List Networks**
   - **Command**: 
     ```bash
     openstack network list
     ```
   - **Use**: List all networks in the OpenStack cloud.

2. **Create Network**
   - **Command**: 
     ```bash
     openstack network create <network-name>
     ```
   - **Use**: Create a new network.

### Block Storage Service (Cinder)

1. **List Volumes**
   - **Command**: 
     ```bash
     openstack volume list
     ```
   - **Use**: List all volumes (block storage) in the cloud.

2. **Create Volume**
   - **Command**: 
     ```bash
     openstack volume create --size <size> <volume-name>
     ```
   - **Use**: Create a new volume with a specific size.

### Object Storage Service (Swift)

1. **List Containers**
   - **Command**: 
     ```bash
     openstack container list
     ```
   - **Use**: List all containers (buckets) in the object storage.

2. **Upload Object**
   - **Command**: 
     ```bash
     openstack object create <container-name> <object-name> --file <local-file>
     ```
   - **Use**: Upload an object (file) to a container.

### Image Service (Glance)

1. **List Images**
   - **Command**: 
     ```bash
     openstack image list
     ```
   - **Use**: List all images available in the cloud.

2. **Upload Image**
   - **Command**: 
     ```bash
     openstack image create --file <image-file> --disk-format <format> --container-format <format> <image-name>
     ```
   - **Use**: Upload an image to the image service.

### Orchestration Service (Heat)

1. **List Stacks**
   - **Command**: 
     ```bash
     openstack stack list
     ```
   - **Use**: List all stacks (orchestrated resources) in Heat.

2. **Create Stack**
   - **Command**: 
     ```bash
     openstack stack create -t <template-file> <stack-name>
     ```
   - **Use**: Create a stack using a Heat template.

### Database Service (Trove)

1. **List Instances**
   - **Command**: 
     ```bash
     openstack database instance list
     ```
   - **Use**: List all database instances managed by Trove.

2. **Create Instance**
   - **Command**: 
     ```bash
     openstack database instance create --flavor <flavor> --size <size> <instance-name>
     ```
   - **Use**: Create a new database instance.

### Telemetry Service (Ceilometer)

1. **List Meters**
   - **Command**: 
     ```bash
     openstack meter list
     ```
   - **Use**: List all meters (metrics) monitored by Ceilometer.

2. **Show Sample**
   - **Command**: 
     ```bash
     openstack sample show <meter-id>
     ```
   - **Use**: Show details of a specific meter sample.




Certainly! Here are more OpenStack commands across various services, along with examples:

### Identity Service (Keystone)

1. **Create Project**
   - **Command**: 
     ```bash
     openstack project create <project-name>
     ```
   - **Use**: Create a new project in the OpenStack cloud.

2. **List Roles**
   - **Command**: 
     ```bash
     openstack role list
     ```
   - **Use**: List all roles available in the cloud.

### Compute Service (Nova)

1. **Show Instance Details**
   - **Command**: 
     ```bash
     openstack server show <instance-id>
     ```
   - **Use**: Display detailed information about a specific instance.

2. **Resize Instance**
   - **Command**: 
     ```bash
     openstack server resize <instance-id> <flavor>
     ```
   - **Use**: Change the size (flavor) of a running instance.

### Networking Service (Neutron)

1. **Create Subnet**
   - **Command**: 
     ```bash
     openstack subnet create --network <network-name> --subnet-range <CIDR> <subnet-name>
     ```
   - **Use**: Create a subnet within a specified network.

2. **Show Router Details**
   - **Command**: 
     ```bash
     openstack router show <router-name>
     ```
   - **Use**: Display details about a specific router.

### Block Storage Service (Cinder)

1. **Show Volume Details**
   - **Command**: 
     ```bash
     openstack volume show <volume-id>
     ```
   - **Use**: Display detailed information about a specific volume.

2. **Attach Volume to Instance**
   - **Command**: 
     ```bash
     openstack server add volume <instance-id> <volume-id>
     ```
   - **Use**: Attach a volume to a running instance.

### Object Storage Service (Swift)

1. **Download Object**
   - **Command**: 
     ```bash
     openstack object save <container-name> <object-name> --file <local-file>
     ```
   - **Use**: Download an object (file) from a container.

2. **Delete Container**
   - **Command**: 
     ```bash
     openstack container delete <container-name>
     ```
   - **Use**: Delete a container (bucket) and all its contents.

### Image Service (Glance)

1. **Show Image Details**
   - **Command**: 
     ```bash
     openstack image show <image-id>
     ```
   - **Use**: Display detailed information about a specific image.

2. **Delete Image**
   - **Command**: 
     ```bash
     openstack image delete <image-id>
     ```
   - **Use**: Delete an image from the image service.

### Orchestration Service (Heat)

1. **Show Stack Details**
   - **Command**: 
     ```bash
     openstack stack show <stack-name>
     ```
   - **Use**: Display detailed information about a specific stack.

2. **Update Stack**
   - **Command**: 
     ```bash
     openstack stack update -t <new-template-file> <stack-name>
     ```
   - **Use**: Update an existing stack using a new Heat template.

### Database Service (Trove)

1. **Show Database Instance Details**
   - **Command**: 
     ```bash
     openstack database instance show <instance-id>
     ```
   - **Use**: Display detailed information about a specific database instance.

2. **List Database Instances**
   - **Command**: 
     ```bash
     openstack database instance list
     ```
   - **Use**: List all database instances managed by Trove.

### Telemetry Service (Ceilometer)

1. **List Alarms**
   - **Command**: 
     ```bash
     openstack alarm list
     ```
   - **Use**: List all alarms configured in Ceilometer.

2. **Show Alarm Details**
   - **Command**: 
     ```bash
     openstack alarm show <alarm-id>
     ```
   - **Use**: Display detailed information about a specific alarm.


In OpenStack, you can pause and unpause an instance using the `openstack server pause` and `openstack server unpause` commands, respectively.

### Pause an Instance

To pause an instance, use the following command:

```bash
openstack server pause <instance-id>
```

### Example:

```bash
openstack server pause 12345678-1234-1234-1234-123456789abc
```

In this example, replace `12345678-1234-1234-1234-123456789abc` with the ID of your instance.

### Unpause an Instance

To unpause an instance, use the following command:

```bash
openstack server unpause <instance-id>
```

### Example:

```bash
openstack server unpause 12345678-1234-1234-1234-123456789abc
```

Again, replace `12345678-1234-1234-1234-123456789abc` with the ID of your instance.

### Verifying the Instance Status

After pausing or unpausing an instance, you can verify the status of the instance using the `openstack server show` command:

```bash
openstack server show <instance-id>
```

### Example:

```bash
openstack server show 12345678-1234-1234-1234-123456789abc
```

This will display the details of the instance, including its current status. When paused, the status will be `PAUSED`, and when unpaused, the status will change to `ACTIVE`.



In OpenStack, flavors define the compute, memory, and storage capacity of virtual machines. To create a flavor in OpenStack, you can use the `openstack flavor create` command. Here's the syntax and an example of how to use it:

### Syntax

```bash
openstack flavor create [OPTIONS] <name>
```

### Options

- `--id <id>`: Optional. Unique ID for the flavor. If not specified, a UUID will be generated.
- `--ram <MB>`: Required. Memory size in megabytes.
- `--disk <GB>`: Required. Root disk size in gigabytes.
- `--vcpus <vcpus>`: Required. Number of virtual CPUs.
- `--swap <MB>`: Optional. Swap space size in megabytes.
- `--ephemeral <GB>`: Optional. Ephemeral disk size in gigabytes.
- `--is-public <true|false>`: Optional. Whether the flavor is available to all projects or not.
- `--rxtx-factor <factor>`: Optional. RX/TX factor.
- `--description <description>`: Optional. Description of the flavor.

### Example

Let's create a flavor with the following specifications:
- Name: `small`
- RAM: 2048 MB
- Disk: 20 GB
- VCPUs: 2
- Swap: 1024 MB
- Ephemeral Disk: 0 GB
- Public: true

```bash
openstack flavor create --id auto --ram 2048 --disk 20 --vcpus 2 --swap 1024 --ephemeral 0 --is-public true small
```

### Breakdown of the Example

- `--id auto`: Let OpenStack automatically generate a unique ID for the flavor.
- `--ram 2048`: The flavor will have 2048 MB (2 GB) of RAM.
- `--disk 20`: The root disk size will be 20 GB.
- `--vcpus 2`: The flavor will have 2 virtual CPUs.
- `--swap 1024`: The swap space size will be 1024 MB (1 GB).
- `--ephemeral 0`: The ephemeral disk size will be 0 GB.
- `--is-public true`: The flavor will be available to all projects.
- `small`: The name of the flavor.

### Creating a Flavor Without Optional Parameters

If you only need to specify the basic parameters (RAM, disk, and vCPUs), the command might look like this:

```bash
openstack flavor create --ram 2048 --disk 20 --vcpus 2 small
```

### Verifying the Created Flavor

After creating the flavor, you can list all flavors to verify it was created successfully:

```bash
openstack flavor list
```

This command will display all available flavors, including the one you just created.



Transferring a volume from one owner to another in OpenStack involves several steps. Here’s a step-by-step explanation of how you can do it:

### Step 1: Create a Volume Transfer Request

1. **Create a Transfer**:
   - You need to create a transfer request for the volume you want to transfer. This generates a transfer ID and an authorization key.
   - Use the following command:
     ```bash
     openstack volume transfer request create --name <transfer-name> <volume-id>
     ```
   - **Example**:
     ```bash
     openstack volume transfer request create --name my-volume-transfer 12345678-1234-1234-1234-123456789abc
     ```
   - This command will return a `transfer-id` and an `auth-key` which are needed for the next steps.

### Step 2: Accept the Transfer

2. **Share Transfer Details with the New Owner**:
   - Share the `transfer-id` and `auth-key` with the new owner. These details are required to accept the volume transfer.

3. **Accept the Transfer**:
   - The new owner needs to accept the transfer using the transfer ID and authorization key.
   - Use the following command:
     ```bash
     openstack volume transfer request accept <transfer-id> <auth-key>
     ```
   - **Example**:
     ```bash
     openstack volume transfer request accept 98765432-4321-4321-4321-987654321def abcdefgh-1234-5678-abcd-efghijklmnop
     ```

### Step 3: Verify the Transfer

4. **Verify the Transfer**:
   - Both the original owner and the new owner can verify the transfer by listing the volumes.
   - Use the following command to list volumes:
     ```bash
     openstack volume list
     ```
   - The volume should now appear under the new owner's list of volumes.

### Summary

1. **Original Owner**:
   - Create a volume transfer request and obtain the `transfer-id` and `auth-key`.
   
2. **New Owner**:
   - Accept the volume transfer using the provided `transfer-id` and `auth-key`.

### Example Workflow

#### Original Owner:
1. Create transfer request:
   ```bash
   openstack volume transfer request create --name my-volume-transfer 12345678-1234-1234-1234-123456789abc
   ```
   - Output:
     ```json
     {
       "transfer_id": "98765432-4321-4321-4321-987654321def",
       "auth_key": "abcdefgh-1234-5678-abcd-efghijklmnop"
     }
     ```

#### New Owner:
2. Accept the transfer:
   ```bash
   openstack volume transfer request accept 98765432-4321-4321-4321-987654321def abcdefgh-1234-5678-abcd-efghijklmnop
   ```

#### Both Owners:
3. Verify the transfer:
   ```bash
   openstack volume list
   ```

By following these steps, you can successfully transfer a volume from one owner to another in OpenStack.




These additional examples cover more OpenStack commands across various services. For detailed options and additional commands, refer to the OpenStack documentation or use `openstack --help` for comprehensive command details and usage examples. Each command typically has detailed documentation and examples to help you understand its usage and parameters.

