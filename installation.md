# Installation

{% tabs %}
{% tab title="Use the installer" %}
### Use the installer

Copy this into your Terminal and press enter.

```bash
bash <(curl -s https://raw.githubusercontent.com/AunePVP/Game-Server-Query-and-Control-Center/main/install.sh)
```

Navigate with your arrow keys and press enter to submit. To focus `<Ok>` or `<Cancel>`, press tab.\
After completing all steps, move to [Web configuration.](https://github.com/AunePVP/Game-Server-Query-and-Control-Center/wiki/Installation#web-configuration)
{% endtab %}

{% tab title="Manual Installation Guide" %}
### Manual installation guide

{% hint style="info" %}
Replace everything between `<` and `>` e.g. _(\</path/to/web-server/> to /var/www/tracker)_
{% endhint %}

Make sure, you have everything required installed.

* Webserver `nginx -v` or `apache2 -v`
* PHP (7.4 or newer) `php -v`
* php-mbstring `php -m`
* Git `git --version`
* Mysql `mysql --version`

**Download and prepare the files.**

Download the latest release [here](https://github.com/AunePVP/Game-Server-Query-and-Control-Center/releases) and move it to your web server directory **or** use your terminal:

```shell
cd </path/to/web-server/>
```

```shell
git clone https://github.com/AunePVP/Game-Server-Query-and-Control-Center
```

Create a config file

```shell
echo "<?php" > Game-Server-Query-and-Control-Center/html/config.php
```

Set the correct permissions for the files

```shell
find Game-Server-Query-and-Control-Center -type d -exec chmod 770 {} \;
find Game-Server-Query-and-Control-Center -type f -exec chmod 640 {} \;
find Game-Server-Query-and-Control-Center/html/type/arkse/ -type f -exec chmod 660 {} \;
```

Determine the user the web server is running as. (most likely **www-data**) Give the web server access to the files and set the correct permissions for the config file.

```shell
sudo chown -R $USER:<webserverusername> Game-Server-Query-and-Control-Center
sudo chown <webserverusername>:$USER Game-Server-Query-and-Control-Center/html/config.php
sudo chmod 640 Game-Server-Query-and-Control-Center/html/config.php
```

If you don't want to run the web app in it's on directory (https://yourdomain.com/Game-Server-Query-and-Control-Center-1.0.0-alpha/index.php), move every file and directory into the current folder.

```shell
mv Game-Server-Query-and-Control-Center/* .
rm -r Game-Server-Query-and-Control-Center;
```

**Create database**

Log in to mysql

```shell
sudo mysql
```

Do you have a mysql user? If not:

```sql
CREATE USER <username>@localhost IDENTIFIED BY '<yoursecurepassword>';
```

Create the database. I called my database "tracker". You can use this name or use your own name.

```sql
CREATE DATABASE <DBName> /*\!40100 DEFAULT CHARACTER SET utf8 */;
```

Give permissions to access the database

```sql
GRANT ALL PRIVILEGES ON <DBName>.* TO '<username>'@'localhost';
FLUSH PRIVILEGES;
```

Create a table for the login/registration

```sql
USE <DBName>;
CREATE TABLE users (id INT auto_increment PRIMARY KEY AUTO_INCREMENT, username VARCHAR(100) NOT NULL, password VARCHAR(100) NOT NULL, server JSON NOT NULL);
```

Exit mysql

```sql
exit
```

After completing all steps, move to [Web configuration.](https://github.com/AunePVP/Game-Server-Query-and-Control-Center/wiki/Installation#web-configuration)
{% endtab %}
{% endtabs %}



### Web configuration

Go to your Webbrowser and type in your Domain/IP. If your website is stored in an extra directory as described earlier, add the directory name to your input. `https://yourdomain/<directoryname>` The website will automatically redirect you to the installation page.

Enter your Steam Web API Key, and your Database credentials. Test the connection. If the connection succeed, click on submit.

Now your going to create an admin user. Enter a secure password and click on submit. You get redirected to the start page.\
Click on _Login_ in the top right corner.

{% hint style="warning" %}
If you're trying to add a Minecraft Server and your server doesn't support the query protocol, use 0 as query port.
{% endhint %}

After logging in click on the user avatar in the top right corner and click on Server in in the left.\
Click on Add a server and fill out the form. If Rcon is disabled, use 0 as Rcon Port.

