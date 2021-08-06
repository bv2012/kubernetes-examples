1. Get API Version
	kubectl api-resources

AME                              SHORTNAMES   APIVERSION                             NAMESPACED   KIND
bindings                                       v1                                     true         Binding
componentstatuses                 cs           v1                                     false        ComponentStatus
configmaps                        cm           v1                                     true         ConfigMap
endpoints                         ep           v1                                     true         Endpoints
events                            ev           v1                                     true         Event
limitranges                       limits       v1                                     true         LimitRange
namespaces                        ns           v1                                     false        Namespace
nodes                             no           v1                                     false        Node
persistentvolumeclaims            pvc          v1                                     true         PersistentVolumeClaim
persistentvolumes                 pv           v1                                     false        PersistentVolume
pods                              po           v1                                     true         Pod


   Check pods API version

2. From output most are v1, with that info we cerate 3 required sections for pods such as metadata, with a name and spec which declares container image to use and a name for container

call this file basic.yaml

3. Create a new pod using created YAML file

   kubectl create -f basic.yaml

4. Make sure the pod has been created then use the describe sub-command to view the details. Among other values in the output you should be about to find the image and the container name.

kubectl get pod

kubectl describe pod basicpod
5. Shut down the pod and verify it is no longer running.
    kubectl delete pod basicpod

    kubectl get pod

6. Configure POD to expose port 80

Edit basic.yaml

7 Create POD and verify it is running. use -o wide option to see the internal IP assigned to the pod . NOMINATED NODE is used by the scheduler and READINESS GATES . Using curl and pods IP address you should get nginx welcome page.

kubectl create -f basic.yaml

kubectl get pod -o wide

curl IP

kubectl delete pod basicpod

8. Create a simple service to expose pod to toher nodes and pods in the cluster



