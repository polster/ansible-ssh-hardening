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

### SSH-Key pair only

* Add the following lines to your Ansible playbook's role section in order to enable SSH-key based authentication only
* Ensure your server side users accept the SSH public key(s) before executing (not to lock you out via SSH)
```
roles:
    - role: ansible-ssh-hardening
      ssh_server_hardening: true
      sshd_password_auth: 'no'
      sshd_pubkey_auth: 'yes'
```

### SSH-Key pair with server side password

* Add the following lines to your Ansible playbook's role section in order to enable SSH-key pair with server side password based authentication
* Ensure your server side users accept the SSH public key(s) and the user passwords are set as well before executing (not to lock you out via SSH)
```
roles:
    - role: ansible-ssh-hardening
      ssh_server_hardening: true
      sshd_auth_methods: 'publickey,password'
```

### Allow different auth methods for different users

* In some situations it might be required to allow a different auth method to a specific user. E.g. a technical user where given by the tooling multi-auth-method is not being supported:
```
roles:
    - role: ansible-ssh-hardening
      ssh_server_hardening: true
      sshd_auth_methods: 'publickey,password'
      sshd_match_users:
         - { user: 'inventory', auth_method: 'publickey' }
```
* The role config above will create the following sshd configuration:
```
# Global auth methods for all users
AuthenticationMethods publickey,password
# Individual rules for user inventory
Match User inventory
    AuthenticationMethods publickey
Match all
```

## Configuration

### Defaults

See [defaults](defaults/main.yml)
