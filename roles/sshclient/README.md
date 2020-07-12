# Ansible Role: sshclient

Performs basic tasks for SSH client systems:

* Ensure sshd is enabled and started.
* Install ssh_host_*_key{,.pub} files for each host.  They should be defined in vars/main.yml as an encrypted vault.  The format is described below.
* Install custom files for SSH clients.  Used for installing user files like:
  * ~/.ssh/authorized_keys
  * ~/.ssh/config
  * ~/.ssh/rc
* Install custom includes for SSH clients.
* Install custom settings for SSH clients.

## Requirements

None

## Role Variables

vars/main.yml should be a vault file because it contains your private key(s) file

Like other roles, there are 'sshclient_custom-*' variables well documented in defaults/main.yml

The format of the vars/main.yml vault file is:

    # Define multiple keys: they will be put in ~/.ssh
    user_ssh_keys:
      - file: id_ed25519
        private_key: |
          -----BEGIN OPENSSH PRIVATE KEY-----
          really private key stuff goes here!
          -----END OPENSSH PRIVATE KEY-----
        public_key: |
          ssh-ed25519 AAAAC3NzaCpubkeystuff user@host
      - file: id_rsa
        private_key: |
          -----BEGIN OPENSSH PRIVATE KEY-----
          other private key stuff goes here!!
          -----END OPENSSH PRIVATE KEY-----
        public_key: |
          ssh-rsa AAAAB3NzaC1yc2pubkeystuff user@host

If user_ssh_keys is not defined, no private/public SSH keys will be copied.
If both file_sources and web_sources are defined, file_sources takes precedence.

For each role in the project, there is a set of custom variables to perform customize the system (documented in defaults/main.yml)

* sshclient_custom_files
* sshclient_custom_includes
* sshclient_custom_settings

## Dependencies

None

## Example Playbook

    ---
    - hosts: localhost
      roles:
        - sshclient

## Tests

### Linting the role

Run: sh ./tests/lint_role

## License

MIT / BSD

## Author Information

Created in 2020 by [Michael Erdely](mike@erdelynet.com)

