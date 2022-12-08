# Home Technology Journal

This document describes what I have done and what I am working related to the technology around the house at 513 S Randall.

# Topics

# Log
Reverse cronological notes. If a topic is ongoing, it should be extracted into its own document and linked above.

## docker-compose in vitl
*2022-12-08*

Trying to fix up vitl. Add docker-compose direct

https://gist.github.com/npearce/6f3c7826c7499587f00957fee62f8ee9


## More features for vitl
*2022-12-06*

There's a docker image that might be a nice way to run autossh, if that's what I need to do

```
https://github.com/sbaerlocher/docker.autossh
```

here's a full dev environment built as a docker container

```
https://github.com/akw/akw.github.io/blob/journals/journal/home-tech.md
```

vitl has problems running things in docker. But I think that is from the lack of all the directories mounted into the vitl. I'm hoping that mounting them all will solve those problems. 

- `/app`
- `/files`

The alternative is to make tools that are all to be run on the host. Is that even possible?

## autossh keeps closing
*2022-11-18*

`autossh` keeps closing. I found an [article](https://askubuntu.com/questions/217513/how-to-prevent-autossh-from-becoming-stuck-once-in-a-while) and I tried to update the command to prevent it from hanging up. I also put a command into `vitl`, my dev environment project.


## Eliminate media server?
*2022-11-08*

### Background

I think that one of the drives (photos) is dying and making a death rattle. I had bought a new drive and was just thinking that I would replace it. Then starting 11/7, it seems like I couldn't log into the server even after reboot. I've decided that since no one else really uses plex, I can move plex to my adaptus laptop and just sell the media server.

### Layout

Drive attached to office router:

- feature videos
- feature music

Media drive attached to laptop:

- photos
- home videos
- home music

Backup drive attached to laptop

- time machine backup of cindy's machine
- time machine backup of alex's laptop
- media drive backup
- feature music backup?

### Open questions

- maybe Cindy should have her own backup drive?
- OPTION: direct attached drive
  - PROS: less complicated. not dependent on me being preset for it to work. Time machine working as intended
  - CONS: would require unmounting drive every time before disconnecting power
- OPTION: set up an rsync on her documents. would require occassional full backup
  - PROS: backs up the most important part of cindy's files.
  - CONS: less standard technology
- OPTION: network time machine to a time capsule
  - PROS: standard technology
- OPTION: icloud backup

### Notes

Time capsule was discontinued. Networked time machine relies on another mac being present. I think we might need to do time machine on an interim basis and doing rsync maybe to a network drive or to alex's laptop.

*2022-11-17*

Okay, I've got a new backup drive and moved the photos and videos and I'm undecided about music and I've put them in the media drive and then started developing a launch daemon to run a script to run rsync to make sure the photo backup is up to date.

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<!-- https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html#//apple_ref/doc/uid/10000172i-SW7-BCIEDDBJ -->
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.adaptus.rsync-media</string>
    <key>ProgramArguments</key>
    <array>
        <string>touch</string>
        <string>/tmp/helloworld</string>
    </array>
    <key>StartCalendarInterval</key>
    <dict>
        <key>Minute</key>
        <integer>00</integer>
        <key>Hour</key>
        <integer>03</integer>
    </dict>
</dict>
</plist>
```

I have an rsync script that does the actual copy:

```
#!/bin/bash
sudo rsync -av --progress --delete /Volumes/Media-2022-11-11/ /Volumes/backup-Media-2012
# see what failed
#sudo rsync -av --dry-run --delete-after /Volumes/Media-2022-11-11/ /Volumes/backup-Media-2012
```

Now I'm also trying to reinstall the OS on the media machine so that I can disconnect it from the network and sell it. I want to attach the ssd to the router to try to have movies always available for running plex on the laptop to be able to watch them on the tv when we want to do that.

I also might want to add a drive to the router to support the time machine if that works.

I might want rsync to run on Cindy's machine or Fiona's to just get the documents stored somewhere safe.

