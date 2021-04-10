# ELK-Stacker-Project
The work I submitted for my Cybersecurity Bootcamp project on ELK Stackers

The files in this repository were used to configure the network depicted below.

![github-small](https://github.com/adiran180/ELK-Stacker-Project/blob/95d080d4a362518e912e43d691110ae64e0bf2ec/ELK-Stacker-Project/My%20Final%20ELK%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

 - https://github.com/Chad-Frickey/KU-Cybersecurity-Bootcamp/tree/master/Ansible

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting overload to the network.
Load balancing protects against DoS or DDoS attacks. Having a Jump Box prevents all machines in the network from being exposed to the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat watches for log files, collects them, and forwards them to Elasticsearch or Logstash.
- Metricbeat records metric data from your system and services. i.e. CPU usage, memory, etc.

The configuration details of each machine may be found below.


| Name               | Function | IP Address | Operating System |
|--------------------|----------|------------|------------------|
|Jump-Box-Provisioner| Gateway  | 10.1.0.5   | Linux            |
|        Web-1       |Web-server| 10.1.0.6   | Linux            |
|        Web-2       |Web-server| 10.1.0.7   | Linux            |
|        Web-3       |Web-server| 10.1.0.9   | Linux            |
|      ELK-server    |ELK-stack | 10.0.0.5   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal public IP address.

Machines within the network can only be accessed by ssh.
- My personal public IP address is the only machine allowed access to the ELK-server via port 5601.

A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible | Allowed IP Addresses |
|--------------------|---------------------|----------------------|
|Jump-Box-Provisioner|         No          |  Personal public IP  |
|        Web-1       |         No          |       10.1.0.6       |
|        Web-2       |         No          |       10.1.0.7       |
|        Web-3       |         No          |       10.1.0.9       |
|      ELK-server    |         No          |  Personal public IP  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible is quick and simple to setup and use.

The playbook implements the following tasks:
- Install Docker
- Install python3-pip
- Install Docker module pip
- Use systemctl to use more memory
- Download and launch Docker container sebp/elk:761

The following screenshot displays the result of running `docker ps -a` after successfully configuring the ELK instance.

![github-small](https://github.com/adiran180/ELK-Stacker-Project/blob/main/ELK-Stacker-Project/Images/Capture.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1, 10.1.0.6
- Web-2, 10.1.0.7
- Web-3, 10.1.0.9

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeat collects system logs, which can be used to track system events, etc.
- Metricbeat collects system and service metric data, which we can use to see CPU usage, etc.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat and metricbeat config files to /etc/ansible/[your_dir]/[your-file-name].
- Update the config files to include your ELK-server's private IP address. (filebeat-config.yml: lines 1106 & 1806, metricbeat-config.yml: lines 62 & 96)
- Run the playbook, and navigate to http://[ELK-server-public-IP]:5601/app/kibana to check that the installation worked as expected.


- /etc/ansible/roles/filebeat-playbook.yml is the filebeat playbook. Copy it to /etc/ansible/[your_dir]/[your-playbook-name]
- /etc/ansible/files/metricbeat-playbook.yml is the metricbeat playbook. Copy it to /etc/ansible/[your_dir]/[your-playbook-name]
- To make Ansible run the playbook on a specific machine(s), update the /etc/ansible/hosts file. Within this file, name groups using square brackets (currently contains '[webservers]' and '[elk]') surrounding the group-name and under the group-name, replace private IP's with your own respective IP's. You then use these group-names behind the "hosts:" field in the playbooks to specify which machines to apply the playbook to.
- To confirm the ELK-server is running go to http://[ELK-server-public-IP:5601]/app/kibana
