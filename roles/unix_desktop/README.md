# Ansible Role: unix_desktop

Performs basic tasks for Unix-like desktop systems:

* Install packages required for this playbook.
* Add desktop-specific packages to the list of packages to be installed.
* Install custom files for a desktop system. Examples:
  * A script to monitor the screensaver and forget ssh agent passphrases.
  * Configuration files for installed applications.
* Install custom includes for a desktop system.
* Install custom settings for a desktop system.
* Add custom repos for a desktop system, for example:
  * Chrome and other 3rd party software.
* Add users to groups (specific to a desktop system.
* Enable/start services specific to a desktop system.
* Install custom Debian 'deb' files for a desktop system.  Example:
  * Discord
* Apply custom .Xresources settings.
* Remove libreoffice on Linux.
* Install p3x-onenote on Linux.

## Requirements

None

## Role Variables

For each role in the project, there is a set of custom variables to perform customize the system (documented in defaults/main.yml)

* desktop_custom_files
* desktop_custom_includes
* desktop_custom_settings
* desktop_custom_repos
* desktop_custom_groups
* desktop_custom_services
* desktop_custom_deb_files

## Dependencies

None

## Example Playbook

    ---
    - hosts: localhost
      roles:
        - unix_desktop

## Tests

### Linting the role

Run: sh ./tests/lint_role

## License

MIT / BSD

## Author Information

Created in 2020 by [Michael Erdely](mike@erdelynet.com)

