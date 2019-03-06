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
1- Virtual Host:
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
