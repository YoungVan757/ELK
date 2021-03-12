# ELK
ELK project using a jump box provisioner to host vm servers with docker and ansible
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the "/etc/ansible/install-elk.yml" file may be used to install only certain pieces of it, such as Filebeat.

  - /etc/ansible/install-elk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting access to the network.
- The web application firewall in load balancers provide security for web apps. The advantage of a jump box is single system that is required to update when a new patch is released.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the filesystem and system metrics such as CPU usage, logins, sudo escalation attempts and more.
- Filebeat searches for log data in specified configured services. 
- Metricbeat records logged events from various services.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name    | Function | IP Address     | Operating System |
|---------|----------|----------------|------------------|
| Jumpbox | Gateway  | 13.72.68.56    | Linux            |
| Web1    | Server   | 52.136.123.254 | Linux            |
| Web2    | Server   | 52.136.123.254 | Linux            |
| Web3    | Server   | 52.136.123.254 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 24.253.137.211

Machines within the network can only be accessed by Jump Box.
- Jump Box machine accessed by my public IP address.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 24.253.137.211       |
| Web-1    |            No       |      52.136.123.254        |
| Web-2    |           No        |      52.136.123.254                 |
| Web-3    |           No        |      52.136.123.254 
| Elk      |           No        |      52.136.123.254 
| Load Balancer          Yes     |      24.253.137.211 
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because using the configuration can be repeated automatically as new machines are added

The playbook implements the following tasks:
- First task installs docker.io
- Python3-pip is installed
- Docker python module is installed
- Virtual machine memory is increased
- Docker elk container is pulled and enable with final task

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.2.0.6
- Web-2 10.2.0.7
- Web-3 10.2.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat is a logging agent that collects log files and ship the data to to either Logstash for more advanced processing or directly into Elasticsearch for indexing. Filebeat will be expected to record the last successful line indexed in the registry so in the event of network issues, Filebeat can locate where it left off when re-establishing a connection. 
- Metricbeat is installed on the servers in the environment to monitor their performances by collecting and shipping various server metrics to a specified destination. You can expect to see Metricbeat to monitor and analyze system CPU, memory and load.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the "elk-install.yml" file to the /etc/ansible folder.
- Update the Anisble "hosts" file to include the new virtual machines' IP addresses.
- Run the playbook, and navigate to http://52.251.50.154:5601/app/kibana to check that the installation worked as expected.
