# Ansible Role : auto_pkg_updates

This role installs and configures packages to allow the server to perform automatic package updates.

- On Debian based systems this is done via the unattended-upgrades package.
- On RedHat 7 based systems this is done via the yum-cron package.
- On RedHat 8 based systems this is done via the dnf-automatic package.

This role was heavily influenced by Jeff Geerlings [Security](https://galaxy.ansible.com/geerlingguy/security) role.

## Requirements

None.

## Role Variables

### defaults/main.yml

    auto_pkg_updates_enabled: true

Should the automatic package updates be configured.

#### Settings for unattended-upgrades

    auto_pkg_updates_Blacklist: []

Paackages to exclude from updating.

    auto_pkg_updates_Reboot: "false"

Should the server reboot without confirmation.

    auto_pkg_updates_Reboot_Time: "03:00"

If automatice reboot is enabled then reboot at a specific time.

    auto_pkg_updates_Mail: ""

The email address to send for problems/package upgrades.

    auto_pkg_updates_MailOnlyOnError: true

Only send email when an error ocurs.

### vars/RedHat-7.yml

    __auto_pkg_updates_config_path: /etc/yum/yum-cron.conf

The full path and filename of the yum-cron configuration file.

    auto_pkg_updates_update_cmd: "security"

Sets the type of update to use.

    auto_pkg_updates_apply_updates: "yes"

Should updates be applied when they are available.

    auto_pkg_updates_service_name: "yum-cron"

The name of the service.

### vars/RedHat-8.yml

    __auto_pkg_updates_config_path: /etc/dnf/automatic.conf

The full path and filename of the dnf-automatic configuration file.

    auto_pkg_updates_upgrade_type: "security"

Sets the type of update to use.

    auto_pkg_updates_apply_updates: "yes"

Should updates be applied when they are available.

    auto_pkg_updates_service_name: "dnf-automatic.timer"

The name of the service.

## Dependencies

None.

## Example Playbook

    - hosts: servers
      vars_files:
        - vars/main.yml
      roles:
        - glillico.auto_pkg_updates

## License

MIT

## Author Information

This role was created in 2020 by Graham Lillico. (Inspired by [geerlingguy/ansible-role-security](https://github.com/geerlingguy/ansible-role-security)).
