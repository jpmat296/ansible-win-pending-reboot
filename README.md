Ansible role: jpmat296.win_pending_reboot
=========================================

This role uses PowerShell module [PendingReboot](https://github.com/bcwilhite/PendingReboot) to
reboot Windows host if it has pending reboot.

Cause of pending reboot is by default explained by printing details given by `PendingReboot` module.

Requirements
------------

This role takes care of `PendingReboot` installation thanks to `win_psmodule` module. The
requirements of `win_psmodule` must be respected, including PowerShell upgrade to recent version.
See documentation here:

https://docs.ansible.com/ansible/latest/collections/community/windows/win_psmodule_module.html#id3

The easiest way to respect requirements is to use my role
[jpmat296.upgrade_powershell](https://github.com/jpmat296/ansible-upgrade-powershell). See
[playbook example](#example-playbook) below.

Role Variables
--------------

```
# Ansible execution log contains cause of pending reboot when 'true'
win_pending_reboot_explain: true
```

Explanation example
-------------------

When variable `win_pending_reboot_explain` is set to `true` (default), the role writes
the cause of pending reboot in Ansible log. Here is an example:

![pending reboot ansible trace](https://user-images.githubusercontent.com/12024504/103619695-7bdd6c80-4f32-11eb-831c-a5e6cd6aad66.png)

Dependencies
------------

No dependency. Use of role `jpmat296.upgrade_powershell` is optional.

Example Playbook
----------------

Here is an example of pending reboot check preceded by upgrade of powershell. Both are idempotent. They will do nothing if powershell is already upgraded and no reboot is pending.

    - hosts: servers
      tasks:
        - name: Upgrade Powershell & Windows Management Framework to 5.1
          import_role:
            name: jpmat296.upgrade_powershell
        - name: Reboot if reboot is pending
          import_role:
            name: jpmat296.win_pending_reboot

License
-------

BSD

Author Information
------------------

This role was created in last days of 2020 by
[Jean-Pierre Matsumoto](https://fr.linkedin.com/in/jpmatsumoto).
