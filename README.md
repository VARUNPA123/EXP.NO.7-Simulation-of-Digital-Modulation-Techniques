# EXP.NO.7-Simulation-of-Digital-Modulation-Techniques
7. Simulation of Digital Modulation Techniques Such as
   i) Amplitude Shift Keying (ASK)
   ii) Frequency Shift Keying (FSK)
   iii) Phase Shift Keying (PSK)

# AIM
To simulate digital modulation techniques such as Amplitude Shift Keying (ASK), Frequency Shift Keying (FSK), and Phase Shift Keying (PSK) using Python, analyze their waveforms, and understand how digital data is transmitted using these modulation techniques.

# SOFTWARE REQUIRED
Google Colab

# ALGORITHMS
1. **Initialize Parameters**: 
   Define binary data (`data`), bit duration, sampling frequency (`Fs`), and carrier frequencies for ASK, FSK, and PSK modulation.

2. **Time Vector Generation**:
   Create a time vector (`t_bit`) corresponding to one bit duration with a high resolution based on the sampling frequency.

3. **Define Modulation Functions**:
   - For ASK: Create a cosine wave when the bit is 1; otherwise, generate a zero signal.
   - For FSK: Generate sine waves with different frequencies (`f1` for 1 and `f0` for 0).
   - For PSK: Generate sine waves with a phase shift of 0 for 1 and π for 0.

4. **Repeat Waveform Function**:
   Implement a function (`repeat_waveform`) to apply modulation functions across the entire binary data stream.

5. **Generate Digital Signal**:
   Expand the binary data into a repeated digital signal matching the sampling resolution.

6. **Apply Modulation Schemes**:
   - **ASK Signal**: Use the `repeat_waveform` function with the ASK modulation function.
   - **FSK Signal**: Generate modulated waves by switching frequencies based on binary data.
   - **PSK Signal**: Generate modulated waves by switching phase based on binary data.

7. **Define Time Axis**:
   Create a global time axis for plotting all signals using the product of the bit duration and data length.

8. **Plotting**:
   - Plot the message signal (digital representation).
   - Plot the ASK, FSK, and PSK modulated signals.
   - Optionally, plot the carrier signal if defined.

# PROGRAM
      import numpy as np
      import matplotlib.pyplot as plt
      
      # Binary data
      data = [1, 0, 1, 0, 1, 0]
      bit_duration = 1
      Fs = 1000  
      t_bit = np.linspace(0, bit_duration, Fs, endpoint=False)
      
      # Carrier frequencies
      f1 = 10  # FSK frequency for bit 1
      f0 = 2   # FSK frequency for bit 0
      f_c = 5  # Common carrier for ASK and PSK
      
      # --- Carrier Signal ---
      carrier_signal = np.cos(2 * np.pi * f_c * np.linspace(0, bit_duration * len(data), Fs * len(data), endpoint=False))
      
      # --- ASK Function ---
      def ask(bit):
          return np.cos(2 * np.pi * f_c * t_bit) if bit == 1 else np.zeros(len(t_bit))
      
      # --- Repeater ---
      def repeat_waveform(fn, bitstream):
          modulated = []
          for b in bitstream:
              modulated.extend(fn(b))
          return modulated
      
      # Generate signals
      digital = np.repeat(data, Fs)
      ask_signal = repeat_waveform(ask, data)
      
      # FSK signal
      fsk_signal = []
      for bit in data:
          freq = f1 if bit else f0
          wave = np.sin(2 * np.pi * freq * t_bit)
          fsk_signal.extend(wave)
      
      # PSK signal
      psk_signal = []
      for bit in data:
          phase = 0 if bit == 1 else np.pi
          wave = np.sin(2 * np.pi * f_c * t_bit + phase)
          psk_signal.extend(wave)
      
      # Time axis
      time = np.linspace(0, bit_duration * len(data), Fs * len(data), endpoint=False)
      
      # --- Reconstructed Signal ---
      # We apply a thresholding technique to recover the message from ASK signal
      reconstructed_signal = np.array(ask_signal) > 0.5  # Threshold to recover original bits
      reconstructed_signal = reconstructed_signal.astype(int)  # Convert boolean to binary (0 or 1)
      
      # Plotting
      plt.figure(figsize=(16, 14))
      
      # Message Signal
      plt.subplot(6, 1, 1)
      plt.plot(time, digital, color='blue')
      plt.title("Message Signal")
      plt.xlabel('Time (s)')
      plt.ylabel("Amplitude")
      plt.grid(True)
      
      # Carrier Signal
      plt.subplot(6, 1, 2)
      plt.plot(time, carrier_signal, color='brown')
      plt.title('Carrier Signal')
      plt.xlabel('Time (s)')
      plt.ylabel('Amplitude')
      plt.grid(True)
      
      # ASK Signal
      plt.subplot(6, 1, 3)
      plt.plot(time, ask_signal, color='green')
      plt.title("Amplitude Shift Keying (ASK)")
      plt.xlabel('Time (s)')
      plt.ylabel("Amplitude")
      plt.grid(True)
      
      # FSK Signal
      plt.subplot(6, 1, 4)
      plt.plot(time, fsk_signal, color='black')
      plt.title("Frequency Shift Keying (FSK)")
      plt.xlabel('Time (s)')
      plt.ylabel("Amplitude")
      plt.grid(True)
      
      # PSK Signal
      plt.subplot(6, 1, 5)
      plt.plot(time, psk_signal, color='red')
      plt.title("Phase Shift Keying (PSK)")
      plt.xlabel("Time (s)")
      plt.ylabel("Amplitude")
      plt.grid(True)
      
      # Reconstructed Signal
      plt.subplot(6, 1, 6)
      plt.plot(time, reconstructed_signal, color='purple', drawstyle='steps-mid')
      plt.title("Reconstructed Signal from ASK")
      plt.xlabel("Time (s)")
      plt.ylabel("Amplitude")
      plt.grid(True)
      
      plt.tight_layout()
      plt.show()


# OUTPUT
![image](https://github.com/user-attachments/assets/5069fc23-7fab-42a3-8d3d-536a3dfa79a6)


 
# RESULT / CONCLUSIONS
Thus, the simulation of digital modulation techniques such as ASK, FSK, and PSK were carried out successfully. The differences between the output waveforms of amplitude, frequency, and phase shift keying were clearly observed.
