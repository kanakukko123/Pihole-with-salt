# Teamspeak3-server
This is my module to setup Teamspeak3-server and make a secure token for it. This project is a part of Tero Karvises course called palvelintenhallinta. [Tero Karvinen](https://terokarvinen.com/).

Teamspeak is a VoIP software where you can speak with people using servers. Teamspeak3 got its last stable update 3.1.10 on 4th of june 2016.
## The module
This module is made using ubuntu 20.04 LTS desktop.
## First I made it manually to see how it works
I used a manual I found online [https://www.hostinger.com/tutorials/how-to-make-a-teamspeak-3-server/](https://www.hostinger.com/tutorials/how-to-make-a-teamspeak-3-server/)

      $ cd /home/teamspeak/
      $ sudo wget https://files.teamspeak-services.com/releases/server/3.13.6/teamspeak3-server_linux_amd64-3.13.6.tar.bz2
      $ sudo tar xvf teamspeak3-server_linux_amd64-3.13.6.tar.bz2
      $ sudo rm teamspeak3-server_linux_amd64-3.13.6.tar.bz2
      $ cd teamspeak3-server_linux_amd64
      $ sudo mv * /home/teamspeak
      $ sudo rmdir teamspeak3-server_linux_amd64/

Now Teamspeak3-server should be installed and moved to /home/teamspeak/

Teamspeak3 needs me to accept a license so lets do that next.

      $ sudo touch .ts3server_license_accpeted

Now that the license has bee accepted we can create a teamspeak.service file to /lib/systemd/system/ so that we can manage the server.

      $ sudoedit /lib/systemd/system/teamspeak.service

![image](/pics/server.PNG)

Then we can start Teamspeak3

      $ sudo systemctl enable teamspeak.service
      $ sudo systemctl start teamspeak.service

Now we can check that is the service actually up.

      $ systemctl | grep teamspeak.service

We can see that the service is up and running.

![image](/pics/sstatus1.PNG)

And just to be sure we can run 

      $ systemctl status teamspeak.service

![image](/pics/sstatus2.PNG)

And everything seems to be working.

Now before we start Teamspeak we need to find the token for the first start of the server.

It is located in /home/teamspeak/logs which we dont have permission to acces but that is easily changed.

Now that we can acces it we can find the token.

![image](/pics/token.PNG)

Now that we got the token. We just need to load the server

      $ sudo wget https://files.teamspeak-services.com/releases/client/3.5.6/TeamSpeak3-Client-linux_amd64-3.5.6.run

And then we start teamspeak and use locahost as the server address and give the server its token.

![image](/pics/Ts1.PNG)

It works!

Now that we have made it manually we can make it into a salt module.
## Init.sls
Now that we have it working manually. Lets make it work on salt as a module. 

So I made /srv/salt/teamspeak directory and edited its init.sls

![image](/pics/init.PNG)

This file has it all. 

 * user.present creates the user teamspeak
 * commands under archive.extraced takes the command from Teamspeak3-server download page and gives it its source_hash. 
 * Next part takes and accepts the license so that we can run Teamspeak
 * Then we check that it is running and working well
 * Last part gives use the token so that we can get admin rights in the server

Now that we run the command:

      $ sudo salt-call --local state.apply teamspeak


![image](/pics/run.PNG)
![image](/pics/run2.PNG)

And it works. Now I will show you the live test of it.

## Sources

* [https://www.hostinger.com/tutorials/how-to-make-a-teamspeak-3-server/](https://www.hostinger.com/tutorials/how-to-make-a-teamspeak-3-server/)
* [https://www.teamspeak.com/en/downloads/#server](https://www.teamspeak.com/en/downloads/#server)
* [https://terokarvinen.com/](https://terokarvinen.com/)
