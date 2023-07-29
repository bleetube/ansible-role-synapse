# Ansible Role: synapse

Install Synapse server using upstream packages from the [matrix-org repositories](https://matrix-org.github.io/synapse/latest/setup/installation.html). It is intended to be composed with separate roles for Postgresql and a [web proxy](https://matrix-org.github.io/synapse/latest/reverse_proxy.html).

This role only installs `matrix-synapse` and stops short of configuring homeserver.yaml.

## Requirements

None.

## Role Variables

```yaml
synapse_name: example.com
synapse_domain: matrix.example.com
```
## Example Playbook

```yaml
- hosts: synapse
  become: true
  roles:
    - role: nginxinc.nginx_core.nginx
    - role: anxs.postgresql
    - role: bleetube.synapse
  tasks:
    - import_tasks: nginx_conf.yml
```

## Troubleshooting

```shell
tail -f /var/log/matrix-synapse/homeserver.log
```