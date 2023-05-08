What is configuration management ?
- Configuration management is a process for maintaining computer systems, servers, and software in a desired, consistent state.
 It’s a way to make sure that a system performs as it’s expected to as changes are made over time. 

 Tools to mmange configuration management -
- Puppet - It uses pull mechanism by using agent as master salve and to use puppet we should learn puppet language
- Ansible - It uses push mechanism it is agent less and it simple to learn becaue we just need to have proper understanding of YAML and ansible uses python programming langauge


Ansible requires password less authentication If ansible can authenticate wihtout any password to any machine after that ansible can configure anything on the server

how ansible communicate to ec2 instances (target server) without password( How to create password less authentication).
- There will be 2 server one is your machine ( ansible server) and other is machine where you want to logged in (Target server)
- first from ansible server you have to generate the key, for that go to terminal and type <ssh-keygen> it will create a public and private key 
- copy the public key by using <cat location-of-file>
- Now go to your target server and again generate key <ssh-keygen>
- after that <ls ~/.ssh/ > you will see three files from there open the authorize key by <vim ~/.ssh/authorized_keys> and paste the public key that you have copied from the ansible server 
- Now go to your ansible server and run <ssh private_IP_address> and you will be logged in without any password authetication

=> summary - you have to copy the public ip address of ansible server and paste it to the authorized keys of the target server.

what is ansible adhoc commands - 
- They are single commands you can run with Ansible, making use of Ansible modules without the need to create or save playbooks. They are very useful for performing
  quick, one-off tasks on a number of remote machines or for testing and understanding the behavior of the Ansible modules

What is ansible playbooks -
- Ordered lists of tasks,(To run multiple commands ) saved so you can run those tasks in that order repeatedly.
- Playbooks can include variables as well as tasks.
- Playbooks are written in YAML and are easy to read, write, share and understand.

Inventory file - In ansible everything is configured in inventory file (all the server name and server details)grouping is done in inventory file 
               - To interact with n numbers of target server we will create Inventory file in this file we store all the private IP address of target servers
               - for example - there are two target server then we will specify each server by square bracker [ ] inside this we will write the name of the server.
               -  [dbsever]
                  17.45.5.4

Adhoc commands
- to list all the files of the target server <ansible -i inventory all -m "shell" -a "ls"> 

playbook commands
- to execute ansible playbook <ansible-playbook -i inventory first-playbook.yml>

whenever you want to write a complex playbooks then you will use ansible galaxy commands to create roles with help of ansible galaxy you can write structured and efficent playbooks
 
Ansible galaxy commands ( Roles are basically created for kubernetes)
- first create a separate folder
- and then execute this command - <ansible-galaxy role init kubernetes>
- and you get output as - Role kubernetes was created successfully