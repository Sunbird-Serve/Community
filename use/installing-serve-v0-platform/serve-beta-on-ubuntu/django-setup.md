# Django Setup

\======================================================================

> _**Important: Do not use sudo once virtual env is activated as all the dependent lib need to be installed within the virtual environment.**_&#x20;

\======================================================================

**Install Django**



```
$ pip install django==1.4 django-mailer==0.1.0 pip south
```

#### Setup PEAK rules – required for some of the generic functions used in python.

```
$ cd PEAK-Rules-0.5a1.dev-r2686
$ python setup.py install
$ cd.. 
//navigate back to previous folder
```

\======================================================================

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

\======================================================================

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
