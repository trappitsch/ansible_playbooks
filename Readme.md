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

### Update existing computers

The playbook `update_apt.yml` updates the apt cache and upgrades all packages.
It is run via:

```
ansible-playbook update_apt.yml
```

### Update Mattermost

The playbook `mattermost_update.yml` updates the version of the Mattermost server.
It is run via:

```
ansible-playbook mattermost_update.yml
```

The playbook first asks which Mattermost version to download and install.
Make sure that you give the three digit version number, e.g. `5.32.1`, that you want to upgrade to.
The playbook then downloads the new version, stops the Mattermost server, and installs the new version.
The upgrade follows the [official Mattermost upgrade guide](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html).

**Warning**: Special instructions are not taken into consideration.
This means that you must ensure that the simple upgrade procedure is adequate for the upgrade you want to perform.
Technically, you can also downgrade the Mattermost server by specifying a lower version number.

#### Setup

- For host setup, see below
- Clone this repository or make sure you have the files `mattermost-update.yml` and `vars/mattermost.yml` locally
- Configure the variables according to your needs in `vars/mattermost.yml`. The top block is for the Mattermost server, the bottom block for the local / control machine.
  - `tmp_path`: Temporary path on the server to download the new Mattermost version to
  - `install_path`: Path where you `mattermost` folder is located
  - `backup_path`: Path where you want to store the backup of the old Mattermost version on the server
  - `do_cntrl_backup`: Boolean to decide if you want to copy the backup to the control machine or not
  - `cntrl_backup_path`: Path where you want to store the backup of the old Mattermost version on the control machine


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
