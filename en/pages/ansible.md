# Ansible - Systems Automation

## Issues

[Ansible: Could not find aptitude. Please ensure it is installed Error and Solution](https://www.cyberciti.biz/faq/ansible-could-not-find-aptitude-please-ensure-it-is-installed/):

Posted on June 13, 2017in Categories Debian / Ubuntu, Linux, Package Management, Troubleshooting last updated June 13, 2017
I am running the ‘ansible-playbook -i hostnames upgrade.yml‘ command but getting an error that read as follows
fatal: [db1]: FAILED! => {“changed”: false, “failed”: true, “msg”: “Could not find aptitude. Please ensure it is installed.“}

My yml file includes the following line:

- apt: update_cache=yes upgrade=yes

How do I fix this error on a Debian or Ubuntu Linux server?


You need to use apt module to manage packages for Debian/Ubuntu Linux using ansible. The apt module runs command depends upon upgrade parameter as follows:

apt module syntax

The syntax is:

- name: Update all packages to the latest version
  apt:
    upgrade: VALUE
Where VALUE can be any one of the following:

if upgrade parameter is no (upgrade=no) – Do NOT upgrade anything (default)
if upgrade parameter is yes (upgrade=yes) – Do upgrade using the aptitude command
if upgrade parameter is safe (upgrade=safe) – Do upgrade using the aptitude command
if upgrade parameter is full (upgrade=full) – Do upgrade using the aptitude command
if upgrade parameter is dist (upgrade=dist) – Do upgrade using the apt-get command
Understanding the error

The following error indicates that you do not have aptitude command installed on the remote Debian/Ubuntu box which is quite common on virtual private servers (VPS) or cloud servers or minimal installation or customized installation:

TASK [Updating host using apt] ***********************************************************************************************
fatal: [db1]: FAILED! => {"changed": false, "failed": true, "msg": "Could not find aptitude. Please ensure it is installed."}
fatal: [db2]: FAILED! => {"changed": false, "failed": true, "msg": "Could not find aptitude. Please ensure it is installed."}
fatal: [www1]: FAILED! => {"changed": false, "failed": true, "msg": "Could not find aptitude. Please ensure it is installed."}
fatal: [www2]: FAILED! => {"changed": false, "failed": true, "msg": "Could not find aptitude. Please ensure it is installed."}
You can verify that by ssh into any one of the server:
$ ssh user@db1 type -a aptitude
bash: line 0: type: aptitude: not found
$ ssh vivek@server1.cyberciti.biz aptitude
bash: aptitude: command not found

How do I fix this problem?

To fix this problem either install aptitude on the remote box using apt module itself and run upgrade:

- name: Update all packages to the latest version
  apt:
    name: aptitude 
    upgrade: yes
Or pass the dist parameter to the upgrade so that it will use apt-get command:

- name: Update all packages to the latest version
  apt:
    upgrade: dist
Another solution is to use the following in your .yml file:

- name: Upgrade all packages to the latest version
  apt:
    name: "*"
    state: latest
For more info see apt – Manages apt-packages documentations.

Posted by: Vivek Gite
The author is the creator of nixCraft and a seasoned sysadmin and a trainer for the Linux operating system/Unix shell scripting. He has worked with global clients and in various industries, including IT, education, defense and space research, and the nonprofit sector. Follow him on Twitter, Facebook, Google+.
GOT FEEDBACK? CLICK HERE TO JOIN THE DISCUSSION

[Ansible - Only if a file exists or does not exist](https://raymii.org/s/tutorials/Ansible_-_Only_if_a_file_exists_or_does_not_exist.html):

[Cisco and Ansible](https://www.reddit.com/r/networking/comments/6ljtpo/bossing_cisco_around_with_ansible/)