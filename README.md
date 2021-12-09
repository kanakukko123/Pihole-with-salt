# Teamspeak3-server
This is my own module to setup a teamspeak server with salt to my windows 10 using saltstack master-slave. This project is a part of Tero Karvises course called palvelintenhallinta. [Tero Karvinen](https://terokarvinen.com/).

## The module
This module is made using ubuntu 20.04 LTS desktop.
## First I made it manually to see how it works
I used a manual I found online [https://www.hostinger.com/tutorials/how-to-make-a-teamspeak-3-server/](https://www.hostinger.com/tutorials/how-to-make-a-teamspeak-3-server/)

      $ cd /home/teamspeak/
      $ sudo wget https://files.teamspeak-services.com/releases/server/3.13.2/teamspeak3-server_linux_amd64-3.13.2.tar.bz2
      $ sudo tar xvf teamspeak3-server_linux_amd64-3.13.2.tar.bz2
      $ sudo rm teamspeak3-server_linux_amd64-3.13.2.tar.bz2
      $ cd teamspeak3-server_linux_amd64
      $ sudo mv * /home/teamspeak
      $ sudo rmdir teamspeak3-server_linux_amd64/
## Init.sls
Under work. It will create the user and the server and then make a password for it
