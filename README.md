# Cyber-Work
The files in this repository were used to configure the network depicted below.

![ELK](https://user-images.githubusercontent.com/90853797/133646496-0f77e213-6b15-4a68-9451-4716da831fe9.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

Playbook1: Pentest.yml

![Pentest](https://user-images.githubusercontent.com/90853797/133649083-5d48c6b9-b47a-4e24-ac20-3d6b1fae4498.PNG)

Playbook2: install-elk.yml

![Elkdocker](https://user-images.githubusercontent.com/90853797/133649673-f1b6918a-f05b-42f5-a421-f0bc18c37efc.PNG)

Playbook3: filebeat-playbook.yml

![filebeatsetup](https://user-images.githubusercontent.com/90853797/133649920-217689c6-fc3b-4868-8265-75e14b7547a1.PNG)

This document contains the following details:
Description of the Topology
Access Policies
ELK Configuration
Beats in Use
Machines Being Monitored
How to Use the Ansible Build
Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Load balancers protect application availability, allowing client requests to be shared across a number of servers
The advantage of a Jump Box is that it minimises the attack surface by ensuring remote connections to the cloud network come through a single VM. Additionally, remote connections to the Jump Box can be monitored easily to identify unusual remote connections.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configuration and system files.

Filebeat is used to monitor logs files
Metricbeat is used to collect operating system and service statistics from monitored VMs
The configuration details of each machine may be found below

| Name      | Function | IP Address | Operating System |
|-----------|----------|------------|------------------|
| JumpBox   | DVWA     | 10.1.0.4   | Linux            |
| Web1      | DVWA     | 10.0.0.5   | Linux            |
| Web2      | DVWA     | 10.0.0.6   | Linux            |
| ProjectVM | DVWA     | 10.0.0.4   | Linux            |

Access Policies
The machines on the internal network are not exposed to the public Internet.

Only the Jump Box machine can accept SSH connections from the Internet. Access to this machine is only allowed from the following IP addresses:
216.237.234.185

Machines within the network can only be accessed by the Jump Box.

The Jump Box can access the ELK VM Elk-1 using SSH. The Jump Box's IP address is 10.1.0.4
A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| JumpBox    | Yes SSH             | 216.237.234.185      |
| Web1       | Yes HTTP            | 216.237.234.185      |
| Web2       | Yes HTTP            | 216.237.234.185      |
| Project VM | Yes HTTP            | 216.237.234.185      |

Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because:

Build and deployment is performed automatically, consistently and quickly
Consistent, rapid configuration and depoloyment of virtual machines ensure all prescribed security meaures can be scripted to minimise attack surfaces while enabling horizontal and elastic scaling by deployment to more or fewer virtual machines in a cluster as required to meet capacity demand.
Facilitates OS and software updates

Playbook1: pentest.yml
pentest.yml is used to set up DMWA servers running in a Docker container on each of the web servies show in the diagram above. It implements the following tasks:

Installs Docker
Installs Python
Installs Docker's Python Module
Downloads and launches the DVWA Docker container
Enables the Docker service

Playbook2: install-elk.yml
install-elk.yml is used to set up and launch the ELK repository server in a Docker Container on the ELK server. It implements the following tasks:

Installs Docker
Installs Python
Installs Docker's Python Module
Increase virtual memory to support the ELK stack
Increase memory to support the ELK stack
Download and launch the Docker ELK container

Playbook3: filebeat-playbook.yml
filebeat-playbook.yml is used to deploy Filebeat on each of the web servers so they can be monitored centrally using ELK services running on Elk-1. It implements the following tasks:

Downloads and installs Filebeat
Enables and congigures the system module
Configures and launches Filebeat
The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.

![4](https://user-images.githubusercontent.com/90853797/133653218-41670182-e24c-4dd3-a583-9882c556be29.PNG)

Target Machines & Beats
This ELK server is configured to monitor the following machines:

Web-1: 10.0.0.5
Web-2: 10.0.0.6

We have installed the following Beats on these machines:

Filebeat

![9](https://user-images.githubusercontent.com/90853797/133655205-bc387917-fd0d-418d-ba1b-527faf572ed6.PNG)


Metricbeat

![12](https://user-images.githubusercontent.com/90853797/133655271-43f59d02-b63f-4415-9860-b06ac5ef4ddd.PNG)


These Beats allow us to collect the following information from each machine:

Filebeat collects and ships (sends to ELK for collation, persistence and reporting) logs from VMs running the Filebeat agent
Metricbeat collects and ships system metrics from the operating system and services of VMs running the Metricbeat

Using the Playbooks

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

Copy the playbook files to Ansible Docker Container.
Update the Ansible hosts file /etc/ansible/hosts to include the following:

[Webservers]
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3

[elkservers]
10.0.0.4 ansible_python_interpreter=/usr/bin/python3

Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

Bonus

1. Start an ssh session with the Jump Box ~$ ssh sysadmin@<Jump Box Public IP> (Mine is 40.118.162.169)

2. Start the Ansible Docker container ~$ sudo docker start <Ansible Container> (Mine is lucid_leakey)

3. Attach a shell to the Ansible Docker container with the command ~$ sudo docker attach <Ansible Container Name> (lucid_leakey)

4. Run the playbooks with the following commands:

ansible-playbook /etc/ansible/pentest.yml
ansible-playbook /etc/ansible/install-elk.yml
ansible-playbook /etc/ansible/roles/filebeat-playbook.yml

Playbook 2 - install_elk.yml configures only the server(s) listed as [elkservers] in /etc/ansible/hosts

Playbook 3 - filebeat-playbook.yml configures the servers listed as [webservers] in /etc/ansible/hosts

If there are no errors after running the playbooks, navigate to Kibana to check that the installation worked as expected by viewing Filebeat and Metricbeat data and reports in the Kibana Dashboard

Kibana can be accessed at http://<elk-server-ip>:5601/app/kibana (My IP ELK IP 52.255.136.216)
  
![6](https://user-images.githubusercontent.com/90853797/133655304-088c9bfc-9c25-4ce2-959f-ad626721b4c6.PNG)
