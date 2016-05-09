---
layout: page 
title: Docker quickreference
excerpt: "Docker quick reference"
---
{% include _toc.html %}

### 1. Dockerfile

+ ***FROM*** - Select base image

+ ***MAINTAINER*** - details about the author

+ ***ADD*** - Adds files from host to container. Can be used to copy files from URL to container. 

+ ***RUN*** - Run commands at build time. CMD will be overwritten by the command specified when running the container

+ ***CMD*** - Run ocommand at runtime. Only one command is run, if specified more than one, the last command will overwrite the others

+ ***VOLUME*** - Adds a volume to the container. You can't specify the host folder to be munted in a Dockerfile

+ ***ENTRYPOINT***- Like CMD, with 2 differences. You can't overwrite it when running the conainer. Averything thet is passed at the end of a docker run command will be used as an argument for the ENTRYPOINT command

+ ***ENV*** - Set a environment variable in the container. Also you can use it as a variable in the Docker file

+ ***WORKDIR*** - Sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile. If the WORKDIR doesn’t exist, it will be created.

+ ***LABEL*** - Used to set metadata on an image. version,description,etc.. LABEL key=value 

+ ***EXPOSE*** I informs Docker that the container listens on the specified network ports at runtime.

+ ***COPY*** - Copies new files or directories from src to dest on the container

+ ***USER*** - Sets the user name or UID to use when running the image and for any RUN, CMD and ENTRYPOINT cmmands

+ ***ARG*** - Defines a variable that users can pass at build-time to the builder with: docker build --build-arg varname=value. Use it in Dokerfile with USER command like this: USER ${user:-some_user} 



> Note: Each entry of the above types in a Dockerfile will be an 
>	intermediate docker image. Use as few entries as possible with "&& \" at the end of the line.

