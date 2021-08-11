4.3: Designing Applications With Duration: Create a CronJob

1. Edit cronjob.yaml

2. Create the new CronJob. View the jobs. It will take two minutes for the CronJob to run and generate a new batch Job

```
kubectl create -f cronjob.yaml

kubectl get cronjobs.batch

kubectl get job

kubectl get cronjobs.batch

kubectl get jobs.batch

kubectl get jobs.batch

```

3. Ensure that if the job continues for more than 10 seconds it is terminated. We will first edit the sleep command to run for 30 seconds then add the activeDeadlineSeconds: entry to the container. Delete and recreate the CronJob. It may take a couple of minutes for the batch Job to be created and terminate due to the timer.


```

kubectl delete cronjobs.batch sleepy

kubectl create -f cronjob.yaml

sleep 120 ; kubectl get jobs

kubectl get cronjobs.batch

kubectl get jobs

kubectl get jobs

kubectl get cronjobs.batch

kubectl delete cronjobs.batch sleepy

```
