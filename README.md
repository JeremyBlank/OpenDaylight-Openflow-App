# OpenDaylight OpenFlow Manager (OFM) App

OpenDaylight (ODL) is an open-source application development and delivery platform. Openflow Manager (OFM) is an application developed to run on top of ODL to visualize openflow (OF) topologies, program OF paths and gather OF stats. 

## Team
- Jan Medved
- Daniel Malachovsky
- Juraj Sebin
- Vijay Kannan
- Daniel Kuzma
- Stanislav Jamrich
- Zdenko Krnac
- Sergey Madaminov

### Project Demo Link:

xxxxx

### Social Tags:

SDN, Open Source, Openflow, NeXt, RESTCONF API, YANG

### Project Kick-Off Date:

January 2014

### Current Status:

Version of OFM is available with the Cisco Open SDN Controller. 

## Application Overview

OpenFlow Manager allows you to manage the OpenFlow-enabled devices in your network.

Application consists from:

*Basic View Tab*, the default tab, displays topology mapping the OpenFlow-enabled devices in your network and the hosts that are connected to them.

*Flow Management Tab* can be used for determining the number of flows for each OpenFlow-enabled device in your network, viewing a listing of all currently configured flows, adding, modifying and deleting the flows.

*Statistics tab* provides statistics for both the flows configured in your network and the corresponding device ports.

*Hosts Tab* provides summary information for the OpenFlow-enabled host devices that OSC manages.

## OpenFlow Manager installation

To run backend for our app you can use pre-build VM image including Mininet downloadable from
http://mininet.org/download/.

To use this VM as a backend for our app you need to install ODL following this tutorial
https://www.opendaylight.org/installing-opendaylight.

To integrate ODL with our standalone app you must enable these features:

`odl-restconf-all`

`odl-openflowplugin-all`

`odl-l2switch-all`

Start Mininet on VM with

`sudo mn --topo tree--controller 'remote,ip=127.0.0.1,port=6653' --switch ovsk,protocols=OpenFlow13`

For adding host nodes (simulated end-user devices connected to the switches) into topology, in the mininet console run command `pingall`. Host nodes appear in the network-topology data.

Before running the OFM standalone application it is important to configure the controller base URL, controller port, ODL username and ODL password. All these information should be written in `env.module.js` file located in directory `ofm src/common/config`.

To run our standalone app on local web server. If you do not have anyone, you can use tool Grunt, which is installable via npm, the Node.js package manager. Follow this tutorial
http://gruntjs.com/getting-started

You can use this simple Gruntfile.js

```
  module.exports = function(grunt) {

    grunt.loadNpmTasks('grunt-contrib-connect');

    grunt.initConfig({
      pkg: grunt.file.readJSON('package.json'),
      connect: {
        def: {
          options: {
            base: 'ofm',
            keepalive: true,
            port: 9000
          }
        }
      },
    });
    grunt.registerTask('default', ['connect:def']);
  };
```
After running grunt you can access OFM standalone app via web browser typing URL http://localhost:9000.
