3.2 Configure A Local Repo

1. Create a simple registry using the easyregistry.yaml file

    cd app1

    find $HOME -name easyregistry.yaml

    kubectl create -f ../Env-prep/easyregistry.yaml

 2. Take note of the ClusterIP for the new registry service. In the example below it is 10.97.40.62
   
    kubectl get svc | grep registry

3. Verify the repo is working. Please note that if the connection hangs it may be due to a firewall issue. f using AWS also make sure all ports are being allowed.
Edit the IP address to that of your localrepo service found in the previous command.

    curl IP:5000/v2/_catalog

4. Configure podman to work with non-TLS repos. Edit the /etc/containers/registries.conf to uncomment and modify some entries. Ensure your location is within double-quotes as you may get an ”Invalid float value” otherwise.
   
    sudo nano /etc/containers/registries.conf

5. Restart crio and make sure it is still running.


    student@cp:˜/app1$ sudo systemctl restart crio

    student@cp:˜/app1$ sudo systemctl status crio

    export repo=IP:5000
    echo "export repo=IP:5000" >> $HOME/.bashrc

7. Download and tag a typical image from hub.docker.com. Tag the image using the IP and port of the registry, via the $repo variable.

    sudo podman pull alpine

    sudo podman tag alpine $repo/tagtest


8. Push the newly tagged image to your local registry.


    sudo podman push $repo/tagtest

9. verify if we can pull images from our local repo.

    sudo podman image rm alpine

    sudo podman image rm $repo/tagtest

    sudo podman pull $repo/tagtest

10. Configure on worker node and Reboot all Nodes

        sudo reboot

11. Test repo works after reboot.

        curl $repo/v2/_catalog

12. Use podman tag to assign the simpleapp image and then push it to the local registry. The image and dependent images should be pushed to the local repository.
    
    sudo podman tag simpleapp $repo/simpleapp

    sudo podman push $repo/simpleapp

13. Test that the image can be found in the repository, from both the cp and the worker

    curl $repo/v2/_catalog 

14. Return to the cp node and deploy the simpleapp in Kubernetes with several replicas

    kubectl scale deployment try1 --replicas=6

    kubectl get pod -o wide

15. Save the try1 deployment as YAML.
    cd $HOME/app1/

    kubectl get deployment try1 -o yaml > simpleapp.yaml

16. Delete and recreate the try1 deployment using the YAML file. Verify the deployment is running with the expected six replicas.
    kubectl delete deployment try1

    kubectl create -f simpleapp.yaml

    kubectl get deployment

