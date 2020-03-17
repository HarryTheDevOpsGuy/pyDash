# Ansible configuration explaination.

Hi! Team,
I'm Harry. Here I have tried to explain of the current Ansible configuration in this repository that has been already shared with you.  
 
 As per your requirements and as i have understood and i have created and configured this -  `nginx` `pydash` `supervisor` etc.
 
Following are the ansible configurations file to create the environment. Usages of file & what these file do has been explained below.  

## Project directory/configuration structure
We  have created different directories for specific task. let me explain more on this.
 1. **ansible.cfg** :  This is global ansible configuration file. Where we can change or modify system related configuration.
 like :  `log_path = /tmp/ansible_pydash.log`  `private_key_file = /home/hari/.ssh/id_rsa` . 
 2.  **inventory/hosts** :  This is `hosts` file configuration we define remote hosts details. 
Like :  `host ip`  `remote user`  `remote port`

 4.  **pyDash.yml** : This is the main ansible playbook where we define roles which will be executed on remote hosts. 
 like : `Hari.PyDash` 
 
 5. **group_vars/all** : This is the common variable file. which variable use in multiple ansible roles.  
 6. **roles/Hari.PyDash** :  This is the common ansible template which we can use to create multiple similar playbooks. where basic structures are same  and changes are as following.
Like : `domain name`  `port number` `username` `log directory`
 
	
This is the role directory structure which contains `defaults` `templates` `tasks` `handlers` ansible roles. which is predefined name and directory structure.	
 - [ ] **defaults** : This variable has been defined for specific roles. this different from common variables.
 - [ ]  **templates** : This is the `jinja2` template directory. `jinja2` template is  a template which converts static configuration into dynamic configurations.
 - [ ]  **tasks** : This is the main directory where we keep main yaml playbooks for `installing configurations`, `copying files`, `copying templates`.
 - [ ] **handlers** :  This directory contains multiple yaml files which is use for `start` `enable` `restart` `stop` services at the end of execution of main playbooks or after installing the services these files executes at the end.

