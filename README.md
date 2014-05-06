st.django
=========

[![Build Status](https://travis-ci.org/Stouts/st.django.png)](https://travis-ci.org/Stouts/st.django)

Ansible role whith setup Django projects.


#### Requirements & Dependencies

- https://github.com/Stouts/st.wsgi


#### Variables

```yaml
django_additional_settings: []                  # Additional Django settings
django_collectstatic: no                        # Run collect static
django_migrate: no                              # Run syncdb and migrations
django_settings_module: main.settings.local     # Path to symlink which generated settings
django_settings_directory: "{{base_source_directory}}/{{django_settings_module.split('.')[:-1]|join('/')}}"
django_settings_path: "{{base_source_directory}}/{{django_settings_module.replace('.', '/')}}.py"
```

Also see documentation for required roles bellow.


#### Usage

Clone dependencies.
Add `st.django` to your roles and change variables in your playbook file.
Example:

```yaml

- hosts: all

  roles:
    - st.django

  vars:
    base_project_name: facebook
    django_additional_settings:
      - OPTION = "VALUE"
      - ANOTHER_OPTION = "{{ansible var}}"
    django_migrate: yes
    django_collectstatic: yes

```

#### License

Licensed under the MIT License. See the LICENSE file for details.


#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/st.django/issues)!
