# Python Installation

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
