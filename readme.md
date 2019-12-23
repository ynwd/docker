# Exploring Docker on Mac

1. Install Docker Machine & Docker Client:
    ```
    $ brew install docker-machine docker
    ```
2. Install `xhyve` Driver:
    ```
    $ brew install docker-machine-driver-xhyve
    ```
3. Create a machine:
    ```
    $ docker-machine create --driver xhyve default
    ```
    Response:
    ```
    Creating CA: /Users/yanu/.docker/machine/certs/ca.pem
    Creating client certificate: /Users/yanu/.docker/machine/certs/cert.pem
    Running pre-create checks...
    Creating machine...
    (default) Image cache directory does not exist, creating it at /Users/yanu/.docker/machine/cache...
    (default) No default Boot2Docker ISO found locally, downloading the latest release...
    (default) Latest release for github.com/boot2docker/boot2docker is v19.03.5
    (default) Downloading /Users/yanu/.docker/machine/cache/boot2docker.iso from https://github.com/boot2docker/boot2docker/releases/download/v19.03.5/boot2docker.iso...
    (default) 0%....10%....20%....30%....40%....50%....60%....70%....80%....90%....100%
    (default) Copying /Users/yanu/.docker/machine/cache/boot2docker.iso to /Users/yanu/.docker/machine/machines/default/boot2docker.iso...
    (default) Creating VM...
    (default) /dev/disk3          	                               	/Users/yanu/.docker/machine/machines/default/b2d-image
    (default) "disk3" ejected.
    (default) Generating 20000MB disk image...
    (default) created: /Users/yanu/.docker/machine/machines/default/root-volume.sparsebundle
    (default) Creating SSH key...
    (default) Fix file permission...
    (default) Generate UUID...
    (default) Convert UUID to MAC address...
    (default) Starting default...
    (default) Waiting for VM to come online...
    (default) Waiting on a pseudo-terminal to be ready... done
    (default) Hook up your terminal emulator to /dev/ttys002 in order to connect to your VM
    Waiting for machine to be running, this may take a few minutes...
    Detecting operating system of created instance...
    Waiting for SSH to be available...
    Detecting the provisioner...
    Provisioning with boot2docker...
    Copying certs to the local machine directory...
    Copying certs to the remote machine...
    Setting Docker configuration on the remote daemon...
    Checking connection to Docker...
    Docker is up and running!
    To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env default
    ```
4. Connect Docker Client to the Docker Engine:
    ```
    $ docker-machine env default
    ```
    Response:
    ```
    export DOCKER_TLS_VERIFY="1"
    export DOCKER_HOST="tcp://192.168.64.11:2376"
    export DOCKER_CERT_PATH="/Users/yanu/.docker/machine/machines/default"
    export DOCKER_MACHINE_NAME="default"
    # Run this command to configure your shell:
    # eval $(docker-machine env default)
    ```
    Run this command to configure your shell
    ```
    $ eval $(docker-machine env default)
    ```
5. Pull ubuntu image:
    ```
    $ docker pull ubuntu
    ```
    Response:
    ```
    Using default tag: latest
    latest: Pulling from library/ubuntu
    2746a4a261c9: Pull complete
    4c1d20cdee96: Pull complete
    0d3160e1d0de: Pull complete
    c8e37668deea: Pull complete
    Digest: sha256:250cc6f3f3ffc5cdaa9d8f4946ac79821aafb4d3afc93928f0de9336eba21aa4
    Status: Downloaded newer image for ubuntu:latest
    docker.io/library/ubuntu:latest
    ```
6. Run `bash` inside ubuntu:
    ```
    $ docker run -it --name hello ubuntu bash
    ```
    Response:
    ```
    root@0682abed1302:/#
    ```
    Exit:
    ```
    root@0682abed1302:/# exit 
    ```
7. List all container:
    ```
    $ docker container ls -a
    ```
    Response:
    ```
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
    0682abed1302        ubuntu              "bash"              15 hours ago        Exited (0) 18 seconds ago                       hello
    ```
8. Run stopped container:
    ```
    $ docker container start -i hello
    ```