Stouts.django
=============

[![Build Status](http://img.shields.io/travis/Stouts/Stouts.django.svg?style=flat-square)](https://travis-ci.org/Stouts/Stouts.django)
[![Galaxy](http://img.shields.io/badge/galaxy-Stouts.django-blue.svg?style=flat-square)](https://galaxy.ansible.com/list#/roles/832)

Ansible role whith setup Django projects.


#### Requirements & Dependencies

- [Stouts.wsgi](https://github.com/Stouts/Stouts.wsgi)


#### Variables

```yaml
---
# vim:sw=2:ft=ansible

django_enabled: yes                           # The role is enabled

django_manage_list:                           # List of commands which will be executed
  - collectstatic
  - syncdb
  - migrate

django_app_dir: "{{wsgi_app_dir}}"           # Path where manage.py is exists
django_etc_dir: "{{wsgi_etc_dir}}"           # Where place a configuration files
django_env_dir: "{{wsgi_virtualenv}}"        # Use virtualenv (set blank "" to disable)

# Generate local settings
django_settings_imports:
  - from .{{deploy_env|default("")}} import *
django_settings_module: main.settings.local
django_settings_dir: "{{django_app_dir}}/{{django_settings_module.split('.')[:-1]|join('/')}}"
django_settings: "{{django_settings_dir}}/{{django_settings_module.split('.')[-1]}}.py"
django_settings_additional: []                # List of strings to add Django settings
                                              # Ex. django_settings_additional:
                                              #       - DEBUG = True
                                              #       - URLCONF = 'urls'
django_settings_databases: []                 # List of databases to add Django settings
                                              # Ex. django_settings_databases:
                                              #       - default:
                                              #           NAME: test
                                              #           USER: test
                                              #           PASSWORD: test
django_settings_caches: []                    # List of cache backends to add Django settings
                                              # Ex. django_settings_caches:
                                              #       - default:
                                              #           BACKEND: django.core.cache.backends.locmem.LocMemCache
                                              #           KEY_PREFIX: my_own_prefix
```

Also see documentation for required roles bellow.


#### Usage

* Clone dependencies.
* Add `Stouts.django` to your roles
* Setup the role variables in your playbook file if needed

Example:

```yaml

- hosts: all

  roles:
    - Stouts.django

  vars:
    deploy_app_name: facebook
    django_manage_list:
      - syncdb
      - migrate
      - collectstatic
    django_settings_additional:
      - OPTION = "VALUE"
      - ANOTHER_OPTION = "{{ansible_var}}"
    django_settings_databases:
      - default:
          NAME: "{{deploy_app_name}}"
          USER: "{{deploy_app_name}}"
          PASSWORD: "{{deploy_app_name}}"

```

#### License

Licensed under the MIT License. See the LICENSE file for details.


#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.django/issues)!
