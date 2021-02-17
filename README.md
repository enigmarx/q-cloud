## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Diagram/Cloud Setup.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ELK_deployment.yml file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting acess to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.

The configuration details of each machine may be found below.

| Name       | Function   | IP Address | Operating System |
|------------|------------|------------|------------------|
| Jump Box   | Gateway    |  10.0.0.4  | Linux            |
| Web-1      | Web Server |  10.0.0.5  | Linux            |
| Web-2      | Web Server |  10.0.0.6  | Linux            |
| ELK.Server | Elk Server |  10.1.0.5  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
  98.148.197.98

Machines within the network can only be accessed by the Jump Box at IP Address 10.0.0.4.


A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses |
|-------------|---------------------|----------------------|
| Jump Box    | Yes                 | 98.148.197.98        |
| Web-1       | No                  | 10.0.0.4             |
| Web-2       | No                  | 10.0.0.4             |
| Elk.Server  | Yes                 | 98.148.197.98        |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it ensures consistency of system builds and allows for virtually error-free scaling and duplication.

The playbook implements the following tasks:
- Installs Docker.io and Python3-PIP via apt command.
- Installs Docker via PIP.
- Installs DVWA docker container and enables Docker service.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


(Diagrams/docker_ps_output.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat allows us to monitor chosen log files and retrieve log events to forward to Elasticsearch or Logstash to be indexed. This can pool together Syslog hostnames and processes like Cron and systemd along with relevant event data.
- Metricbeat allows us to periodically collect operating system and active service metrics from the server. When looking at system metrics, this would provide total CPU and Memory usage, Inbound and Outbound traffic, as well as a breakdown by host or containers of usages. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat configuration file to /etc/ansible/files/filebeat-config.yml
- Update the file /etc/ansible/hosts to include the following:
[webservers]

10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3

[elk]

10.1.0.5 ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to [Elk server public IP]:5601/app/kibana to check that the installation worked as expected.