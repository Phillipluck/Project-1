## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/Phillipluck/Project-1/blob/main/Images/Elk%20Stack%20Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  (Images/elk_stack_playbook.png)
  (Images/filebeat_playbook.png)
  (Images/metricbeat_playbook.png)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load balancers distribute network traffic accross multiple servers to ensure that no single server is overworked by too much demand.
- The advantage of jump box servers is that they can be configured with a set of specific rules so that devices can can be accessed via secure methods, such as SSH.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.
- Filebeat is used to monitor the system logs, while Metricbeat is used to monitor and gather metrics on system resource usage.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web1    |Web Server          |10.0.0.6         | Linux             |
| Web2     |Web Server          |10.0.0.5            |Linux         |
| Web3     |Web Server          |10.0.0.7            |Linux    |
| ELK-Web1     |Elk Stack          |10.1.0.4            |Linux                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 67.188.142.150

Machines within the network can only be accessed by jump box.
- My Elk VM was only accessible through my jump box machine.
- IP Address: 13.64.215.250 (public) 10.0.0.4 (private)

A summary of the access policies in place can be found in the screenshots below.

(Images/VM_NSG.png)
(Images/Elk_Web_NSG.png)

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- You can fully automate the launch of a new server, deploy it on multiple machines very quickly, and reduces the chance of configuration errors.

The playbook implements the following tasks:
- Set memory usage to max
- Install Docker.io
- Install Python3-pip
- Install Docker
- Install Elk container and enable on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/Sudo docker ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.7
- 10.1.0.4

We have installed the following Beats on these machines:
- I installed Metricbeat and Filebeat on Web1, Web2, Web3, and Elk-Web-1.

These Beats allow us to collect the following information from each machine:
- Filebeat monitors system logs and forwards them to a central location for analysis, such as viewing recent logins or system startup/shutdown.
- Metricbeat collections information such as CPU usage. During our class activity I was able to stress test the CPU of one my web servers to see a massive spike in resource usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_playbook.yml file to /etc/ansible
- Update the hosts file to include include the elk webserver (see image below)...
(Images/Elk hosts image.png)
- Run the playbook, and navigate to http://[elk_server_ip]:5601/app/kibana to check that the installation worked as expected.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
