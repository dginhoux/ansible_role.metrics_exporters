# ROLE dginhoux.metrics_exporters



## DESCRIPTION

This ansible role install, configure and uninstall multiples prometheus exporters.<br />
Exporters can be deployed as binary OR as docker instance (binary-chroot and podman are planned).<br />
<br />
For binary deployment mode, it use, on the ansible controller a path where files are stored ; see `defaults/main.yml` you'll see a "tree" of mine.




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

The mains lists `metrics_exporters_lists` like described in ths variables sections must be defined and set ; There no defaults values.


#### EXAMPLE PLAYBOOK FOR DO EVERYTHING... IT JUST FOLLOW THE "metrics_exporters_lists"

```yaml
- name: Playbook
  hosts: all
  tasks:
    - name: Start role dginhoux.metrics_exporters
      ansible.builtin.include_role:
        name: dginhoux.metrics_exporters
```

#### EXAMPLE PLAYBOOK FOR JUST INSTALL "node_exporter" AND LET DEPLOY MODE LIKE SPECIFIED IN "METRICS_EXPORTERS_LISTS"

```yaml
- name: Playbook
  hosts: all
  tasks:
    - name: Metrics exporters
      vars:
        metrics_exporters_force_state: present
        metrics_exporters_limit_list:
          - node_exporter
      ansible.builtin.include_role:
        name: dginhoux.metrics_exporters
```

#### EXAMPLE PLAYBOOK FOR JUST INSTALL "node_exporter" AND FORCE DEPLOY MODE "docker"

```yaml
- name: Playbook
  hosts: all
  tasks:
    - name: Metrics exporters
      vars:
        metrics_exporters_force_state: present
        metrics_exporters_force_deploy: docker
        metrics_exporters_limit_list:
          - node_exporter
      ansible.builtin.include_role:
        name: dginhoux.metrics_exporters

```

## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml`

#### EXAMPLES METRICS_EXPORTERS_LISTS

Theses lists are used to specify wich exporters are useds, deploy mode is set here and common option too.


