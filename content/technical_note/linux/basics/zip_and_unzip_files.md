---
title: "Zip And Unzip Files Hello"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to zip and unzip files using the Linux command line."
type: technical_note
draft: false
---

## Make Files

{{< highlight markdown >}}
echo "The number of soldiers in the regiment is 24." > regiment.txt
echo "The regiment has seen five battles." > battles.txt
{{< /highlight >}}

## Zip Files

The `-v` argument is optional, prints an output with the details of the operation.

{{< highlight markdown >}}
gzip regiment.txt battles.txt -v
{{< /highlight >}}
```
regiment.txt:	 -2.2% -- replaced with regiment.txt.gz
battles.txt:	 -5.6% -- replaced with battles.txt.gz
```

## View Contents Of Directory

{{< highlight markdown >}}
ls -l
{{< /highlight >}}
```
total 8
-rw-rw-r-- 1 othrif othrif 68 Jul 31 13:15 battles.txt.gz
-rw-rw-r-- 1 othrif othrif 78 Jul 31 13:15 regiment.txt.gz
```

## Unzip Files

{{< highlight markdown >}}
gunzip regiment.txt battles.txt
{{< /highlight >}}

## View Contents Of Directory

{{< highlight markdown >}}
ls -l
{{< /highlight >}}
```
total 8
-rw-rw-r-- 1 othrif othrif 36 Jul 31 13:17 battles.txt
-rw-rw-r-- 1 othrif othrif 46 Jul 31 13:17 regiment.txt
```