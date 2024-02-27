joenyland.off_site_backup
===================

[![CI](https://github.com/JoeNyland/ansible-off-site-backup-role/actions/workflows/ci.yml/badge.svg)](https://github.com/JoeNyland/ansible-off-site-backup-role/actions/workflows/ci.yml)

Sets up off-site backups using ZFS and Syncoid.

Requirements
------------

* SSH
* cron
* ZFS
* Sanoid

Role Variables
--------------

### `off_site_backup_tasks`

A list of hashes, representing each off-site backup task.

### `off_site_backup_user`

The user to create and use for off-site backups. This user will need ZFS permissions to allow backups.

The following permissions should be sufficient on the source host:

```
hold,send,snapshot,destroy
```

The following permissions should be sufficient on the destination host:

```
create,destroy,mount,receive,rollback
```

Dependencies
------------

Roles:

* joenyland.zfs
* joenyland.ssh
* joenyland.sanoid

Example Playbook
----------------

```yaml
- hosts: server,backup
  roles:
    - role: joenyland.off_site_backup
      vars:
        off_site_backup_tasks:
          - name: Off-site backup
            hour: 1
            minute: 0
            tasks:
              - source: syncoid@server:bpool
                destination: off-site/bpool
```

License
-------

MIT

Author Information
------------------

⌨️ with ❤️ by [Joe Nyland](https://joe.nyland.io)
