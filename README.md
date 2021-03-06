# system-setup Ansible Project

This is an Ansible project to take a system from "new install + sshd + python" to configured with my settings and preferences.

## Getting Started

### Build your inventory

Either use your main inventory (/etc/ansible/hosts) or what's defined in ~/.ansible.cfg or system-setup/ansible.cfg 'inventory' variable.  Or specify '-i inventory' on the command line.

### Working with role vaults

Refer to the README.md in the 'become' role for managing different become passwords.

If you use any encrypted vaults (become, sshclient, sshserver roles can/should have encrypted vaults), run ansible-playbook(1) with '--ask-vault-pass'.  If you do not use the become role, pass '-K' to prompt for the one become password the whole inventory will use.

Use 'ansible-vault create $role/vars/main.yml' and 'ansible-vault edit $role/vars/main.yml' to get started with encrypted vaults for each of the become (for multiple become passwords), sshserver (for installing ssh_host_*_key files), and sshclient (for installing personal ssh key files) roles.

### Setting up role variables

Go through the $role/default/main.yml files and create $role/vars/main.yml files with variables corresponding to your setup.

### Preparing playbooks

Either edit laptop-setup.yml/server-setup.yml or create a similar playbook.

### Preparing the target system

While the initial goal of this project was to take a newly installed system from fresh to configured easily, this could be used on existing systems too.

1. Install OS
2. Make sure sshd is started
3. Download SSH Public Key into ~/.ssh/authorized_keys
4. Make sure user can run sudo to run commands as root
5. Make sure python is installed

### Running playbooks

Run the ansible-playbook(1) command with the laptop-setup.yml or playbook created above.

## Roles

### become

This role stores become passwords in a vault allowing the user enter one vault password and become root with other passwords stored in the vault.
This role has no tasks or handlers.

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

