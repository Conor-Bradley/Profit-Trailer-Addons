# PtTracker - The ProfitTrailer Tracking Addon
PtTracker is a ProfitTrailer addon that uses the bot trading data (from the log file) to automatically track your daily and monthly profits in real time.

<b>Website: <a href="http://pttracker.net/?r=3" onclick="window.open(this.href); return false;" onkeypress="window.open(this.href); return false;">http://pttracker.net/</a></b>
  
<a href="https://ibb.co/nLjtox"><img src="https://preview.ibb.co/b8R68x/Screenshot_2018_02_06_12_30_41.jpg" alt="Screenshot_2018_02_06_12_30_41" border="0"></a>

<h1>FAQ</h1>
<b>Is my setup supported?</b> Yes, PtTracker will work on any operating system that ProfitTrailer supports.
<br><br>
<b>Will it work with the ProfitTrailer Feeder addon?</b> Yes, PtTracker does not make any changes to your setup or files.
<br><br>
<b>Are all base currencies are supported?</b> Yes, PtTracker will work on any base currencies that ProfitTrailer supports Ex. BTC, ETH, USDT and BNB.
<br><br>
<b>Are all exchanges are supported?</b> Yes, PtTracker will work on any extange that ProfitTrailer supports.
<br><br>
<b>Is my data safe?</b> Yes, PtTracker is simply an html file and works by reading the ProfitTrailerData.json file created by ProfitTrailer. Since this file only contains bot trading data, PtTracker is safe, secure, and does not access or use any api keys or other sensitive information.
<br><br>
<b>Can I use PtTracker on more than one bot/exchange?</b> Your PtTracker license key will work for as many bots as you want as long as they are on the same IP address. If you use bots on different machines, a license key will need to be purchased for each machine. (Note: Your license key has single user access. If you give it to someone else, your tracker will no longer work.)
<br><br>
<b>Is PtTracker officially endorsed by ProfitTrailer?</b> Not yet! However, we hope to make this happen soon. Hint hint @ProfitTrailer ;)
<br><br>
<b>Do you have any other questions?</b> Join our Discord and we will be happy to help you in the #pt-tracker-support channel! <b>Discord: <a href="https://discord.gg/FPXZVf" onclick="window.open(this.href); return false;" onkeypress="window.open(this.href); return false;">https://discord.gg/FPXZVf</a></b>


<h1 id="#purchasing">How To Purchase</h1>
1. Go to Website: <a href="http://pttracker.net/?r=3" onclick="window.open(this.href); return false;" onkeypress="window.open(this.href); return false;">http://pttracker.net/</a>
2. Click on "BUY NOW" button
3. Enter your email address and click next
4. Send the currency to the address provided
5. Sit back and wait for confirmations on the blockchain
6. Check your email for the files and licence key

<h1>How To Install and Configure PtTracker</h1>
1. Change trading.logHistory in the application.properties file in your ProfitTrailer folder to `trading.logHistory = 99999999` to prevent data removal:

2. Extract the PtTracker.zip and move all the files directly into your ProfitTrailer Folder (same directory as profittrailer.jar and application.properties)

3. Open PtTracker.json in your favorite text editor, add your username, license key, starting value, and any deposits and withdrawals then save and close the file.

	* <b>StartingValue</b> is the balance you started with when you first purchased the bot and is needed to calculate your current balance. If you do not update this, your balance will not be accurate. If you do not know your starting value you can put a number you think is close then once it is running there will be a fix button on the top right next to current value. Click this button and put your actual current value and it will tell you how much your starting balance was.

	* <b>Deposits/Withdrawls</b> can be added by editing the transfers section in PtTracker.json. Simple add the date (mm/dd/yyyy format) and a positive or negative value. (Do not add a comma to the last item or PtTracker will not work.)

		```
		"Transfers": {
		"01/07/2018": "0.06",
		"02/02/2018": "-0.02",
		"02/14/2018": "0.8"
		}
		```

<h1>Running PtTracker (Windows / Mac) </h1>
1. After installing PtTracker, <a href="https://cesanta.com/binary.html">Download Mongoose (Windows / Mac)</a> and place the executable file in your ProfitTrailer Folder.<br>
2. Open Mongoose (Double click executable file)<br>

<h2>Security</h2>
Mongoose is a standalone web server. It is reccomended to block port 8084 in your firewall for security

<h1>Running PtTracker (Linux)</h1>

1. Install Apache https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-16-04

2. Copy the PtTracker.html and PtTracker.json files to your web root (/var/www/html)

3. Copy the ProfitTrailerData.json file from PT folder to your webroot ```cp /home/profitTrailer/ProfitTrailerData.json /var/www/html/ProfitTrailerData.json```

4. Create a shell script to automatically copy your Profit Trailer data to web root: ```nano /var/scripts/getPtTrackerData.sh```

Add the following lines
```
#!/bin/sh
rm /var/www/html/ProfitTrailerData.json
cd /home/profitTrailer
cp /home/profitTrailer/ProfitTrailerData.json /var/www/html/ProfitTrailerData.json
cd /var/www/html
chown www-data:www-data /var/www/html/ProfitTrailerData.json
```

5. Setup crontab to run script every three minutes.<br>
Give full permission: ```sudo chmod a+x /var/scripts/getPtTrackerData.sh```<br>
Edit crontab: ```crontab -e command```<br>
Add a new line: ``` */3 * * * * /var/scripts/getPtTrackerData.sh```<br>

6. Access PtTracker at http://{YourIp}/PtTracker.html

<h2>Security</h2>
It is reccomended to add htaccess and htpassword for extra security. http://www.htaccesstools.com/articles/password-protection/

<h1>Running PtTracker (Raspberry Pi)</h1>
<h2>Python 2</h2>

Change directory into the ProfitTrailer folder using the command ```cd /path/to/your/ProfitTrailer```

Start up a Python web server using the command ```python -m SimpleHTTPServer 8084```

This will start a web server that hosts PtTracker, which will be made accessible through the following URL: http://localhost:8084/PtTracker.html OR http://{YourServerIp}:8084/PtTracker.html

This approach is built in to any Python installation.

<h2>Python 3</h2>
Do the same steps, but use the following command instead ```python3 -m http.server 8084```

<h2>Security</h2>
For extra security, you can block port 8084 in your firewall and add authentication using: https://github.com/tianhuil/SimpleHTTPAuthServer

<h1>Running PtTracker using your own web server (Any OS)</h1>

Configure your webserver to serve your ProfitTrailer folder as webroot directory locally.<br>
Access with: http://localhost/PtTracker.html<br>

<h1>Contact / Support</h1>
<a target="_blank" href="https://discord.gg/FPXZVf">Discord:</a> https://discord.gg/FPXZVf<br>
<a href="http://PtTracker.net" target="_blank">Website:</a> http://PtTracker.net

<h1>Donate</h1>
And let me know on discord or telegram if you do so I can thank you!<br>
BTC: 13EUZ5juobs1XfZW6Ad3QTkbhvchsKbbJN<br>
LTC: LbmkWmVP1npYtcZtW44Xq1SSGJsRCFZNvC<br>
ETH: 0xAcc1416387B7C3f9AF0E93A9583C95EB441dDD6