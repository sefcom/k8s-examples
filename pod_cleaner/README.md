Pod Cleaner
===

Tired of spinning up 2M pod jobs only to see it bring the entire cluster crashing down?
Wish there was a way to just make those completed pods go away?
Well look no more!
With Pod Cleaner 3000, all your completed pods can be gone!

# How it works
Pod cleaner makes a Kubernetes CronJob, which is an object that spawns a job based on a cron schedule.
Every 20 minutes, the CronJob creates a Job that spawns a Pod that deletes all sucecssfully completed pods in the namespace.
A service account is created and configured to give the pod the necessary permissions to delete pods.

# Usage
To create a copy of pod-cleaner in your namespace, just run:
```
kubectl create -f pod_cleaner.yaml
```

If you are unsatisfied with your pod-cleaner for any reason, returns are accepted by running:
```
kubectl delete -f pod_cleaner.yaml
```

The CronJob can also be suspended and unsuspended:
```
kubectl patch cronjobs pod-cleaner -p '{"spec" : {"suspend" : true }}'
kubectl patch cronjobs pod-cleaner -p '{"spec" : {"suspend" : false }}'
```

# More info

Kubernetes docs on CronJobs: https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/

CronJob Schema: https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.21/#cronjob-v1-batch
