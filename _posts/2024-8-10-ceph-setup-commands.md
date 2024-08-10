Great! `cephadm` is a powerful tool for deploying and managing Ceph clusters using containerized services. Here’s a step-by-step guide to help you get started with `cephadm`.

### Step 1: Prerequisites

1. **Ubuntu 20.04 or later installed on all nodes.**
2. **SSH access between nodes.**
3. **Docker installed on all nodes.** (`cephadm` relies on Docker to run Ceph services in containers.)

   Install Docker:
   ```bash
   sudo apt update
   sudo apt install -y docker.io
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

### Step 2: Install `cephadm`

On your admin node, install `cephadm`:

```bash
sudo apt install -y cephadm
```

### Step 3: Bootstrap the Cluster

1. **Create a bootstrap keyring:**

   ```bash
   cephadm bootstrap --mon-ip <admin-node-ip>
   ```

   Replace `<admin-node-ip>` with the IP address of your admin node.

2. **Deploying the Ceph Dashboard:**

   After bootstrapping, you can deploy the Ceph Dashboard:

   ```bash
   cephadm shell -- ceph mgr module enable dashboard
   cephadm shell -- ceph dashboard create-self-signed-cert
   cephadm shell -- ceph dashboard set-login-credentials admin admin
   ```

3. **Access the Dashboard:**

   Open your browser and navigate to `https://<admin-node-ip>:8443`. Use the credentials `admin/admin` (or the ones you set).

### Step 4: Adding Nodes

1. **Install `cephadm` on each node:**

   ```bash
   sudo apt install -y cephadm
   ```

2. **Add nodes to the cluster:**

   From the admin node, run:
   ```bash
   cephadm shell -- ceph orch host add <node-ip>
   ```

   Repeat this for each node you want to add.

### Step 5: Deploying Ceph Services

1. **Deploy OSDs:**

   ```bash
   cephadm shell -- ceph orch daemon add osd <node-ip>:<disk-path>
   ```

   Replace `<node-ip>` with the IP of the node and `<disk-path>` with the path to the disk you want to use (e.g., `/dev/sdb`).

2. **Deploy MDS (for CephFS):**

   ```bash
   cephadm shell -- ceph fs set <fs-name> max-mds <num>
   ```

   Replace `<fs-name>` with your CephFS name and `<num>` with the number of MDS you want.

3. **Deploy RGW (for object storage):**

   ```bash
   cephadm shell -- ceph orch daemon add rgw <node-ip>:<rgw-name>
   ```

   Replace `<rgw-name>` with a name for the RGW instance.

### Step 6: Managing the Cluster

1. **Check cluster status:**

   ```bash
   cephadm shell -- ceph status
   ```

2. **View logs:**

   ```bash
   cephadm shell -- ceph log last
   ```

3. **Scale services:**

   To scale up or down, use:
   ```bash
   cephadm shell -- ceph orch daemon set <service-type> <count>
   ```

   Replace `<service-type>` with `osd`, `mds`, or `rgw` and `<count>` with the desired number.

### Additional Tips

- **Configuration:**
  You can manage configuration through `cephadm` or directly edit the configuration files in `/etc/ceph/`.

- **Documentation:**
  Refer to the [Ceph documentation on cephadm](http://docs.ceph.com/docs/master/cephadm/) for more detailed information and advanced configurations.

Feel free to ask if you have specific questions or run into any issues!
