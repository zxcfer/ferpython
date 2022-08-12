---
layout: post
title: "Filename Rename"
tags: ["filename", "rename"]
---

- Filename rename

```bash
ls -d *.php3 | sed 's/\(.*\).php3$/mv "&" "\1.php"/' | sh
```

- Using `for`:

```bash
for x in `ls -d *.php3 | sed 's/.php3$//'`; do mv $x.php3 $x.php; done
for i in `ls -d *.sql | sed 's/^izvjestajac_//'`; do mv izvjestajac_$i $i; done
```

- Alternatives

```bash
mv `ls -l *.txt | cut -d ":" -f 2 | cut -d " " -f 2`
for f in *.txt; do mv "${f}" "${f/.txt/.nfo}"; done; 
for f in /export/home/data/cdrsSS/SS/*.viejo; do mv "${f}" "${f/.viejo/}"; done;
```
