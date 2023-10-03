# Ansible Role: Yugabyte

An opinionated Ansible Role to install and configure YugabyteDB.<br />
- By default, uses a replication factor of 3.<br />
- PostgreSQL is configured.<br />
- Cassandra is configured. <br />
- YEDIS is not configured. More information: [YEDIS](https://docs.yugabyte.com/preview/yedis/)
  > Given that YEDIS is not a focus, it must be viewed as a deprecated API for new application development purposes.

## Role Variables

Please refer to the [defaults file](/defaults/main.yml) for an up to date list of input parameters.

## Dependencies

By default this role does not depend on any external roles. <br />
If any such dependency is required please [add them](/meta/main.yml) according to [the documentation](http://docs.ansible.com/ansible/playbooks_roles.html#role-dependencies)

## Example Playbook
**Inventory**<br />
In order for the playbook to work, you need to have the following structure on your inventory:
```
yb_nodes:
  children:
    yb_master:
    yb_tserver:

yb_master:
  hosts:
    host_01:
    host_02:
    host_03:

yb_tserver:
  hosts:
    host_01:
    host_02:
    host_03:
```

**main.yml**
```
- name: Yugabyte Ansible Role
  become: true
  gather_facts: true
  hosts: yb_nodes

  roles:
    - role: "ansible-role-yb"
```

**Run playbook:**<br />
`ansible-playbook -i inventory/example main.yml -e address_type=hostname`

## License

This project is licensed under the terms of the [MIT License](/LICENSE)
