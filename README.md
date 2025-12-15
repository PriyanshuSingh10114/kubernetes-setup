<h3>Checking installation after running install_kind.sh setup</h3>

    ubuntu@ip-172-31-46-155:~$ docker --version
    Docker version 28.2.2, build 28.2.2-0ubuntu1~24.04.1
    ubuntu@ip-172-31-46-155:~$ kubectl version
    Client Version: v1.34.3
    Kustomize Version: v5.7.1
    The connection to the server localhost:8080 was refused - did you specify the right host or port?
    ubuntu@ip-172-31-46-155:~$ kind --version
    kind version 0.29.0


<h3>Granting docker permission </h3>

    ubuntu@ip-172-31-46-155:~$ docker ps
    permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.50/containers/json": dial unix /var/run/docker.sock: connect: permission denied
    ubuntu@ip-172-31-46-155:~$ whoami
    ubuntu
    ubuntu@ip-172-31-46-155:~$ sudo usermod -aG docker $USER && newgrp docker

<h3>Creating kind Cluster</h3>

    ubuntu@ip-172-31-46-155:~/kind-cluster$ kind create cluster --name=tws-cluster --config=config.yml

    Creating cluster "tws-cluster" ...
     ✓ Ensuring node image (kindest/node:v1.31.2) 🖼
     ✓ Preparing nodes 📦 📦 📦 📦
     ✓ Writing configuration 📜
     ✓ Starting control-plane 🕹️
     ✓ Installing CNI 🔌
     ✓ Installing StorageClass 💾
     ✓ Joining worker nodes 🚜
    Set kubectl context to "kind-tws-cluster"
    You can now use your cluster with:
    
    kubectl cluster-info --context kind-tws-cluster

<h3>Cluster Info</h3>

    ubuntu@ip-172-31-46-155:~/kind-cluster$ kubectl cluster-info --context kind-tws-cluster
    
    #Kubernetes control plane is running at https://127.0.0.1:36087
    #CoreDNS is running at https://127.0.0.1:36087/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

<h3>Get Nodes</h3>
        
        ubuntu@ip-172-31-46-155:~/kind-cluster$ kubectl get nodes
        NAME                        STATUS   ROLES           AGE     VERSION
        tws-cluster-control-plane   Ready    control-plane   7m30s   v1.31.2
        tws-cluster-worker          Ready    <none>          7m14s   v1.31.2
        tws-cluster-worker2         Ready    <none>          7m14s   v1.31.2
        tws-cluster-worker3         Ready    <none>          7m15s   v1.31.2

