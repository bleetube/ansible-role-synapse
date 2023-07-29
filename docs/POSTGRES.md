# PostgreSQL

Here is an example using [anxs.postgresql](https://github.com/ANXS/postgresql)

Relevant `requirements.yaml` snippet:

```yaml
  - src: https://github.com/ANXS/postgresql
    name: anxs.postgresql
```
## Example Playbook

```yaml
  roles:
    - anxs.postgresql
```

## Example Variables

```yaml
postgresql_users:
  - name: synapse
    pass: "{{ lookup('ansible.builtin.env', 'synapse_POSTGRES_PASSWORD') }}"
    encrypted: yes
    state: present

postgresql_databases:
  - name: synapse
    owner: synapse
    state: present
```

In this example, there are two users because both `localhost` and `%` (all-hosts wildcard) are [mutually exclusive](https://stackoverflow.com/q/10823854/9290). I am also using environment variables to  separate secret stores from the repository.
