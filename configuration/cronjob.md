# Cronjob

In order to retreive historical data (player count, uptime...) you need to setup a [cronjob](https://en.wikipedia.org/wiki/Cron).

{% hint style="info" %}
Replace \</path/to/directory> with the path to the directory, where the web-app is operating at.
{% endhint %}

Setting up a cronjob is as easy as a pie. In your shell type: `crontab -e` and append this line to the end of the file, that just opened.

```
*/10 * * * * cd </path/to/directory>/query/&& php -f cron.php > /dev/null 2>&1
```

Close the file. Now every 10 minutes, the cronjob executes a php script, which queries every game-server and stores the needed information as a json inside a file.\
