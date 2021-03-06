#### WELCOME To PyDash

#### Step 1 : Clone repostiory and setup.

```bash
git clone <repo_url>
cd <project_dir>
export ANSIBLE_CONFIG=<project_dir>/ansible.cfg

```

#### Step 2 : Update ansible.cfg file.
We need to update required configs [`remote_user`, `private_key_file` ] according to our server details.

```bash
#cat ansible.cfg
[defaults]
inventory = inventory/hosts
#roles_path = roles
remote_user = harry
become_user = root
become_method = sudo
log_path = /tmp/ansible_pydash.log
private_key_file = /home/hari/.ssh/id_rsa
roles_path    = roles
deprecation_warnings=False

# Merge hashes together
hash_behaviour = merge
```


#### Step 3 : Update hosts file
update inventory details in `inventory/hosts` file according to our remote server.

```bash
#cat inventory/hosts
[web]
192.168.43.148 ansible_user=harry ansible_port=22
```

#### Step 4 : Now test ssh connection.
```bash
cd <project_dir>
export ANSIBLE_CONFIG=ansible.cfg
ansible-playbook test.yml
ansible-playbook pyDash.yml
```

if you get below output after executing `ansible-playbook test.yml`. it means we are able to ping or authenticate remote server.

```
hari@DELL:~/Documents/workspace/ansible$ ansible-playbook test.yml

PLAY [web] *******************************************************************************************************************************************

TASK [ping all hosts] ********************************************************************************************************************************
ok: [192.168.43.148]

PLAY RECAP *******************************************************************************************************************************************
192.168.43.148             : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#### Setup application
its time to execute `ansible-playbook pyDash.yml` successfully and we will get below output.

```bash
# ansible-playbook pyDash.yml

## output
PLAY [Install PyDash - with Nginx Gunicorn and supervisor] *******************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************
ok: [192.168.43.148]

TASK [Hari.PyDash : Installing dependant packages] ***************************************************************************************************
ok: [192.168.43.148] => (item=[u'software-properties-common', u'unzip', u'nginx', u'python-pip', u'python-dev', u'python3-dev', u'build-essential', u'libpq-dev', u'virtualenv', u'virtualenvwrapper', u'supervisor', u'git'])

TASK [Hari.PyDash : Downloading PyDash] **************************************************************************************************************
ok: [192.168.43.148]

TASK [Hari.PyDash : Create Custom 404 error page] ****************************************************************************************************
changed: [192.168.43.148]

TASK [Hari.PyDash : Configure gunicorn_start script] *************************************************************************************************
changed: [192.168.43.148]

TASK [Hari.PyDash : Configure nginx configs] *********************************************************************************************************
changed: [192.168.43.148]

TASK [Hari.PyDash : remove sites-enabled/default] ****************************************************************************************************
ok: [192.168.43.148]

TASK [Hari.PyDash : Configure Nginx site configs for PyDash as enabled] ******************************************************************************
changed: [192.168.43.148]

TASK [Hari.PyDash : Configure gunicorn configs for pydash] *******************************************************************************************
ok: [192.168.43.148]

TASK [Hari.PyDash : Create virtualenv for pydash.] ***************************************************************************************************
ok: [192.168.43.148]

TASK [Hari.PyDash : Install Gunicorn for pydash.] ****************************************************************************************************
ok: [192.168.43.148] => (item=[u'gunicorn'])

TASK [Hari.PyDash : Setting Directory Permission for pydash.] ****************************************************************************************
changed: [192.168.43.148]

TASK [Hari.PyDash : Run below command to Create super users.] ****************************************************************************************
ok: [192.168.43.148] => {
    "msg": "source /var/www/html/PyDash/venv/bin/activate && /var/www/html/PyDash/venv/bin/python /var/www/html/PyDash/pydash/manage.py syncdb"
}

TASK [Hari.PyDash : Initializing Python App - pydash] ************************************************************************************************
changed: [192.168.43.148]

RUNNING HANDLER [Hari.PyDash : restart nginx] ********************************************************************************************************
changed: [192.168.43.148]

RUNNING HANDLER [Hari.PyDash : restart supervisor] ***************************************************************************************************
changed: [192.168.43.148]

PLAY RECAP *******************************************************************************************************************************************
192.168.43.148             : ok=16   changed=8    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```


##### Test application
We need to make entry in `/etc/hosts` to test application on local server.
```bash
192.168.43.148  harrythedevopsguy.in www.harrythedevopsguy.in
```

now open http://harrythedevopsguy.in or http://www.harrythedevopsguy.in in your browser.

`http://harrythedevopsguy.in` >>  `http://www.harrythedevopsguy.in/static/400.html ` </br>
`http://www.harrythedevopsguy.in`  >> `http://www.harrythedevopsguy.in/login/?next=/` </br>

**login details** </br>
    - URL : http://www.harrythedevopsguy.in/login/?next=/ </br>
    - user : admin </br>
    - Pass: 123456 </br>


---
Thanks</br>
Harry </br>
Stay touch with us : https://harrythedevopsguy.github.io
