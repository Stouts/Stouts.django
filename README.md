Stouts.django
=============

[![Build Status](https://travis-ci.org/Stouts/Stouts.django.png)](https://travis-ci.org/Stouts/Stouts.django)

Ansible role whith setup Django projects.


#### Requirements & Dependencies

- https://github.com/Stouts/Stouts.wsgi


#### Variables

```yaml
django_enabled: yes                           # The role is enabled
django_collectstatic: no                      # Run collectstatic on provision
django_migrate: no                            # Run migrations on provision
django_app_path: "{{base_source_directory}}"  # Path to django application
django_settings_imports:                    # List of requirements
  - from .{{base_environment}} import *
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
    base_project_name: facebook
    django_migrate: yes
    django_collectstatic: yes
    django_settings_additional:
      - OPTION = "VALUE"
      - ANOTHER_OPTION = "{{ansible var}}"
    django_settings_databases:
      - default:
          NAME: "{{base_project_name}}"
          USER: "{{base_project_name}}"
          PASSWORD: "{{base_project_name}}"

```

#### License

Licensed under the MIT License. See the LICENSE file for details.


#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.django/issues)!
