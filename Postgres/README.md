![image](https://user-images.githubusercontent.com/29688323/156474260-1ffb7446-d6dd-4a73-bbec-30789a8d63f8.png)


### Install Postgres 
-----------------
- apt-get update -y && apt-get install wget -y 
- wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
- sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -sc)-pgdg main" > /etc/apt/sources.list.d/PostgreSQL.list'
- apt-get -y update
- apt-get install python3-psycopg2 python3-pip openssl python3-disutils postgresql-10 postgresql-10-prefix postgres-contrib -y 
- systemctl restart postgresql


for more info - https://www.liquidweb.com/kb/install-and-connect-to-postgresql-10-on-ubuntu-16-04/

### Configuring as master 
-------------------

- change the configs in /etc/postgresql/10/main/postgresql.conf

```
listen_addresses = "*"
wal_level = hot_standby
synchronous_commit = local
synchronous_standby_name = '2(slave1,slave2)'
archive_mode = on
archive_command = 'cp -i %p /var/lib/postgresql/10/main/archive/%f'
max_wal_senders = 3
wal_keep_segments = 64
```

- create archive directory /var/lib/postgresql/10/main/archive & change the permission

```
mkdir -p /var/lib/postgresql/10/main/archive
chmod 700 /var/lib/postgresql/10/main/archive
chown -R postgres:postgres /var/lib/postgresql/10/main/archive
```

- execute below commands for login into psql and create replica user 

```
su - postgres
psql
CREATE USER replica REPLICATION LOGIN ENCRYPTED PASSWORD 'replica';
\q
ctrl d
```

- allow egress request in postgres and add entry to slave in /etc/postgresql/10/main/pg_hba.conf

```
host    all all 0.0.0.0/0 md5
host   replication replica slave_ip/24 md5

```

### Configuring slave 
-------------------
