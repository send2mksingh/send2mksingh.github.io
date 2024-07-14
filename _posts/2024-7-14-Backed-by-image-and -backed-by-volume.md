---
 layout: post
 title: Backed by image and backed by volume
---

In OpenStack, when you create an instance (virtual machine), it can be backed by either an image or a volume. These terms refer to the source and type of storage that the instance's root filesystem is based on.

### Backed by Image

When an instance is backed by an image instance root disk created from the image directly and exist as long as the instance exist.

- **Image**: A read-only template file that contains os, softwares and supporting libraries. Images are stored in the OpenStack Image service (Glance).
- **Instance Creation**: The instance's root disk is created directly from this image. During boot, the image is copied to ephemeral storage on the compute node.
- **Ephemeral Storage**: The root disk is ephemeral, meaning that any changes made to the disk are lost if the instance is terminated. The disk exists only as long as the instance is running.
- **Use Case**: Ideal for stateless applications where the root disk does not need to persist beyond the life of the instance.

### Example

Creating an instance backed by an image:
```sh
openstack server create --image <image-id> --flavor <flavor-id> --network <network-id> <instance-name>
```

### Backed by Volume

When an instance is backed by a volume the instance root disk is created from the any volume and that exist even after the instance is terminated.

- **Volume**: A persistent block storage device managed by the OpenStack Block Storage service (Cinder). Volumes can persist beyond the life of the instance and can be detached and reattached to different instances.
- **Instance Creation**: The root disk of the instance is a volume created from an image or an existing volume. This volume is attached to the instance and acts as its root disk.
- **Persistent Storage**: Changes to the root disk persist even if the instance is terminated, as the volume continues to exist independently of the instance.
- **Use Case**: Ideal for stateful applications where the data needs to persist beyond the life of the instance, or where you need to reattach the root disk to another instance.

### Example

Creating an instance backed by a volume:
```sh
openstack server create --flavor <flavor-id> --block-device source=image,id=<image-id>,dest=volume,size=<volume-size>,shutdown=remove,bootindex=0 --network <network-id> <instance-name>
```

### Key Differences

1. **Persistence**:
   - **Image**: Root disk is ephemeral.
   - **Volume**: Root disk is persistent.

2. **Flexibility**:
   - **Image**: Simpler and faster for short-lived instances.
   - **Volume**: More flexibility for long-term data storage and management.

3. **Data Safety**:
   - **Image**: Data is lost when the instance is terminated.
   - **Volume**: Data is retained in the volume even if the instance is terminated.

4. **Usage Scenarios**:
   - **Image**: Suitable for temporary workloads, testing, and stateless applications.
   - **Volume**: Suitable for databases, long-running applications, and stateful services where data integrity and persistence are crucial.

By choosing between image-backed and volume-backed instances, you can optimize your infrastructure based on the specific requirements of your applications.



In OpenStack, you can create an instance (virtual machine) backed by an image using the `openstack` CLI command. Here is the basic syntax and an example of how to do it:

### Basic Syntax
```sh
openstack server create --image <image-id> --flavor <flavor-id> --network <network-id> <instance-name>
```

### Detailed Example

Assume you have the following details:
- **Image ID**: `1234abcd-5678-efgh-9101-ijklmnopqrst`
- **Flavor ID**: `m1.small`
- **Network ID**: `5678efgh-1234-abcd-9101-ijklmnopqrst`
- **Instance Name**: `my-instance`

The command to create an instance backed by the specified image would be:

```sh
openstack server create --image 1234abcd-5678-efgh-9101-ijklmnopqrst --flavor m1.small --network 5678efgh-1234-abcd-9101-ijklmnopqrst my-instance
```

### Additional Options

You can include additional options to specify other aspects such as security groups, key pairs, availability zones, and more:

- **Security Group**: `--security-group <security-group-name>`
- **Key Pair**: `--key-name <keypair-name>`
- **Availability Zone**: `--availability-zone <zone-name>`
- **Block Device Mapping**: `--block-device-mapping <device-name>=<volume-id>:<type>:<size>:<delete-on-terminate>`
- **User Data**: `--user-data <file-path>`
- **Metadata**: `--property <key>=<value>`

### Example with Additional Options

