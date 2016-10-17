Ansible role for SSH hardening
==============================

This role allows to harden an existing SSH server (sshd) supporting OSX/macOS as well.

## Prerequisites

* Add the role to the project's Ansible galaxy requirements file and install it via the ansible-galaxy command

## Supported Systems

See the [meta info](meta/main.yml) for more details related to the supported target systems.

## User Manual

### Minimal usage

* Add the following lines to your Ansible playbook's role section:
```
roles:
    - role: ansible-ssh-hardening
      ssh_server_hardening: true
```
* Please note that a very minimalistic hardening will be performed according to the [defaults](defaults/main.yml)

### SSH-Key pair with server side password

* Add the following lines to your Ansible playbook's role section in order to enable SSH-key pair with server side password based authentication
* Ensure your server side users accept the SSH public key(s) and the user passwords are set as well (not to lock you out via SSH)
```
roles:
    - role: ansible-ssh-hardening
      ssh_server_hardening: true
      sshd_auth_methods: "publickey,password"
      sshd_password_auth: "yes"
      sshd_pubkey_auth: "yes"
```

## Configuration

### Defaults

See [defaults](defaults/main.yml)
