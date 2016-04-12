---
layout: page 
title: Docker quickreference
excerpt: "Docker quick reference"
---
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
<tr><td> </td><td></td></tr>
</tbody>
</table>
