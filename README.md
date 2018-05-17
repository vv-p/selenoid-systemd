# Selenoid with Systemd and Ansible

## How to use it ?

Just add your selenoid server to **hosts** file, check environment variables in **selenoid.yml** playbook and run:
```bash
ansible-playbook -b -i hosts selenoid.yml
```

## Variables

All variables stored in **selenoid.yml** playbook file:

```
    selenoid_version: "latest-release"
    vnc: false
    shmSize: 268435456
    tmpSize: 512m
    varSize: 128m
    timezone: "Europe/Moscow"
    selenoid_port: 4444
    selenoid_ui_port: 8080
```

Look at the official selenoid page to more information - https://aerokube.com/selenoid/latest/#_configuration

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
