# Ansible IOS Backups

This script can be run in one of two ways.

The first is running it locally or even on an external server by using the ansible-playbook command.

The second way (the way this script is designed to be run) is with AWX or Ansible Tower.

Due to this, there will need to be some configuration made to make this work.

The first section will be for running on a machine with ansible-playbook.

## Ansible-Playbook

First you will need to clone this repo `git clone https://github.com/slightcisco/Ansible_backups` into a folder that you require.

You can then `cd` into the Ansible_backups folder.

We can then start configuring the script

### Passwords

Firstly we need to add a section of code to allow passwords to be passed into, this goes under the `tasks``````````````````:` heading on line 7.

The code goes as follows:

`- name: SYS | Including passwords file
  include_vars:
    file: passwords.yml`

You will then need to configure the passwords file.

This can be done one of 2 ways:

The first is to create a new passwords file called `passwords.yml` and create a dictionary inside specifying both `user` , `pass` and `teams_email`

The second is to rename `demo_passwords.yml` to `passwords.yml` and change the values as required. 

### Inventory

Ansible uses inventory files to operate on.

This is essentially a list of devices you want to run the script on.

You can see `uktme.inv` as an example of what sort of thing to include in your inventory file, or see [here](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html) for more info.

### Running the playbook

Everything should now be configured ready to run the playbook.

This can be run with the following command: `ansible-playbook -i INVENTORY playbook.yml` where INVENTORY is the name of your inventory file.

This should now run through and provide debug information throughout.

In the debug messages, you should see many colors.

Green means that everything is okay.

Orange/Yellow means that everything is okay and there have been changes made.

Red means that there has been a problem that has resulted in the script failing.

This usually comes with a reason why.

To see the backups, we have to navigate to the folder that they are in.

This is done with `cd ~/ansible/backups/`

There should now be one folder in here with todays date.

Confirm this with the `ls` command.

We can then `cd` into that folder and `ls` again to see the backups

## AWX

This section details how to deploy to AWX or ansible tower.

## Installation

Firstly we need to create a new project.

We need to provide a name, organisation and give the scm type of git.

We can now paste the URL for this repo (`https://github.com/slightcisco/Ansible_backups`) in the SCM URL box.

It should look like the following:

![Creating new project](https://github.com/slightcisco/Ansible_backups/pictures/new_project.png)
