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

![creating new project](https://github.com/slightcisco/Ansible_backups/blob/master/pictures/new_project.png)

The next thing you need to do is create an inventory.

This is fairly straight forward. 

You need to provide a name as well as an organisation.

You then need to add a series of hosts which can be created in the inventory page.

You then need to define 4 variables.

These are `user pass api_key room_token`.

User and pass are the username and password you provide when logging onto the ios devices.

api_key is the key for the webex team bot.

You can create your own or use mine `ZmYwMjRmYjEtNWM4ZC00NGQ0LTk3NmMtNTZhZDE1ZmM0OTc4ZDEzMTk4OWUtMDhj_PF84_1eb65fdf-9643-417f-9974-ad72cae0e10f`

room_token is the token for the room you want the bot to post into.

This can be found [here](https://developer.webex.com/docs/api/v1/rooms/get-room-details).

The next thing to do is create a new job template.

This is essentially the way that we can run the playbook.

This is fairly straight forward and you should be able to see below for help.

![template](https://github.com/slightcisco/Ansible_backups/blob/master/pictures/template.png)

You can now setup a schedule for that job to run daily/weekly or however you like
