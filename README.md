# 10sec-Language-Translation-into-English
# This python script will translate a 10 second clip of most languages (supported by Whisper by OpenAI) into English. The translation command is set to translate Japanese at the moment.

// Import appropiate packages
import sounddevice as sd
import numpy as np
import wave

// Settings
duration = 10  # seconds
filename = "japanesetest.wav"
samplerate = 44100  # CD quality

// Prompt the user to speak to the recording device.
print(f"🎙️ Recording for {duration} seconds... Speak now!")
recording = sd.rec(int(duration * samplerate), samplerate=samplerate, channels=1, dtype='int16')
sd.wait()
print(f"✅ Done! Saved as '{filename}'")

// Save as WAV
with wave.open(filename, 'w') as wf:
    wf.setnchannels(1)
    wf.setsampwidth(2)  # 16-bit audio = 2 bytes
    wf.setframerate(samplerate)
    wf.writeframes(recording.tobytes())


# Once you run the above script, enter this command: whisper japanesetest.wav --language Japanese --task translate --model medium
# This command will translate the Japanese or any language into English. Just change "Japanese" to whatever language you want to translate!
