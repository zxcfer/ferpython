---
layout: post
title: "My favorite Tools for Daily Development"
tags: ["tools"]
---

## cmd

- Terminal

```bash
set term=xterm-256color
chcp 65001
cmd /k C:\bin\cmder_mini\vendor\init.bat
```

## JSON Tools

* [Json Explorer](https://json-smp8.onrender.com/)
* [Json as Table](http://json2table.com/)

## Compression 

- tar and zstd

```bash
tar --exclude={.git,node_modules} -cf poco.tar file1 dir1 file2 dir2
zstd poco.tar
zstd -d poco.tar 
```

- 7 Zip, rename `7zip.exe` to `zzip.exe`:

```bash
zzip a -t7z bkp.7z *.txt -mmt    # (-tgzip, -tzip, -tbzip2), (multithread)
zzip a bkp.7z *.txt -pP4SS
zzip e bkp.7z
zzip e bkp.7z -oC:\opt *.cpp -r  # recursive extract
```

- Lazyness again: I reamed Youtube downloader to a shorter name:

```bash
mv C:\bin\youtube-dl.exe C:\bin\zxc.exe
zxc -F http://www.youtube.com/watch?v=
zxc -f 140 http://www.youtube.com/watch?v=
zxc --extract-audio --audio-format mp3 https://www.youtube.com/watch?v=LMuu4h6RdyQ
```

## rclone

- https://github.com/rclone/rclone

```bash
rclone config create bkpmon dropbox [client_id = ] [client_secret = ]

~\.config\rclone
rclone sync bkpmon: /bkp   # download
rclone sync bkp bkpmon:    # sync upload
rclone copy /tmp/bkp bkpmon:/tmp    # only upload
```

- Sample **rclone.conf** file

```ini
[bkpmon]
type = dropbox
client_id = 
client_secret = 
token = {"access_token":"","token_type":"bearer","refresh_token":"","expiry":""}
```
