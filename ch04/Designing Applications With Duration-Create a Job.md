4.2: Designing Applications With Duration: Create a Job

1. Create a job which will run a container which sleeps for three seconds then stops.

2. Create the job, then verify and view the details. The example shows checking the job three seconds in and then again after it has completed. You may see different output depending on how fast you type.

```
   kubectl create -f job.yaml

    kubectl get job

    kubectl describe jobs.batch sleepy

    kubectl get job
```
3. View the configuration information of the job. There are three parameters we can use to affect how the job runs. Use -o yaml to see these parameters.

AS the Job continues to AGE in a completion state, delete the Job

```
    kubectl get jobs.batch sleepy -o yaml

    kubectl delete jobs.batch sleepy
```
4. add the completions: parameter and set it to 5. Create the job again. As you view the job note that COMPLETIONS begins as zero of 5. View the pods that running. Again the output may be different depending on the speed of typing. Eventually all the jobs will have completed. Verify then delete the job.
   

```
kubectl create -f job.yaml

kubectl get jobs.batch

kubectl get jobs

kubectl delete jobs.batch sleepy
```

5. adding parallelism: parameter :
    Edit the YAML again. Set it to 2 such that two pods at a time will be deployed.

    Create the job again. You should see the pods deployed two at a time until all five have completed.

```
kubectl create -f job.yaml

kubectl get jobs.batch

kubectl get jobs
```

6. Add activeDeadlineSeconds: to 15.

    Edit YAML again. Add a parameter which will stop the job after a certain number of seconds.

    Delete and recreate the job again. It should run for four times then continue to age without further completions.

```
kubectl delete jobs.batch sleepy

kubectl create -f job.yaml

kubectl get jobs.batch

kubectl get jobs
```

7. View the message: entry in the Status section of the object YAML output. You may see less status if the job has yet to run. Wait and try again, if so.

```
kubectl get job sleepy -o yaml

kubectl delete jobs.batch sleepy
```