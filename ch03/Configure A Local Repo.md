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

