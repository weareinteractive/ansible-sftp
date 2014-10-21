# Ansible Sftp Role

[![Build Status](https://travis-ci.org/weareinteractive/ansible-sftp.png?branch=master)](https://travis-ci.org/weareinteractive/ansible-sftp)
[![Stories in Ready](https://badge.waffle.io/weareinteractive/ansible-sftp.svg?label=ready&title=Ready)](http://waffle.io/weareinteractive/ansible-sftp)

> `sftp` is an [ansible](http://www.ansible.com) role which: 
> 
> * adds sftp users
> * configures user access to chroot environment
> * adds writable user folders
> * mounts system paths 
> 
> Note: see this [blog post](http://www.foomo.org/2012/09/chroot-users-with-openssh-and-expose-specific-resources/) for more details.


## Installation

Using `ansible-galaxy`:

```
$ ansible-galaxy install franklinkim.sftp
```

Using `arm` ([Ansible Role Manager](https://github.com/mirskytech/ansible-role-manager/)):

```
$ arm install franklinkim.sftp
```

Using `git`:

```
$ git clone https://github.com/weareinteractive/ansible-sftp.git
```

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```
# sftp_users:
#   - username: foobar
#     name: Foo Bar
#     # openssl passwd -salt 'somesalt' -1 'secret'
#     password: '$1$somesalt$jezmI5TSY7mVTzHLgsK5L.'
#     authorized_keys: []
#     home: /home
#     group: ftp
#     groups:
#       - staff
#       - www-data
#     mount_points:
#       - { name: foo, path: /path/to/foo }
#

# list of sftp users
sftp_users: []
# default user group
sftp_users_group:
# default user groups
sftp_users_groups: []
# users home directory
sftp_users_home: /home
# list of user writeable folders
sftp_users_folders: ['files']
```

## Handlers

These are the handlers that are defined in `handlers/main.yml`.

* `restart sftp` 

## Example playbook

```
- hosts: all
  sudo: yes
  roles:
    - franklinkim.sftp
  vars:
    sftp_users_group: ftp
    sftp_users:
      - username: foobar
        name: Foo Bar
        password: '$1$somesalt$jezmI5TSY7mVTzHLgsK5L.'
        mount_points:
          - name: tmp
            path: /tmp
```

## Testing

```
$ git clone https://github.com/weareinteractive/ansible-sftp.git
$ cd ansible-sftp
$ vagrant up
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License
Copyright (c) We Are Interactive under the MIT license.
