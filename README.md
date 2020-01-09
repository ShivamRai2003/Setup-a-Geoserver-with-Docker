![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/GeoServer.png)
  ## Task : Setup-a-Geoserver-with-Docker



## Basic Descriptive Works

### Why Geoserver is an important factor in a GIS stack.

**GEOSERVER**

GeoServer is an open source server for sharing geospatial data. Designed for interoperability, it publishes data from any major spatial data source using open standards. GeoServer has evolved to become an easy method of connecting existing information to virtual globes such as Google Earth and NASA World Wind as well as to web-based maps such as OpenLayers, Leaflet, Google Maps and Bing Maps
GeoServer functions as the reference implementation of the Open Geospatial Consortium Web Feature Service standard, and also implements the Web Map Service, Web Coverage Service and Web Processing Service specifications. 

**GOALS**

GeoServer aims to operate as a node within a free and open Spatial Data Infrastructure. Just as the Apache HTTP Server has offered a free and open web server to publish HTML, GeoServer aims to do the same for geospatial data.

**Features**

GeoServer reads a variety of data formats including: 
•	PostGIS
•	Oracle Spatial
•	ArcSDE
•	DB2
•	MySQL
•	MongoDB
•	Apache Solr
•	Shapefiles
•	GeoTIFF
•	GTOPO30
•	ECW, MrSID
•	JPEG2000

**Note : It’s an Important factor in GIS(Geographic Information System) stack because GeoServer makes it easier for geospatial data to be stored, exchanged, analyzed and edited. It's like a foundation for the entire stack, as a way to connect knowledge and resources together to function in unison.**

## What Docker is and why Docker should be used to containerise Geoserver.

Docker: The Modern Platform for High-Velocity Innovation. Docker is a set of platforms as a service product that use OS-level virtualization to deliver software in packages called containers. Containers are isolated from one another and bundle their own software, libraries and configuration files; they can communicate with each other through well-defined channels.

**DOCKER’S FEATURES**
•	Easy and Faster Configuration.
•	Increase productivity.
•	Application Isolation.
•	Swarm.
•	Routing Mesh.
•	Services.
•	Security Management.

**WHY DOCKER ?**
Docker is a beast, it can be remotely daunting for incipient users who aren’t habituated with the command-line, but it provides you with an expedient to build and run software in a very consistent and controlled way by building upon a technology called LXC containers. we can  download and run software like Postgres + PostGIS on any machine with minimal configuration very quickly.

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/Docker%20Architecture%203.png)

•	With containers, you can approach the database as an on-demand utility, which means that each application can have its own dedicated database that can be spun up as needed. This overcomes the disadvantages of large, monolithic databases with a microservices architecture supported by smaller, containerized databases
.
•	Containerized databases separate storage from compute, denoting storage performance and capacity can be scaled independently of compute resources. This provides more flexibility in upfront database capacity orchestrating and provisioning, since changes are much more facile to make later

•	Software-defined containerized databases provide a crucial missing link in high-velocity DevOps cycles, allowing development and operations teams to collaborate seamlessly. At the same time, however, containerized databases have a unique set of challenges in terms of high data availability, backup and recovery, and other critical database performance and compliance requirements.

**The above three points tell us  why Docker should be used to containerise with GeoServer.**

## Environment Setup

Guys, my experience was with docker was amazing I faced a lot of difficulties. But finally, I got to know it’s easy to install. So I will tell you how to install docker on your desktop with safely and easily.

## How to Install Docker on your local machine ?

1.	Docker for windows required  windows 10 with Hyper-V virtualization enabled. which is only available on Windows 10 Professional or Enterprise 64 bit versions. But I will be not using Docker For Desktop as I told you the reason.

2.	I will be Installing Docker Toolbox which is available for all OS(Operating System). And It uses VirtualBox to run your containers in conjunction with Docker.

3.	Download the Docker Toolbox installer from here https://github.com/docker/toolbox/releases

4.	See the Image below I have Downloaded the Installer.

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/Installer.JPG)

5.	Then I installed Docker Toolbox and it created the image in virtual box and it was running successfully. 

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/Docker%20running.JPG)

## Let’s Get familiar with some basic Docker commands

1.	`` docker ps `` this command will tell us how many containers are running. At same time. See the output below.

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/docker-ps.JPG)

2. ``docker --version``  this command will tell you the which version of docker you are running.

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/docker--version.JPG)

3.	``docker stop`` this command will stop the current container running.

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/docker%20stop.JPG)

4.	``docker rm `` will remove the container from docker.

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/docker%20rm.JPG)

5. ``docker ps -a`` this command will tell us the status of the container whether it’s running or not.

https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/docker%20ps-a.JPG

6.	``docker pull`` this command is used to download the image file from repository of docker.

## Creating the container

1.	To start, I have pulled the image of GeoServer From this link https://hub.docker.com/r/kartoza/geoserver/  or you can also buil the script which is available on Github.

  Command : docker pull kartoza/geoserver

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/Installing_geoserver.JPG)

2.	To run the Geoserver on Localhost just type command 

`` docker run --name "geoserver"  --link postgis:postgis -p 8080:8080 -d -t kartoza/geoserver``

3.	Now GeoServer is running. So, Navigate ``http://192.168.99.100:8080/geoserver/web/?0`` in your web browser. And login with ``Username : admin and Password : geoserver`` as default

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/GeoServer_Welcome_Screen.JPG)

**Note: Please Note that this ip 192.168.99.100 is for Docker. To check Ip just type ``ifconfig``**

4.	You can also use the following environment variables to pass a user name and password to PostGIS

•	-e USERNAME=<PGUSER>
•	-e PASS=<PGPASSWORD>
  
5.	Now Create a workspace so you can uploads the layer and create the store. And note that under ``services`` don’t forget to choose WFS and WMS.

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/create%20a%20workspace.JPG)

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/WFS%20AND%20WMS.JPG)

6.	Now create a store and under **Raster Data Source.** Choose GeoTIFF (Tagged Image File Format with Geographic information).

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/GeoTIFF.JPG)

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/data%20store.JPG)

7.	Now , In order to show the layer first you have to Transfer the GeoTIFF file to container because It’s downloaded in our Windows. So In order to use this transfer this `.tif` file to container ID First. 

   To do this first know the container id running on that. Open Docker Terminal.
``Command : docker container ls >> It will give you the Id of that container.``

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/Container%20Id.JPG)

``Note that Container Id is 745c4500de6d. Running  Kartoza/GeoServer.``

Now go to that director where .tiff file is present and use this command to move the file into ``745c4500de6d`` this container.

See Below we successfully move the file into the container. And now you can browse it and select.

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/Succesfully%20Executed.JPG)
**Command : docker cp <File> <Container_Id>:/File**

8.	Now Create A New Layer. Via `` Layer > Add a new layer ``

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/Preview_Layer.JPG)

9.	Now I will use the  Layer Preview via OpenLayers to render and view the layer via the browser.

![](https://github.com/ShivamRai2003/Setup-a-Geoserver-with-Docker/blob/master/IMAGES/Layer_Preview.JPG)

  That's All -- Thank You !
