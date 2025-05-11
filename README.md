# EXP.NO.8-Simulation-of-QPSK

8.Simulation of QPSK

# AIM
To analyse the modulation of QPSK Signal.

# SOFTWARE REQUIRED
Python Colab

# ALGORITHMS

Initialize Parameters

Define number of QPSK symbols.

Set symbol duration T and sampling frequency fs.

Generate Random Bits

Create 2 × num_symbols random bits (since QPSK maps 2 bits per symbol).

Bit Separation

Split the bits into two streams:

Even bits for the In-phase component (I).

Odd bits for the Quadrature component (Q).

Map Bits to Amplitude Levels

Convert bits: 0 → -1, 1 → +1 for both I and Q.

Modulate Signal for Each Symbol

For each symbol:

Generate cosine wave scaled by I-bit.

Generate sine wave scaled by Q-bit.

Sum them to get the QPSK signal.

Concatenate all symbols to form the full signal.

Create Time Vector

Construct a time vector for the complete signal using total number of symbols.

Plot the Signals

Plot:

In-phase (cosine) signal.

Quadrature (sine) signal.

Combined QPSK signal.

# PROGRAM
import numpy as np

import matplotlib.pyplot as plt


num_symbols = 10  # Number of QPSK symbols (each with 2 bits)

T = 1.0           # Symbol period

fs = 100.0        # Sampling frequency

t = np.arange(0, T, 1/fs)


bits = np.random.randint(0, 2, num_symbols * 2)


i_bits = bits[0::2]  # Even-indexed bits

q_bits = bits[1::2]  # Odd-indexed bits


i_values = 2 * i_bits - 1

q_values = 2 * q_bits - 1


i_signal = np.array([])

q_signal = np.array([])

combined_signal = np.array([])

symbol_times = []


for i in range(num_symbols):

   i_carrier = i_values[i] * np.cos(2 * np.pi * t / T)
    
   q_carrier = q_values[i] * np.sin(2 * np.pi * t / T)
   
   symbol_times.append(i * T)
    
   i_signal = np.concatenate((i_signal, i_carrier))
    
   q_signal = np.concatenate((q_signal, q_carrier))
    
   combined_signal = np.concatenate((combined_signal, i_carrier + q_carrier))

    

t_total = np.arange(0, num_symbols * T, 1/fs)


plt.figure(figsize=(14, 9))


plt.subplot(3, 1, 1)

plt.plot(t_total, i_signal, label='In-phase (cos)', color='blue')

for i, symbol_time in enumerate(symbol_times):

   plt.axvline(symbol_time, color='red', linestyle='--', linewidth=0.5)
    
   plt.text(symbol_time + T/4, 0.8, f'{i_bits[i]}', fontsize=12, color='black')
    
plt.title('In-phase Component (Cosine) - One Bit per Symbol')

plt.xlabel('Time')

plt.ylabel('Amplitude')

plt.grid(True)

plt.legend()


plt.subplot(3, 1, 2)

plt.plot(t_total, q_signal, label='Quadrature (sin)', color='orange')

for i, symbol_time in enumerate(symbol_times):

   plt.axvline(symbol_time, color='red', linestyle='--', linewidth=0.5)
    
   plt.text(symbol_time + T/4, 0.8, f'{q_bits[i]}', fontsize=12, color='black')

    
plt.title('Quadrature Component (Sine) - One Bit per Symbol')

plt.xlabel('Time')

plt.ylabel('Amplitude')

plt.grid(True)

plt.legend()



plt.subplot(3, 1, 3)

plt.plot(t_total, combined_signal, label='QPSK Signal = I + Q', color='green')

for i, symbol_time in enumerate(symbol_times):

   plt.axvline(symbol_time, color='red', linestyle='--', linewidth=0.5)
    
   plt.text(symbol_time + T/4, 0.8, f'{i_bits[i]}{q_bits[i]}', fontsize=12, color='black')

    
plt.title('Combined QPSK Waveform')

plt.xlabel('Time')

plt.ylabel('Amplitude')

plt.grid(True)

plt.legend()


plt.tight_layout()

plt.show()


# OUTPUT

![image](https://github.com/user-attachments/assets/656d6fa9-cd3c-4ca9-a0fb-9fbfe1d4ba8a)

# RESULT / CONCLUSIONS
Thus QPSK modulation is implemented using Python. 
