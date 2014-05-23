Stouts.django
=============

[![Build Status](https://travis-ci.org/Stouts/Stouts.django.png)](https://travis-ci.org/Stouts/Stouts.django)

Ansible role whith setup Django projects.


#### Requirements & Dependencies

- https://github.com/Stouts/Stouts.wsgi


#### Variables

```yaml
django_enabled: yes                           # The role is enabled
django_manage_list:                           # List of commands which will be executed
  - collectstatic
  - syncdb
  - manage
django_app_path: "{{deploy_source_dir}}"    # Path to django application
django_settings_imports:                    # List of requirements
  - from .{{deploy_environment}} import *
django_settings_module: main.settings.local
django_settings_directory: "{{django_app_path}}/{{django_settings_module.split('.')[:-1]|join('/')}}"
django_settings_path: "{{django_app_path}}/{{django_settings_module.replace('.', '/')}}.py"
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

Clone dependencies.
Add `Stouts.django` to your roles and change variables in your playbook file.
Example:

```yaml

- hosts: all

  roles:
    - Stouts.django

  vars:
    deploy_project_name: facebook
    django_manage_list:
      - syncdb
      - migrate
      - collectstatic
    django_settings_additional:
      - OPTION = "VALUE"
      - ANOTHER_OPTION = "{{ansible var}}"
    django_settings_databases:
      - default:
          NAME: "{{deploy_project_name}}"
          USER: "{{deploy_project_name}}"
          PASSWORD: "{{deploy_project_name}}"

```

#### License

Licensed under the MIT License. See the LICENSE file for details.


#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.django/issues)!
