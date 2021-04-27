ansible-ovhbastion
=========
This role installs and configures [OVH Cloud](https://www.ovh.com/world/)'s [the Bastion](https://github.com/ovh/the-bastion) secured jump host server. The ovhbastion role is based on the [official  Bastion installation instructions](https://ovh.github.io/the-bastion/installation/basic.html). Please visit [the official Bastion documentation](https://ovh.github.io/the-bastion/index.html) for more information.

Once you run this role, [click here](https://ovh.github.io/the-bastion/using/basics.html) to view the next steps in configuring the Bastion.

Tested On
------------

- Debian 8+
- Ubuntu 18+
- CentOS 8

Role Variables
--------------

#### Required
`ssh_key`: string with public ssh key for access to initial admin account

#### Recommended
`bastion_name`: string with name of bastion host. the system's actual hostname is _not_ recommended\
`bastion_create_admin`: toggle creation of the superadmin account\
`bastion_superadmin_uname`: string with username for the bastion superadmin (if enabled)\
`bastion_initial_users`: list of users to create after bastion setup\
`bastion_initial_groups`: list of groups to create after bastion setup

See `defaults/main.yml` for optional variables that can be set.

#### User detail

|attribute|type|description|required|
|---|---|---|---|
|name|string|name of the user to create|true|
|public_key|string|SSH ingress key for the bastion user. The key must be generated as either: <br/><ul><li>ed25519</li><li>ecdsa</li><li>rsa 4096 bits</li></ul>|true|
|hosts|list(string)|List of DNS records/IP addresses to grant initial access to|false|
|groups|list(string)|List of groups the new user should belong to (currently disabled)|false|

#### Group detail

|attribute|type|description|required|
|---|---|---|---|
|name|string|Group name|true|
|owner|string|Username of the group owner|true|
|hosts|list(string)|List of DNS records/IP addresses to grant initial access to|false|

Role Installation
------------

```bash
$ ansible-galaxy install adamsbytes.ovhbastion
```

Example Playbook
----------------

```yaml
- hosts: all
  become: yes
  gather_facts: yes
  roles:
    - role: adamsbytes.ovhbastion
  vars:
    ssh_key: "YOUR_PUBLIC_SSH_KEY_HERE"
```

License
-------

GPLv3

Author Information
------------------

https://github.com/adamsbytes
