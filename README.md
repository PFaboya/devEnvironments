# Dev environment

Dev environments are set up so that it is possible to use all the tools required to set up a web app and to easily transfer the product into a production environment

## Instructions

First thing to do is to download Vagrant which is a tool to build and managing virtual machine environment and virtual box which enables you to emulate an operating system on your own local machine.

Afterwards in the terminal run 'Vagrant init ubuntu/Xenial64'. Ubuntu/Xenial64 is a flavour of operating system and running Vagrant init grabs the operating system and runs it in the virtual machine environment.

Next is to run 'vagrant up' in the terminal, this runs the vagrant file that was created when running vagrant init previously. Immediately afterwards running 'vagrant ssh' on the terminal which will log into virtual box and enter into our dev environment. typing 'exit' will leave the dev Environment and go back into the host environment.

So those are instructions on how to enter and exit the virtual environment but there will need to be packages to be installed, a way to do this is to make a provisions file that contains all the necessary commands to install packages. in the vagrant file there will need to be a code linking towards the provisions.sh file:
config.vm.provision("shell", path: "environment/provisions.sh")

config.vm.provision("shell", path: "environment/provisions.sh")

In the provisions.sh file the following commands are tyed in to install packages:

sudo apt-get update -y

sudo apt-get upgrade -y

sudo apt-get install nginx -y

nginx is a web server that will display the app on a web browser. after node.js needs to be installed which is a javascript run time engine which executes javascript code outside of a browser. To install the node.js the following command is required in provisions.sh:

curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install nodejs -y

npm install pm2 -g

And finally to install pm2, a process manager for node.js. This enables the app to run forever and reload them without downtime which means updating the app will be easier:

cd /app

pm2 start app.js

With all this it should be possible to run the app in the development.local web address in port 3000.
