# system-setup Ansible Project

This is an Ansible project to set up my systems with my preferences.

## Roles

### become

This role stores become passwords in a vault allowing the user enter one vault password and become root with other passwords stored in the vault.
This role has no tasks or handlers.

### configfiles

This role installs my config files on my systems.
The config files are stored in lists in vars/main.yml

### sshclient

This role configures the ssh client, installing personal ssh keys from a vault stored in vars/main.yml

### sshserver

This role configures the ssh server, installing ssh host keys for each server from a vault stored in vars/main.yml

### unix_system

This role installs and configures base level packages and services

### unix_desktop

This role installs and configures the system for running desktop applications

### gnome_desktop

This role installs and configures the system to run Gnome

## Requirements

None

## Dependencies

None

## License

MIT / BSD

## Author Information

Created in 2020 by [Michael Erdely](mike@erdelynet.com)

