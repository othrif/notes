---
title: "Transcribe audio: speech to text"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

```python
filename = '/Users/othrif/github/dataInsights/courses/datacamp/spoken_language/stereo_phone_call.wav'
```

# Using `speech_recognition`


```python
import speech_recognition as sr

recognizer = sr.Recognizer()
recognizer.energy_threshold = 300
tmg_file = sr.AudioFile(filename)

with tmg_file as source:
    tmg_audio = recognizer.record(source, duration=None, offset=None)

text = recognizer.recognize_google(audio_data=tmg_audio, language='en-US')
print(text)
```

    hello this is Daniel from Acme Studios how can I best help you I was just wondering if I could get some support yeah sure thing what's your name and what's wrong with your device and not one of large some of my my my farts okay nice to meet you Josh what's the serial number of your device so I can track it down the serial number is 176-4588

