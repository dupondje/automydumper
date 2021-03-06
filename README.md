Automydumper handles backups, retention and rotation for MySQL, Percona Server and Mariadb servers. It uses Mydumper under the hood.

### Configuring Automydumper

Configuration takes place in /etc/automydumper.cfg. 

### Running Automydumper

Running 'automydumper' ( or waiting for the cron ) is all you need to do to get an actual backup.
By default, backups are placed in /var/backups/automydumper/<YYYY-mm-dd>/<HH:ss>.

### Restoring backups

Restoring backups can be done either with myloader ( part of the mydumper package ), or by manually zcat'ing a table backup to mysql.
Please refer to the myloader man page for more details. Below are some of the mostly-used use-cases.

##### Restoring a full MySQL instance ( all databases, all tables ), overwriting existing tables:

myloader -d /var/backups/automydumper/2015-12-31/16:00 -o -v 3

##### Restoring a single database (db1), overwriting existing tables:

myloader -d /var/backups/automydumper/2015-12-31/16:00 -o -v 3 -s db1

##### Restoring a single table 't1' from database db1:

zcat /var/backups/automydumper/2015-12-31/16:00/db1.t1.sql.gz | mysql db1
