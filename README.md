# The JPV (Jumia Phone Validator) Microservice CD Pipeline

## Contents
- Microservice application Source codes (provided)
- Infrastructure codes (for AWS CloudFormation)
- Ansible Playbooks

The infrastructure codes is to automate all configurations and processes including but not only:
- Servers Provisioning
- Docker images builds
- Network management 
- Firewall management, etc

## Goals
- Automatically configure servers: install required software, configure firewalls and configure SSH access 
- Automatically deploy the microservice jumia_phone_validator with all the required configurations 
- Automatically deploy the database service with all the required configurations

## Limitations 
- Inability to use any roles from Ansible Galaxy 

## Server Provisioning 
- Servers access should be SSH only (port 1337) with SSH Key
- Password authentication should be disabled 
- Root login should be disabled 
- Firewall should deny all the incoming traffic and only expose the required ports to the internet (e.g. SSH port, HTTP port) 

## Configurations Required:
## Servers Features
1) Load-balancer  
  a) Run a application load balancer to expose the microservice API via port 80 and 443
2) Database   
  a) Run the PostgreSQL service on a RDS  
  b) Create database: jumia_phone_validator  
  c) Create database user (jumia) with secure password  
  d) Grant privileges to read and write  
  e) Dump the SQL file "sample.sql" into the database
3) Microservice  
  a) Run the microservice jumia_phone_validator on a Docker container (take into account the requirements described in the README file).  
  b) Connect to the PostgreSQL database.  

## Network configuration 
Using the operating system firewall (e.g. iptables, ufw, etc): 
1) Load-balancer  
  a) Accept SSH connections from any IP address  
  b) Accept requests from any IP address via port 80  
2) Database  
  a) Accept SSH connections from any IP address  
  b) Accept requests from the microservice IP address  
3) Microservice  
  a) Accept SSH connections from any IP address  
  b) Accept requests from the load-balancer IP address  
