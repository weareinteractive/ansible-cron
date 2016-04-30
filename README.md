# Ansible Cron Role

[![Build Status](https://img.shields.io/travis/weareinteractive/ansible-cron.svg)](https://travis-ci.org/weareinteractive/ansible-cron)
[![Galaxy](http://img.shields.io/badge/galaxy-franklinkim.cron-blue.svg)](https://galaxy.ansible.com/list#/roles/1408)
[![GitHub Tags](https://img.shields.io/github/tag/weareinteractive/ansible-cron.svg)](https://github.com/weareinteractive/ansible-cron)
[![GitHub Stars](https://img.shields.io/github/stars/weareinteractive/ansible-cron.svg)](https://github.com/weareinteractive/ansible-cron)

> `cron` is an [ansible](http://www.ansible.com) role which:
>
> * installs cron
> * adds cron tasks
> * configures service

## Installation

Using `ansible-galaxy`:

```
$ ansible-galaxy install franklinkim.cron
```

Using `requirements.yml`:

```
- src: franklinkim.cron
```

Using `git`:

```
$ git clone https://github.com/weareinteractive/ansible-cron.git franklinkim.cron
```

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```
# cron_tasks
#   - name: ...
#     cron_file: ...
#     day: ...
#     hour: ...
#     job: ...
#     minute: ...
#     month: ...
#     special_time: ...
#     state: ...
#     user: ...
#     weekday: ...
#

# list of cron entries (@see http://docs.ansible.com/cron_module.html)
cron_tasks: []
# start on boot
cron_service_enabled: yes
# current state: started, stopped
cron_service_state: started


# .. envvar:: cron_vars
#
# List of ``cron`` variables.
# Refer to the `cronvar Ansible module documentation <https://docs.ansible.com/ansible/cronvar_module.html>`_ for details.
#
# Example::
#
#    cron_vars:
#      - name: 'PATH'
#        value: '/usr/bin:/bin:/usr/local/bin'
#        user: 'root'
#
cron_vars: []
```

## Handlers

These are the handlers that are defined in `handlers/main.yml`.

* `restart cron`

## Example playbook

```
- hosts: all
  sudo: yes
  roles:
    - franklinkim.cron
  vars:
    cron_tasks:
      - name: checking dirs
        special_time: daily
        job: "ls -alh > /dev/null"
```

## Testing

```
$ git clone https://github.com/weareinteractive/ansible-cron.git
$ cd ansible-cron
$ vagrant up
```

## Contributing
In lieu of a formal style guide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License
Copyright (c) We Are Interactive under the MIT license.
