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
    - role: bleetube.ntfy
  tasks:
    - import_tasks: nginx_conf.yml
```

## Android Notifications

The [ntfy role](https://github.com/bleetube/ansible-role-ntfy) is recommended. To enable your own self-hosted push notifications with Matrix, install [ntfy-android](https://ntfy.sh/) and set your ntfy url as default server in ntfy-android. Then restart your matrix app.

## Troubleshooting

```shell
tail -f /var/log/matrix-synapse/homeserver.log
```