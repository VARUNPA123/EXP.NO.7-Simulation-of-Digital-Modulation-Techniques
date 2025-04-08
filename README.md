# EXP.NO.7-Simulation-of-Digital-Modulation-Techniques
7. Simulation of Digital Modulation Techniques Such as
   i) Amplitude Shift Keying (ASK)
   ii) Frequency Shift Keying (FSK)
   iii) Phase Shift Keying (PSK)

# AIM

# SOFTWARE REQUIRED

# ALGORITHMS

    # PROGRAM
    import matplotlib.pyplot as plt

    # Binary data
    data = [1, 0, 1, 0, 1]
    bit_duration = 1
    Fs = 1000  
    t_bit = np.linspace(0, bit_duration, Fs, endpoint=False)

    # Carrier frequencies
    f1 = 10  # FSK freq for bit 1
    f0 = 2   # FSK freq for bit 0
    f_c = 5  # Common carrier for ASK and PSK

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

    # Plotting
    plt.figure(figsize=(16, 12))

    # Digital Signal
    plt.subplot(4, 1, 1)
    plt.plot(time, digital, color='brown')
    plt.title("Digital Input Signal")
    plt.ylabel("Amplitude")
    plt.grid(True)

    # ASK Signal
    plt.subplot(4, 1, 2)
    plt.plot(time, ask_signal, color='green')
    plt.title("Amplitude Shift Keying (ASK using Cosine Carrier)")
    plt.ylabel("Amplitude")
    plt.grid(True)

    # FSK Signal
    plt.subplot(4, 1, 3)
    plt.plot(time, fsk_signal, color='black')
    plt.title("Frequency Shift Keying (FSK)")
    plt.ylabel("Amplitude")
    plt.grid(True)

    # PSK Signal
    plt.subplot(4, 1, 4)
    plt.plot(time, psk_signal, color='red')
    plt.title("Phase Shift Keying (PSK)")
    plt.xlabel("Time (s)")
    plt.ylabel("Amplitude")
    plt.grid(True)

    plt.tight_layout()
    plt.show()

# OUTPUT
 
# RESULT / CONCLUSIONS
