# LCD_Test_Script

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
 ExecStart=/usr/bin/python3 /home/ubuntu/lcd/l1.py<br>
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
