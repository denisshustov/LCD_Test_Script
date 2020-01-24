# LCD_Test_Script
<h2>
 16×2 LCD 1602a to raspberry pi 3
 </h2>
https://www.raspberrypi-spy.co.uk/2012/07/16x2-lcd-module-control-using-python/
<table><tbody><tr><td>LCD Pin</td><td>Function</td><td>Pi Function</td><td>Pi Pin</td></tr><tr><td>01</td><td>GND</td><td>GND</td><td>P1-06</td></tr><tr><td>02</td><td>+5V</td><td>+5V</td><td>P1-02</td></tr><tr><td>03</td><td>Contrast</td><td>GND</td><td>P1-06</td></tr><tr><td>04</td><td>RS</td><td>GPIO7</td><td>P1-26</td></tr><tr><td>05</td><td>RW</td><td>GND</td><td>P1-06</td></tr><tr><td>06</td><td>E</td><td>GPIO8</td><td>P1-24</td></tr><tr><td>07</td><td>Data 0</td><td></td><td></td></tr><tr><td>08</td><td>Data 1</td><td></td><td></td></tr><tr><td>09</td><td>Data 2</td><td></td><td></td></tr><tr><td>10</td><td>Data 3</td><td></td><td></td></tr><tr><td>11</td><td>Data 4</td><td>GPIO25</td><td>P1-22</td></tr><tr><td>12</td><td>Data 5</td><td>GPIO24</td><td>P1-18</td></tr><tr><td>13</td><td>Data 6</td><td>GPIO23</td><td>P1-16</td></tr><tr><td>14</td><td>Data 7</td><td>GPIO18</td><td>P1-12</td></tr><tr><td>15</td><td>+5V via 560ohm</td><td></td><td></td></tr><tr><td>16</td><td>GND</td><td></td><td>P1-06</td></tr></tbody></table>



<h2>
 Add service
</h2>
sudo touch /lib/systemd/system/lcd.service<br>
sudo nano /lib/systemd/system/lcd.service<br>
<br>
#--------------------content--------------------<br>
 [Unit]<br>
 Description=Lcd service on boot up<br>
 After=multi-user.target<br>
<br>
 [Service]<br>
 Type=idle<br>
 ExecStart=/usr/bin/python /home/ubuntu/lcd/l1.py<br>
 StandardOutput=syslog<br>
 StandardError=syslog<br>
 SyslogIdentifier=ServiceScript<br>
<br>
 [Install]<br>
 WantedBy=multi-user.target<br>
#--------------------content--------------------<br>
<br>
sudo chmod 644 /lib/systemd/system/lcd.service<br>
sudo systemctl daemon-reload<br>
sudo systemctl enable lcd.service<br>
<br>
sudo nano /etc/rsyslog.d/lcd.conf<br>
#--------------------content--------------------<br>
if $programname=='lcd' then /home/ubuntu/logs/lcd.log & stop<br>
#--------------------content--------------------<br>
<br>
sudo systemctl restart rsyslog<br>
sudo systemctl start lcd.service <br>
<br>
