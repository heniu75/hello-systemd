A service file should be placed in /etc/systemd/system
A service should have a .service extension
e.g. '/etc/systemd/system/hello-systemd.service'

A sample service file should look similar to:

------------------------------------------------------------------------
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

[Unit]
  -> Description -> Self explanatory
  -> After -> Describes that the unit should be actioned after the network is up

[Service]
  -> User -> The user to run the service as
  -> WorkingDirectory -> The working directory
  -> ExecStart -> The process / cmd line to execute

[Install]
  -> WantedBy -> The target to install this service into.
