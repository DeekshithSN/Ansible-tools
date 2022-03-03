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

