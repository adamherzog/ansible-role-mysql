mysql
=====

Install MySQL server and set up basic security. Manage databases and users.

 * Sets up mysql repository
 * Installs mysql server and client
 * Sets root password
 * Removes empty users and test database
 * Configures /etc/my.cnf
 * Configures /root/.my.cnf
 * Creates/removes databases
 * Creates/removes users
 * Enables daily mysqldump backups

Role Variables
--------------

 * mysql_root_password: ''
    Specifies the root password

 * mysql_databases: []
    Specifies a list of mysql databases to manage, with the following args:
        name: db1                    # required
        encoding: utf8               # optional
        collation: utf8_general_ci   # optional
        state: present               # optional

 * mysql_users: []
    Specifies a list of mysql users to manage, with the following args:
        name: user1                  # required
        host: localhost              # optional
        password: $3C43T             # required
        priv: '*.*:USAGE'            # optional
        state: present               # optional

 * mysql_daily_backup: no
    Determines whether a daily backup should be made automatically, via cron
    and mysqldump.

 * mysql_root_password: ''
    Specifies the mysql root user password.

Example Playbook
----------------

    - hosts: servers
      vars:
        mysql_databases:
         - name: db1
         - name: dbold
           state: absent
        mysql_users:
         - name: user1
           password: $3C43T
           priv: 'db1.*:ALL'
        mysql_daily_backup: yes
      roles:
         - { role: mysql }

