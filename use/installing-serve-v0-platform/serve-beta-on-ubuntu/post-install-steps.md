# Post Install Steps

#### Activate Environment

```
cd /var/www/serve-beta/env
source bin/activate
```

#### Interface Command

```
uwsgi --touch-reload=/var/www/serve-beta/evd/reload_uwsgi.ini --close-on-exec -s /tmp/uwsgi_evd.sock --chdir /var/www/serve-beta/evd/ --pp .. -w django_wsgi -C666 -p 32 -H /var/www/serve-beta/env --daemonize /tmp/uwsgi.log
```

#### Set Global sql mode

```
SET GLOBAL sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));
```

\
