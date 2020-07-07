# Ansible Role: become

Sets a list of variables containing the become passwords for the hosts in the inventory

If every host has a different become password, the inventory can look like:
    [group1]
    host1 password_type=host1
    host2 password_type=host2

The corresponding variables (in vars/main.yml) would be:
    ---
    become_passwords:
      host1: password4host1
      host2: "host2'sp@ss"

If different groups of hosts have different become passwords, the inventory can look like:
    [all:vars]
    password_type=default

    [group1:vars]
    password_type=group1

The corresponding variables (in vars/main.yml) would be:
    ---
    become_passwords:
      default: "default*password"
      group1: pass4group1

A utilities/setup_become_vault.yml playbook has been included to create a become password vault from the inventory (looking for all password_type variables). Any existing vars/main.yml must be moved out of the way before running utilities/setup_become_vault.yml.

## Requirements

None

## Role Variables

Lists of variables for each password_type listed in the inventory
    become_passwords: A list of become passwords for each password type (hosts or groups)
    test_variables: A list of test variables for each password type

test_variables are simply a way to test that the become role is functioning properly without having to print a real password

The actually setting of the password ansible will use for 'become: true' is stored in default/main.yml:
    ansible_become_password: "{{ become_passwords[password_type] }}"

## Dependencies

ansible-playbook must be run with '--ask-vault-pass' or '--vault-password-file path-to-file' or '--vault-id vaultid@method'

## Example Playbook

    ---
    - hosts: localhost
      roles:
        - become

## Test

A test for the role has been included.

### Test Requirements

Create a vars/main.yml with a "default" become password. Make sure there is no "bad_password_type" password.

### Run the test

Run: sh ./tests/run_test

### Expected output

    $ ./tests/run_test 
    Vault password: 
    
    PLAY [local_hosts] **********************************
    
    TASK [List files in /root] **************************
    fatal: [hostfailure]: FAILED! => {"msg": "The field 'become_pass' has an invalid value, which includes an undefined variable. The error was: 'dict object' has no attribute 'bad_password_type'"}
    ok: [hostsuccess]
    
    PLAY RECAP ******************************************
    hostfailure                : ok=0    changed=0    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
    hostsuccess                : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

### Linting the role

Run: sh ./tests/lint_role

## License

MIT / BSD

## Author Information

Created in 2020 by [Michael Erdely](mike@erdelynet.com)

