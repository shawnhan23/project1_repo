## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Network Diagram](../project1_repo/Diagrams/ELK_network.drawio)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. 
Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - See the following files:
  project1_repo/Ansible/web-playbook.yml,
  project1_repo/Ansible/elk-playbook.yml,
  project1_repo/Ansible/filebeat-playbook.yml,
  project1_repo/Ansible/filebeat-config.yml,
  project1_repo/Ansible/metricbeat-config.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
Load balancers protect availability because if one webserver goes down, the load balancer will direct traffic to another
machine that is up and running. The advantage of using a jump box is security because there is only a single machine that is exposed 
to the internet. Other machines on the network can then be accessed after ssh'ing into the jump box. The same idea applies to the
load balancer. The load balancer is accesible to the internet, but the 3 webservers are not.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system logs.
Filebeat can watch for any changes to system files and logs.
Metricbeat collects metrics from the system and services running on the server.

The configuration details of each machine may be found below.

| Name       | Function    | IP Address | Operating System |
|------------|-------------|------------|------------------|
| Jump Box   | Gateway     | 10.0.0.4   | Linux            |
| Web 1      | Web Server  | 10.0.0.5   | Linux            |
| Web 2      | Web Server  | 10.0.0.6   | Linux            |
| Web 3      | Web Sever   | 10.0.0.8   | Linux            |
| Elk Server | SIEM        | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
174.108.93.225

Machines within the network can only be accessed by SSH.
The Jump Box can access the ELK Server. 

A summary of the access policies in place can be found in the table below.

| Name       | Publically Accessible | Allowed IP Address     |
|------------|-----------------------|------------------------|
| Jump Box   | Yes                   | 174.108.93.225         |
| Web 1      | No                    | Allows SSH connections |
| Web 2      | No                    | Allows SSH connections |
| Web 3      | No                    | Allows SSH connections |
| Elk Server | Yes                   | 174.108.93.225         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
it is faster and more efficient to automate machine configuration. It ensures that multiple machines can be set up similarly.
Any changes that need to be made can be made to the configuration scripts and then deployed quickly and accurately. One file needs to
be maintained. This is an example of Infrastruture as Code (IaC).

The playbook implements the following tasks:
- Install docker
- Install python3-pip
- Set the default to pip and not pip3
- Increase the virtual memory so that the elk container runs proper
- Install the elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[docker ps](/Images/docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects information about logs and metricbeat collects information about system processes. For example, filebeat can collect info about sudo commands
  or new users. Metricbeat can collect info about CPU usage.
  
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration files to /etc/ansible/files/.
- Update the config files to include the IP address and port of the elk server running elasticsearch (10.1.0.4:9200) and kibana (10.1.0.4:5601)
- Run the playbook, and navigate to the public IP of the elk server using a web browser to check that the installation worked as expected.


- The playbook is filebeat-playbook.yml. Copy the playbook files to /etc/ansible/roles/.
- Update the hosts file to include the ip addresses of the machines you want to install 
  filebeat and metricbeat on under the [webservers]. 
- Update the hosts file to include the ip address of the machine you want to install the 
  ELK container on under [elk].
  
- Check the ELK server is running at http://public_ip:5601/app/kibana (20.110.194.84:5601/app/kibana)
