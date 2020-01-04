# Ansible
This is good for provisioning and automation, it will improve scalability, consistency and reliability in the IT environment

You need to configure the vagrantfile to make sure it reads that it is going to get its provisioning from Ansible rather than the provision script.

How to install ansible on the Ubuntu virtual machine:

````
sudo apt-get install software-properties-common
````

- This initial command provides the virtual machine OS with the location of the key required to download the dependencies and libraries for the software in question
  which in this instance is Ansible, so sudo runs the command as an admin, while apt-add-repository adds the following repo to the list of places that the system goes to look for software.
````
sudo add-apt-repository ppa:ansible/ansible
````

- (apt-get update updates the list of available packages and their versions, but it does not install or upgrade any package)
````
sudo apt-get update
````

-  install is an extra command that tells the computer that you want to install software with the package name as follows.
````
sudo apt install ansible
````

## Check ansible files

from ubuntu you want to cd into /etc/Ansible

check to see if there is something along the lines of vars or roles
if not:
````
sudo mkdir -p /usr/local/etc/ansible/group_vars
````

also check to see if there is a hosts file
if not:
````
sudo touch /usr/local/etc/ansible/hosts
````
Hosts file should contain your ansible inventory, group_vars should contain the ansible playbook variables.

## Configuring file for ansible
etc/ansible/ansible.config

use the command sudo vim to get into this file

Unhash inventory and sudo_user using 'I' to turn on the insert mode within the file.

to save ctrl C, then :x

## How to run the database
1. 1. if you have not then you need to install ansible on ubuntu using the steps above

2. check to see that ansible has been installed with:
````
ansible -version
````

3. Go to environment in your VM and then run the playbook using:
````
ansible-playbook <example_playbook.yml>
````

4. check to see the database is running by executing the command:
````
mongod --version
````

5. An extra step to perform as a sanity check to ensure everything is running, is by navigating to the 'tests' folder
and running 'rake spec'. It important to mention here that this is performed outside the VM and rather on the local host machine
git bash.

# Task

The tasks were to specify the version of the mongodb and configure the mongod.conf file so that we replace the default ips
with the new bindip that we wanted to specify, and doing so thorough 3 main steps.

1. specify the synced folder on the host machine that holds the file we want to replace it with and syncs that with the virtual machine path.
2. removes the default mongod.conf file so we can replace it
3. syncing the first location WITHIN the vm with second location WITHIN the vm so the configurations can take effect.


In order to find the database network details we used cat/etc/mongod.conf and copied those to the one on our host machine
which we wanted the virtual machine to synced with and move to another folder within the vm for it to take effect. but first
on the host machine location we changed the bind ip so that the bindip was auto changed in the vm spin up.

Note: Don't do bind_ip = 0.0.0.0 in production!! Or you will publicly expose your server.
