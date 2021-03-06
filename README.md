## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(README/Images/diagram_network.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - /README/files
  - ansible.cfg
  - hosts
  - install-elk.yml
  - Filebeat-config.yml
  - Metricbeat Config.yml
  - Filebeat/Metricbeat Playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly protected, in addition to restricting traffic to the network.
-  The load balancer protects the server from overloading, and distributes traffic equally. If a sever goes down, the load balancer is able to redirect traffic to the other servers that are functioning. The advantage of a Jump Box is one point of entry, allowing for a more secure connection between over other VMs and preventing it to be accessible to the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat watches log files or locations specified, collects log events, and sends them to Elasticsearch or Logstash.
- Metricbeat records the metrics collected from Operating systems and services on servers and outputs them to Elasticsearch or Logstash

The configuration details of each machine may be found below.

| Name     |  Function  | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box |  Gateway    | 10.0.0.7  | Linux            |
| Web1     |   Server   |  10.0.0.6  | Linux            |
| Web2     |   Server   |  10.0.0.5  | Linux            |
| Web3     |   Server   |  10.0.0.8  | Linux            |
| ELK.VM   | Monitoring |  10.2.0.6  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the ELK VM machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 104.208.158.89:5601

Machines within the network can only be accessed by Jump Box Provisioner.
- Which machine did you allow to access your ELK VM? JumpBoxProvisioner
- What was its IP address? 10.0.0.7

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses    |
|----------|---------------------|-------------------------|
| Jump Box | Yes                 | 10.0.0.7 40.88.5.101    |
| Web1     | No                  | 10.0.0.6                |
| Web2     | No                  | 10.0.0.5                |
| Web3     | No                  | 10.0.0.8                |
| ELK.WM   | No                  | 10.2.0.6 104.208.158.89 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Anisble is an open source software that is powerful, yet has simple infrastructure

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install Docker module
- Increase virtual memory
- Use more memory with vm.max_map_count
- Download and launch a docker elk container
- Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
(README/Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| Name     | IP Addresses |
|----------|--------------|
| Web1     | 10.0.0.6     |
| Web2     | 10.0.0.5     |
| Web3     | 10.0.0.8     |

We have installed the following Beats on these machines:
- filebeat
- metricbeat

These Beats allow us to collect the following information from each machine:
- filebeat collects logs or logs at specific locations and forwards them to Elasticsearch or Logstash
- metricbeat collects metrics and statistics from the operating system or services on servers and outputs them to Elasticsearch or Logstash

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the playbook file to Ansible.
- Update the hosts file to include webservers and elk
- Run the playbook, and navigate to http://[your.ELKVM.IP]:5601/app/kibana to check that the installation worked as expected.

The specific commands the user will need to run to download the playbook, update the files, etc.
- cd /etc/ansible
- nano host
  - Navigate to the README folder into Files to see the hosts file
  - edit and add webservers and elk with IP addresses + add ansible_python_interpreter=/usr/bin/python3 at the end of each IP address
  - Ctrl + x to exit the file
- nano ansible.cfg
  - on line 107 edit ##remote_user = root to remote_user = azadmin
  - Ctrl + x to exit the file
- nano install-elk.yml /etc/ansible
  - Navigate to the README folder into Files to see the YAML file of install-elk.yml copy and paste into nano file
  - Ctrl + x to exit the file
- ansible-playbook install-elk.yml
