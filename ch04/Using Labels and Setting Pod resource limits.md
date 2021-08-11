4.4: Using Labels

1. Create a new deployment called design2
2. View the wide kubectl get output for the design2 deployment and make note of the SELECTOR
3. Use the -l option to use the selector to list the pods running inside the deployment. There should be only one pod running. 
4. View the pod details in YAML format using the deployment selector. This time use the –selector option. Find the pod label in the output. It should match that of the deployment.
5. Edit the pod label to be your favorite color.
6. Now view how many pods are in the deployment. Then how many have design2 in their name. Note the AGE of the pods.
7. Delete the design2 deployment.
8. Check again for pods with design2 in their names. You should find one pod, with an AGE of when you first created the deployment. Once the label was edited the deployment created a new pod in order that the status matches the spec and there be a replica running with the intended label.
9. Delete the pod using the -l and the label you edited to be your favorite color in a previous step. The command details have been omitted. Use previous steps to figure out these commands.

```
kubectl create deployment design2 --image=nginx

kubectl get deployments.apps design2 -o wide

kubectl get -l app=design2 pod

kubectl get --selector app=design2 pod -o yaml

kubectl edit pod design2-

kubectl get deployments.apps design2 -o wide

kubectl get pods | grep design2

kubectl delete deploy design2

kubectl get pods | grep design2


```

4.5 Setting Pod Resource Limits and Requirements


1. Create a new pod running the vish/stress image. A YAML stress.yaml file has been included in the course tarball

