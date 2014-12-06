
Use Case
========
These units may be helpfull when setting up selenium grid on Fedora 20 or on CentOS/RHEL 7.

Install
=======
Run (or follow) the `setup-selenium` script to setup the selenium user on your system.  Then copy the units to /etc/systemd/system/ and reload:
```
systemctl daemon-reload
```

Next you will need to setup vncserver for the selenium user:
```
su - # switch to root
su - selenium
vncserver :1
# enter a password twice
vncserver -kill :1
# modify ~/.vnc/xstartup to use your favorite window manager
exit
exit
```

Run Standalone Selenium Server
==============================
To start the standalone selenium server execute
```
systemctl start selenium
```
Selenium standalone server should start at port 4444 and vncserver should start display :44.

If you have issues with twm replace it with openbox.


Run Selenium Grid
=================
```
systemctl start 'selenium.grid*'
```

Systemd units can be started by a pattern.

View Logs
=========
Journalctl can be used to view the log files for the services.
```
journalctl -f -u vncserver@\:44  # view the vncserver's log

journalctl -f -u selenium        # view standalone selenium server log

journalctl -f -u selenium.grid.hub

journalctl -f -u selenium.grid.node

journalctl -f -u 'selenium.grid*'     # view all selenium logs
```
