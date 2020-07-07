# Ansible Role: configfiles

This is the configfiles role to update configuration files on my systems.

Using a separated out 'configfiles' role from the other roles allows for pushing updates to configuration files without having to include the other roles.

## Requirements

None

## Role Variables

* custom_config_files
* custom_config_includes
* custom_config_settings

These are documented well in defaults/main.yml

## Dependencies

None

## Example Playbook

    ---
    - hosts: configs
      roles:
        - configfiles

## Tests

### Linting the role

Run: sh ./tests/lint_role

## License

MIT / BSD

## Author Information

Created in 2020 by [Michael Erdely](mike@erdelynet.com)
