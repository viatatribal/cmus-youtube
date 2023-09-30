# cmus-youtube
A patch that allows you to download youtube songs from cmus 

# What should I know before applying this patch?
This patch was created on an ubuntu distro with the following version: 

    $ lsb_release -a
    Distributor ID: Ubuntu
    Description:    Ubuntu 22.04.3 LTS
    Release:        22.04
    Codename:       jammy

Because of that, I can only say that if you are using the same distro, this patch may work on your computer. For any other distro or OS, I can't confirm anything as I don't have any of them to test it right now. If this patch works for your OS/distro, do tell me.  
Also, the cmus version used to create this patch was: 

    $ cmus --version
    cmus 1849b0a
    Copyright 2004-2006 Timo Hirvonen
    Copyright 2008-2016 Various Authors

# How to apply the patch
Place the file ytcmd.diff on your local cmus source code folder and apply it with: 

    git am ytcmd.diff

After that, compile cmus, start it and type ":yt youtube-link", where youtube-link is the link of the youtube video. 
yt-dlp will download the video, convert it to m4a and then add it to the playlist (technically, it adds the folder where the file was saved). 

# Dependencies
The patch requires the user to have yt-dlp installed on his computer. The version used when this patch was created was: 

    $ yt-dlp --version
    2023.07.06

# Some important stuff
This patch saves the audio file in a folder called /youtube at your home directory. If the folder doesn't exist, cmus will create it. However, if you want to use another directory, just change the following line: 

    char *dirname = xstrjoin(home_dir, "/youtube");

Also, if you want to save the audio file in a different format, change the following line: 

    snprintf(cmd, sizeof(cmd), "yt-dlp -P %s -x -S acodec:m4a %s", dirname, arg);

If you are unsure how yt-dlp extract the audio and what format it can use, just check the manpage for yt-dlp.

# Credits
This patch is based on [cmus youtube](https://github.com/invicnaper/cmus-youtube). Sadly that patch doesn't work anymore and I also removed many things I considered useless for my usercase.
