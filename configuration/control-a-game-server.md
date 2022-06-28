# Control A Game Server

{% hint style="info" %}
Please make sure your webserver user has access with a ssh key to the remote game-server.
{% endhint %}

{% hint style="info" %}
Replace everything between `<` and `>` e.g. _(\</path/to/web-server/> to /var/www/tracker)_
{% endhint %}

Go to the folder, create a file and give the webserver the correct permissions for the file.

```
cd </path/to/your/webapp>/html/server
touch <ServerID>.php
sudo chown <username>:<webserverusername> <ServerID>.php
sudo chmod 640 <ServerID>.php
```

**Now open the file and add all the lines and replace everything with your data.**

```php
<?php
$sip = 'example.com'; // IP or Domain of the game-server
$sport = 22; // SSH Port of the game-server
$susername = 'gameserver'; // User, who controls the server
$keypathpub = '/var/www/.ssh/idgsever_rsa.pub'; // Path to local ssh public key
$keypath = '/var/www/.ssh/idgsever_rsa'; // Path to local ssh private key
// Commands \\
$sstart = "./vhserver start"; // Command to start the server
$sstop = "./vhserver stop"; // Command to stop the server
$srestart = "./vhserver restart"; // Command to restart the server
$sbackup = "./vhserver backup"; // Command to back up the server
$supdate = "./vhserver update"; // Command to update the server
```

## See logs and live console&#x20;

**There are three ways, how to retrieve the logs from your external game-server.**

* SCP Copy
* Rsyslog
* Lightweight webserver on the remot machine

**SCP** is not recommended. It is the easiest to setup, though. If there are only one or two people watching the logs at the same time, you can use SCP without any doubt. If there are more than two or three users, at the same time, I wouldn't recommend using SCP for retrieving the live logs.\
**Rsyslog** is lightning fast and requires way less performance than using SCP. It's harder to setup though and I won't explain how to setup.\
**Webserver** is also fast. The webserver on the remote machine exposes the logs to the web, if the ip address matches with the set address. I recommend this way, as it is easy to setup and fast.

## Settings
