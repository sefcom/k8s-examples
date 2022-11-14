# VNC

`vnc-app` is a sample deployment for running Ubuntu with a desktop GUI. You can connect to the container with VNC to have a full desktop for running experiments that require a display. There is also an alternate deployment, `vnc-app-with-nfs`, which connects the container to the NFS shared volume.

## Prerequisites

Create the VNC deployment and service.
```
$ kubectl create -f vnc-app.yaml
$ kubectl create -f vnc-service.yaml
```

Ensure that the VNC application is running.
```
$ kubectl get pods
NAME                       READY   STATUS      RESTARTS   AGE
vnc-app-5f5f48d6b8-sv8fz   1/1     Running     0          1d
```

Ensure that the VNC service is running. Note the port after the colon on the `PORT(S)` column.
```
$ kubectl get services
NAME          TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
vnc-service   NodePort   xx.xxx.xx.xxx   <none>        5900:30755/TCP   1d
```

## Connecting with VNC Viewer

Install [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/) so that we can interact with the desktop.

Check the description of the `vnc-app` pod to see which node it's running on. Note the IP address after the slash on the `Node` line.
```
$ kubectl describe pods
Name:             vnc-app-5f5f48d6b8-sv8fz
Namespace:        mitch
Priority:         0
Service Account:  default
Node:             node29/xxx.xxx.xxx.xx
...
```

Load up VNC Viewer and connect with the node IP and service port.
```
xxx.xxx.xxx.xx:30755
```

Enter the default VNC password for the deployment. This can be changed in `vnc-app.yaml`.
```
Password: Hacking!
```
