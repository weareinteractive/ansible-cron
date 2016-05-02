# Ansible franklinkim.cron role

[![Build Status](https://img.shields.io/travis/weareinteractive/ansible-cron.svg)](https://travis-ci.org/weareinteractive/ansible-cron)
[![Galaxy](http://img.shields.io/badge/galaxy-franklinkim.cron-blue.svg)](https://galaxy.ansible.com/franklinkim/cron)
[![GitHub Tags](https://img.shields.io/github/tag/weareinteractive/ansible-cron.svg)](https://github.com/weareinteractive/ansible-cron)
[![GitHub Stars](https://img.shields.io/github/stars/weareinteractive/ansible-cron.svg)](https://github.com/weareinteractive/ansible-cron)

> `franklinkim.cron` is an [Ansible](http://www.ansible.com) role which:
>
> * installs cron
> * adds cron tasks
> * configures service

## Installation

Using `ansible-galaxy`:

```shell
$ ansible-galaxy install franklinkim.cron
```

Using `requirements.yml`:

```yaml
- src: franklinkim.cron
```

Using `git`:

```shell
$ git clone https://github.com/weareinteractive/ansible-cron.git franklinkim.cron
```

## Dependencies

* Ansible >= 2.0

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```yaml
---
# cron_tasks:
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
#
# refer to the `cronvar Ansible module documentation <https://docs.ansible.com/ansible/cronvar_module.html>`_ for details.
#
# cron_vars:
#   - name: 'PATH'
#     value: '/usr/bin:/bin:/usr/local/bin'
#     user: 'root'
#
cron_vars: []

```

## Handlers

These are the handlers that are defined in `handlers/main.yml`.

```yaml
---
# For more information about handlers see:
# http://www.ansibleworks.com/docs/playbooks.html#handlers-running-operations-on-change
#

- name: restart cron
  service:
    name: "{{ cron_service_name }}"
    state: restarted
  when: cron_service_state != 'stopped'

```


## Usage

This is an example playbook:

```yaml
---

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

```shell
$ git clone https://github.com/weareinteractive/ansible-cron.git
$ cd ansible-cron
$ make test
```

## Contributing
In lieu of a formal style guide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

*Note: To update the `README.md` file please install and run `ansible-role`:*

```shell
$ gem install ansible-role
$ ansible-role docgen
```

## License
Copyright (c) We Are Interactive under the MIT license.
