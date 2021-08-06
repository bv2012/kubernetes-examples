2.4 Multi-Container Pods

Using a single container per pod allows for the most granularity and decoupling. There are still some reasons to deploy multiple containers, sometimes called composite containers, in a single pod. The secondary containers can handle
logging or enhance the primary, the sidecar concept, or acting as a proxy to the outside, the ambassador concept, or modifying data to meet an external format such as an adapter. All three concepts are secondary containers to perform
a function the primary container does not.

1. Edit basic.yaml and add a fluentd container. 
        add a second container to the pod to handle logging

2. Delete and create the pod again.

kubectl delete pod basicpod ; kubectl create -f basic.yaml

kubectl get pod

kubectl describe pod basicpod

3. For now shut down the pod

kubectl delete pod basicpod