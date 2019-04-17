# Ansible IOS Backups

## Installation

First you will need to clone this repo `git clone https://github.com/slightcisco/Ansible_backups`

### Passwords

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



