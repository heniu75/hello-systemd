1. SAMPLE SHELL SCRIPT
1.1 Create a sample shell script to execute at startup:
run
  nano /home/hein/bin/echo_date_to_textfile

The contents of this file could be:
------------------------------------------------------------------------
#!/bin/sh
echo date > /home/hein/bin/a_text_file.txt
------------------------------------------------------------------------

Note that the script has the shebang line!

1.2 Make sure this file is executable
chmod +x /home/hein/bin/echo_date_to_textfile

2. Test the sample script

run
  sudo /home/hein/bin/echo_date_to_textfile

run
  ls -al /home/hein/bin

The output should be similar to
------------------------------------------------------------------------
hein@ubu-svr:~/bin$ ls -al
total 132
drwxrwxr-x  2 hein hein   4096 Jul 17 06:59 .
drwxr-xr-x 12 hein hein   4096 Jul 16 12:47 ..
-rw-rw-r--  1 hein hein      5 Jul 17 00:09 a_text_file.txt
-rwxrwxr-x  1 hein hein 116587 Jun 24 12:04 dropbox.py
-rwxrwxr-x  1 hein hein     53 Jul 17 06:59 echo_date_to_textfile
------------------------------------------------------------------------

2. SAMPLE SYSTEMD SERVICE
2.1 Create a sample service file
run
  sudo nano /etc/systemd/system/hello-systemd.service

The content should be similar to:
------------------------------------------------------------------------
hein@ubu-svr:~/bin$ cat /etc/systemd/system/hello-systemd.service
[Unit]
Description=Sample hello to systemd
After=network.target

[Service]
User=hein
WorkingDirectory=/home/hein/bin
ExecStart=/home/hein/bin/echo_date_to_textfile

[Install]
WantedBy=multi-user.target
------------------------------------------------------------------------

3. START AND ENABLE THE SERVICE
3.1 Reload the systemd daemon
  sudo systemctl daemon-reload

3.1 Start the service
  sudo systemctl start hello-systemd.service

3.2 Enable the service
  sudo systemctl enable hello-systemd.service
  sudo systemctl status hello-systemd

3.3 Reboot the system
  sudo shutdown -r now

3.4 Test that the script ran at startup
run
  cd /home/hein/bin
  ls -al

The content of the directory listing should show that the a_text_file.txt's
date and time stamp would have been updated.:
------------------------------------------------------------------------
hein@ubu-svr:~/bin$ ls -al
total 132
drwxrwxr-x  2 hein hein   4096 Jul 17 06:59 .
drwxr-xr-x 12 hein hein   4096 Jul 16 12:47 ..
-rw-rw-r--  1 hein hein      5 Jul 17 07:07 a_text_file.txt
-rwxrwxr-x  1 hein hein 116587 Jun 24 12:04 dropbox.py
-rwxrwxr-x  1 hein hein     53 Jul 17 06:59 echo_date_to_textfile
------------------------------------------------------------------------
