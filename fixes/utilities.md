# Utilities

### Crontab \(Mac OS X\)

When trying to add a command in crontab, you might get an error like:

```text
rsync: opendir "/Users/sdfsfdas/Downloads/WebsitesVisitedArchives" failed: Operation not permitted (1)
```

The comand needs to be added to Full Disk Access under System Preverences -&gt; Privacy -&gt; Full Disk Access. If you can't find a file like rsync when selecting the app under Full Disk Access, thry clicking Command-Shift-. to see hidden files.

Launchd probably is a better way of doing this, but here it is for now.

### Github Push

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



