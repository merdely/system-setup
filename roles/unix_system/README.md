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

## Host Variables

To set an FQDN for the system, define a host variable for the system "fqdn=system.domain.name"
This can be set in the inventory or inventory host_vars.
To set it in the inventory:
    [group]
    system fqdn=system.domain.name

## Role Variables

A custom CA certificate file can be downloaded if defined like in one of the examples below
custom_ssl_certs:
- {type: 'file', src: 'files/cert1.crt', dest: 'ca-cert1.crt'}
- {type: 'web', src: 'https://yoursite.my.domain/cert2.crt', dest: 'ca-cert2.crt'}

A custom search domain can be added by defining dns_search_domain like the example below
* dns_search_domain: 'my.domain'

A way to bail on adding the dns_search_domain in RedHat (e.g. the computer is not on its home network)
* dns_search_exception: '[ "$dg" != "192.168.25.1" -a "$dg" != "192.168.122.1" ] && unset dg && exit'

For each role in the project, there is a set of custom variables to perform customize the system (documented in defaults/main.yml)

* system_custom_add_packages
* system_custom_remove_packages
* system_custom_files
* system_custom_includes
* system_custom_settings
* system_custom_repos
* system_custom_groups
* system_custom_services
* system_custom_deb_files

For packages that are required for this playbook to work, use the system_pkgs_install dict for each OS family/system.

The playbook makes other changes to Debian/Ubuntu that can be skipped with:
* dont_modify_dash_as_sh
* dont_modify_select_editor

By default, if the Debian selected editor is to be modified (see above), it will set it to /usr/bin/vim.basic.  Override with:
* debian_select_editor: '/usr/bin/your_editor'

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

