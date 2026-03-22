# Ansible Pycharm

This role will download, extract and configure Jetbrains PyCharm.

---

## Requirements


This role requires two separate tools be installed.

First it requires the 'ansible.utils' collection be installed from Ansible-Galaxy via:

```shell
ansible-galaxy collection install ansible.utils
```

Secondly it requires the `jsonschema` Python package be installed via:

```shell
pip install jsonschema
```

## Setup

Before the role can be used it needs to be added to the machine running the playbook, and as of writing this, this role is not hosted on Ansible-Galaxy only on Github.

1. Create a requirements.yml file in the root directory of the playbook being worked on.

2. Add the following definition inside the requirements.yml file:

```yaml
- name: hth-jetbrains-pycharm
  src: https://github.com/hrafnthor/ansible-jetbrains-pycharm.git
  scm: git
````

3. Install the requirements by executing

```yaml
ansible-galaxy install -r .requirements.yml
```

This will allow any playbook run from this machine to use the role hth-jetbrains-pycharm.

### Variables


All variables are optional unless otherwise stated.

```yaml
pycharm:
  location:
    path:         [string]  The installation location where community and professional versions will be installed. Defaults to '/opt/jetbrains/pycharm'
    owner:        [string] The owner of the installation location. Defaults to 'root'.
    group:        [string] The group owning the installation location. Defaults to 'root'
    mode:         [string]  The mode for the installation location. Defaults to '0755'
  clients:
    - version:    [string] The version to install. Find it at https://www.jetbrains.com/pycharm/download/other.html [required if installing]
      checksum:   [string] The checksum of the version archive. See below. [required if installing]
      remove:     [boolean] Indicates if this edition should be removed.
      desktop:
        name:     [string] The display name to for the launcher.
        remove:   [boolean] Indicates if a desktop entry should be removed.
        keywords: [array] Array of string keywords to add to the desktop launcher, to help with search.
```

Checksums for versions can be found by locating the appropriate tar archive [here](https://www.jetbrains.com/pycharm/download/other.html) and navigating to the url linked with `.sha256` appended (for example https://download.jetbrains.com/python/pycharm-2025.3.3.tar.gz.sha256).


#### Example Playbook


```yaml
 - hosts: all
      vars:
        pycharm:
          location:
            owner: root
            group: "developers"
            mode: "0775"
          clients:
            - version: "2025.3.3"
              checksum: "347752040eb83eb79f5eb0458a556d2cb306ac0e1d973c3e73743f9cdb8a4a0a"
              remove: false
              desktop:
                remove: false
                keywords:
                  - python
                  - jetbrains
                  - ide
                  - dev
                  - development
                  - django
      roles:
         - hth-jetbrains-pycharm
```

License
-------

Apache License 2.0. See attached license file.

Author Information
------------------

Hrafn Thorvaldsson.
http://www.hth.is
