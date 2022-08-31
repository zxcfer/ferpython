---
layout: post
title: "Command Line Image Edition"
tags: ["image edition", "cli"]
---

## Image magick

```bash
magick img.jpg -brightness-contrast 10x20 img.jpg
magick img.jpg -background white -page a4 doc.pdf
magick img.jpg -rotate 270 -resize 70% -background white -page a4 doc.pdf
magick img.jpg -rotate 270 -background white -page a4 doc.pdf
magick img.jpg -background white -page a4 -gravity center croquis.pdf
```

- Resizing images: pixel, percent and proportionally

```bash
magick im.png -resize 90x90 out.png
magick im.png -resize 50% out.png
magick im.png -resize 4096@ out.png
```

- Export to PDF resizing (for printing)

```bash
magick img.jpg -resize 800x600 -background white -page a4 -gravity center -extent 800x600 doc.pdf
```

## jpegoptim

- Download from https://github.com/tjko/jpegoptim/releases

```bash
jpegoptim --size=90k tecmint.jpeg
```

### Inkscape

- Convert SVG to PNG or PDF

```bash
inkscape -z -e __OUTPUT__.png -w 1024 -h 1024 __INPUT__.svg
inkscape -f file.svg -A file.pdf
```