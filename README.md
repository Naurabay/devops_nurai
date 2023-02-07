# devops_nurai
Devops django gunicorn 
CREATE DATABASE devops_nurai;
CREATE USER admin WITH PASSWORD 'password123';
ALTER ROLE admin SET client_encoding TO 'utf8';
ALTER ROLE admin SET default_transaction_isolation TO 'read committed';
ALTER ROLE admin SET timezone TO 'UTC';\
GRANT ALL PRIVILEGES ON DATABASE devops_nurai TO admin;
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'devops_nurai',
        'USER': 'admin',
        'PASSWORD': 'password123',
        'HOST': 'localhost',
        'PORT': '',
    }
}

main0PROfile

gunicorn --bind 0.0.0.0:8000 devops_o_nurai.wsgi

[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target

[Service]
User=nurai
Group=www-data
WorkingDirectory=/home/nurai/devops_nurai
ExecStart=/home/nurai/devops_nurai/venv/bin/gunicorn \
          --access-logfile - \
          --workers 3 \
          --bind unix:/run/gunicorn.sock \
          devops_o_nurai.wsgi:application
[Install]
WantedBy=multi-user.target