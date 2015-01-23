# Ansible Cron Role

[![Build Status](https://travis-ci.org/weareinteractive/ansible-cron.png?branch=master)](https://travis-ci.org/weareinteractive/ansible-cron)
[![Stories in Ready](https://badge.waffle.io/weareinteractive/ansible-cron.svg?label=ready&title=Ready)](http://waffle.io/weareinteractive/ansible-cron)

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

Using `arm` ([Ansible Role Manager](https://github.com/mirskytech/ansible-role-manager/)):

```
$ arm install franklinkim.cron
```

Using `git`:

```
$ git clone https://github.com/weareinteractive/ansible-cron.git
```

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```
# cron_tasks
#   - '*/5 * * * *  /bin/sh /absolute/path/to/cron.sh'
#

# list of cron entries
cron_tasks: []
# service name
cron_service_name: cron
# start on boot
cron_service_enabled: yes
# current state: started, stopped
cron_service_state: started
```

## Handlers

These are the handlers that are defined in `handlers/main.yml`.

* `restart cron` 

## Example playbook

```
- host: all
  roles: 
    - franklinkim.cron
  vars:
    crontab_tasks:
      - '*/5 * * * * /bin/sh /absolute/path/to/cron.sh'
```

## Testing

```
$ git clone https://github.com/weareinteractive/ansible-cron.git
$ cd ansible-cron
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
