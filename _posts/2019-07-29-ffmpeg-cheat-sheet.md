---
layout: post
title: "Video Command Line Edition with FFMPEG"
tags: ["ffmpeg", "CLI"]
---

* Download [.exe](http://ffmpeg.zeranoe.com/builds/)

## Exctract MP3

```bash
ffmpeg -i __IN__ -vn -ar 44100 -ab 192k -ac 2 -f mp3 __OUT__.mp3
ffmpeg -i __IN__ -vn -ar 44100 -ab 128k -y __OUT__.mp3
ffmpeg -t 30 -i __IN__.mp3 -acodec copy __OUT__.mp3
ffmpeg -t 52.07 -i amigos.mp3 -acodec copy .mp3
ffmpeg -i __IN__.ogg -acodec libmp3lame __OUT__.mp3
```

## Create gif from Video, image magic

```bash
convert some.gif some%05d.png
ffmpeg -i some%05d.png some.avi
rm some*.png
```

## Create video from images

```bash
ffmpeg -f image2 -i image%d.jpg video.mpg
convert 'images.gif[0]' image.png
```

```
set FOLDER=C:\Users\user\Downloads\Telegram Desktop\fun
set IMAGE=ss2
magick.exe "%FOLDER%\%IMAGE%.png" -resize 50% "%FOLDER%\%IMAGE%_50.jpg"
```

# remove audio

```
ffmpeg -i %in% -vcodec copy -an %out% 
```