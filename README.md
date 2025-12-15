<h3>Checking installation after running kind-cluster setup</h3>

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

