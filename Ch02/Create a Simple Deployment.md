Create a Simple Deployment

1. Create a containerized webserver nginx

Use kubectl create to create a simple, single replica deployment running
the nginx web server. It will create a single pod as we did previously but with new controllers to ensure it runs as well as
other features.
 
 kubectl create deployment firstpod --image=nginx

2. Verify the new deployment exists and the desired number of pods matches the current number

    kubectl get deployment,pod

3. View the details of the deployment, then the pod

    kubectl describe deployment firstpod

4. Note that the resources are in the default namespace. Get a list of available namespaces.
    kubectl get namespaces

5. Look at the pods in the kube-system namespace.
    kubectl get pod -n kube-system

6. look at the pods in a namespace that does not exist
    kubectl get pod -n fakenamespace

7. view resources in all namespaces at once
short name such as 
    rs for ReplicaSet, 
    po for Pod,
    svc for Service, 
and ep for endpoint.

    kubectl get pod --all-namespaces

8. View several resources at once

    kubectl get deploy,rs,po,svc,ep

9. Delete the ReplicaSet and view the resources again

kubectl delete rs firstpod-

kubectl get deployment,rs,po,svc,ep

10. This time delete the top-level controller. After about 30 seconds for everything to shut down you should only see the cluster service and endpoint remain for the cluster and the service we created.
 kubectl delete deployment firstpod

 kubectl get deployment,rs,po,svc,ep

11. As we won’t need it for a while, delete the basicservice service as well.
 kubectl delete svc basicservice
