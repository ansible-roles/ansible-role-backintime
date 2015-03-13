Role configs examples
=====================

Extra packages installation
---------------------------

If you use this ansible role to install backintime to your Ubuntu Desktop, you may also need front-end package for Gnome. So your playbook may look like this:

```yml
vars:
  backintime_install:
    - backintime-common
    - backintime-gnome
roles:
  - { role: igor_mukhin.backintime, tags: backup }
```

Default variables usage example:

```yml
vars:
  # Delete old backups when free space < 10 Gb
  backintime_min_free_space_defaults: 10

  # Delete old backups when free inodes < 2%
  backintime_min_free_inodes_defaults: 10

  # Delete files older than 365 days
  backintime_remove_old_snapshots_defaults: 365

  backintime_profiles:
      # Profile name will be generated automatically
    - include:
        - /var/www
      path: /mnt/external/www-backup
      exclude:
        - .git
        - *~
      # This profile will be executed automatically on startup/shutdown
      # See `vars/main.yml` for more `const_*`
      automatic_backup_mode: "{{ const_backintime_automatic_backup_startup }}"

    - name: Backup configs
      include:
        - /etc/apache2/sites-available
        - /etc/php5/mods-available
      path: /mnt/external/configs-backup

      # Default exclude list `backintime_exclude_defaults`
      # will be used here as we dont specify `exclude` here

      # This profile will NOT automatically executed
      # (only manual via front-end, cli or cli via cron)
      # because `backintime_automatic_backup_mode_default`
      # is set to `const_backintime_automatic_backup_disabled`
      # at `defaults/main.yml` and not changed at this playbook

roles:
  - { role: igor_mukhin.backintime, tags: backup }
```
