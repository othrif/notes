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
    



```python
!ffprobe -i /Users/othrif/spectrum/voice/datasets/free-spoken-digit-dataset/recordings/4_yweweler_5.wav
```

    ffprobe version 4.3.1 Copyright (c) 2007-2020 the FFmpeg developers
      built with Apple clang version 12.0.0 (clang-1200.0.32.28)
      configuration: --prefix=/usr/local/Cellar/ffmpeg/4.3.1_8 --enable-shared --enable-pthreads --enable-version3 --enable-avresample --cc=clang --host-cflags= --host-ldflags= --enable-ffplay --enable-gnutls --enable-gpl --enable-libaom --enable-libbluray --enable-libdav1d --enable-libmp3lame --enable-libopus --enable-librav1e --enable-librubberband --enable-libsnappy --enable-libsrt --enable-libtesseract --enable-libtheora --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxml2 --enable-libxvid --enable-lzma --enable-libfontconfig --enable-libfreetype --enable-frei0r --enable-libass --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libopenjpeg --enable-librtmp --enable-libspeex --enable-libsoxr --enable-videotoolbox --enable-libzmq --enable-libzimg --disable-libjack --disable-indev=jack
      libavutil      56. 51.100 / 56. 51.100
      libavcodec     58. 91.100 / 58. 91.100
      libavformat    58. 45.100 / 58. 45.100
      libavdevice    58. 10.100 / 58. 10.100
      libavfilter     7. 85.100 /  7. 85.100
      libavresample   4.  0.  0 /  4.  0.  0
      libswscale      5.  7.100 /  5.  7.100
      libswresample   3.  7.100 /  3.  7.100
      libpostproc    55.  7.100 / 55.  7.100
    Input #0, wav, from '/Users/othrif/spectrum/voice/datasets/free-spoken-digit-dataset/recordings/4_yweweler_5.wav':
      Duration: 00:00:00.33, bitrate: 129 kb/s
        Stream #0:0: Audio: pcm_s16le ([1][0][0][0] / 0x0001), 8000 Hz, 1 channels, s16, 128 kb/s


# Convert file to a specified bit and sample rates

``` bash 
sox <input> -b 16 -r 16000 <output>
soxi <input>
```
