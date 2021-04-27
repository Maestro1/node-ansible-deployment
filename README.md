# node-ansible-deployment
Automation of node js app using express framework and pm2 on Amazon EC2 using ansible play book for orchestration. The playbook includes a role ansible-role-nvm found at https://github.com/morgangraphics/ansible-role-nvm.git . This is used in installation of nvm and npm.

The File Structure is as follows: -files folder ----nodeapp.conf -nodeapp folder ----app.js ----index.html ----package.json -roles -nodejs.yaml -requirements.yaml -test.yaml

The procedure for running is : 1.Install ansible on your local machine - sudo apt-get update && sudo apt install ansible -y 2.Spin up an EC2 instace on Amazon. 3.Download private key for your Amazon EC2 in a folder on your local machine 4.Open /etc/ansible/ansible.cfg using nano or your favorite editor and add the following lines

ansible.cfg

[defaults] private_key_file = #Location of your private key file ie /nodeapp/files/private-key.pem remote_user = ubuntu #Default for EC2 is ubuntu but you can change to the user you want

5.Open /etc/ansible/hosts and add the public dns to your amazon EC2 instance

hosts

[awServers] ec2-##-###-###-###.eu-west-2.compute.amazonaws.com

Clone this repository - git clone https://github.com/Maestro1/node-ansible-deployment.git

cd to the directory where you have cloned the repository.

Edit nodeapp.conf and replace the servername declaration with your ec2 public dns and proxy_pass variable ip address with private EC2 ip address from your aws account.

nodeapp.conf

servername ec2-##-###-###-###.eu-west-2.compute.amazonaws.com

proxy_pass http://Amazon-EC2-Private-IP:5000;

9.Install role ansible-role-nvm by running the command below.This role installs npm which is a package manager for node js using nvm.

username@hostname:$ ansible-galaxy install ansible-role-nvm

The nodejs.yaml is the main playbook file run using the command below username@hostname:$ ansible-playbook nodejs.yaml

10.Cross your fingers , drink some coffee and wait for the playbook to complete
