# Linux Server Configuration

by Philip Harms


## About

This project contains information about the ubuntu server hosted by me and its configurations.


## How to access

#### IP address:				54.93.243.128
#### SSH port: 				2200
#### URL:					http://ec2-54-93-243-128.eu-central-1.compute.amazonaws.com/

### 1. Download private key:
Get the private key supported in the instructor notes and save it to the ~/.ssh directory as, for example, 'lightsail'.
### 2. Connect via ssh:
In your terminal type 'ssh -i ~/.ssh/lightsail -p 2200 grader@54.93.243.128' to access the server via ssh on port 2200 as the user 'grader'.
### 3. Enter PW:
The password for the private key is 'SEE INSTRUCTOR NOTES'.

## Installed software

- Pip
- Virtualenv
- Apache2
- PostgreSQL

## Third-party resources

Besides the material provided by Udacity and helpful threads in the Udacity forums, I used the following tutorial to deploy
the Flask-Application on Ubuntu:
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps

## Summary of configurations made

In order to complete the setup of the Ubuntu server, I made the following configurations:

### Create new user "Grader" and give the permission to sudo
```
$ sudo adduser grader
$ sudo nano
$ sudo nano /etc/sudoers.d/grader
```
- add '''grader ALL=(ALL:ALL) ALL'''

### Set SSH login via Key
- Generate public and private key on local machine via ```ssh-keygen```, save to ~/.ssh
- In the ubuntu system:
``` 
$ su - grader
$ mkdir .ssh
$ touch .ssh/authorized_keys
$ nano .ssh/authorized_keys
- Copy in the content of the newly created public key
- Change permissions:
$ chmod 700 .ssh
$ chmod 644 .ssh/authorized_keys
```
### Update & Upgrade
```
$ sudo apt-get update && sudo apt-get upgrade
```
### Set Timezone to UTC
```
$ sudo dpkg-reconfigure tzdata
```
- Select "other options" then "UTC"

### Change SSH Port
```
$ sudo nano /etc/ssh/sshd_config
```
- change port from 20 to 2200
- go to the Amazon Lightsail "Networking"-Configuration and add port 2200 to the connections accepted by the Firewall

### Configure the UFW
```
$ sudo ufw allow 2200/tcp
$ sudo ufw allow 80/tcp
$ sudo ufw allow 123/udp
$ sudo ufw enable 
```
### Disable login for root user
- Run ```$ sudo nano /etc/ssh/sshd_config```
- Set PermitRootLogin to no

### Install apache2
```$ sudo apt-get install apache2```

### Deploy Flask App
- Follow the detailed instructions on https://goo.gl/CPZuh5
- Instead of the described FlaskApp, clone the directory of Project 3
- Change the name of the app.py to __init__.py
- Update the client_secrets.json file with the new IP and the server alias and update the location of the .json file in the app.py file

### Install PostgreSQL
```
$ sudo apt-get install postgresql
$ sudo su - postgres
$ psql
postgres=# CREATE DATABASE catalog;
postgres=# CREATE USER catalog;
postgres=# ALTER ROLE catalog WITH PASSWORD 'YOUR PASSWORD';
postgres=# GRANT ALL PRIVILEGES ON DATABASE catalog TO catalog;
```
### Restart Apache
```$ sudo service apache2 restart```
