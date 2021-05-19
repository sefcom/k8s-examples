Kubernetes Examples
===

This repository holds examples that can be used to quickly get an experiment running on the lab kubernetes cluster.

## Scenarios

### I have a specific number of tasks I need to run:
Check out `indexed_job`!
If your tasks run more than a thousand or so, please look at `pod_cleaner`.

### I have a variable number of tasks, which cannot be determined statically:
TBD, probably a queue and a replicaset
