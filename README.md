About
-----

Ansible role for install and configure backintime on Debian/Ubuntu.

Installation
------------

```bash
ansible-galaxy install igor_mukhin.backintime
```

Variables
---------

See defaults/main.yml and vars/main.yml to see all variables.

Usage Example
-------------

Minimal usage example:

```yml
vars:
  backintime_profiles:
    - include:
        - /var/www
        - /etc/php5
        - /etc/apache2
      path: /mnt/external/backup-directory

roles:
  - { role: igor_mukhin.backintime, tags: backup }
```

or

```yml
vars:
  backintime_path_default: /mnt/external/backup-directory
  backintime_profiles:
    - include:
        - /var/www
        - /etc/php5
        - /etc/apache2

roles:
  - { role: igor_mukhin.backintime, tags: backup }
```

More examples
-------------

Read [docs/EXAMPLES.md](https://github.com/ansible-roles/ansible-role-backintime/blob/master/docs/EXAMPLES.md) for more examples.

Also, you can read `templates/etc/backintime/config.j2` and [backintim-config man-page](http://manpages.ubuntu.com/manpages/utopic/man1/backintime-config.1.html) to know more about backintime configuration file.

Testing
-------

```bash
cd tests
vagrant up --provision
```

or

```bash
sudo ansible-playbook tests/playbook.yml -i tests/inventory -vvvv
```
