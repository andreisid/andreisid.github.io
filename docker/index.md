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

<tr><td>docker pull ubuntu</td><td>  download prebuilt image</td></tr>
<tr><td>docker run -i -t ubuntu /bin/bash </td><td> run in interactive mode</td></tr>
<tr><td>docker images </td><td> shows existent images</td></tr>
<tr><td>docker build -t <tag> . </td><td> builds an image from a Dockerfile</td></tr>
<tr><td>docker ps -a </td><td> shows all existing containers</td></tr>
<tr><td>ctrl+p ctrl+q </td><td> detach docker</td></tr>
<tr><td>docker attach <container id> </td><td> attach a running container</td></tr>
<tr><td>docker run -d -p 80:80 -name <container name> <image repo>:<image tag> </td><td>	run a container from an image in daemon mod and publish port</td></tr>
<tr><td>ID=$(docker ps -l -q) </td><td> getting the ID of last image run</td></tr>
<tr><td>PID=$(docker inspect --format "{{ .State.Pid }}" $ID) </td><td> getting PID from the image</td></tr>
<tr><td>sudo nsenter --target $PID --mount --uts --ipc --net --pid </td><td> enter the docker container</td></tr>
<tr><td>IP=$(docker inspect --format "{{ .NetworkSettings.IPAddress }}" $ID) </td><td> getting the private IP address of docker container</td></tr>
<tr><td>docker run -p <host_port1>container_port1> -p <host_port2>container_port2> </td><td> map multiple ports</td></tr>
<tr><td>nsenter --target $(docker inspect --format "{{ .State.Pid }}" $(docker ps -l -q)) --mount --uts --ipc --net --pid </td><td> enter docker container oneline</td></tr>
<tr><td>docker rm $(docker ps -a -q) </td><td> remove all stopped docker instances</td></tr>
<tr><td>docker rmi $(docker images -q) </td><td> remove all stopped docker images</td></tr>

<tr><td>nsenter --target $(docker inspect --format {{.State.Pid}} <container_name_or_ID>) --mount --uts --ipc --net --pid			</td><td>enter in a running container</td></tr>
<tr><td>docker save -o image.tar <image>:version	</td><td> save an image to tar</td></tr>
<tr><td>docker load -o image.tar </td><td> load image from tar</td></tr>

<tr><td>docker build -t username/imagename:v1 . </td><td> builds an image version1 using user</td></tr>

<tr><td>docker run -d --name <name_to_run_as> <image_name>:<version> </td><td> run an image in daemon mode</td></tr>
<tr><td>docker run -d --name gmw --link gma:rom2vm702 -p 80:80 -p 443:443 a rcade:gmw  </td><td> run and link to another container</td></tr>
<tr><td>docker run -d --name gwb -p 8080:8080 <image_name>:<version>   </td><td> run and publish port to the host</td></tr>

<tr><td>docker stop <id>	 </td><td> stops running container</td></tr>
</tbody>
</table>
