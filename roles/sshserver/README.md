# Ansible Role: sshserver

Performs basic tasks for SSH server systems:

* Ensure sshd is enabled and started.
* Install ssh_host_*_key{,.pub} files for each host.  They should be defined in vars/main.yml as an encrypted vault.  The format is described below.
* Install custom files for SSH servers.
* Install custom includes for SSH servers.
* Install custom settings for SSH servers.

## Requirements

None

## Role Variables

vars/main.yml should be a vault file because it contains your ssh host private key(s) file

Like other roles, there are 'sshserver_custom_*' variables that are well defined in defaults/main.yml

The format of the vars/main.yml vault file is:

    # Define keys for multiple servers: they will be put in ~/.ssh
    ssh_host_keys:
      name: host1
        - file: '/etc/ssh/ssh_host_ed25519_key'
          key: |
            -----BEGIN OPENSSH PRIVATE KEY-----
            really private key stuff goes here!
            -----END OPENSSH PRIVATE KEY-----
        - file: '/etc/ssh/ssh_host_ed25519_key.pub'
          key: |
            ssh-ed25519 AAAAC3NzaCpubkeystuff root@host1
        - file: '/etc/ssh/ssh_host_id_rsa_key'
          key: |
            -----BEGIN OPENSSH PRIVATE KEY-----
            other private key stuff goes here!!
            -----END OPENSSH PRIVATE KEY-----
        - file: '/etc/ssh/ssh_host_id_rsa_key.pub'
          key: |
            ssh-rsa AAAAB3NzaC1yc2pubkeystuff root@host1
      name: host2
        - file: '/etc/ssh/ssh_host_ed25519_key'
          key: |
            -----BEGIN OPENSSH PRIVATE KEY-----
            really private key stuff goes here!
            -----END OPENSSH PRIVATE KEY-----
        - file: '/etc/ssh/ssh_host_ed25519_key.pub'
          key: |
            ssh-ed25519 AAAAC3NzaCpubkeystuff root@host2
        - file: '/etc/ssh/ssh_host_id_rsa_key'
          key: |
            -----BEGIN OPENSSH PRIVATE KEY-----
            other private key stuff goes here!!
            -----END OPENSSH PRIVATE KEY-----
        - file: '/etc/ssh/ssh_host_id_rsa_key.pub'
          key: |
            ssh-rsa AAAAB3NzaC1yc2pubkeystuff root@host2

If ssh_host_keys[inventory_hostname] is not defined, no SSH host keys will be copied.
If both file_sources and web_sources are defined, file_sources takes precedence.

For each role in the project, there is a set of custom variables to perform customize the system (documented in defaults/main.yml)

* sshserver_custom_files
* sshserver_custom_includes
* sshserver_custom_settings

## Dependencies

None

## Example Playbook

    ---
    - hosts: localhost
      roles:
        - sshserver

## Tests

### Linting the role

Run: sh ./tests/lint_role

## License

MIT / BSD

## Author Information

Created in 2020 by [Michael Erdely](mike@erdelynet.com)

