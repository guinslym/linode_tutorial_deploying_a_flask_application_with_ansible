
## LINODE: Deploying a Flask Application using Ansible


### Description
<p>
  Using ansible to deply a flask application on Linode. The original <a href="https://www.linode.com/docs/development/python/flask-and-gunicorn-on-ubuntu/" target="_blank">tutorial is located here</a>
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
#### Screenshots
  1. Choose Ubuntu 20.04 LTS
  2. Choose your preferred Region
  3. Choose Nanode or Linode
  4. Choose a password for this tutorial
  5. I would suggest that you add a ssh key. That will ease the login to the Remote Host (see point 5)
<p float="left">
    <img src="images/screenshot.png" width="700"/>
</p>

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

[flaskbox_dev]
???.??.???.?? ansible_ssh_user=root ansible_ssh_pass=myPasswrd2

[flaskbox_prod]

```
#### 5. Try to login to your Nanode to add the ECDSA key fingerprint on your host (laptop/machine)
```shell 
$ ssh root@???.???.?.??
The authenticity of host '???.???.?.?? (???.???.?.??)' can't be established.
ECDSA key fingerprint is SHA256:cKRKaNMOcD7yuT6lOoqrte8oNmDuczXM47mcgmFPAFg.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```
once logged in, exit the remote host
```shell 
root@localhost:~# exit
```

#### 5. Run the Ansible playbook
```shell 
ansible-playbook -i inventory ubuntu20-04.yml 
```
