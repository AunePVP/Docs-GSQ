# Game Server Console

{% hint style="warning" %}
Pleas make sure, you didnt skip the previous step!
{% endhint %}

**There are three ways, how to retrieve the logs from your external game-server.**

* SCP Copy
* Rsyslog
* Rsync

**SCP** is not recommended. It is the easiest to setup, though. If there are only one or two people watching the logs at the same time, you can use SCP without any doubt. If there are more than two or three users, at the same time, I wouldn't recommend using SCP for retrieving the live logs.\
**Rsyslog** is lightning fast and requires way less performance than using SCP. It's harder to setup though and I won't explain how to setup.\
**Rsync** is also fast. The website executes a shell script. The shell script checks, if the shell script is already running. If not, it will ask the remote machine every 3 seconds for the console-log. This is the fastest and my preferred methode.



{% hint style="info" %}
Don't forget to uncomment the lines, you edit.
{% endhint %}

<details>

<summary>SCP</summary>

Open the file from the last step

```
nano <ServerID>.php
```

Choose `scp` as logtype

```
$logtype = "scp"; // Choose scp, rsync or path
```

Set your scp command

```
$scpcommand = "cat <path/to/log/on/remote>"; //(cat log/console/vhserver-console.log
```

Save and close the file.

</details>

<details>

<summary>Rsyslog</summary>

**I won't explain how to setup Rsyslog**.&#x20;

Open the file from the last step

```
nano <ServerID>.php
```

Choose `path` as logtype

```
$logtype = "path"; // Choose scp, rsync or path
```

Set your log path

```
$logpath = "</path/to/console.log>";
```

Save and close the file.

</details>

<details>

<summary>Rsync</summary>

**I won't explain how to setup Rsyslog**.

Open the file from the last step

```
nano <ServerID>.php
```

Choose  `rsync` as logtype

```
$logtype = "rsync"; // Choose scp, rsync or path
```

Set the path, where rsync writes the log to

```
$rsynclogpath = "../../html/server/log/<log-name>"; 
```

Set the path to the log on the remote machine.

```
$rsyncremotelog = "/path/to/log/<log-name";
```

Don't forget to uncomment the other rsync related lines. (remove the #)

Save and close the file.

</details>

