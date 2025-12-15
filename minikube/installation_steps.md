Step 1: Update System Packages

    sudo apt update

Step 2: Install Required Packages

    sudo apt install -y curl wget apt-transport-https

Step 3: Install Docker

    sudo apt install -y docker.io

Start and enable Docker.
    
    sudo systemctl enable --now docker
    
Add current user to docker group (To use docker without root)

    sudo usermod -aG docker $USER && newgrp docker

Step 4: Install Minikube

    curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    
Make it executable and move it into your path:
    
    chmod +x minikube
    sudo mv minikube /usr/local/bin/

minkube version

    ubuntu@ip-172-31-46-155:~/minikube$ minikube version
    minikube version: v1.37.0
    commit: 65318f4cfff9c12cc87ec9eb8f4cdd57b25047f3
    ubuntu@ip-172-31-46-155:~/minikube$

Step 5: Install kubectl
Download kubectl, which is a Kubernetes command-line tool.
    
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"


    chmod +x kubectl
    sudo mv kubectl /usr/local/bin/

Step 6: Start Minikube

    minikube start --driver=docker --vm=true 
    
Step 7: Check Cluster Status
Check the cluster status with:

    minikube status

You can also use kubectl to interact with your cluster:

    kubectl get nodes
    
Step 8: Stop Minikube
When you are done, you can stop the Minikube cluster with:

    minikube stop
    
Optional: Delete Minikube Cluster
If you wish to delete the Minikube cluster entirely, you can do so with:

    minikube delete

