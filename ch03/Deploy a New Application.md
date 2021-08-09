3.1: Deploy a New Application

1. Install python on your cp node

    sudo apt-get -y install python3

2. Create a simple python app
    simple.py
    Test the app
7. Create a text file named Dockerfile

 8. Build the container

    sudo podman build -t simpleapp .

9. Verify you see images

    sudo podman images

10. Run container

    sudo podman run localhost/simpleapp

11. Locate file : date.out

    sudo find / -name date.out

sudo tail /var/lib/containers/storage/overlay/f66a5829cc034a461fe87b5ed4b6db7b73d5107213edbb92a35d5702a7460913/diff/date.out
