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

Playbook4: install-metricbeat.yml

![Metricbeat](https://user-images.githubusercontent.com/90853797/133650162-9f031d2c-1178-4bf4-91fd-367bee165676.PNG)

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

