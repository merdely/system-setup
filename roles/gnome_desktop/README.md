# Ansible Role: gnome_desktop

Performs basic tasks for Gnome desktop systems

* Install packages required for this playbook.
* Add Gnome-specific packages to the list of packages to be installed.
* Install custom files for Gnome.
* Install custom includes for Gnome.
* Install custom settings for Gnome.
* Add custom repos for Gnome.
* Add users to groups (specific to Gnome).
* Enable/start services specific to Gnome.
* Install custom Debian 'deb' files for Gnome.
* Install autostart files to start programs when Gnome starts.
* Install a script make DBUS address info available from SSH.
* Pause for the user to log into Gnome.
* Disables a list of Gnome Shell Extensions (already installed).
* Install a list of Gnome Shell Extensions.
* Tweak GDM so it prompts for username and passwords instead of providing a list.
* Configure a list of Gnome Shell/Gnome Terminal settings.

## Requirements

None

## Role Variables

The window_manager should be set to 'gnome-session' to use Gnome. Ensure that window_manager is not set in the unix_desktop role's defaults/main.yml or vars/main.yml

The autostart_files variable contains a list of programs to run when Gnome starts.
- name: name of the startup icon
- exec: command to run
- icon: path to an icon (defaults to an icon with 'name')
- terminal: whether to open a terminal window for this program (defaults to false)
- os_family: a list of ansible_os_family values for which the autostart file pertains autostart_files:
  - {name: 'myprogram', exec: '\~/bin/myprog', icon: '\~/Pictures/myprog.png'}

The vars/main.yml has many Gnome settings that are modified during installation.
The gnome_settings_list variable is a list of parameters for settings:

* path: The base path of the Gnome/dconf setting
* key: The setting to be changed
* value: The value of the setting to be changed
* min: (optional) If the current value is less than or equal to min, the value is changed to value.  But if someone went in an changed the setting (say for the number of columns in Terminal's profile from 80 to 100), the playbook won't change it from 100 to 200 (or whatever gets set in vars/main.yml).
* skip: (optional) A true/false test whether to skip setting this value or not. For instance, if Terminal's profile is set to use the System Theme, it won't go changing the background color (which would have no affect).

The value parameter has weird quoting issues. Strings have to be quoted like '''foo''' so that "'foo'" gets passed.  Otherwise, ansible or dconf loses the single quote in the double quotes.  Additionally, the multi-value (array) settings have escaping and quoting problems of the elements.  It's best to define the array as a variable and then pass the variable with "[{{ variable | join(', ') | string }}]".  The array would be defined using the weird triple single quoting with ['''element1''', '''element2'''].

New values can be added to vars/main.yml's gnome_settings{,_openbsd}_list. The best way is to go into a system, run 'dconf dump / > before', change the setting, and run 'dconf dump / > after' and compare the results.

For each role in the project, there is a set of custom variables to perform customize the system (documented in defaults/main.yml)

* gnome_custom_files
* gnome_custom_includes
* gnome_custom_settings
* gnome_custom_repos
* gnome_custom_groups
* gnome_custom_services
* gnome_custom_deb_files

## Dependencies

None

## Example Playbook

    ---
    - hosts: localhost
      roles:
        - gnome_desktop

## Tests

### Linting the role

Run: sh ./tests/lint_role

## License

MIT / BSD

## Author Information

Created in 2020 by [Michael Erdely](mike@erdelynet.com)

