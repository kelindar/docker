#  Zookeeper Cluster

First, we need to spin a cluster of kafka and bootstrap it. On Google Compute Engine, we can spin a cluster in the following way:
```
gcloud compute instances create kafka-1 kafka-2 --image coreos --zone europe-west1-b --machine-type n1-highmem-2 --metadata-from-file user-data=coreos-gcloud.yaml --tags zookeeper --network emitter-bus --boot-disk-type pd-ssd --boot-disk-size 50GB
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
