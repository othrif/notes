---
title: "Command line tools"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
type: technical_note
draft: false
---

### Grep commands

#### Count occurences
``` bash
grep -c '<event>'
```

### Concatenate PDFs
``` bash
gs -q -sPAPERSIZE=letter -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -sOutputFile=out.pdf in1.pdf in2.pdf in3.pdf
```


### Match regular expressions
``` bash
echo mc16_13TeV.366035.Sh_221_NN30NNLO_Znunu_PTV280_500_CVetoBVeto.recon.AOD.e7033_e9238_s3126_r10724 | grep -Eq 'AOD.e[0-9]+_s[0-9]+_r[0-9]+' && echo "Match"
```

### Find pattern anywhere recursively
``` bash
grep -rnw '/path/to/somewhere/' -e 'pattern'
```

### Write to someone in linux:
`write <username>`

### If you want to find the size of a subdirectory
``` bash
 ls -FaGl "${@}" | awk '{ total += $4; print }; END { print total }';
 ls -FaGl <dir path> | awk '{ total += $4; print }; END { print total }';
```

### If you want to find matches in the same line and get the word that comes after the space
``` bash
echo "blabla THIS ... a bunch of random stuff ... blabla THIS" | grep -oP "(?<=blabla )[^ ]+"
```
OR
``` bash
echo "blabla THIS ... a bunch of random stuff ... blabla THIS" | awk '{for(i=1;i<=NF;i++) if ($i=="blabla") print $(i+1)}'
```
Let's you want to add numbers:
``` bash
echo "blabla 111 ... a bunch of random stuff ... blabla 222" | awk '{for(i=1;i<=NF;i++) if ($i=="blabla") print $(i+1), total += $(i+1)} END{ print total}'
```

### To copy data from the "machine-where-precious-data-is" to the machine you are working on
``` bash
ssh user@machine-where-precious-data-is "tar czpf - /some/important/data" | tar xzpf - -C /new/root/directory
```

### Reversly
``` bash
tar cpf - /some/important/data | ssh user@destination-machine "tar xpf - -C /some/directory/"
```

### Kill all remote sessions of a user:
``` bash
pkill -KILL -u othrif
```

### Remove ^M
``` bash
dos2unix <filename>
```

###  Device or resource busy
``` bash
lsof +D <path>
```
Then kill PID with `kill -9 <PID>`
