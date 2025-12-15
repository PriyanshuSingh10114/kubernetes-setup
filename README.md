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
        
<h3>Context switching in cluster if we have oth minikube and kind cluster installed</h3>

        ubuntu@ip-172-31-46-155:~/minikube$ kubectl get nodes --context kind-tws-cluster
        NAME                        STATUS   ROLES           AGE   VERSION
        tws-cluster-control-plane   Ready    control-plane   32m   v1.31.2
        tws-cluster-worker          Ready    <none>          32m   v1.31.2
        tws-cluster-worker2         Ready    <none>          32m   v1.31.2
        tws-cluster-worker3         Ready    <none>          32m   v1.31.2
        ubuntu@ip-172-31-46-155:~/minikube$


<h3>To get namespaces</h3>

    ubuntu@ip-172-31-46-155:~/kubernetes-in-one-shot$ kubectl get ns
    NAME                 STATUS   AGE
    default              Active   3h24m
    kube-node-lease      Active   3h24m
    kube-public          Active   3h24m
    kube-system          Active   3h24m
    local-path-storage   Active   3h24m
    
<h3>Setting Default Context</h3>

    kubectl config use-context kind-tws-cluster

---

    ubuntu@ip-172-31-46-155:~/kubernetes-in-one-shot$ kubectl get pods -n kube-system
    NAME                                                READY   STATUS    RESTARTS        AGE
    coredns-7c65d6cfc9-7zb4d                            1/1     Running   1 (8m41s ago)   3h28m
    coredns-7c65d6cfc9-zv6gx                            1/1     Running   1 (8m41s ago)   3h28m
    etcd-tws-cluster-control-plane                      1/1     Running   1 (8m41s ago)   3h28m
    kindnet-2s6gh                                       1/1     Running   1 (8m41s ago)   3h28m
    kindnet-b8zsp                                       1/1     Running   1 (8m41s ago)   3h28m
    kindnet-jct5v                                       1/1     Running   1 (8m41s ago)   3h28m
    kindnet-mqhrk                                       1/1     Running   1 (8m41s ago)   3h28m
    kube-apiserver-tws-cluster-control-plane            1/1     Running   1 (8m41s ago)   3h28m
    kube-controller-manager-tws-cluster-control-plane   1/1     Running   1 (8m41s ago)   3h28m
    kube-proxy-7xdgl                                    1/1     Running   1 (8m41s ago)   3h28m
    kube-proxy-l7lkh                                    1/1     Running   1 (8m41s ago)   3h28m
    kube-proxy-qgxdl                                    1/1     Running   1 (8m41s ago)   3h28m
    kube-proxy-tcxm2                                    1/1     Running   1 (8m41s ago)   3h28m
    kube-scheduler-tws-cluster-control-plane            1/1     Running   1 (8m41s ago)   3h28m
    
    ubuntu@ip-172-31-46-155:~/kubernetes-in-one-shot$ kubectl create ns nginx
    namespace/nginx created
    
    ubuntu@ip-172-31-46-155:~/kubernetes-in-one-shot$ kubectl run nginx --image=nginx
    pod/nginx created
    
    ubuntu@ip-172-31-46-155:~/kubernetes-in-one-shot$ kubectl get pods
    NAME    READY   STATUS    RESTARTS   AGE
    nginx   1/1     Running   0          55s
    ubuntu@ip-172-31-46-155:~/kubernetes-in-one-shot$ kubectl delete pod nginx
    pod "nginx" deleted from default namespace
    
    ubuntu@ip-172-31-46-155:~/kubernetes-in-one-shot$


