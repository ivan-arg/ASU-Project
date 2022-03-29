# ASU-Project
ASU Cybersecurity Bootcamp Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](https://github.com/ivan-arg/ASU-Project/blob/main/Diagrams/Cloud_Infrastructure.draw.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Elk_packages.yml file may be used to install only certain pieces of it, such as Filebeat.

  [Elk Playbook](https://github.com/ivan-arg/ASU-Project/blob/main/Ansible/Elk_packages.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unauthorized users to the network.
_A load balancer can help protect a network from DDoS attacks as it is placed in front of the firewall. Using a jump box prevents having virtual machines exposed to the public by allowing an authorized host connection to it via the SSH protocol_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat helps us to collect logs files to forward them. 
- Metricbeat records metrics from system and services running.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump-Box | Gateway    | 10.1.0.4   | Linux            |
| Web-1    | Web Server | 10.1.0.5   | Linux            |
| Web-2    | Web Server | 10.1.0.6   | Linux            |
| Elk-VM   | Kibana     | 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Host IP

Machines within the network can only be accessed by the Jump-Box.
- Host machine IP, was allowed access to the Elk-VM. 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | Host IP              |
| Web-1    | No                  | 10.1.0.1-254         |
| Web-2    | No                  | 10.1.0.1-254         |
| Elk-Vm   | No                  | 10.1.0.1-254         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
- Ansible allows easy agentless deployment of automated tasks by adding them as needed to an easy to read playbook written in YAML.

The playbook implements the following tasks:
- Installing latestes version of docker.io
- Installing pip3 and python 
- Increased virtual memory
- Specify specific ports to be used
- Launch Docker containers with an image 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ElkDockerPs](https://github.com/ivan-arg/ASU-Project/blob/main/Images/Elk_docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.1.0.5
- Web-2 10.1.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects log events from our VM's to be forward to Elasticsearch or Logstash for indexing.
- Metricbeat collects metric from our system, such as CPU to memory. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [Filebeat Playbook file](https://github.com/ivan-arg/ASU-Project/blob/main/Ansible/Filebeat_playbook.yml) and [Metricbeat Playbook file](https://github.com/ivan-arg/ASU-Project/blob/main/Ansible/Metricbeat_playbook.yml) to /etc/ansible
- To make ansible run the playbook on a specific machine, the /etc/ansible/hosts file must be edited with targeted machines IP address under the desired groups (webservers or ELK).
- To verify ELK server is running navigate to Kibana via http://ELK-VM public ip:5601/app/kibana
