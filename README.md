# AnonBoard
An application for anonymously discussing certain topics. This project is for a module in school.

# Installation

## Vagrant

Please install **all** of the following packages:

**Prequisites:**
* python3.5
* python-pip
* nodejs
* npm
* bower
* uwsgi
* systemd
* nginx
* postgres-server
* postgres-client

After you installed those packages clone the repository into `/usr/share/anonboard`:
```bash
$ git clone https://github.com:anehx/anonboard.git /usr/share/anonboard
```

Then change into the repositories directory and clone its submodules:
```bash
$ cd /usr/share/anonboard
$ git submodule init --update
```

After this (still in the repository) run the installation and create a database:
```bash
$ make setup
```

By now you should have [created a new postgresql database](http://www.postgresql.org/docs/9.1/static/manage-ag-createdb.html). So you can edit the settings in `/usr/share/anonboard/backend/anonboard/settings_production.py`:
```python
DATABASES = {
    'default': {
        'ENGINE':   'django.db.backends.postgresql_psycopg2',
        'NAME':     'anonboard', # Change this to your db name
        'USER':     'anonboard', # Change this to your db user
        'PASSWORD': '*********', # Change this to your db password
        'HOST':     'localhost'
    }
}
```

After you've done this you can run your first deploy and create a new user:
```bash
$ make deploy
$ DJANGO_SETTINGS_MODULE=anonboard.settings_production createsuperuser
```

You may have to change the server name and the SSL settings in your nginx config (`/etc/nginx/sites-enabled/anonboard.conf`).
Now you should be able to browse to http://yoururl.com/admin where you can login with your created superuser and configure the topics. The frontend is available at http://yoururl.com and the API at http://yoururl.com/api/v1.

# License
MIT - more [here](LICENSE)
