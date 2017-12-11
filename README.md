# AWS-Lightsail-Apache-server-on-Linux
Linux sever for project 6 for Udacity which uses AWS Lightsail to deploy the Catalog web application with postgresql from project 4 on Apache server and enforces key-based SSH authentication.

### IP 35.177.100.65
### SSH port 2200
### URL 35.177.65

## Technologies used

1.  [AWS Lightsail Ubuntu instance](https://lightsail.aws.amazon.com/)
     - set up rsa key from lightsail account in local machine
     - changed SSH port to 2200
     - configured ufw  
       -`sudo ufw default deny incoming`  
       -`sudo ufw default allow outgoing`   
       -`sudo ufw allow ssh`   
       -`sudo ufw allow 2200/tcp`   
       -`sudo ufw allow www`  
       -`sudo ufw allow 123/udp`   
       -`sudo ufw deny 22`  
     - configured timezone  
       -`sudo dpkg-reconfigure tzdata`
     - set up user grader and catalog with sudo permissions
   
2. Apache  `sudo apt-get install apache2`
    - Installed mod-wsgi to serve flask applications on Apache  
     `sudo apt-get install libapache2-mod-wsgi python-dev`
  
3. Postgresql `sudo apt-get install postgresql`
    - Created a new postgresql user with Create DB permissions

4. Git   `sudo apt-get install git`  
    - Cloned [https://github.com/16sheep/Catalog](https://github.com/16sheep/Catalog) to /var/www/catalog directory
      
5. Python, pip  
    `sudo apt-get install python-pip`  
    
6. Virtual Environment   `sudo apt-get install python-virtualenv`  
    - Created new virtualenv in  app directory /var/www/catalog/catalogproject  
    - Installed python packages  
    `pip install httplib2`  
    `pip install requests`  
    `pip install --upgrade oauth2client`  
    `pip install sqlalchemy`  
    `pip install flask`  
    `sudo apt-get install libpq-dev`  
    `pip install psycopg2`  
    `pip install flask-httpauth`  
  
7. Other fixes to the app  
    - Changed views.py line 27, adddata.py line 8 and modules.py line 106 to   
      `engine = create_engine('postgresql://catalog:PASSWORD_FOR_DATABASE_HERE@localhost/catalog')`  
    - Changed views.py line 22 to  
      `open('/var/www/catalog/catalogproject/client_secrets.json', 'r').read())['web']['client_id']`  
    - Changed views.py line 56 to  
     `oauth_flow = flow_from_clientsecrets('client_secrets.json', scope='')`  
    - Configured Google app again from [developer console](https://console.cloud.google.com/) and updated client.secrets.json  
    - Renamed views.py to __init__.py  
    
    