> Use [this link](https://docs.docker.com/engine/reference/builder/) for a full Dockerfile reference.



### 2.Docker commands

<style type="text/css">
.tftable {font-size:12px;color:#333333;width:100%;border-width: 1px;border-color: #729ea5;border-collapse: collapse;}
.tftable th {font-size:12px;background-color:#acc8cc;border-width: 1px;padding: 8px;border-style: solid;border-color: #729ea5;text-align:left;}
.tftable tr {background-color:#d4e3e5;}
.tftable td {font-size:12px;border-width: 1px;padding: 8px;border-style: solid;border-color: #729ea5;}
.tftable tr:hover {background-color:#ffffff;}
</style>

<table class="tftable" border="1">
<tbody>
<tr><th>Command</th><th>Description</th></tr>

<tr><td>docker pull ubuntu</td><td>  Download prebuilt image</td></tr>
<tr><td>docker pull centos:5</td><td>  Download centos 5 version</td></tr>
<tr><td>docker pull centos -a</td><td>  Download all centos versions</td></tr>
<tr><td>docker run -i -t ubuntu /bin/bash </td><td> run in interactive mode</td></tr>
<tr><td>docker run centos:7 /usr/bin/echo hello </td><td> Run container and echo</td></tr>
<tr><td>docker run --net bridge -ti centos6/httpd </td><td> Run the run the container in specific network</td></tr>
<tr><td>docker run -it -name=andrei centos:6 </td><td> change the nme of the container</td></tr>
<tr><td>docker run -it -d centos:6 </td><td> Run in daemon mode. Use attach to get in</td></tr>
<tr><td>docker run -it -d -p 3305:3306  mysql </td><td> Forward local port 3305 to container port 3306</td></tr>
<tr><td>docker run -it -v /data --name duck centos:6 </td><td> Attach volume. You can fnd volume in /var/lib/docker/volumes</td></tr>
<tr><td>docker run -it -v /srv/folder:/data --name duck centos:6</td><td>Attach a local specific drectory to the container</td></tr>
<tr><td>docker inspect <docker_id> </td><td> Show details about container</td></tr>
<tr><td>docker networks </td><td> Show/add/delete docker networks</td></tr>
<tr><td>docker images </td><td> Shows existent images</td></tr>
<tr><td>docker build -t <tag> . </td><td> Builds an image from a Dockerfile</td></tr>
<tr><td>docker ps -a </td><td> Shows all existing containers</td></tr>
<tr><td>docker ps -a -s </td><td> Shows all existing containers with size</td></tr>
<tr><td>ctrl+p ctrl+q </td><td> Detach docker</td></tr>
<tr><td>docker attach <container id> </td><td> Attach a running container</td></tr>
<tr><td>docker run -d -p 80:80 -name <container name> <image repo>:<image tag> </td><td> Run a container from an image in daemon mod and publish port</td></tr>
<tr><td>ID=$(docker ps -l -q) </td><td> Get the ID of last image run</td></tr>
<tr><td>PID=$(docker inspect --format "{{ .State.Pid }}" $ID) </td><td> Get PID from the image</td></tr>
<tr><td>sudo nsenter --target $PID --mount --uts --ipc --net --pid </td><td> Enter the docker container</td></tr>
<tr><td>IP=$(docker inspect --format "{{ .NetworkSettings.IPAddress }}" $ID) </td><td> Getting the private IP address of docker container</td></tr>
<tr><td>docker run -p <host_port1>container_port1> -p <host_port2>container_port2> </td><td> Map multiple ports</td></tr>
<tr><td>nsenter --target $(docker inspect --format "{{ .State.Pid }}" $(docker ps -l -q)) --mount --uts --ipc --net --pid </td><td> Enter docker container oneline</td></tr>
<tr><td>docker rm $(docker ps -a -q) </td><td> Remove all stopped docker instances</td></tr>
<tr><td>docker rmi $(docker images -q) </td><td> Remove all stopped docker images</td></tr>
<tr><td>nsenter --target $(docker inspect --format {{.State.Pid}} <container_name_or_ID>) --mount --uts --ipc --net --pid			</td><td>Enter in a running container</td></tr>
<tr><td>docker save -o image.tar <image>:version	</td><td> Save an image to tar</td></tr>
<tr><td>docker load -o image.tar </td><td> load image from tar</td></tr>
<tr><td>docker build -t username/imagename:v1 . </td><td> Builds an image version1 using user</td></tr>
<tr><td>docker run -d --name <name_to_run_as> <image_name>:<version> </td><td> Run an image in daemon mode</td></tr>
<tr><td>docker stop <id>	 </td><td> Stops running container</td></tr>
<tr><td>docker search <id>	 </td><td> Dearch images</td></tr>
<tr><td>docker top <id>	 </td><td> What command is running in the container</td></tr>
<tr><td>docker info  </td><td>Information about current docker settings </td></tr>
<tr><td>usermod -G docker <user>      </td><td>Add your user to docker group to run docker without sudo </td></tr>
<tr><td>docker -H 192.168.0.2 -d &    </td><td>Run docker in network mode and not use local socket (/run/docker.sock) </td></tr>
<tr><td>export DOCKER_HOST="tcp://192.168.0.2:2375"   </td><td>To use docker over network </td></tr>
<tr><td>docker -H 192.168.0.2 -H UNIX:///var/run/docker.sock -d &     </td><td>Bind docker service to both the local socket and network </td></tr>
<tr><td>/var/lib/docker/aufs/diff/    </td><td>Location of container data even after container stopped </td></tr>
<tr><td>/var/lib/docker/containers    </td><td>Location of container configurations </td></tr>
<tr><td>docker commit <container_id> <image_name> </td><td>Save an image from running container</td></tr>
<tr><td>docker history <image_id> </td><td>shows history of an image</td></tr>
<tr><td>docker inspect <container_id>|grep Pid </td><td>Get the pid of the container</td></tr>
<tr><td>nsenter -m -u -n -p -i -t <Pid> </td><td>Get shell to the container with <Pid></td></tr>
<tr><td>docker-enter <container_id> </td><td>Get shell to a running container</td></tr>
<tr><td>docker exec -it ffb718704ed0 /bin/bash </td><td>Recommended method to get shell inside acontainer</td></tr>
<tr><td>docker run -v /usr/local/bin:/target jpetazzo/nsenter </td><td>Get the nsenter command if missing from your host</td></tr>
<tr><td>docker logs <container_id> </td><td>Shows output of PID 1 on container</td></tr>
<tr><td>docker tag <image_id> username/imagename:version </td><td>Set different tag for image before pushing to hub</td></tr>
<tr><td>docker push username/imagename:1.0 </td><td>Push image to hub</td></tr>
<tr><td>docker run -it --volumes-from=<container_name> centos:6 /bin/bash </td><td>Share a volume with an existing container</td></tr>
<tr><td>docker -v rm <container_id>  </td><td>Remove container and the volume. Without -v the volume is not deleted</td></tr>
<tr><td>docker logs -f <container_id> </td><td>Sows logs for PID 1 in tail -f form</td></tr>
<tr><td>docker kill $(docker ps|grep -v "CONTAINER"|awk '{print $1}'|head -1)</td><td>Kill last opened container</td></tr>
<tr><td>docker exec -it $(docker ps|grep -v "CONTAINER"|awk '{print $1}'|head -1) /bin/sh</td><td>Enter last opened container</td></tr>
<tr><td>docker rmi $(docker images | grep "^<none>" | awk "{print $3}")</td><td>Remove docker images without tag</td></tr>
<tr><td>docker volume rm $(docker volume ls -qf dangling=true)</td><td>Remove all volumes</td></tr>
<tr><td></td><td></td></tr>

</tbody>
