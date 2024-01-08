[Install instructions](#installing) at the end of the document.

## Commands

* `docker pull [image-name]`: Download an image to run containers from the default repository [hub.docker.com](https://hub.docker.com)
* `docker run [image-name]`: Create a container from the indicated image
* `docker ps`: View the running containers
* `docker ps -a`: View all created containers 
* `docker stop [container-name]`: Stop the indicated container.
* `docker start [container-name]`: Start the indicated container.
* `docker exec [container-name] /path/executable`: run a executable file from inside the container (sample: docker exec -it container-name bash)

### Images

* `docker image ls`: view downloaded images
* `docker image rm [image-name]`: remove image-name image

### Network

* `docker network ls`: show created networks
* `docker network create [network-name]`: create a new network

### Volumes

Docker has many ways to work with persistence.

You can bindmount a local folder to share data between your host and the container:
* `docker run -v /path-to-localfolder:/path-to-containerfolder [image-name]`

You can create a docker volume to persist data and allow acces from the container:
* `docker run -v volume-name:/path-to-containerfolder [image-name]`

### Docker Compose

You can use predefined container orquestrations with docker-compose. A docker-compose.yml is a YAML file where you can describe your microservices architechture with code.

* `docker compose up -d`: dowload required images from docker hub and then launch all containers defined in the yaml file. (-d for --detach mode)
* `docker compose down`: destroy the current orquestration and stops all the defined services 

**docker-compose.yml** (sample)
```
version: '3'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
volumes:
    db_data:
```


## Installing

### Windows 

Docker is a linux technology so you need to [install WSL](wsl.md#installing) in order to use docker over Windows.

After installing WSL in Windows, download and install Docker Desktop.

1. Download [Docker Desktop](https://www.docker.com/products/docker-desktop/)
2. Install Docker Desktop (admin privileges needed)

Docker Desktop install process adds the user who runs the installation to the docker-users local group. Add new users to that group if you want to allow them to run docker desktop.


### GNU/Linux 

https://docs.docker.com/engine/install/ubuntu/

1. Set up Docker's apt repository.
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

2. Install the Docker packages.
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

3. Verify that the Docker Engine installation is successful by running the hello-world image.
```
sudo docker run hello-world
```

4. Manage Docker as a non-root user
    1. Create docker group (if neccesary): 
    ```sudo groupadd docker```
    2. Add your user to the docker group: 
    ```sudo usermod -aG docker $USER```

5. Verify that you can run containers from your own user:
```
docker run hello-world
```


## How to mount your own Registry
We use to get docker images from [hub.docker.com](https://hub.docker.com), the main repository offered by docker.com but it is possible to moutn our own local Registry.

In this tutorial we are going to launch a minimal insecure Registry:

**Create new registry host name_host (or ip_host)**
1. Launch a registry image

    docker run -d -p 5000:5000 --name my-registry registry:2

**Client host - Configure client to user insecure registries**

1. Create/Edit /etc/docker/daemon.json
```
{
        "insecure-registries": ["name_host/ip_host:5000"]
}
```
2. Restart docker service

    sudo systemctl restart docker


**Client host - Upload new image to registry**
1. Download a sample image from hub.docker.com

    docker pull busybox
2. Tag the image pointing to the new repository 

    docker image tag busybox name_host:5000/new-busybox
3. Push the new image to the private registry

    docker push name_host:5000/new-busybox
4. Verify the new added image

    curl http://name_host:5000/v2/_catalog

**Another client host - Download image from private registry**
1. Download image

    docker pull name_host:5000/new-busybox
2. Launch container

    docker run name_host:5000/new-busybox