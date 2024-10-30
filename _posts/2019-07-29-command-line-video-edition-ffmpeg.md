---
layout: post
title: "Video Command Line Edition with FFMPEG"
tags: ["ffmpeg", "cli"]
---

* Download [executable](http://ffmpeg.zeranoe.com/builds/) and put in your PATH.

## Exctract MP3

```bash
ffmpeg -i __IN__ -vn -ar 44100 -ab 192k -ac 2 -f mp3 __OUT__.mp3
ffmpeg -i __IN__ -vn -ar 44100 -ab 128k -y __OUT__.mp3
ffmpeg -i __IN__.ogg -acodec libmp3lame __OUT__.mp3
```

## Create gif from Video, image magic

```bash
ffmpeg -i video%05d.png video.avi
convert video.gif video%05d.png
```

## Create video from images

```bash
ffmpeg -f image2 -i image%d.jpg video.mpg
convert 'images.gif[0]' image.png
```

## Remove audio

```bash
ffmpeg -i %in% -vcodec copy -an %out% 
```

## Join video and audio

```bash
ffmpeg -i video.mp4 -i audio.m4a -c:v copy -c:a aac output.mp4
```
