# Installation Guide

> This is an installation guide for serve beta version.&#x20;
>
> **Versions**: Python Version - 2.7.18
>
> &#x20;                pip version - 20.3.4
>
> Don't copy-paste the `$` signs, they indicate that what follows is a terminal command

**Initial Installation and Code Setup**

* Download and Install Visual Studio Code or any code editor **** from [here ](https://code.visualstudio.com/download)
*   Clone the git repo directly to VS code editor.

    Open VS code editor window, select the source control from the left hand side corner.

    Select “Clone Repository” and provide the git repo url mentioned [here](https://github.com/Sunbird-Serve/serve-beta.git).&#x20;
* Download and Install python 2.7 version [here](https://www.python.org/downloads/release/python-2717/).&#x20;

\====================================================================

**Creating and Setting up of Virtual environment**

Create virtual environment to install all the necessary applications and dependent libraries within the virtual environment.&#x20;

Open the terminal in VS Code

```
$ pip install virtualenv
$ virtualenv env --python=python2.7
$ cd env
$ \Scripts\activate

//The virtual environment is now activated. 
```

\======================================================================

**Install pip and Django**

Check pip version: python -m pip --version

If the pip version is not 20.3.4 then upgrade the version to 20.3.4

If pip is not installed, install pip by the below command.&#x20;

```
$ apt install python-pip 20.3.4
```

Install Django:

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

**Database Setup**

Download mysql package and install [here](../capabilities/demand.md).&#x20;

start mysql server and connect to localhost instance - Mysql@localhost:3306

Once connected, within the Administration tab select “Data Import/Restore” .

Select Import from the self contained file and provide the path for the .sql file.

Within the default target schema, create a new schema and select the new schema as the target db.

Select ‘Start Import’

.sql file is now imported to new db with all the tables and data.

.sql file is provided in the github repo.&#x20;

Install python packages to mysql

```
$ pip install mysqlclient mysql-connector-python pymysql
```

### Code Modification is the env folder

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

### Execute the Application

Edit the local\_settings.py and .env file with the database name given and the password.

```
python manage.py runserver --settings=local_settings
```
