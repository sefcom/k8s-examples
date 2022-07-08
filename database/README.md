# A simple database deployment

When you're running a large experiment which is at least partially I/O bound, the NFS share may not cut it.
Instead, you will want to host a persistent database somewhere on the cluster which you can connect to via TCP.
This directory contains configuration for a postgres server running off of a persistent directory allocated at creation time from one of the hosts.

Tune the values in `database.yaml`, and then deploy it do your namespace: `kubectl create -f database.yaml`
You can then access it on any public IP address for the cluster, for example, 206.206.192.23, on a certain port.
You can retrieve this port with `kubectl get svc postgres -o template='{{ (index .spec.ports 0).nodePort }}'`.
This port will be valid for the lifetime of the server.

To clean up the database (i.e., wipe its contents forever and reclaim its resources), run `kubectl delete -f database.yaml`.
