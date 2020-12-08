---
title: "Sound file properties"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
filename = '/Users/othrif/spectrum/voice/datasets/free-spoken-digit-dataset/recordings/4_yweweler_5.wav'
```

# In python


```python
import sox
sox.file_info.info(filename)
```




    {'channels': 1,
     'sample_rate': 8000.0,
     'bitdepth': 16,
     'bitrate': 129000.0,
     'duration': 0.333875,
     'num_samples': 2671,
     'encoding': 'Signed Integer PCM',
     'silent': False}



# In CLI


```python
!soxi /Users/othrif/spectrum/voice/datasets/free-spoken-digit-dataset/recordings/4_yweweler_5.wav
```

    
    Input File     : '/Users/othrif/spectrum/voice/datasets/free-spoken-digit-dataset/recordings/4_yweweler_5.wav'
    Channels       : 1
    Sample Rate    : 8000
    Precision      : 16-bit
    Duration       : 00:00:00.33 = 2671 samples ~ 25.0406 CDDA sectors
    File Size      : 5.39k
    Bit Rate       : 129k
    Sample Encoding: 16-bit Signed Integer PCM
    


# Convert file to a specified bit and sample rates

``` bash 
sox <input> -b 16 -r 16000 <output>
soxi <input>
```
