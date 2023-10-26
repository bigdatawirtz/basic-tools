[Install instructions](#installing) at the end of the document.

## Commands

* `docker pull [image-name]`: Download an image to run containers from the default repository [hub.docker.com](https://hub.docker.com)
* `docker run [image-name]`: Create a container from the indicated image
* `docker ps`: View the running containers
* `docker ps -a`: View all created containers 
* `docker stop [container-name]`: Stop the indicated container.
* `docker start [container-name]`: Start the indicated container.

### Images

* `docker image ls`: view downloaded images
* `docker image rm [image-name]`: remove image-name image

### Network

* `docker network ls`: show created networks
* `docker network create [network-name]`: create a new network


## Installing

### Windows 


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
