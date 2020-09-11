# Utilities

## Crontab \(Mac OS X\)

When trying to add a command in crontab, you might get an error like:

```text
rsync: opendir "/Users/sdfsfdas/Downloads/WebsitesVisitedArchives" failed: Operation not permitted (1)
```

The comand needs to be added to Full Disk Access under System Preverences -&gt; Privacy -&gt; Full Disk Access. If you can't find a file like rsync when selecting the app under Full Disk Access, thry clicking Command-Shift-. to see hidden files.

Launchd probably is a better way of doing this, but here it is for now.

## Github Push

If we get the following error when trying to push:

```text
! [remote rejected] master -> master (push declined due to email privacy restrictions)
error: failed to push some refs to 'https://github.com/nickali/configs.git'
```

It's because 'Block command line pushes that expose my email' is checked under the [Security settings](https://github.com/settings/emails). Use the email provided under 'Keep my email addresses private' as username:

```text
$ git config user.email "<RANDOM_DIGITS>+<USERNAME>@users.noreply.github.com"
```

The -global flag can be added if you will be only using github repositories.

To continue the push:

```text
$ git commit --amend --reset-author
$ git push
```
## fail2ban: Failed during configuration: Have not found any log file for sshd jail

If you run into this when starting up fail2ban for the first time, it's probably because fail2ban isn't set up to work with systemd logging. I've run across this on images from cloud providers. To run agents that do logging and other sysadmin tasks, cloud providers will mess with expected functionality. 

To check systemd is logging your sshd calls, run the following:
```shell
$ journalctl -b -u ssh
```

If your output references ssh like:
```
Sep 11 18:59:03 main-server sshd[3798]: Server listening on :: port 22.
Sep 11 18:59:03 main-server systemd[1]: Started OpenBSD Secure Shell server.
Sep 11 18:59:14 main-server sshd[3812]: Accepted publickey for ubuntu from AB.CD.EF.GH port 61506 ssh2: RSA SHA256:qewQCU2iLEE5moFo7SMjQ0u28c77VERqET5q1471KYg
```

systemd is handling your ssh logs. 

Open up /etc/fail2ban/jail.local (which you should have copied from jail.conf).

Then search for 'backend' and you will probably find that it is set to 'backedn = auto'.

Change auto to 'systemd' (w/o quotes).

Restart fail2ban with ```sudo systemctl restart fail2ban```

Then run ```sudo fail2ban-client status sshd```

The output should look like:

```shell
status for the jail: sshd
|- Filter
|  |- Currently failed:	0
|  |- Total failed:	0
|  `- Journal matches:	_SYSTEMD_UNIT=sshd.service + _COMM=sshd
`- Actions
   |- Currently banned:	0
   |- Total banned:	0
   `- Banned IP list:
```

Note 'Journal matches' is now pointing to systemd. That's it.


