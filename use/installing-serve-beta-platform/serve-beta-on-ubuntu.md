# Serve Beta on Ubuntu

#### Python:

```
sudo apt install python2.7
```

Since the default python version is 3, change the default python version priority by following

```
$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1 
$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 2
$ sudo update-alternatives --config python
```

#### Clone Git Repo

```
cd /var
sudo mkdir www
cd www
sudo git clone https://github.com/Sunbird-Serve/serve-beta.git
```

\====================================================================

**Creating and Setting up of Virtual environment**&#x20;

Create virtual environment to install all the necessary applications and dependent libraries within the virtual environment.&#x20;

```
Check pip version: python -m pip --version

//If pip not installed, execute below commands
curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py
sudo python2 get-pip.py

//If pip version is not 20.3.4
sudo apt install python-pip 20.3.4
```

Create Virtual Environment

```
cd /var/www/serve-beta
sudo pip install virtualenv
sudo virtualenv env --python=python2.7
cd env
source bin/activate
```

\======================================================================

> _**Important: Do not use sudo once virtual env is activated as all the dependent lib need to be installed within the virtual environment.**_&#x20;

\======================================================================

**Install Django**



```
$ pip install django==1.4 django-mailer==0.1.0 pip south
```

Setup PEAK rules – required for some of the generic functions used in python.

```
$ cd PEAK-Rules-0.5a1.dev-r2686
$ python setup.py install
$ cd.. 
//navigate back to previous folder
```

**Install Remaining Packages**

```
$ pip install turbogears xlwt registration notification django-notification==0.2
django-social-auth==0.7.28 Pillow reportlab xhtml2pdf==0.2.4 html5lib==1.0b8 xlwt pisa

$ pip install django-registration==0.8 xlrd python-social-auth==0.2.14
$ pip install pydrive (If version error, then install rsa==4.0) (global)
$ pip install feedparser chronograph simplejson python-dateutil

$ pip install reportlab pypdf2 google-auth-oauthlib boto3~=1.16.57 python-dotenv
$ pip install django-cors-headers==0.11 pyfcm openpyxl redis
```

\=======================================================================

#### Backend Setup

Install mysql server

```
sudo apt update  
(update package index)

sudo apt install mysql-server

systemctl is-active mysql
(To verify installation, should return active)

sudo systemctl start mysql.service
(To start mySQL)
```

Change password of the sql server

```
open /etc/mysql/debian.cnf in vi and note down mysql username and password

mysql -u debian-sys-maint -p

sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password';
```

Import sql file to mysql server

```
mysql -u root -p
create database servebeta;
use servebeta;
source <path to sql filename>;
```

Setup Python mysql client connector

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

### Code Modification in the env folder

1\)      Navigate to the file - env/lib/python2.7/site-packages/notification/view.py

In this file at line 7 change feed to Feed

```
from django.contrib.syndication.views import Feed
```

2\)     Navigate to the file - env/lib/python2.7/site-packages/sx/pisa3/pisa\_util.py

In this file replace lines 55 to 57 with following

```
if not (reportlab.Version[:3]>="2.1"):
    raise ImportError("Reportlab Version 2.1+ is needed!")
REPORTLAB22 = (reportlab.Version[:3]>="2.1")
```

#### Nginx and Interface Setup

```
sudo apt-get install nginx
sudo uwf app list
sudo uwf allow 'nginx http'
sudo uwf allow 'nginx https'
sudo uwf allow 'nginx full'
```

Certification Generation

```
sudo apt install certbot python3-certbot-nginx
update the conf file
sudo ln -s /etc/nginx/sites-available/vidyasahyog.lotuspetalfoundation.org /etc/nginx/sites-enabled/vidyasahyog.lotuspetalfoundation.org.conf
restart nginx
sudo certbot --nginx -d vidyasahyog.lotuspetalfoundation.org
restart nginx
update the conf file and restart nginx again

unlink the default conf file - sudo unlink /etc/nginx/sites-enables/default
sudo unlink /etc/nginx/sites-available/default
restart nginx

permissions:
sudo chown -R www-data:www-data /var/www/serve-beta/*
sudo chmod -R 775 /var/www/serve-beta/
```
