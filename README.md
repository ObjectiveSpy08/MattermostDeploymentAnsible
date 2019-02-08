# Submission HW2 - Devops

* Name: Shantanu Bhoyar
* unity id: sbhoyar

## Aim

To idempotently automate the installation and configuration of a Mattermost server using Ansible and Baker.

The code does the following: 

* Creates one VM each for an Ansible server and a Mattermost server. The database will reside on the same server as Mattermost.
* Runs an Ansible playbook on the Ansible server to setup the following on the Mattermost server:
  * Update the Linux system.
  * Install and configure MySQL.
  * Install and configure Mattermost

## Design

The functionality has been distributed into three roles respectively for each of the configuration tasks mentioned above that Ansible has to perform:

* server-setup
* mysql
* mattermost

## Pre-requisites

* Make sure you do not have anything running on 192.168.33.100 and 192.168.33.20.

## Execution

* Go inside the *mattermost-srv* folder.
* Run `baker bake` in the terminal to setup the mattermost VM.
* Go inside the *ansible-srv/group_vars* folder.
* Delete *mattermost.yml* file.
* Go up one level to *ansible-srv*.
* Run `baker bake` to setup the configuration server.
* Since we need to use anisble-vault, we are going to have to ssh into the VM. Run `baker ssh` to ssh into the Ansible server.
* Run `ansible-vault create mattermost.yml' and give a password for the vault. This will open an editor.
* In the editor give vaules for `admin_pwd: your_mattermost_admin_password` and `mysql_pwd: your_mysql_database_password` on 2 separate lines. Save and exit.
* Run `mv mattermost.yml /ansible-srv/playbook/group_vars` to move the new vault file to the playbook.
* Exit the ssh session.
* Run `baker install-mm` to run the ansible playbook.
* Navigate to 192.168.33.100:8065 to test the server.
* Admin username is **admin**. Password will be the value set for *admin_pwd*.
* You can also signup as a new user as that has been enabled in the config.json.
* The admin can then add the new user to a team and send them notifications.

## Screencast

* The screencast is available on [YouTube](#)
