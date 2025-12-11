# 10sec-Language-Translation-into-English

This Python script records a **10-second audio clip** using your microphone and saves it as a WAV file.  
You can then use **Whisper (OpenAI)** to translate the audio into English.  
The example below is set to translate **Japanese**, but you can change the language flag to anything Whisper supports.

---

## 🎧 How It Works

1. The script records 10 seconds of audio.
2. Saves it as `japanesetest.wav`.
3. You run a Whisper command to translate the audio into English.

---

## 🧩 Python Code (audio recording script)

```python
import sounddevice as sd
import numpy as np
import wave

# Settings
duration = 10  # seconds
filename = "japanesetest.wav"
samplerate = 44100  # CD quality

print(f"🎙️ Recording for {duration} seconds... Speak now!")
recording = sd.rec(int(duration * samplerate), samplerate=samplerate, channels=1, dtype='int16')
sd.wait()
print(f"✅ Done! Saved as '{filename}'")

# Save as WAV
with wave.open(filename, 'w') as wf:
    wf.setnchannels(1)
    wf.setsampwidth(2)  # 16-bit audio = 2 bytes
    wf.setframerate(samplerate)
    wf.writeframes(recording.tobytes())

# whisper japanesetest.wav --language Japanese --task translate --model medium
# This is to translate the Japanese (the fix was using the medium model :)
