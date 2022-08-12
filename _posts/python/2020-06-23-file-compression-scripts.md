---
layout: post
title: "Compressing files with Python"
description: "Script examples to compress files using Python"
tags: ["compression", "python"]
---


## Using tar and zip

```py
import tarfile

def make_tarfile(output_filename, source_dir):
    with tarfile.open(output_filename, "w:gz") as tar:
        tar.add(source_dir, arcname=os.path.basename(source_dir))

# "w:bz2"

tar = tarfile.open("sample.tar.gz", "w:gz")
for name in ["file1", "file2", "file3"]:
    tar.add(name)
tar.close()
```

## Using tar and Bzip

Bzip2 is also available, and you can try the following example:

```py
import bz2

compressionLevel = 9
source_file = '/foo/bar.txt' #this file can be in a different format, like .csv or others...
destination_file = '/foo/bar.bz2'

tarbz2contents = bz2.compress(open(source_file, 'rb').read(), compressionLevel)
```

https://docs.python.org/3/library/bz2.html


## Extraction

```py
zipfile.ZipFile('myarchive.zip').extractall(pwd='P4$$W0rd')
```