## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Alt text](https://github.com/edwink93/Edwin-Project/blob/main/Diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

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

Load balancing ensures that the application will be highly efficient, in addition to restricting incoming traffic to the network.
Load balancers can protect the network by restriciting incoming traffic and preventing SQL injection. The Jump Box can prevent those attacks by reinforcing the security to block them.    

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat watches for both log files and locations. 
- Metricbeat records statistical data from the operating system; moreover, it collects metrics and runs services from the CPU to memory. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.10.0.150| Linux ec2        |
| DVWA     | Webserver| 10.10.2.54 | Ubuntu           |
| DVWA2    | Webserver| 10.10.2.80 | Ubuntu           |
| ELK      | Logger   | 10.10.2.17 | Ubuntu           |
| RDP      | Viewer   | 10.10.0.80 | Windows          |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box and RDP machines can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
DVWA - Webserver - 10.10.2.54
DVWA - Webserver - 10.10.2.80 

Machines within the network can only be accessed by SSH connection through Linux EC2 and RDP. 
- ELK VM can be only accessed through the Jump box which IP address is 10.10.0.150.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | NO                  | 10.0.0.1 10.0.0.2    |
| DVWA     | NO                  | 10.10.2.54           |
| DVWA 2   | NO                  | 10.10.2.80           |
| ELK      | NO                  | 10.10.2.17           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- It is easier to install easily by having automated configuration. Plus, automate configuration will be deployed efficiently without having troubleshooting issues. Lastly, it   saves time than maunally configured. 

The playbook implements the following tasks:
- Install install-elk.yml
- Copy to Jump Box using the following command
  - scp -i "Ohio_Key.pem" install-elk.yml ec2-user@ec2-18-189-170-152.us-east-2.compute.amazonaws.com:/home/ec2-user
- Check status of Docker before using command 
  - sudo service docker status -> To check the status either active or inactive 
  - sudo service docker start -> To start docker: "sudo docker pull cyberxsecurity/ansible bash"
- Open new window for SSH into Jump Box. This task will copy keys and install-elk.yml. 
  1. sudo docker ps -> It shows the container id. 
  2. sudo docker cp install-elk.yml <container id>:/root  
  3. sudo docker cp Ohio_key.pem <container id>:/root 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- DVWA 10.10.2.54 
- DVWA 10.10.2.80

We have installed the following Beats on these machines:
From these steps, I succesfully downloaded Kibana and Filebeat. 

These Beats allow us to collect the following information from each machine:
- Filebeat collects the changes done 
- Metricbeat collects metrics and statistics. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible.yml to ansible:/root.
- Update the filebeat.yml to include the IP address of ELK Server
- Run the playbook, and navigate to RDP Machine which includes Kibana to check that the installation worked as expected. 

The file is located in /etc/ansible/file/filebeat-configuration.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- eidt the /etc/ansible/host file to add webserver and elkserver IP addresses. 
- We need to use http://10.10.2.31:5601/ for navigating into the system to check that filebeat is working properly. 

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

