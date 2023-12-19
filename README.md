# ROLE dginhoux.metrics_exporters



## DESCRIPTION

This ansible role install, configure and uninstall prometheus exporters.<br />
It can be deploy as binary OR as docker instance.



## REQUIREMENTS

#### SUPPORTED PLATFORMS

| Platform | Versions |
|----------|----------|
| Debian | all |
| EL | all |
| Fedora | all |
| Ubuntu | all |

#### ANSIBLE VERSION

Ansible >= 2.13

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.metrics_exporters
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.metrics_exporters dginhoux.metrics_exporters
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- name: Playbook
  hosts: all
  roles:
    - name: Start role dginhoux.metrics_exporters
      ansible.builtin.include_role:
        name: dginhoux.metrics_exporters
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml

```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

`NOT USED BY THIS ROLE`



## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
