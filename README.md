# ROLE dginhoux.prometheus_node_exporter



## DESCRIPTION

This ansible role install, configure and uninstall prometheus node exporter.<br />
It can be deploy as binary downloaded from github OR as docker (no public image, you have to build an image and push to a registry)



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
ansible-galaxy install dginhoux.prometheus_node_exporter
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.prometheus_node_exporter dginhoux.prometheus_node_exporter
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- hosts: all
  roles:
    - name: start role dginhoux.prometheus_node_exporter
      ansible.builtin.include_role:
        name: dginhoux.prometheus_node_exporter
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml
deploy_node_exporter: install
deploy_node_exporter_mode: binary
prometheus_node_exporter_docker_image: registry-cache.infra.ginhoux.net:5000/prom/node-exporter
prometheus_node_exporter_name: node_exporter
prometheus_node_exporter_version: 1.3.1
prometheus_node_exporter_arch: amd64
prometheus_node_exporter_download_url: >-
  https://github.com/prometheus/node_exporter/releases/download/
  v{{prometheus_node_exporter_version}}/
  {{prometheus_node_exporter_name}}-{{prometheus_node_exporter_version}}.
  linux-{{prometheus_node_exporter_arch}}.tar.gz
prometheus_node_exporter_bin_path: /usr/local/bin/{{prometheus_node_exporter_name}}
prometheus_node_exporter_options: ""
prometheus_node_exporter_state: started
prometheus_node_exporter_enabled: true
prometheus_node_exporter_port: 9100
prometheus_node_exporter_run_user: node_exporter
prometheus_node_exporter_nice_level: 0
```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

`NOT USED BY THIS ROLE`



## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
