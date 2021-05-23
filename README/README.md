![ELK Server Project](https://user-images.githubusercontent.com/78285552/119273521-5303fe00-bbd9-11eb-94fd-8b0bcd97625d.png)
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

ELK Server Project.jpg

Alternate Links to Diagrams:
https://app.diagrams.net/#G1InCspHDEMkhWHANEQzS0teS4l0A8c0Ua
or
https://drive.google.com/file/d/1hWXJbItFTumNoRE0xbjXRvuVNBr5dZX2/view?usp=sharing


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible and Docker file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml
  - metricbeat-playbook.yml
  - metricbeat-config.txt
  - filebeat-config.txt
  - filebeat-playbook.ymlinstall-elk.yml
  

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avaialable, in addition to restricting unwanted access and attacks to the network.
In a security aspect, Load Balancers are effective by redirecting traffic from a compromised server to a secondary servers in the event of a DDoS attck or similar compromise. To help avoid unwanted traffic to the backend we also employeed a Jump Box VM. The jumpbox restricts access to a single node thru the use of SSH-RSA public key authentication. 

  
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the resources and system logs.
- Filebeat is used to monitor the Syslog of the host along with any activity involving SSH logins, Users and groups, and sudo commands.
- Metricbeat monitors resources and metrics of the vulnerable VM's and associated website.

The configuration details of each machine may be found below.

| Name       | Function    | IP Address              | Operating System |
|------------|-------------|-------------------------|------------------|
| Jump Box   | Gateway     | 10.0.0.4, 104.211.5.95  | Linux - Ubuntu   |
| Red Web 1  | Web Server  | 10.0.0.5                | Linux - Ubuntu   |
| Red Web 2  | Web Server  | 10.0.0.6                | Linux - Ubuntu   |
| ELK Server | ELK Server  | 10.1.0.4, 52.175.253.49 | Linux - Ubuntu   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Whitelist: 45.31.134.87


Machines within the network can only be accessed by the Red Team Jump Box
- Whitelist: Public IP 104.211.5.95 and  Private IP 10.0.0.4
- Elk Machine is only Accessible from the Jump Box via 10.0.0.4

					      

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | Yes                 | 45.31.134.87         |
| ELK Server | No                  | 10.0.0.4             |
| Red Web 1  | No                  | 10.0.0.4             |
| Red Web 2  | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows rapid deployment accross multiple machines with a set group of parameters. Once set up correctly, this eliminates any key stroke errors.

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install docker via pip
- Increase vitual memory
- Use more memory
- Download and launch a docker elk container - starts docker and establishes the ports being used

The following screenshots display the result of running `docker ps` after successfully configuring the ELK instance.

ELK Instance.png
ELK Instance 2.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| Name       | IP Address |
|------------|------------|
| Red Web 1  | 10.0.0.5   |
| Red Web 2  | 10.0.0.6   |

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat
| Name       | IP Address              |
|------------|-------------------------|
| Red Web 1  | 10.0.0.5                |
| Red Web 2  | 10.0.0.6                |
| ELK Server | 10.1.0.4, 52.175.253.49 |

These Beats allow us to collect the following information from each machine:
- Filebeats collects syslogs and forwards it to the Elasticsearch thru Logstash which we can view using Kibana for items like SSH Login Attemps ECS. While Metricbeats reports the resources being used by the hosts such as CPU and Meory usage. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to /etc/ansible/files/ directory.
- Update the hosts file to include webserver and ELK IP addresses
- Run the playbook, and navigate to Kibana @ ( http://[your.VM.IP]:5601/app/kibana ) to check that the installation worked as expected.

