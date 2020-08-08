
## LINODE: Deploying a Flask Application using Ansible


### Description
<p>
  Using ansible to deply a flask application on Linode. The original tutorial is located <a href="https://www.linode.com/docs/development/python/flask-and-gunicorn-on-ubuntu/" target="_blank">here</a>
</p>

## Steps

#### 1. Create a Nanode on Linode using UBUNTU 20.04 LTS.
<p>
  Login on Linode and create a <a href="https://cloud.linode.com/linodes/create" target="_blank">Nanode (or Linode)</a>
</p>

#### 2. On your host (laptop/computer) install Ansible
```shell 
pip install ansible
```
#### 3. git clone this repo
```shell 
git clone git@github.com:guinslym/linode_tutorial_deploying_a_flask_application_with_ansible.git
```
#### 4. Edit the Inventory file
<p>
 Add your Nanode IP address in the `inventory` file to replace all **???** and add your Nanode **password** into this file. For security reasons it's better to use ansible-vault for password. But for this tutorial we can use leave it blank. **For production servers*** please use ansible-vault.
</p>
```shell 
[all:vars]
ansible_python_interpreter= /usr/bin/python3

## my box VMs ##
[flaskbox_dev]
???.??.???.?? ansible_ssh_user=root ansible_ssh_pass=myPasswrd2

[flaskbox_prod]
```
#### 5. Login to your Nanode to add the ECDSA key fingerprint on your host (laptop/machine)
```shell 
$ ssh root@???.???.?.??
The authenticity of host '???.???.?.?? (???.???.?.??)' can't be established.
ECDSA key fingerprint is SHA256:cKRKaNMOcD7yuT6lOoqrte8oNmDuczXM47mcgmFPAFg.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```
once logged in exit the remote host
```shell 
root@localhost:~# exit
```

#### 5. Run the Ansible playbook
```shell 
ansible-playbook -i inventory ubuntu20-04.yml 
```
