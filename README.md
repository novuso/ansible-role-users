# Ansible Role: Users

[![Ansible Galaxy](http://img.shields.io/badge/galaxy-novuso.users-000000.svg)](https://galaxy.ansible.com/list#/roles/3871)
[![MIT License](http://img.shields.io/badge/license-MIT-003399.svg)](http://opensource.org/licenses/MIT)
[![Build Status](https://travis-ci.org/novuso/ansible-role-users.svg)](https://travis-ci.org/novuso/ansible-role-users)

An Ansible role that manages users on Ubuntu 14.04

## Requirements

None

## Role Variables

Ansible variables are listed here along with their default values:

`users` is a list of user configurations. Each entry in the list may designate:

* **name** username *required*
* **password** user password *required*
    * [Encrypted Password](http://docs.ansible.com/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module)
* **uid** *required*
* **state** (default present)
* **shell** (default is value of `users_default_shell`)
* **createhome** (default is yes)
* **home** (default is `/home/{{name}}`)
* **comment** (default is omitted)
* **force_del** `userdel --force` when `state` is absent (default is omitted)
* **generate_ssh_key** (default is no)
* **ssh_key_bits** when `generate_ssh_key` is yes (default is 4096)
* **ssh_key_comment** when `generate_ssh_key` is yes (default is `{{name}}@$HOSTNAME`)
* **ssh_key_file** when `generate_ssh_key` is yes (default is omitted)
* **ssh_key_passphrase** when `generate_ssh_key` is yes (default is omitted)
* **ssh_key_type** when `generate_ssh_key` is yes (default is omitted)
* **move_home** (default is no)
* **remove** `userdel --remove` when `state` is absent (default is omitted)
* **system** when creating, makes system user (default is no)
* **update_password** `always` or `on_create` (default is always)
* **append_groups** (default is yes)
* **groups** list of secondary groups (default is omitted)
* **ssh_keys** list of authorized_keys (default is omitted)

By default, no users are used:

    users: []

`users_groups` is a list of secondary group configurations. Each entry in the
list may designate:

* **name** *required*
* **state** (default is present)
* **gid** (default is omitted)
* **system** (default is no)

By default, no secondary groups are used:

    users_groups: []

`users_default_shell` sets the default shell for users.

    users_default_shell: "/bin/bash"

`users_create_home_dir` flags whether to create home directories for users by
default.

    users_create_home_dir: "yes"

`users_default_home_prefix` sets the root path for home directories.

    users_default_home_prefix: "/home"

`users_create_username_group` flags whether or not primary group should match
the username.

    users_create_username_group: true

`users_default_group` sets the default users group when
`users_create_username_group` is false.

    users_default_group: "users"

## Dependencies

None

## Example Playbook

    ---
    - hosts: all
      vars:
      - users:
        - name: "bob"
          password: "$6$L9QhtLnh/$IOl4UR7r7yjAID3MztDBEkxTrFTdxx4KQcrORFkKWLkK6LT45PZoghUSuSX71ufR0oA6etkZ5xCyZ/m0FuHlA."
          uid: "3001"
      - users_create_username_group: false
      roles:
      - novuso.users

## License

This is released under the [MIT license](http://opensource.org/licenses/MIT).
