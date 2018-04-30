## Node-RED + npix rs232 nodes

Made for [netPI](https://www.netiot.com/netpi/), the Open Edge Connectivity Ecosystem

### Debian with Node-RED and rs232 nodes for netPI's NIOT-E-NPIX-RS232 extension module

The image provided hereunder deploys a container with installed Debian, Node-RED and rs232 nodes to communicate with an extension module NIOT-E-NPIX-RS232.

Base of this image builds the latest version of [debian:jessie](https://hub.docker.com/r/resin/armv7hf-debian/tags/) with installed Internet of Things flow-based programming web-tool [Node-RED](https://nodered.org/) and two extra nodes *serial rs232 (in/out)* providing access to the RS232 serial port of the module NIOT-E-NPIX-RS232. The nodes communicate to the module across a serial connection over device `/dev/ttyS0`.

ATTENTION! Never plug or unplug any extension module if netPI is powered. Make sure a module is already inserted before applying 24VDC to netPI. 

#### License

The software includes modified third party software from the Github repository [serialport](https://github.com/node-red/node-red-nodes/tree/master/io/serialport) which is distributed in accordance with [the Apache license, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html).

#### Container prerequisites

##### Port mapping

To allow the access to the Node-RED programming tool over a web browser the container TCP port `1880` needs to be exposed to the host.

##### Host device

The serial port device `/dev/ttyS0` needs to be added to the container. The device is available only if an inserted module has been recognized by netPI during boot process. Else the container will fail to start.

#### Getting started

STEP 1. Open netPI's landing page under `https://<netpi's ip address>`.

STEP 2. Click the Docker tile to open the [Portainer.io](http://portainer.io/) Docker management user interface.

STEP 3. Enter the following parameters under **Containers > Add Container**

* **Image**: `hilschernetpi/netpi-nodered-npix-rs232`

* **Port mapping**: `Host "1880" (any unused one) -> Container "1880"` 

* **Restart policy"** : `always`

* **Runtime > Devices > add device**: `Host "/dev/ttyS0" -> Container "/dev/ttyS0"`

* **Runtime > Privileged mode** : `On`

STEP 4. Press the button **Actions > Start container**

Pulling the image from Docker Hub may take up to 5-10 minutes.

#### Accessing

After starting the container open Node-RED in your browser with `http://<netpi's ip address>:<mapped host port>` e.g. `http://192.168.0.1:1880`. Two nodes *serial rs232 (in/out)* in the nodes *npix* library palette provides you access to the RS232 interface of the NPIX module. The nodes' info tab in Node-RED explains how to use them.

#### Tags

* **hilscher/netPI-nodered-npix-rs232:latest** - non-versioned latest development output of the master branch. Can run on any netPI system software version.

#### GitHub sources
The image is built from the GitHub project [netPI-nodered-npix-rs232](https://github.com/Hilscher/netPI-nodered-npix-rs232). It complies with the [Dockerfile](https://docs.docker.com/engine/reference/builder/) method to build a Docker image [automated](https://docs.docker.com/docker-hub/builds/).

View the license information for the software in the Github project. As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).
As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.

To build the container for an ARM CPU on [Docker Hub](https://hub.docker.com/)(x86 based) the Dockerfile uses the method described here [resin.io](https://resin.io/blog/building-arm-containers-on-any-x86-machine-even-dockerhub/).

[![N|Solid](http://www.hilscher.com/fileadmin/templates/doctima_2013/resources/Images/logo_hilscher.png)](http://www.hilscher.com)  Hilscher Gesellschaft fuer Systemautomation mbH  www.hilscher.com
