## NPIX-RS232 nodes

[![](https://images.microbadger.com/badges/image/hilschernetpi/netpi-nodered-npix-rs232.svg)](https://microbadger.com/images/hilschernetpi/netpi-nodered-npix-rs232 "NPIX-RS232")
[![](https://images.microbadger.com/badges/commit/hilschernetpi/netpi-nodered-npix-rs232.svg)](https://microbadger.com/images/hilschernetpi//netpi-nodered-npix-rs232 "NPIX-RS232")
[![Docker Registry](https://img.shields.io/docker/pulls/hilschernetpi/netpi-nodered-npix-rs232.svg)](https://registry.hub.docker.com/u/hilschernetpi/netpi-nodered-npix-rs232/)&nbsp;
[![Image last updated](https://img.shields.io/badge/dynamic/json.svg?url=https://api.microbadger.com/v1/images/hilschernetpi/netpi-nodered-npix-rs232&label=Image%20last%20updated&query=$.LastUpdated&colorB=007ec6)](http://microbadger.com/images/hilschernetpi/netpi-nodered-npix-rs232 "Image last updated")&nbsp;

Made for [netPI](https://www.netiot.com/netpi/), the Raspberry Pi 3B Architecture based industrial suited Open Edge Connectivity Ecosystem

### Node-RED and rs232 nodes for netPI's NIOT-E-NPIX-RS232 extension module

The image provided hereunder deploys a container with installed Debian, Node-RED and rs232 nodes to communicate with extension modules NIOT-E-NPIX-RS232.

Base of this image builds [debian](https://www.balena.io/docs/reference/base-images/base-images/) with installed Internet of Things flow-based programming web-tool [Node-RED](https://nodered.org/) and two extra nodes *serial rs232 (in/out)* providing access to the RS232 serial port of the module NIOT-E-NPIX-RS232. The nodes communicate to the module across a serial connection over device `/dev/ttyS0` using the CPU's so-called "mini UART" mentioned in the [BCM2835 ARM Peripherals manual](https://www.raspberrypi.org/app/uploads/2012/02/BCM2835-ARM-Peripherals.pdf). This UART has some restrictions supporting for example 8,7 Databits only or does not support partity handling and hence is not a 16650 compatible UART.

ATTENTION! Never plug or unplug any extension module if netPI is powered. Make sure a module is already inserted before applying 24VDC to netPI. 

#### License

The software includes modified third party software from the Github repository [serialport](https://github.com/node-red/node-red-nodes/tree/master/io/serialport) which is distributed in accordance with [the Apache license, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html).

#### Container prerequisites

##### Port mapping

To allow the access to Node-RED over a web browser the container TCP port `1880` needs to be exposed to the host.

##### Host device

The serial port device `/dev/ttyS0` needs to be added to the container. The device is available only if an inserted module has been recognized by netPI during boot process. Else the container will fail to start.

#### Getting started

#### Getting started

STEP 1. Open netPI's website in your browser (https).

STEP 2. Click the Docker tile to open the [Portainer.io](http://portainer.io/) Docker management user interface.

STEP 3. Enter the following parameters under *Containers > + Add Container*

Parameter | Value | Remark
:---------|:------ |:------
*Image* | **hilschernetpi/netpi-nodered-npix-rs232** |
*Port mapping* | *host* **1880** -> *container* **1880** | *host*=any unused
*Restart policy* | **always**
*Runtime > Devices > +add device* | *Host path* **/dev/ttyS0** -> *Container path* **/dev/ttyS0** |

STEP 4. Press the button *Actions > Start/Deploy container*

Pulling the image may take a while (5-10mins). Sometimes it may take too long and a time out is indicated. In this case repeat STEP 4.

#### Accessing

After starting the container open Node-RED in your browser with `http://<netpi's ip address>:<mapped host port>` e.g. `http://192.168.0.1:1880`. Two nodes *serial rs232 (in/out)* in the nodes *npix* library palette provides you access to the RS232 interface of the NPIX module. The nodes' info tab in Node-RED explains how to use them.

#### Automated build

The project complies with the scripting based [Dockerfile](https://docs.docker.com/engine/reference/builder/) method to build the image output file. Using this method is a precondition for an [automated](https://docs.docker.com/docker-hub/builds/) web based build process on DockerHub platform.

DockerHub web platform is x86 CPU based, but an ARM CPU coded output file is needed for Raspberry systems. This is why the Dockerfile includes the [balena](https://balena.io/blog/building-arm-containers-on-any-x86-machine-even-dockerhub/) steps.

#### License

View the license information for the software in the project. As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).
As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.

[![N|Solid](http://www.hilscher.com/fileadmin/templates/doctima_2013/resources/Images/logo_hilscher.png)](http://www.hilscher.com)  Hilscher Gesellschaft fuer Systemautomation mbH  www.hilscher.com
