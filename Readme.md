# Ansible Workflows

My ansible workflows are here to:

 - Update existing computers
 - Setup new raspberry pi's and lab computers running Linux

The latter workflow is adopted from online workflows.
Check out the vars folder for settings on which keys to copy!

## Playbooks

Run the playbooks via:

```
ansible-playbook PLAYBOOK-NAME.yml
```

## Host setup

The hosts are set up in `/etc/ansible/hosts`.
For lab computers and webservers,
the configuration can look something like this:

```
# ubuntu lab computers
[lab_ubuntu]
sassseeli ansible_host=sassseeli.physics.brandeis.edu

# actual servers
[webservers]
mattermost-droplet-do ansible_host=159.223.133.198


[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

## Help

A good digital ocean article on ansible is 
[here](https://www.digitalocean.com/community/cheatsheets/how-to-use-ansible-cheat-sheet-guide) and 
[here's a cheat sheet](https://intellipaat.com/mediaFiles/2019/03/Ansible-cheat-sheet.pdf).
The original playbooks that I adopted for my cases were from the
[DO community GitHub](https://github.com/do-community/ansible-playbooks).
