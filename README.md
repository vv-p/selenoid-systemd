# Selenoid with Systemd and Ansible

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)

## Before you start

Selenoid doesn't download docker images by himself, so this playbook does it. Therefore you need to install
[docker-py](https://pypi.org/project/docker-py/) python package before running it (I don't know how is you manage your python modules, so I don't want to 
install something in unusual way in your environment). Look at the 
[docker_image ansible module documentation](http://docs.ansible.com/ansible/latest/modules/docker_image_module.html)
to more information about how this playbook manage docker images.

## How to use it ?

Just add your selenoid server to **hosts** file, check environment variables in **selenoid.yml** playbook and run:
```bash
ansible-playbook -b -i hosts selenoid.yml
```

## Variables

All default variable values stored in **roles/selenoid/defaults/main.yml** file:

```yaml
vnc: false
shmSize: 268435456
tmpSize: 512m
varSize: 128m
timezone: "Europe/Moscow"
selenoid_port: 4444
selenoid_ui_port: 8080
browsers:
  - name: "chrome"
    default: "66.0"
    versions:
      - "66.0"
      - "65.0"
  - name: "firefox"
    default: "59.0"
    versions:
      - "59.0"
      - "58.0"
  - name: "opera"
    default: "52.0"
    versions:
      - "52.0"
      - "51.0"

```

Look at the official selenoid page to more information - [Selenoid Documentation](https://aerokube.com/selenoid/latest/#_configuration)

You can overwrite it in **selenoid.yml** role file:

```yaml
- hosts: all
  vars:
    vnc: true
    browsers:
      - name: "chrome"
        default: "66.0"
        versions:
          - "66.0"
          - "65.0"

  roles:
    - selenoid
    - selenoid-ui
```

or pass it as command-line arguments:

```bash
ansible-playbool -b -i hosts selenoid.yml --extra-vars "vnc=false"
```

Look at the [Ansible documentation](http://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html) for details.


## Q&A:

### How to check selenoid (or selenoid-ui) status ?
```bash
systemctl status selenoid
```

### How to start or stop selenoid (selenoid-ui) ?
```bash
systemctl start selenoid
systemctl stop selenoid
```

### Where is selenoid logs ?
```bash
journalctl -u selenoid -f
```
