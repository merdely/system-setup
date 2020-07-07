# Ansible Role: handlers

Defines handlers for all of the roles so that the order of execution can be controlled.

Some handlers need to occur in a specific order.  Ansible executes the handlers in the order they are defined.  Additionally, when multiple roles define the same handler, the last one defined overwrites the prior definitions.  Because handlers could be defined in a specific order in earlier roles, but then described again in later roles, the order isn't predictable when the handlers are defined in each role.

Having a role just for handlers allows them to be defined in the order required.

## Requirements

None

## Role Variables

None

## Dependencies

None

## Example Playbook

    ---
    - hosts: localhost
      roles:
        - handlers

## License

MIT / BSD

## Author Information

Created in 2020 by [Michael Erdely](mike@erdelynet.com)

