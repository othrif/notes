---
title: "Record my voice"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
See resources here: https://realpython.com/playing-and-recording-sound-python/

# Record in CLI
From `sox`: 
``` bash 
rec new-file.wav

rec -b 16 -r 16000 new-file.wav
```

# Record with `sounddevice`


```python
import sounddevice as sd
from scipy.io.wavfile import write

fs = 44100  # Sample rate
seconds = 3  # Duration of recording

myrecording = sd.rec(int(seconds * fs), samplerate=fs, channels=1)
sd.wait()  # Wait until recording is finished
write('output.wav', fs, myrecording)  # Save as WAV file 

```


```python
import IPython.display as ipd
import matplotlib.pyplot as plt
ipd.Audio('output.wav')
plt.plot(myrecording)
```




    [<matplotlib.lines.Line2D at 0x12bdb8700>]




![png](record_sound_5_1.png)

