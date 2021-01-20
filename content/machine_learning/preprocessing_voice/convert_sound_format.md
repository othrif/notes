---
title: "Convert between audio formats"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Convert in CLI

``` bash 
sox new.wav new.mp3
```

### Convert to a different bit depth and sampling rate

``` bash 
ffmpeg -i  input.wav -ar 16000 -sample_fmt s16 output.wav
```
Available bit depth optons:
``` bash 
ffmpeg -sample_fmts
```

# Convert Numpy to WAV with `wavio`
`wavio.write` writes a numpy array to a WAV file, optionally using a specified sample width.

### Create a numpy array of 16-bit sine wave


```python
import numpy as np

frequency = 440  # Our played note will be 440 Hz
fs = 44100  # 44100 samples per second
seconds = 3  # Note duration of 3 seconds
t = np.linspace(0, seconds, seconds * fs, False)
note = np.sin(frequency * t * 2 * np.pi)
audio = note * (2**15 - 1) / np.max(np.abs(note)) # Ensure that highest value is in 16-bit range
my_np_array = audio.astype(np.int16) # Convert to 16-bit data
```

### Save to `wav` file


```python
import wavio
wavio.write('/tmp/myfile.wav', my_np_array, fs, sampwidth=2)
```


```python
!ls /tmp/myfile*.wav
```

    /tmp/myfile.wav


# Convert with `pydub`
Can convert between all [ffmpeg formats](https://www.ffmpeg.org/general.html#File-Formats)


```python
from pydub import AudioSegment
sound = AudioSegment.from_file('/tmp/myfile.wav', format='wav')
sound.export('/tmp/myfile.mp3', format='mp3')
```




    <_io.BufferedRandom name='/tmp/myfile.mp3'>




```python
!ls /tmp/myfile*
```

    /tmp/myfile.mp3 /tmp/myfile.wav


# Convert with `soundfile`
Can convert between all [libsndfile formats](http://www.mega-nerd.com/libsndfile/#Features)


```python
import soundfile as sf

# Extract audio data and sampling rate from file 
data, fs = sf.read('/tmp/myfile.wav') 
# Save as FLAC file at correct sampling rate
sf.write('/tmp/myfile.flac', data, fs)  
```


```python
!ls /tmp/myfile*
```

    /tmp/myfile.flac /tmp/myfile.mp3  /tmp/myfile.wav

