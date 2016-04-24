# Making syslog log to a remote server

You can simply edit the ``/etc/syslog.conf`` file and, wherever
``/var/adm/messages`` appears, duplicate the line and replace
``/var/adm/messages`` by ```@remoteSystem``` with remoteSystem being the
``IP`` address or ```hostname``` of the remote server where to send the
``logs``.

eg:

before:

```bash
*.err;kern.debug;daemon.notice;mail.crit    /var/adm/messages
```

after:

```bash
*.err;kern.debug;daemon.notice;mail.crit    /var/adm/messages
*.err;kern.debug;daemon.notice;mail.crit    @jaylogserver
```

Restart syslogd for the change to be taken into account:

```bash
adrian@openindiana-tuts:~$ sudo svcadm restart system-log
```

Note that the remote server must be configured to accept remote messages.
If on Solaris too, that would be done with this command:

```bash
:~$ sudo svccfg -s system-log setprop config/log_from_remote = true
:~$ sudo svcadm restart system-log
```

credit for these docs go to [/u/127b](https://www.reddit.com/user/127b)
