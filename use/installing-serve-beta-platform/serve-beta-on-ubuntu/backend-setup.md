# Backend Setup

#### Install mysql server

```
sudo apt update  
(update package index)

sudo apt install mysql-server

systemctl is-active mysql
(To verify installation, should return active)

sudo systemctl start mysql.service
(To start mySQL)
```

\======================================================================

#### Change password of the sql server

```
open /etc/mysql/debian.cnf in vi and note down mysql username and password

mysql -u debian-sys-maint -p

sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password';
```

\======================================================================

#### Import sql file to mysql server

```
mysql -u root -p
create database servebeta;
use servebeta;
source <path to sql filename>;
```

\======================================================================

#### Setup Python mysql client connector

```
//Activate the virtual environment
cd /var/www/serve-beta/env

source bin/activate
cd /var/www/serve-beta/evd
----
pip install mysqlclient
sudo apt-get install python2-dev
sudo apt-get install libffi-dev
sudo apt-get install mysql-client
sudo apt-get install libmysqlclient
pip install mysql-connector-python
pip install pymysql
```

\======================================================================
