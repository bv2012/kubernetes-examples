3.3 Configure Probes

When large datasets need to be loaded or a complex application launched prior to client access, a readinessProbe can be used. The pod will not become available to the cluster until a test is met and returns a successful exit code.

Both readinessProbes and livenessProbes use the same syntax and are identical other than the name. Where the readinessProbe is checked prior to being ready, then not again, the livenessProbe continues to be checked.

There are three types of liveness probes: 
    a command returns a zero exit value, meaning success, 
    an HTTP request returns a response code in the 200 to 399 range, 
    and the third probe uses a TCP socket. In this example we’ll use a
command, cat, which will return a zero exit code when the file /tmp/healthy has been created and can be accessed.


1. Edit YAML deployment file and add the stanza for a readinessprobe
```
readinessProbe:
  exec:
    command:
    - cat
    - /tmp/healthy
  initialDelaySeconds: 5
  periodSeconds: 5
```
2. Delete and recreate the try1 deployment.
   
    kubectl delete deployment try1

    kubectl create -f simpleapp.yaml

    kubectl get deployment

    kubectl get pods

    for name in $(kubectl get pod -l app=try1 -o name); do kubectl exec $name -c simpleapp -- touch /tmp/healthy; done

    kubectl get pods

3. Edit YAML deployment file and add this for livenessprobe

```
apiVersion: v1
kind: Pod
metadata:
  name: goproxy
  labels:
    app: goproxy
spec:
  containers:
  - name: goproxy
    image: k8s.gcr.io/goproxy:0.1
    ports:
    - containerPort: 8080
    readinessProbe:
      tcpSocket:
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 10
    livenessProbe:
      tcpSocket:
        port: 8080
      initialDelaySeconds: 15
      periodSeconds: 20
```

4. Delete and recreate the try1 deployment.
   
    kubectl delete deployment try1

    kubectl create -f simpleapp.yaml

    kubectl get deployment

    kubectl get pods

    for name in $(kubectl get pod -l app=try1 -o name); do kubectl exec $name -c simpleapp -- touch /tmp/healthy; done

    kubectl get pods

5. View the events for a particular pod. Even though both containers are currently running and the pod is in good shape, note the events section shows the issue, but not a change in status or the probe success.

    kubectl describe pod try1-TAB | tail

6. If you look for the status of each container in the pod, they should show that both are Running and ready showing True.

    kubectl describe pod try1-TAB | grep -E 'State|Ready'
