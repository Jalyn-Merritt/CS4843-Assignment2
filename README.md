# CS4843-Assignment2

Uploaded the necessary files for the infastructure to be created. These YAML files work as templates to be used in AWS's CloudFormation to aid in the creation of infastructure for a Instagram-like application. With the use of YAML files, JSON parameter files, and bash scripts, creating said infastructure can be accomplished in as easy as a couple of lines. For example, and to start, to create the network, all one would have to do is type the following in a terminal with the AWS CLI available:

```sh
> ./create.sh cloudapp-net network.yml net_params.json
```

To form the rest, enter these into the comand line:

```sh
> ./create.sh cloudapp-serv serverNsecurity.yml serv_params.json
> ./create.sh cloudapp-data storageNdatabase.yml db_params.json
```

# Network

The network YAML template deploys a VPC with a pair of public and private subnets across two Availability Zones. Along with that an Internet Gateway is deployed with a default route on the public subnets. A pair of NAT Gateways, one for each Availability Zone, are deployed with default routes for them both in the private subnets.

# Server

The server YAML template sets up an Autoscaling group and a Load Balancer. Some security groups are made, one to allow http to the hosts and SSH from local only, and another to allow http to the Load Balancer. The servers sit behind the previously made private subnets.

# Database

The storage YAML template deploys a RDS MySQL 8.0.27 database. The primary database is created in the first private subnet and has a secondary database created in the second private subnet. Should the accompanying parameter file be edited and errors occur, the storage YAML file details the constraints that need to be adhered for the database to form.
