# Ansible Role: unix_system

Performs basic tasks for Unix-like systems:

* Update Debian Apt cache.
* Set vim as default editor (select-editor) for Debian.
* Install packages required for this role:
  * gtar
  * unzip
* Add system-specific packages to the list of packages to be installed.
* Install custom files for a Unix-like system. Examples:
  * ~/.profile.local
  * ~/.tmux.conf
  * ~/.vimrc
* Install custom includes for a Unix-like system:
  * A line in ~/.bash_profile: [ -r ~/.profile.local ] && . ~/.profile.local
  * A line in ~/.profile: [ -r ~/.profile.local ] && . ~/.profile.local
* Install custom settings for a Unix-like system.
* Add custom repos for a Unix-like system.
* Add users to groups (specific to a Unix-like system. Example:
  * Add user to operator group.
* Enable/start services specific to a Unix-like system.
* Install custom Debian 'deb' files for a Unix-like system.
* Download custom and install CA certificates.
* Add to DNS domain search list.

## Requirements

None

## Role Variables

A custom CA certificate file can be downloaded if defined like in one of the examples below
* file_ca_certificate: files/ca.crt
* web_ca_certificate: 'https://ca.erdelynet.com/ca.crt'

A custom search domain can be added by defining dns_search_domain like the example below
* dns_search_domain: 'my.domain'

A way to bail on adding the dns_search_domain in RedHat (e.g. the computer is not on its home network)
* dns_search_exception: '[ "$dg" != "192.168.25.1" -a "$dg" != "192.168.122.1" ] && unset dg && exit'

For each role in the project, there is a set of custom variables to perform customize the system (documented in defaults/main.yml)

* system_custom_files
* system_custom_includes
* system_custom_settings
* system_custom_repos
* system_custom_groups
* system_custom_services
* system_custom_deb_files

The ca_certification_dest variable contains the location for custom CA certificates in Debian & RedHat

## Dependencies

None

## Example Playbook

    ---
    - hosts: localhost
      roles:
        - unix_system

## Tests

### Linting the role

Run: sh ./tests/lint_role

## License

MIT / BSD

## Author Information

Created in 2020 by [Michael Erdely](mike@erdelynet.com)

