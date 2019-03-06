# Project_Linux_Configuration
Thir project in Udacity Full Stack Developer, where the 2nd project(item_catalog) is deployed to a linux server.
The server is hosted at Amazon lightsail, using Ubuntu 16.04.6 LTS instance

## server details
* ip address: 3.120.204.206
* url 3.120.204.206.xip.io

## server configuration
* The root user is disabled
* ssh with a private key is the only way to connect to the server
* grader account is created with private key content in Notes to Reviewer" field so the review can access the server.
* Grader account is added to sudoers.
* ssh port is changed to 2200
* password authentication is disabled
* server time is set to UTC.
* Allowed ports on firewall:
```
  1- Port 80 HTTP
  2- Port 123 NTP
  3- Port 2200/tcp (for ssh connection)
```
  
## Software installed
Apache2
mod-wsgi
Postgresql
psycopg2
python
pip
flask
sqlalchemy
oauth2client
werkzeug==0.8.3
Flask-Login==0.1.3

## Application Deployment

### 1- Virtual Host:
```
<VirtualHost *:80>
	ServerName 3.120.204.206
	ServerAlias 3.120.204.206.xip.io
	ServerAdmin admin@mywebsite.test
	WSGIScriptAlias / /var/www/project/catalog.wsgi
   	<Directory /var/www/project/>
        	Order allow,deny
        	Allow from all
    	</Directory>
   	 Alias /static /var/www/project/catalog/static
    	<Directory /var/www/project/catalog/static/>
        	Order allow,deny
        	Allow from all
    	</Directory>
    	ErrorLog ${APACHE_LOG_DIR}/error.log
    	LogLevel warn
		CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

```
### 2- Project files
project is in the following  directory /var/www/project/catalog

### 3- WSGI file

the wsgi fie is in the project folder and it's content as following:
```
	#!/usr/bin/python
	import sys
	import logging
	logging.basicConfig(stream=sys.stderr)
	sys.path.insert(0, "/var/www/project/")

	from catalog import app as application
	application.secret_key = 'secret key'
	
```

## Database

database installed is postgre
new user and db are created with name catalog with password: password

## References

Source: [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)
