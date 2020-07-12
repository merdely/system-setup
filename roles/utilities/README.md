# Ansible Role: utilities

This role contains some utility playbooks to be included in other playbooks/roles

## Requirements

None

## Role Variables

None

## Dependencies

None

## Example Playbook Usage

    ---
    - hosts: ...
    ...

      tasks:
      ...

        - include_role:
            name: utilities
            tasks_from: _custom_files.yml
          with_items: '{{ my_custom_files | default([]) }}'

## Tests

### Linting the role

Run: sh ./tests/lint_role

## License

MIT / BSD

## Author Information

Created in 2020 by [Michael Erdely](mike@erdelynet.com)
