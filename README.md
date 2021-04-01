## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![github logo]/Images/CloudProject.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

![github]https://github.com/JRowe25/CyberSecurityCloudProject/blob/main/Ansible/elk-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting public access to the network.
  -Load Balancers will protect the virtual network against DDoS attacks by ditrubuting traffic betwen servers.
  -The Jump-Box is hidden from public networks and can only be accessed by the administrator

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems and system metrics.
  -Filebeat will monitor the log files looks for changes on the machine
  -Metribeat collect metrix from the OS and any serves running on the server

The configuration details of each machine may be found below.
| Name     	| Function  	| IP Address 	| Operating System 	|
|----------	|-----------	|------------	|------------------	|
| Jump-Box 	| Gateway   	| 10.0.04    	| Linux            	|
| Web-1    	| Webserver 	| 10.0.0.5   	| Linux            	|
| Web-2    	| Webserver 	| 10.0.0.6   	| Linux            	|
| ElkVM    	| Monitor   	| 10.1.0.4   	| Linux            	|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-174.222.131.24

Machines within the network can only be accessed by SSH.
  -The ElkVM can only be accesed though the System Admin's IP adress

A summary of the access policies in place can be found in the table below.

| Name     	| Publicly Accessible 	| Allowed IP Address 	|
|----------	|---------------------	|--------------------	|
| Jump-Box 	| yes                 	| 174.222.3.130     	|
| Web-1    	| no                  	| 10.0.0.1-254       	|
| Web-2    	| no                  	| 10.0.0.1-254       	|
| ElkVM    	| no                  	| 10.0.0.1-254       	|
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
  -Ansible allows us to install, update, and add web servers to the network quickly and efficently 

The playbook implements the following tasks:
  -Install docker to all the network machines
  -Install Ansible to the Jump-Box to allow it to distrubte docker containers to the VMs across the network
  -The Ansible playbooks are then used to install the Elk stack container onto the ElkVM

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text]https://github.com/JRowe25/CyberSecurityCloudProject/blob/main/Images/docker.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
 -Web-1/10.0.0.5
 -Web_2/10.0.0.6
 -ElkVM/10.0.0.7

We have installed the following Beats on these machines:
  -Filebeat
  -Metricbeat

These Beats allow us to collect the following information from each machine:
 -Filebeat: Looks for any changes to the file system and monitors Web Log data
 -Metricbeat:Looks for changes in the system metrics like SSH connection and sudo commands.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the .yml file to ansible directory.
- Update the hosts file to include VM IP addresses
- Run the playbook, and navigate to Kibana http://hostIP:5601/app/kibana to check that the installation worked as expected.
