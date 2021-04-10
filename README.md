# ELK-Stacker-Project
This is the work that I submitted for my Cybersecurity Bootcamp project on ELK Stackers

The files in this repository were used to create the network depicted below.

![github-small](https://github.com/adiran180/ELK-Stacker-Project/blob/95d080d4a362518e912e43d691110ae64e0bf2ec/ELK-Stacker-Project/My%20Final%20ELK%20Diagram.png)

These files may be used to recreate the entire project pictured above. On the other hand, select pieces can be used to replicate only part of the project, like the Metricbeat section.

 - https://github.com/adiran180/ELK-Stacker-Project/tree/main/ELK-Stacker-Project/Ansible

This foldert holds the following:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Rundown of the Topology

The reason for creating this network was to expose an instance of DVWA that was being monitored as well as load-balanced.

Load balancing the network offers the benefits of ensuring a highly responsive application, keeping the network from being overloaded, and protecting against DoS and DDoS attacks.
The reason for having a JumpBox was to preven the machines in the network from being exposed to the public.

The ELK server takes care of monitoring the vulnerable VMs for any log and/or system traffic changes.
- Filebeat watches for log files, collects them, and forwards them to Elasticsearch or Logstash.
- Metricbeat records metric data from your system and services. i.e. CPU usage, memory, etc.

Each Machine's details are provided below


| Name               | Function | IP Address |
|--------------------|----------|------------|
|Jump-Box-Provisioner| Gateway  | 10.1.0.5   |
|        Web-1       |Web-server| 10.1.0.6   |
|        Web-2       |Web-server| 10.1.0.7   |
|        Web-3       |Web-server| 10.1.0.9   |
|      ELK-server    |ELK-stack | 10.0.0.5   |

All the machines are using Linux as the operating system (OS).

### Rules for Access

The machines inside the network cannot be accessed from any public network.

The JumpBox is the only machine capable of connecting to the internet, and the JumpBox can only be accessed from the following IP Addresses:
- Personal public IP address.

Using ssh is the only way of accessing the machines iside of the network.
- The ELK server only allows my Personal IP address to access the machine while using a specific port.

The table below can be used to summarize the things mentioned above.

| Name               | Allowed IP Addresses |
|--------------------|----------------------|
|Jump-Box-Provisioner|  Personal public IP  |
|        Web-1       |       10.1.0.6       |
|        Web-2       |       10.1.0.7       |
|        Web-3       |       10.1.0.9       |
|      ELK-server    |  Personal public IP  |

Note that none of the machines were accesible from the public for this project.

### Configuring the ELK

The reason why Ansible was employed is that it automates the configuration for the ELK machine. The main benefit of doing this is that:
- Ansible's automatic configuration is quick and simple to setup and use.

The following taks are taken care of by the playbook:
- Install Docker
- Install python3-pip
- Install Docker module pip
- Use systemctl to use more memory
- Download and launch Docker container sebp/elk:761

Running `docker ps -a` after the ELK instance was succesfully set up yielded the following:

![github-small](https://github.com/adiran180/ELK-Stacker-Project/blob/main/ELK-Stacker-Project/Images/Capture.PNG)

### Target Machines & Beats
The Following machines are the focus of ELK server set up in this project:
- Web-1, 10.1.0.6
- Web-2, 10.1.0.7
- Web-3, 10.1.0.9

The Beats used for the poject were:
- Filebeats
- Metricbeats

Each Beat has its own purpose inside of the machines:
- Filebeat focuses on tracking system events by gathering system logs.
- Metricbeat focuses on monotoring the usage of resources by collecting system and service metric data.

### Playbook Usage
Note that an Ansible control node is required for using the playbook. For the sake of simplicity, that step will be skipped:

SSH into the control node and follow the steps below:
- Copy the filebeat and metricbeat config files to /etc/ansible/[your_dir]/[your-file-name].
- Update the config files to include your ELK-server's private IP address. (filebeat-config.yml: lines 1106 & 1806, metricbeat-config.yml: lines 62 & 96)
- Run the playbook, and navigate to http://[ELK-server-public-IP]:[your port]/app/kibana to check that the installation worked as expected.


- /etc/ansible/roles/filebeat-playbook.yml is the filebeat playbook. Copy it to /etc/ansible/[your_dir]/[your-playbook-name]
- /etc/ansible/files/metricbeat-playbook.yml is the metricbeat playbook. Copy it to /etc/ansible/[your_dir]/[your-playbook-name]
- To make Ansible run the playbook on a specific machine(s), update the /etc/ansible/hosts file. Within this file, name groups using square brackets (currently contains '[webservers]' and '[elk]') surrounding the group-name and under the group-name, replace private IP's with your own respective IP's. You then use these group-names behind the "hosts:" field in the playbooks to specify which machines to apply the playbook to.
- To confirm the ELK-server is running go to http://[ELK-server-public-IP:[your port]/app/kibana
