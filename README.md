## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](/Resources/Images/ELK_Stack_Network_Diagram.png?raw=true)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Elk_Stack_Setup.yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting downtime of the network.
- The distribution of traffic helps prevent possible distributed denial-of-service (DDoS) attacks. Using a Jump Box allows for a unified space to distribute necessary software to the network, while maintaining a single point of access for security purposes.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.

The configuration details of each machine may be found below.

| Name     | Function            | IP Address | Operating System |
|----------|---------------------|------------|------------------|
| Jump Box | Gateway             | 10.0.0.5   | Linux            |
| ELK VM   | Host ELK Stack      | 10.0.0.6   | Linux            |
| DVWA-VM1 | Host DVWA Container | 10.0.0.8   | Linux            |
| DVWA-VM2 | Host DVWA Container | 10.0.0.9   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 76.176.158.223

Machines within the network can only be accessed by the Jump Box (10.0.0.5).

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 76.176.158.223       |
| ELK VM   | No                  | 76.176.158.223       |
| DVWA-VM1 | No                  | 10.0.0.5             |
| DVWA-VM2 | No                  | 10.0.0.5             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it provides an autonomous delivery which removes any discrepencies caused by human error aswell as saves time which can be used to perform other tasks.

The playbook implements the following tasks:
- Configure DVWA virtual machines with Docker, Pip, Python Module and the DVWA web container.
- Configures ELK Server with Docker, Pip, Python and the ELK container with Kibana.
- Installs and configures Filebeat to run within Kibana.
- Installs and configures Metricbeat to run within Kibana. 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK Command](/Resources/Images/ELK_PS_CMD.png?raw=true)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| DVWA-VM1 | 10.0.0.8 |
| DVWA-VM2 | 10.0.0.9 |

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects and parses logs created by the system logging service in order to easily monitor the server(s).
- Metricbeat collects metrics from your systems and services, which we can use to make sure system functions are performing as expected and not utilizing too many resources.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ELK_Stack_Setup.yml file to "/etc/ansible/".
- Copy the Metricbeat_Configuration.yml file to "/etc/ansible/".
  - Change "10.0.0.6" on line 46 & 70 to the internal IP of your ELK server.
- Copy the Filebeat_Configuration.yml file to "/etc/ansible/".
  - Change "10.0.0.6" on line 1105 & 1804 to the internal IP of your ELK server.
- Update the "/etc/ansible/hosts" file to include the internal IPs of your "Webservers" and your "Elkserver".
- Run the playbook, and navigate to "PublicIPofELKServer:5601" to check that the installation worked as expected.

### Commands To Initialize Software
- ssh username@JumpboxIP
- sudo docker container start containername
- sudo docker container attach containername
  - ssh username@DVWA-VM1
    - exit
  - ssh username@DVWA-VM2
    - exit
  - ssh username@ELKServer
    -exit
  - cd /etc/ansible
  - ansible-playbook ELK_Stack_Setup.yml

After completing all of these commands aswell as the instructions from "Using the Playbook" you should have a fully functional ELK Stack.