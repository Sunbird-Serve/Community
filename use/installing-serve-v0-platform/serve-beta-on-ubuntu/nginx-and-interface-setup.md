# Nginx and Interface Setup

#### Nginx Installation

```
sudo apt-get install nginx
sudo uwf app list
sudo uwf allow 'nginx http'
sudo uwf allow 'nginx https'
sudo uwf allow 'nginx full'
```

#### Certification Generation

```
sudo apt install certbot python3-certbot-nginx
update the conf file
sudo ln -s /etc/nginx/sites-available/domain_name /etc/nginx/sites-enabled/vidyasahyog.lotuspetalfoundation.org.conf
//restart nginx
sudo certbot --nginx -d domain_name
//restart nginx
//update the conf file and restart nginx again

//unlink the default conf file - 
sudo unlink /etc/nginx/sites-enables/default
sudo unlink /etc/nginx/sites-available/default
//restart nginx

permissions:
sudo chown -R www-data:www-data /var/www/serve-beta/*
sudo chmod -R 775 /var/www/serve-beta/
```
