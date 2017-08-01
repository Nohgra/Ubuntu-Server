# Linux Server Configuration

by Philip Harms


### About

This project contains information about the ubuntu server hosted by me and its configurations.


### How to access

IP address				54.93.243.128
URL						http://ec2-54-93-243-128.eu-central-1.compute.amazonaws.com/

1. Download private key:
Get the private key supported in the instructor notes and save it to the ~/.ssh directory as, for example, 'lightsail'.
2. Connect via ssh:
In your terminal type 'ssh -i ~/.ssh/lightsail -p 2200 grader@54.93.243.128' to access the server via ssh on port 2200 as the user 'grader'.
3. Enter PW:
The password for the private key is 'SEE INSTRUCTOR NOTES'.


### Third-party resources

Besides the material provided by Udacity and helpful threads in the Udacity forums, I used the following tutorial to deploy
the Flask-Application on Ubuntu:
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
