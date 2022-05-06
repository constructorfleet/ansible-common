# Ansible-Common

<!-- MarkdownTOC -->

- Requirements
- Role Variables
    - defaults/main.yml
  - vars/Debian.yml
  - vars/RedHat.yml
- Dependencies
- Example Playbook
- License
- Author Information

<!-- /MarkdownTOC -->

Deploy common configurations and packages to servers.


## Requirements

N/A


## Role Variables

#### defaults/main.yml
```
consoletty: tty1
serialtty: ttyS1

timezone: UTC
```

### vars/Debian.yml
```
common_pkgs:
  - screen
  - vim
  - ipmitool
  - freeipmi-tools
  - software-properties-common
  - python-pip
  - python3-pip
  - python3-software-properties
  - zsh
  - sudo
  - tzdata

common_uninstall_pkgs:
  - python-setuptools

common_python_pkgs:
  - setuptools

autoupdate_services:
  - apt-daily-upgrade.timer
  - apt-daily.timer
  - unattended-upgrades.service
```

### vars/RedHat.yml
```
common_pkgs:
  - vim-enhanced
  - screen
  - ipmitool
  - zsh

serialunit: 0
serialport: ttyS0
serialspeed: 115200
serial_efi_grub_cfg: "/boot/efi/EFI/centos/grub.cfg"
serial_bios_grub_cfg: "/boot/grub2/grub.cfg"
serial_efi_path: "/sys/firmware/efi"
serial_grub_defaults: "/etc/default/grub"
serial_grub_terminal: "console serial"

autoupdate_services:
```

## Dependencies

N/A


## Example Playbook
```
- name: Deploy common server configurations
  hosts: all
  become: true
  remote_user: root
  tasks:
    - include_role:
        name: common
      tags:
        - common
        - packages
        - cloudinit
        - ssh
        - sol
        - sudo
        - autoupdate
        - hostfile
        - timezone
```

## License

MIT

## Author Information

Created by Alan Janis
