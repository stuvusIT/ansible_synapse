# Ansible role for synapse, the Matrix reference homeserver

This role installs and configures [synapse](https://github.com/matrix-org/synapse).

## Example Playbook

The following is a minimal example playbook using this role.

```yml
- hosts: matrix-server01
  become: true
  roles:
    - role: synapse
      synapse_homeserver_config:
        # The content of the `homeserver.yaml` config file goes here.
      synapse_signing_key: ed25519 signing_key_name <censored>
```

## Configuration

At the very least the following two role variables are required.

* `synapse_homeserver_config`:
  The content of the `homeserver.yaml` config file goes here.
  You have to make yourself familiar with how to configure a synapse homeserver.
  A good place to start is this sample config:
  https://github.com/matrix-org/synapse/blob/develop/docs/sample_config.yaml
* `synapse_signing_key`:
  Secret base64-encoded ED25519 signing key.
  It can be generated using the python module
  [PyNaCl](https://pynacl.readthedocs.io/)
  as follows:

  ```bash
    $ python3 -c 'import nacl.signing; print("ed25519 signing_key_name {}".format(nacl.signing.SigningKey.generate().encode(encoder=nacl.encoding.Base64Encoder).decode()))'
  ```

  Hereby `signing_key_name` is the name of the key and can be chosen to your liking.

For further configuration options, see [role variables](#role-variables).

## Role variables

| Name                        | Default                 | Description                                    |
| :-------------------------- | :---------------------- | :--------------------------------------------- |
| `synapse_data_dir`          | `/etc/synapse`          | Directory to store config and database         |
| `synapse_homeserver_config` |                         | [#configuration](#configuration) |
| `synapse_install_dir`       | `/opt/synapse`          | Directory to store the synapse installation    |
| `synapse_log_config`        | See `defaults/main.yml` | Content of `<server_name>.log.config` |
| `synapse_signing_key`       |                         | [#configuration](#configuration) |
| `synapse_user`              | `synapse`               | The user running the synapse service           |
