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


        # Note: Include the _custom_repos.yml tasks with loop_control setting the loop_var to repo_item
        # This is necessary because _custom_repos.yml includes _custom_add_packages.yml in a loop and
        # the loop variables would conflict otherwise.
        - name: add custom repos
          include_role:
            name: utilities
            tasks_from: _custom_repos.yml
          loop: '{{ desktop_custom_repos | default([]) }}'
          loop_control: {loop_var: 'repo_item'}
          tags: 'customrepos'

## Tests

### Linting the role

Run: sh ./tests/lint_role

## License

MIT / BSD

## Author Information

Created in 2020 by [Michael Erdely](mike@erdelynet.com)
