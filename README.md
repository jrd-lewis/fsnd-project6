[logo]: https://udacity.com/favicon.ico "Udacity"
![udacity][logo] Project 6: Linux Server Configuration
====================================

## IP Address:
 - **54.71.235.138**
    - SSH Port: 2200

## URL:
 - **http://ec2-54-71-235-138.us-west-2.compute.amazonaws.com/**

## Software Installed:
 - **Apache**
    - `sudo apt-get install apache2`
 - **PostgreSQL**
    - `sudo apt-get install postgresql`
 - **GIT**
    - `sudo apt-get install git-all`
 - **Flask**
    - `sudo apt-get install python-pip`
    - `sudo pip install virtualenv`
    - `sudo virtualenv venv`
    - `source venv/bin/activate`
    - `sudo pip install Flask`
 - **Item Catalog**
    - `sudo git clone https://github.com/jslewis90/item-catalog.git /var/www/Catalog/`
    - Python Libraries      
      - `sudo apt-get install python-psycopg2`
      - `sudo pip install SQLAlchemy`
      - `sudo pip install --upgrade oauth2client`
      - `sudo pip install httplib2`
      - `sudo pip install werkzeug==0.8.3`
      - `sudo pip install flask==0.9`
      - `sudo pip install Flask-Login==0.1.3`
    - mod_wsgi
      - `sudo apt-get install libapache2-mod-wsgi`
      - `sudo nano /etc/apache2/sites-available/CatalogApp.conf`
      - `sudo a2dissite 000-default.conf`
      - `sudo a2ensite CatalogApp`
      - `sudo nano /var/www/html/catalogapp.wsgi`
      - `sudo apache2ctl restart`
    
## Configuration Changes:
 - **Grader User**
    - `sudo adduser grader`
    - `nano /etc/sudoers.d/grader`
      - `grader ALL=(ALL) PASSWD:ALL`
    - `cd /home/grader`
    - `mkdir .ssh`
    - `cd /root`
    - `cp authorized_keys /home/grader/.ssh/authorized_keys`
    - `cd /home/grader`
    - `chmod 700 .ssh`
    - `chmod 644 .ssh/authorized_keys`
    - `chown grader .ssh`
    - `chgrp grader .ssh`
    - `cd .ssh`
    - `chown grader authorized_keys`
    - `chgrp grader authorized_keys`
    - *Password:*
      - `BrFP7gUqJ`
 - **Disable Root Access**
    - `nano /etc/ssh/sshd_config`
      - `PermitRootLogin no`
      - `DenyUsers root`
 - **SSH Port**
    - `nano /etc/ssh/sshd_config`
      - `Port 2200`
    - `sudo /etc/init.d/ssh restart`
    - `sudo reboot`
 - **Firewall**
    - `sudo ufw default deny incoming`
    - `sudo ufw default all outgoing`
    - `sudo ufw allow 2200/tcp`
    - `sudo ufw allow ntp`
    - `sudo ufw allow www`
    - `sudo ufw enable`
 - **Update Packages**
    - `sudo apt-get update`
    - `sudo apt-get upgrade`
 - **UTC Timezone**
    - `sudo dpkg-reconfigure tzdata`
      - None of the above
      - UTC
 - **Catalog PostgreSQL User**
    - `sudo -i -u postgres`
    - `psql`
      - `createuser catalog`
      - `createdb catalog`
      - `\q`
   - `logout`
   - `sudo adduser catalog`
   - `sudo -i -u catalog`
   - `psql`
     - `\password`
       - `udacity`
     - `\q`
   - `logout`

## Third-party Resources Used:
 - **https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps**
