# EXP 1 :  ANALYSIS OF DFT WITH AUDIO SIGNAL

# AIM: 

  To analyze audio signal by removing unwanted frequency. 

# APPARATUS REQUIRED: 
   
   PC installed with SCILAB/Python. 

# PROGRAM: 

// analyze audio signal
```
!pip install scipy matplotlib numpy
import numpy as np
import matplotlib.pyplot as plt
from scipy.io import wavfile
from scipy.fft import fft, fftfreq, ifft

# Step 1: Load the audio
fs, data = wavfile.read("dog bark sound.wav")  
if data.ndim > 1:   # if stereo, take one channel
    data = data[:,0]

# Step 2: Plot original waveform
plt.figure(figsize=(10,4))
plt.plot(data)
plt.title("Original Audio Signal")
plt.xlabel("Samples")
plt.ylabel("Amplitude")
plt.show()

# Step 3: Do FFT (DFT)
N = len(data)
yf = fft(data)
xf = fftfreq(N, 1/fs)

plt.figure(figsize=(10,4))
plt.plot(xf[:N//2], np.abs(yf[:N//2]))
plt.title("Frequency Spectrum")
plt.xlabel("Frequency (Hz)")
plt.ylabel("Magnitude")
plt.show()

# Step 4: Remove unwanted frequency (example: remove around 1000 Hz)
filtered = yf.copy()
low, high = 995, 1005   # frequency range to remove
filtered[(xf>low) & (xf<high)] = 0
filtered[(xf<-low) & (xf>-high)] = 0

# Step 5: Inverse FFT to reconstruct signal
cleaned = np.real(ifft(filtered))

# Step 6: Plot cleaned waveform
plt.figure(figsize=(10,4))
plt.plot(cleaned)
plt.title("Filtered Audio Signal")
plt.xlabel("Samples")
plt.ylabel("Amplitude")
plt.show()

# Step 7: Save filtered audio
wavfile.write("cleaned_audio.wav", fs, cleaned.astype(np.int16))
print("Filtered audio saved as cleaned_audio.wav")
```
# OUTPUT: 
![WhatsApp Image 2025-10-24 at 14 07 16_58bd98f6](https://github.com/user-attachments/assets/0455bc2e-75aa-4d51-a73f-699cb977fbc8)
![WhatsApp Image 2025-10-24 at 14 07 30_557e4c4a](https://github.com/user-attachments/assets/c952a32c-ff63-487a-b14c-8f19d840ee68)
![WhatsApp Image 2025-10-24 at 14 07 41_d8355753](https://github.com/user-attachments/assets/70017b29-8b25-430e-a5f1-37670e26a135)


# RESULTS
The audio file has a sampling rate of 44100 Hz and contains 1428558 samples. The waveform shows the variations in amplitude over time, representing the dog bark sound.
