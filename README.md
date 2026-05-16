# Pulse-Code-Modulation

# Aim
Write a simple Python program for the modulation and demodulation of PCM, and DM.

# Tools required
Google Colab
# Program
# PCM
```
import numpy as np
import matplotlib.pyplot as plt

# Time axis
t = np.linspace(0, 0.1, 1000)

# Message signal
fm = 50
msg = np.sin(2 * np.pi * fm * t)

# Sampling
fs = 1000
ts = np.arange(0, 0.1, 1/fs)
sampled = np.sin(2 * np.pi * fm * ts)

# Quantization
levels = 16
q_signal = np.round(sampled * (levels/2)) / (levels/2)

# Demodulated signal
demod = q_signal

# Clock signal
clock = np.sign(np.sin(2 * np.pi * 200 * t))

# Plotting
plt.figure(figsize=(10,8))

plt.subplot(4,1,1)
plt.plot(t, msg, 'b')
plt.title("Message Signal (Analog)")
plt.grid()

plt.subplot(4,1,2)
plt.plot(t, clock, 'g')
plt.title("Clock Signal")
plt.grid()

plt.subplot(4,1,3)
plt.step(ts, q_signal, 'r')
plt.title("PCM Modulated Signal")
plt.grid()

plt.subplot(4,1,4)
plt.plot(ts, demod, '--m')
plt.title("PCM Demodulated Signal")
plt.grid()

plt.tight_layout()
plt.show()
```
# DM
```
import numpy as np
import matplotlib.pyplot as plt

# Time axis
t = np.linspace(0, 1, 1000)

# Original signal
fm = 10
x = np.sin(2 * np.pi * fm * t)

# Delta Modulation
step = 0.1
dm = np.zeros(len(x))
demod = np.zeros(len(x))

for i in range(1, len(x)):
    
    if x[i] > demod[i-1]:
        dm[i] = 1
        demod[i] = demod[i-1] + step
    else:
        dm[i] = -1
        demod[i] = demod[i-1] - step

# Plotting
plt.figure(figsize=(10,7))

plt.subplot(3,1,1)
plt.plot(t, x)
plt.title("Original Signal")
plt.grid()

plt.subplot(3,1,2)
plt.step(t, demod)
plt.title("Delta Modulated Signal")
plt.grid()

plt.subplot(3,1,3)
plt.plot(t, demod, ':')
plt.title("Demodulated Signal")
plt.grid()

plt.tight_layout()
plt.show()

```
# Output Waveform

<img width="933" height="762" alt="image" src="https://github.com/user-attachments/assets/b8d6ca95-bb59-4d29-afcd-7af5508f0337" />
<img width="937" height="656" alt="image" src="https://github.com/user-attachments/assets/a0c43b51-c22a-44d4-9b00-e228c1a8728a" />


# Results
Thus, The output waveform of PCM and DM is verfied successfully.

