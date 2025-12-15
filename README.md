<h3>Granting docker permission </h3>

    ubuntu@ip-172-31-46-155:~$ docker ps
    permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.50/containers/json": dial unix /var/run/docker.sock: connect: permission denied
    ubuntu@ip-172-31-46-155:~$ whoami
    ubuntu
    ubuntu@ip-172-31-46-155:~$ sudo usermod -aG docker $USER && newgrp docker

