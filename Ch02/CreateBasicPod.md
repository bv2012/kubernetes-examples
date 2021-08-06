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

