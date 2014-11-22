
Use Case
========
These are a collection of systemd units that run docker containers as a service.

Install
=======
Copy the units to /etc/systemd/system/ then execute
```
systemctl daemon-reload
```

To start the standalone selenium server execute:
```
systemctl start selenium-standalone
```
Selenium server runs at port 4444 and vncserver runs at port 5910.  The unit is configured such that the docker service will start if it's not already running.

You should be able to view the running tests with vncviewer:
```
vncviewer localhost::5910
```

Selenium's log can be viewed with journalctl:
```
journalctl -f -u selenium-standalone
```

On Fedora 20 you may need to add the `--privileged` flag to docker's run command in the unit file.
