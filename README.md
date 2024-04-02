### **Instructions**

Remember that task where you deployed an open source app on GitHub using Apache?
you would be deploying same but this time around using ansible.

- Your ansible slave will consist of one ubuntu node and one centos(rhel) node.
- Your master node can be of any Linux distribution of your choice(3 nodes in all).
- Explore using variables in ansible while executing this task.
- You will push your playbooks to your GitHub account and submit a link to same


### **Solution**

1. I setup a multimachine environment on Vagrant by creating a vagrant file and
editing the vagrant file by adding the following lines of code to my vagrant file

(```
  config.vm.define "master" do |subconfig|
    subconfig.vm.box = "ubuntu/focal64"
    subconfig.vm.hostname = "master"
    subconfig.vm.network "private_network", ip: "192.168.50.10"
  end

  config.vm.define "client1" do |subconfig|
    subconfig.vm.box = "centos/7"
    subconfig.vm.hostname = "client1"
    subconfig.vm.network "private_network", ip: "192.168.50.11"
  end

  config.vm.define "client2" do |subconfig|
    subconfig.vm.box = "ubuntu/focal64"
    subconfig.vm.hostname = "client2"
    subconfig.vm.network "private_network", ip: "192.168.50.12"
  end

```)

2. I generated the ssh keys using ``ssh-keygen`` and copied them into the authorized keys
of my client nodes.

3. I added the ip addresses of my client nodes to the inventory file

4. I wrote the playbook to Deploy the website from Github with the following tasks

    - Install Git
    - Remove Files in the Github Repo Path on the client nodes
    - Update the Github Repo
    - Install Apache on both CentOS and Apache2 servers
    - Start Apache server if it isn't started

5. I pinged the clients nodes via ansible to ensure they were working
with the ansible adhoc command ``ansible webservers --key-file ~/.ssh/id_rsa  -m ping``