```yaml
metrics_exporters_list:
  - name: node_exporter
    version: v1.7.0
    platform: linux_amd64
    deploy: docker
    state: present
    cfg_files: []
      # - dest: /tmp/1.cfg
      #   src: ""
      #   content: ""
      #   mode: "0755"
      #   owner: root
      #   group: root
    # install_path: /usr/local/bin
    docker_published_ports:
      - 9100:9100
    docker_volumes:
      - /sys:/host/sys:ro
      - /proc:/host/proc:ro
      - /:/host:ro
    options:
      - "--web.listen-address=:9100"
      - "--web.telemetry-path=/metrics"
      - "--web.disable-exporter-metrics"
      - "--web.max-requests=20"
      - "--log.level=warn"
      - "--log.format=logfmt"
      - "--collector.disable-defaults"
      - "--collector.arp"
      - "--no-collector.bcache"
      - "--no-collector.bonding"
      - "--no-collector.btrfs"
      - "--no-collector.buddyinfo"
      - "--collector.conntrack"
      - "--collector.cpu"
      - "--no-collector.cpu.guest"
      - "--no-collector.cpu.info"
      - "--no-collector.cpufreq"
      - "--collector.diskstats"
      - "--no-collector.dmi"
      - "--no-collector.drbd"
      - "--no-collector.drm"
      - "--no-collector.edac"
      - "--collector.entropy"
      - "--no-collector.ethtool"
      - "--no-collector.fibrechannel"
      - "--collector.filefd"
      - "--collector.filesystem"
      - "--no-collector.hwmon"
      - "--no-collector.infiniband"
      - "--no-collector.interrupts"
      - "--collector.ipvs"
      - "--no-collector.ksmd"
      - "--collector.lnstat"
      - "--collector.loadavg"
      - "--collector.logind"
      - "--no-collector.mdadm"
      - "--collector.meminfo"
      - "--no-collector.meminfo_numa"
      - "--collector.mountstats"
      - "--collector.netclass"
      - "--collector.netdev"
      - "--collector.netstat"
      - "--collector.network_route"
      - "--collector.nfs"
      - "--collector.nfsd"
      - "--collector.ntp"
      - "--collector.ntp.server=127.0.0.1"
      - "--collector.ntp.server-is-local"
      - "--no-collector.nvme"
      - "--collector.os"
      - "--no-collector.perf"
      - "--no-collector.powersupplyclass"
      - "--no-collector.pressure"
      - "--no-collector.processes"
      - "--no-collector.qdisc"
      - "--no-collector.rapl"
      - "--no-collector.runit"
      - "--collector.schedstat"
      - "--collector.sockstat"
      - "--collector.softnet"
      - "--collector.stat"
      - "--no-collector.supervisord"
      - "--no-collector.systemd"
      - "--no-collector.tapestats"
      - "--collector.tcpstat"
      - "--no-collector.textfile"
      - "--no-collector.thermal_zone"
      - "--collector.time"
      - "--collector.timex"
      - "--collector.udp_queues"
      - "--no-collector.uname"
      - "--collector.vmstat"
      - "--no-collector.wifi"
      - "--collector.xfs"
      - "--no-collector.zfs"
      - "--no-collector.zoneinfo"

  - name: process_exporter
    version: "0.7.10"
    platform: linux_amd64
    deploy: binary
    state: present
    cfg_files:
      - dest: /etc/process_exporter.cfg
        # src: ""
        content: |
          ---
          process_names:
            # - name: group_glusterfs
            #   exe:
            #     - glusterfs
            # - name: group_ssh
            #   exe:
            #     - sshd
            #     - ssh
            # - name: group_pxe
            #   exe:
            #     - dhcpd
            #     - in.tftpd
            #     - nginx
            # - name: group_docker
            #   exe:
            #     - docker
            #     - dockerd
            #     - containerd
            # - name: "\{\{.Comm\}\}"
            #   cmdline:
            #     - ".+"
            - name: all
              cmdline:
              - '.+'
        mode: "0755"
        owner: root
        group: root
    install_path: /usr/local/bin
    # docker_published_ports:
    #   - 9256:9256
    # docker_volumes:
    #   - /etc/process_exporter.cfg:/etc/process_exporter.cfg:ro
    #   - /proc:/host/proc:ro
    options:
      - "--children"
      - "--threads"
      - "--procfs=/host/proc"
      - "--config.path=/etc/process_exporter.cfg"
      - "--web.listen-address=:9256"
      - "--web.telemetry-path=/metrics"

metrics_exporters_list_group: []
metrics_exporters_list_host: []
```

NOTE : Theses 3 lists `metrics_exporters_list`, `metrics_exporters_list_group` and `metrics_exporters_list_host` are merged. <br />
You can use the `_host` and `_group` lists to specify per host and/or per group content.




#### EXAMPLES METRICS_EXPORTERS_SPECS

This dict is a system oriented dict, it is used to store and define for each exporter it's own information for deployment.


```yaml
metrics_exporters_specs:
  node_exporter:
    nice_level: 0
    run_user_name: node_exporter
    run_user_uid: 1700
    deploy:
      binary:
        executable: node_exporter
        bin_files:
          - src: node_exporter
            dest: node_exporter
            mode: "0755"
            owner: root
            group: root
      docker:
        specs:
          # user: ""
          privileged: false
          pid_mode: host
          network_mode: host
          restart_policy: unless-stopped
          cpus: "0.15"
          memory: 128m
        images:
          linux_amd64:
            docker_image: registry-cache.infra.ginhoux.net:5000/prom/node-exporter
          linux_arm64:
            docker_image: registry-cache.infra.ginhoux.net:5000/prom/node-exporter

  process_exporter:
    nice_level: 0
    run_user_name: root
    run_user_uid: 0
    deploy:
      binary:
        executable: process-exporter
        bin_files:
          - src: process-exporter
            dest: process-exporter
            mode: "0755"
            owner: root
            group: root
      docker:
        specs:
          # user: ""
          privileged: false
          pid_mode: host
          network_mode: host
          restart_policy: unless-stopped
          cpus: "0.15"
          memory: 128m
        images:
          linux_amd64:
            docker_image: ncabatoff/process-exporter
          linux_arm64:
            docker_image: ncabatoff/process-exporter
```


#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

`NOT USED BY THIS ROLE`



## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
