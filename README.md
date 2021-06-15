Cloud Formation templates to setup a highly available, load balanced, auto scaling infrastructure on AWS.

Architecture
------------
![Architecture](https://user-images.githubusercontent.com/5586070/122102314-ede7a500-ce32-11eb-8512-a544ecdd9678.png)

Deployment
----------
The cloudformation scripts have been separated out into two modules - `network.yml` and `server.yml`

`network.yml` and its associated parameter file `network-parameters.json` contains the cloudformation 
specification for networking related deployments such as VPC, private and public subnets, Routing Tables, Internet and
NAT gateways.

`server.yml` and its associated parameter file `server-parameters.json` contains the cloudformation specification for
server and application related deployments such as Load Balancer, Launch Configuration, and the servers running the application.

The overall setup can be deployed by first creating the network related infrastructure and then deploying the server related 
infrastructure.

1. `./create.sh networkdeployment network.yml network-parameters.json`
2. `./create.sh serverdeployment server.yml server-parameters.json`

Successful deployment of both network and server infrastructure will result in the Elastic Load Balancer domain being output.
This can be checked in the outputs of the `serverdeployment` stack and used to verify that our infrastruture has been created and our application is running.

Updating
--------

Changes to parameters or the infrastructure itself will require the stack to be updated. This can be done
by running the following commands after the templates have been changed.

1. `./update.sh networkdeployment network.yml network-parameters.json`
2. `./update.sh serverdeployment server.yml server-parameters.json`

Test
----
The application that has been created in these deployments can be temporarily accessed at [http://serve-webap-t7w2oc5f11oz-1568862367.us-west-2.elb.amazonaws.com/](http://serve-webap-t7w2oc5f11oz-1568862367.us-west-2.elb.amazonaws.com/)
