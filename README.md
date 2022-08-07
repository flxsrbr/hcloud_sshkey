hcloud_sshkey
=========

Role to manage public sshkeys on Hetzner Cloud.

Requirements
------------

* Hetzner Python library on target host: [hcloud](https://pypi.org/project/hcloud/)
* Ansible Hetzner collection on control node: [Hetzner.Hcloud](https://docs.ansible.com/ansible/latest/collections/hetzner/hcloud/)

Role Variables
--------------

**Default Variables**

| Variable                     | Type | Description                                                        | Default                      |
|------------------------------|------|--------------------------------------------------------------------|------------------------------|
| hcloud_sshkey_api_token_rw   | str  | Read-write Hetzner Cloud api token                                 | -                            |
| hcloud_sshkey_api_token_ro   | str  | Read-only Hetzner Cloud api token, defaults to rw-token if not set | hcloud_sshkey_api_token_rw   |

**SSH Key Variables**

| Variable           | Subitem | Type     | Description                                             | Example           |
|--------------------|---------|----------|---------------------------------------------------------|-------------------|
| hcloud_sshkey_keys |         | lst/dict | List of public ssh keys to manage                       |                   |
|                    | name    | str      | Name of public key associated with key on Hetzner Cloud | "ansible"         |
|                    | key     | str      | Public ssh key.                                         | "ssh-ed25519 ..." |
|                    | state   | str      | Desired state of key on Hetzner Cloud.                  | "present"         |

Dependencies
------------

none

Example Playbook
----------------

    - name: "Manage ssh keys on Hetzner Cloud."
      hosts: localhost
      gather_facts: false
      vars_files:
        - vars/vault.yml

      roles:

        - name: hcloud_sshkey
          vars:
            hcloud_sshkey_api_token_rw: "{{ vault_hcloud_token_rw }}"
            hcloud_sshkey_api_token_ro: "{{ vault_hcloud_token_ro }}"
            hcloud_sshkey_keys:
              - name: "ansible"
                file: "{{ lookup('file', '/path/to/file/id_ed25519.pub') }}"
                state: present


License
-------

BSD

Author Information
------------------

[flxsrbr](https://github.com/flxsrbr)
