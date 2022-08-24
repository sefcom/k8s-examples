# HTTPS

This is a short guide on using the nginx ingress controller, cert-manager, and LetsEncrypt to serve https from the cluster.

## Background: Services

In order to give a pod some well-known name for the rest of the cluster or the world to be able to talk to it, we use a service.
Services can do lots of things, including load balancing, but for now you probably just want a simple service that maps to one port on one pod.
For the purposes of this demo, you probably want a ClusterIP service, which is the default kind.

## Prerequisites

Ensure that cert-manager is running:
(this command only works if you've installed it in a namespace named cert-manager)

```
$ kubectl get pods -n cert-manager
NAME                                      READY   STATUS    RESTARTS        AGE
cert-manager-c76cfb476-kbc5b              1/1     Running   0               12d
cert-manager-cainjector-5dd75b745-g9q2s   1/1     Running   0               12d
cert-manager-webhook-788455fbfb-sbqfd     1/1     Running   1 (7d12h ago)   12d
```

Ensure that the nginx ingress controller is running:
(this command only works if you've installed it in a namespace named ingress-nginx)

```
$ kubectl get pods -n ingress-nginx
NAME                             READY   STATUS    RESTARTS        AGE
ingress-nginx-controller-26ddt   1/1     Running   0               14d
ingress-nginx-controller-2qh4b   1/1     Running   0               14d
ingress-nginx-controller-2vzfv   1/1     Running   0               14d
...
```

## Configure an Issuer

```
$ kubectl apply -f letsencrypt.yaml
```

This creates an issuer, a mechanism by which certificates can be acquired.
It actually creates two issuers, one for testing and one for creating real certificates which will be respected by browsers.

## Point your DNS at the cluster

You can use any public IP address which routes to any of your cluster nodes.
An example IP for the SEFCOM cluster is 206.206.192.69.

## Set up an Ingress

```
$ vim http.yaml    # change these values!
$ kubectl apply -f ingress.yaml
```

This creates an ingress, or an application-layer routing rule to map a given HTTP or HTTPS request to a service.
There are several values you need to change in the yaml file to configure the ingress for your desires, which are marked as CHANGEME.
