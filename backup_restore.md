## VMs and Services
Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

## MySQL
Restore `MySQL` data from the backup:

    $ sudo -u backup bash -c "duplicity --no-encryption restore rsync://pavroto@backup.pavroto.ttu/mysql /home/backup/restore/mysql"
    $ sudo -u root bash -c "mysql agama < /home/backup/restore/mysql/agama.sql"

## InfluxDB
Restore `InfluxDB` data from the backup

    $ sudo -u backup bash -c "duplicity --no-encryption restore rsync://pavroto@backup.pavroto.ttu/influxdb /home/backup/restore/influxdb" 
    $ sudo systemctl stop telegraf
    $ influx -execute 'DROP DATABASE telegraf'
    $ sudo influxd restore -portable -database telegraf /home/backup/restore/influxdb
    $ sudo systemctl start telegraf

You may get next error:

    error updating meta: DB metadata not changed. database may already exist
    restore: DB metadata not changed. database may already exist

It's a known issue with InfluxDB restore, you can ignore these. Just make sure that telegraf database is restored correctly.