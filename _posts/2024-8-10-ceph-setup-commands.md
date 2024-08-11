1.  sudo apt update
2.  sudo apt install -y docker.io
3.  systemctl status docker
4.  docker --version
5.  curl --silent --remote-name --location https://raw.githubusercontent.com/ceph/ceph/quincy/src/cephadm/cephadm    #Make sure to download the correct cephadm script from the Ceph repository. Use the following command:

6.  cat cephadm | head -n 10           #Ensure that the script is downloaded correctly:
7.  chmod +x cephadm                  #Make the script executable
8.  sudo mv cephadm /usr/local/bin/
9.  sudo cephadm bootstrap --mon-ip 192.168.3.57             #Bootstrapping the Ceph cluster 
10.  cephadm version    #check the version
11.  apt install ceph-common  -y
12.  sudo apt install ceph-common  -y
