# Utilities

### Crontab \(Mac OS X\)

When trying to add a command in crontab, you might get an error like:

```text
rsync: opendir "/Users/sdfsfdas/Downloads/WebsitesVisitedArchives" failed: Operation not permitted (1)
```

The comand needs to be added to Full Disk Access under System Preverences -&gt; Privacy -&gt; Full Disk Access. If you can't find a file like rsync when selecting the app under Full Disk Access, thry clicking Command-Shift-. to see hidden files.

Launchd probably is a better way of doing this, but here it is for now.

