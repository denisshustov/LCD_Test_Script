# LCD_Test_Script

sudo touch /lib/systemd/system/lcd.service
sudo nano /lib/systemd/system/lcd.service

#--------------------content--------------------
 [Unit]
 Description=Lcd service on boot up
 After=multi-user.target

 [Service]
 Type=idle
 ExecStart=/usr/bin/python3 /home/ubuntu/lcd/l1.py
 StandardOutput=syslog
 StandardError=syslog
 SyslogIdentifier=ServiceScript

 [Install]
 WantedBy=multi-user.target
#--------------------content--------------------

sudo chmod 644 /lib/systemd/system/lcd.service
sudo systemctl daemon-reload
sudo systemctl enable lcd.service

sudo nano /etc/rsyslog.d/lcd.conf
#--------------------content--------------------
if $programname=='lcd' then /home/ubuntu/logs/lcd.log & stop
#--------------------content--------------------

sudo systemctl restart rsyslog
sudo systemctl start lcd.service 
