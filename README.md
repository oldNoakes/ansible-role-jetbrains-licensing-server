# Maven Role

[![Build Status](https://travis-ci.org/oldNoakes/ansible-role-jetbrains-licensing-server.svg?branch=master)](https://travis-ci.org/oldNoakes/ansible-role-jetbrains-licensing-server)

This role installs the jetbrains licensing server, configures it and then makes it a service available on the system.  Documentation for supporting and setting up the licensing server can be found [here](https://www.jetbrains.com/help/license_server/getting_started.html).

## Role Depenendencies

This role requires:
  * java to be installed - it currently depends on [geerlingguy.java](https://galaxy.ansible.com/geerlingguy/java) and installs OpenJDK 8
  * unzip to be installed (due to the unarchive module requiring unzip for zipped packages) - it currently depends on [kbrebanov.unzip](https://galaxy.ansible.com/kbrebanov/unzip/)

## Role Variables

### Defaults

All role default variables can be seen in the [defaults/main.yml file](https://github.com/oldNoakes/ansible-role-jetbrains-licensing-server/blob/master/defaults/main.yml).

### Custom variables

When running the licensing server behind a reverse proxy, you will need to provide the variable ```jb_licensing_server_virtualhost``` so that the jetty server running the application is able to understand the incoming requests.  Here is a quick example:

```
- hosts: all
  roles:
    - role: jetbrains-licensing-server
      jb_licensing_server_virtualhost: "jetbrains.licensing.company.com"
```

## Role Usage

### Ansible Galaxy Requirements.yml

* Add the following content into the requirements.yml (Ansible Galaxy file).  If you need a specific version, add that based on the [available tagged versions](https://github.com/oldNoakes/ansible-role-jetbrains-licensing-server/tags) 

```yaml
---
# from Github with specific tagged version and rename
- src: https://github.com/oldNoakes/ansible-role-jetbrains-licensing-server.git
  name: jetbrains-licensing-server
  version: 1.0.0

# from Galaxy with specific tagged version
- src: oldNoakes.jetbrains-licensing-server
  version : 1.0.0

# from Galaxy 
- src: oldNoakes.jetbrains-licensing-server
```

### Role usage in playbook

* Use the role in your playbook:

```yaml
- hosts: servers
  roles:
    - oldNoakes.jetbrains-licensing-server
```