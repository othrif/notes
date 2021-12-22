---
title: "Audio file duration comparisons in Python"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
filename = '/Users/othrif/spectrum/voice/datasets/free-spoken-digit-dataset/recordings/4_yweweler_5.wav'
```


```python
import timeit
import sox
import subprocess
import soundfile as sf

def get_length_with_ffprobe(input_audio):
    result = subprocess.run(['ffprobe', '-i', input_audio, '-show_entries', 'format=duration', '-v', 'quiet', '-of', 'default=noprint_wrappers=1:nokey=1'], stdout=subprocess.PIPE, stderr=subprocess.STDOUT)
    return float(result.stdout)
```


```python
%time sf.info(filename).duration
```

    CPU times: user 1.61 ms, sys: 3.46 ms, total: 5.07 ms
    Wall time: 7.5 ms





    0.333875




```python
%time get_length_with_ffprobe(filename)
```

    CPU times: user 2.78 ms, sys: 8.43 ms, total: 11.2 ms
    Wall time: 92.1 ms





    0.333875




```python
%time sox.file_info.info(filename)['duration']
```

    CPU times: user 9.91 ms, sys: 29.6 ms, total: 39.5 ms
    Wall time: 112 ms





    0.333875


