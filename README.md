# Ansible Role: sixteenone.user-create

This Ansible role creates and manages users on target systems. It provides functionality to create users, set passwords, manage SSH keys, configure sudo access, and control SSH settings.

## Requirements

- Ansible 2.9 or higher
- Target systems running a Unix-like operating system

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `user_create_users` | List of users to create or manage, see structure below |  |
| `user_create_disable_ssh_root` | Disable root login via SSH, boolean value | `false` |
| `user_create_disable_ssh_password` | Disable password authentication for SSH, boolean value | `false` |

### User Dictionary Structure

Each user in the `user_create_users` list can have the following properties:

| Property | Description | Default |
|----------|-------------|---------|
| `username` | User's login name | (Required) |
| `password` | User's password (will be hashed) | (Required) |
| `update_password` | When to update the password | `on_create` |
| `groups` | List of groups the user should belong to |  |
| `append` | Whether to append the user to groups or set groups exclusively |  |
| `shell` | User's login shell | `/bin/bash` |
| `state` | Whether the user should be present or absent | `present` |
| `uid` | User's UID |  |
| `system` | Whether the user should be a system user, hides from login screen |  |
| `admin` | Whether the user should have sudo access | `false` |
| `ssh_key` | Path to the user's SSH public key file | (Optional) |

## Dependencies

None.

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: sixteenone.user-create
      vars:
        user_create_users:
          - username: johndoe
            password: secretpassword
            groups: ['users', 'developers']
            admin: true
            ssh_key: /path/to/johndoe_id_rsa.pub
          - username: janedoe
            password: anothersecret
            shell: /bin/zsh
        user_create_disable_ssh_root: true
        user_create_disable_ssh_password: true
```


## License

MIT

## Author Information

This Role was created by [SixteenOne](https://twitter.com/sixteenone)