Indexed Job
===

This example shows how to create and manage a job with the `Indexed` completion mode.
There are two example yaml files for you to choose from, one with and one without an NFS shared volume.

# What this example does
This works by creating a "Job" object in Kubernetes, which in turn creates pods.
The number of pods that will be created depends on the `completions` value in the PodSpec, 100 in this case.
Because this is an `Indexed` completion job, each pod will get a different value for `${JOB_COMPLETION_INDEX}`, from zero to `completions` - 1. Your application should be able to take this index value from stdin or an enviroment variable, and determine its task statically.
If you configure the pod `restartPolicy` to `OnFailure`, Kubernetes will automatically re-run contianers that have failed, though it will back off if it fails repeatedly.

# `kubectl` commands
To create your job: `kubectl create -f job.yaml`

To see currently running jobs in your namespace: `kubectl get jobs`

To see currently running pods in your namespace: `kubectl get pods`

To get much more detail for jobs or pods including info useful for debugging, replace `get` with `describe`.

To get logs for a pod: `kubectl logs <pod>`

To delete a job: `kubectl delete job <job>` or `kubectl delete -f job.yaml`

# More info

Kubernetes Job docs: https://kubernetes.io/docs/concepts/workloads/controllers/job/

JobSpec: https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.21/#job-v1-batch

PodSpec: https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.21/#podspec-v1-core

Container: https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.21/#container-v1-core
