## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Images/Network Topology.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

Ansible/filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound traffic to the network.
- Load balancers protect the availability of data by distributing data across multiple servers. Load balancers are useful in protecting against server downtime or attacks so that services can still continue. 
- Using a Jumpbox is advantageous because it can be used to access machines through a separate security zone.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.
- What does Filebeat watch for?
	- Filebeat watches for log files and collects data on events that have changes on those log files. 
- What does Metricbeat record?
	- Metricbeat monitors and collects metrics on your server and can easily ship out those metrics to a specified output. 

The configuration details of each machine may be found below.


| Name     | Function   | IP Address               | Operating System |
|----------|------------|--------------------------|------------------|
| Jump Box | Gateway    | 20.228.201.99 / 10.0.0.1 | Linux            |
| ELK      | ELK Server | 10.0.0.4                 | Linux            |
| Web-1    | VM         | 10.1.0.5                 | Linux            |
| Web-2    | VM         | 10.1.0.6                 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Jumpbox Private IP: 20.228.201.99

Machines within the network can only be accessed by SSHing into the Jumpbox Provisioner.
- Which machine did you allow to access your ELK VM? What was its IP address?
	- Jumpbox Provisioner (PUBLIC: 20.228.201.99/PRIVATE: 10.1.0.4)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.1 10.0.0.2    |
| ELK      | No                  | 10.0.0.4             |
| Web-1    | No                  | 10.1.0.5             |
| Web-2    | No                  | 10.1.0.6             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
	- Ansible allows you to automate configuration into multiple servers using a single playbook. 

The playbook implements the following tasks:
- Configure Elk VM with Docker
- Install docker.io
- Install python3-pip
- Increase virtual memory (on restart as well)
- Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.1.0.5)
- Web-2 (10.1.0.6)

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors and alerts us of any changes to our system. 
- Metricbeat detects changes in server metrics, such as memory and CPU usage and traffic.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible.
- Update the playbook file to include our virtual machines and their private IP addresses.
- Run the playbook, and navigate to the ELK VM to check that the installation worked as expected.

- Which file is the playbook? Where do you copy it?
	- filebeat-playbook.yml and metricbeat-playbook.yml, copied in /etc/ansible/files
- Which file do you update to make Ansible run the playbook on a specific machine? 
	- filebeat-config.yml and metricbeat-config.yml
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?
	- In each of the configuration files, you can edit the configuration under "setup.kibana" to go to your ELK VM IP address (10.0.0.4). 
- Which URL do you navigate to in order to check that the ELK server is running?
	- Your ELK server's public IP address:5601/app/kibana.


