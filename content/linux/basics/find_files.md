---
title: "Find Files"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to find files using the Linux command line."
type: technical_note
draft: false
---

## Make Files And Directories
{{< highlight markdown >}}
touch sales.txt, marketing.txt, data_science.csv, product.html; mkdir sales marketing
{{< /highlight >}}

## View Files And Directories
{{< highlight markdown >}}
ls -l
{{< /highlight >}}
```
total 8
-rw-rw-r-- 1 othrif othrif    0 Jul 29 21:21 data_science.csv,
drwxrwxr-x 2 othrif othrif 4096 Jul 29 21:21 marketing
-rw-rw-r-- 1 othrif othrif    0 Jul 29 21:21 marketing.txt,
-rw-rw-r-- 1 othrif othrif    0 Jul 29 21:21 product.html
drwxrwxr-x 2 othrif othrif 4096 Jul 29 21:21 sales
-rw-rw-r-- 1 othrif othrif    0 Jul 29 21:21 sales.txt,
```

## Find All Files In A Given File Path

`-type f` indicates we want to find only files.

{{< highlight markdown >}}
find ~/example_directory -type f
{{< /highlight >}}
```
/home/othrif/example_directory/data_science.csv,
/home/othrif/example_directory/product.html
/home/othrif/example_directory/sales.txt,
/home/othrif/example_directory/marketing.txt,
```