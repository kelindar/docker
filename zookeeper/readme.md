#  Zookeeper Cluster

First, we need to spin a cluster of zookeeper and bootstrap it. On Google Compute Engine, we can spin a cluster in the following way:
```
gcloud compute instances create discovery-1 discovery-2 discovery-3 --image coreos --zone europe-west1-b --machine-type g1-small --metadata-from-file user-data=coreos-gcloud.yaml --tags zookeeper --network emitter-bus --boot-disk-type pd-ssd --boot-disk-size 10GB
```

For CoreOS we should provide a cloud-config file. In the command above we named it *coreos-gcloud.yaml*:
```
#cloud-config

coreos:
  etcd:
    discovery: https://discovery.etcd.io/<TOKEN>
    addr: $private_ipv4:4001
    peer-addr: $private_ipv4:7001
  units:
    - name: etcd.service
      command: start
    - name: fleet.service
      command: start
```
If you have an error: Cannot sync with the cluster using peers 127.0.0.1:4001 that can be fixed by requesting a new token from: https://discovery.etcd.io/new

# Deploy Zookeeper
In the repository here we provide a [unit template for zookeeper](https://github.com/Kelindar/docker/blob/master/zookeeper/zookeeper%40.service) which should be copied onto the cluster. This can be done by simply ssh'ng to any of the nodes and copying/pasting this template. 

Once we have it there, we need to add it to the fleet registry and start our service. This should do the trick and go and deploy zookeeper on 3 instances within our cluster.
```
fleetctl submit zookeeper\@.service
fleetctl start zookeeper\@{1,2,3}.service
```