Assume you also have:
- **Security Group Name**: `default`
- **Key Pair Name**: `my-key`
- **Availability Zone**: `nova`
- **User Data File**: `user-data.txt`

The command would be:

```sh
openstack server create --image 1234abcd-5678-efgh-9101-ijklmnopqrst --flavor m1.small --network 5678efgh-1234-abcd-9101-ijklmnopqrst --security-group default --key-name my-key --availability-zone nova --user-data user-data.txt my-instance
```

### Checking Available Resources

Before creating an instance, you may want to check the available images, flavors, and networks. Here are the commands to list them:

- **List Images**:
  ```sh
  openstack image list
  ```

- **List Flavors**:
  ```sh
  openstack flavor list
  ```

- **List Networks**:
  ```sh
  openstack network list
  ```

- **List Security Groups**:
  ```sh
  openstack security group list
  ```

- **List Key Pairs**:
  ```sh
  openstack keypair list
  ```

By using these commands, you can gather the necessary IDs and names required to create an instance.



To create an instance in OpenStack backed by a volume, you need to use the `--block-device` option in the `openstack server create` command. Here is the basic syntax and an example of how to do it:

### Basic Syntax
```sh
openstack server create --flavor <flavor-id> --block-device <block-device-mapping> --network <network-id> <instance-name>
```

### Block Device Mapping Format
The `--block-device` option uses a specific format to define the volume source, device name, and other properties:

```
source=<source>,dest=<destination>,id=<id>,size=<size>,shutdown=<shutdown-behavior>,bootindex=<boot-index>
```

- `source`: Source type (`image`, `volume`, `snapshot`)
- `dest`: Destination type (`volume`, `local`)
- `id`: ID of the source (image ID, volume ID, or snapshot ID)
- `size`: Size of the volume in GB (optional if the volume already exists)
- `shutdown`: Shutdown behavior (`preserve` or `remove`)
- `bootindex`: Boot index (usually `0` for the primary boot device)

### Example

Assume you have the following details:
- **Image ID**: `1234abcd-5678-efgh-9101-ijklmnopqrst` (to create a new volume from this image)
- **Flavor ID**: `m1.small`
- **Volume Size**: `20` GB
- **Network ID**: `5678efgh-1234-abcd-9101-ijklmnopqrst`
- **Instance Name**: `my-instance`

The command to create an instance backed by a volume would be:

```sh
openstack server create --flavor m1.small --block-device source=image,id=1234abcd-5678-efgh-9101-ijklmnopqrst,dest=volume,size=20,shutdown=remove,bootindex=0 --network 5678efgh-1234-abcd-9101-ijklmnopqrst my-instance
```

### Additional Options

You can include additional options to specify other aspects such as security groups, key pairs, availability zones, and more:

- **Security Group**: `--security-group <security-group-name>`
- **Key Pair**: `--key-name <keypair-name>`
- **Availability Zone**: `--availability-zone <zone-name>`
- **User Data**: `--user-data <file-path>`
- **Metadata**: `--property <key>=<value>`

### Example with Additional Options

Assume you also have:
- **Security Group Name**: `default`
- **Key Pair Name**: `my-key`
- **Availability Zone**: `nova`
- **User Data File**: `user-data.txt`

The command would be:

```sh
openstack server create --flavor m1.small --block-device source=image,id=1234abcd-5678-efgh-9101-ijklmnopqrst,dest=volume,size=20,shutdown=remove,bootindex=0 --network 5678efgh-1234-abcd-9101-ijklmnopqrst --security-group default --key-name my-key --availability-zone nova --user-data user-data.txt my-instance
```

### Checking Available Resources

Before creating an instance, you may want to check the available images, flavors, volumes, and networks. Here are the commands to list them:

- **List Images**:
  ```sh
  openstack image list
  ```

- **List Flavors**:
  ```sh
  openstack flavor list
  ```

- **List Networks**:
  ```sh
  openstack network list
  ```

- **List Volumes**:
  ```sh
  openstack volume list
  ```

- **List Security Groups**:
  ```sh
  openstack security group list
  ```

- **List Key Pairs**:
  ```sh
  openstack keypair list
  ```

By using these commands, you can gather the necessary IDs and names required to create an instance backed by a volume.