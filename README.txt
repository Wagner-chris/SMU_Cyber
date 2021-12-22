## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting high-traffic to the network.
- What aspect of security do load balancers protect? 
	- Load balancers work to prevent overloading servers with network traffic, ensuring Availability is protected. 

- What is the advantage of a jump box?
	- Jump-boxes provided an avenue to carry out back-end administrative tasks through a highly secured machine. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- What does Filebeat watch for?
	- It provides monitoring services for log files and communicates them to Elasticsearch/Logstash for analysis. 
- What does Metricbeat record?
	- It monitors system metrics and data which may be crucial to know if a network is under attack. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address              | Operating System |   |
|----------|----------|-------------------------|------------------|---|
| Jump Box | Gateway  | 10.0.0.4/20.118.202.215 | Linux            |   |
| Elk-VM   | Server   | 10.1.0.4                | Linux            |   |
| Web-1    | Server   | 10.0.0.5                | Linux            |   |
| Web-2    | Server   | 10.0.0.6                | Linux            |   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Whitelisted IP addresses: 70.119.65.188

Machines within the network can only be accessed by the Jump Box.
- Which machine did you allow to access your ELK VM? Jump Box

- What was its IP address? 10.0.0.4 (Private IP)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |   |   |
|----------|---------------------|----------------------|---|---|
| Jump Box | Yes/No              | 70.119.65.188        |   |   |
| Elk-VM   | No                  | 10.0.0.4             |   |   |
| Web-1    | No                  | 10.0.0.4             |   |   |
| Web-2    | No                  | 10.0.0.4             |   |   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage to automating configuration with Ansible is the use of YAML playbooks. These allow from the implmentation of multiple
  instructions to be fulfill with a single command and ensures that there will be uniformed deployment across all VMs. 

The playbook implements the following tasks:

Docker Installation 
- SSH into the Jump-Box-Provisioner (ssh *username@*Jump Box Public IP)
- Start/Attach to the ansible docker <sudo docker start *container ID*>/<sudo docker attach *container ID>
- Went to /etc/ansible/roles directory and created the ELK playbook <Elk_Playbook.yml>
- Run the Elk_Playbook.yml in that same directory <ansible-playbook Elk_Playbook.yml>
- Finally, SSH into the ELK-VM to verify the server is up and running.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 & 10.0.0.6 (Web Servers)

We have installed the following Beats on these machines:
- File Beat & Metric Beat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- Filebeat: Collects system log files from specified files located on remote devices. There are many different types of files that it can collect, including
	    Apache, Nginx web server and others. One of the items that displays is failed log-in attempts. This is helpful to know if your network is underattack from 
	    a bad-actor. 
- Metricbeat: Metric beat collects and displays the current and past metrics of your machines. This includes cpu usage, ram availibility, etc. It is a quick way to 
	      view the health of your monitored machines and also helpful to spot attacks such as DOS events. 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/roles/.
- Update the config file to include the ELK Server private IP in lines 1106 and 1806
- Run the playbook, and navigate to http://13.72.114.246:5601/app/kibana#/home to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- Which file is the playbook? filebeat-playbook.yml 
- Where do you copy it? /etc/ansible/roles
- Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible/hosts
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? Within the hosts file, 
	groups can be created that specific IP addresses are assigned to. When designing the ansible playbook, be sure to specify
	which group you would like the playbook to target. 
- Which URL do you navigate to in order to check that the ELK server is running? http://13.72.114.246:5601/app/kibana#/home

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._