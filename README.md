# Optical Amplifier (EDFA) Performance Analysis

## Aim: 
To study the gain and noise performance of an Erbium Doped Fiber Amplifier (EDFA) using Python simulation.

## Apparatus/Software Required:
	Python (NumPy) in Google Colab

## Theory:
	EDFA amplifies optical signals in the C band (1530–1565 nm) using stimulated emission.
	Gain depends on wavelength and pump power.
	Noise figure quantifies SNR degradation.

## Formulas:
## Key Equations
## 1. Gain
Amplifier gain:
G=P_out/P_in 

Gain in dB:
G_dB=10〖log⁡〗_10 (P_out/P_in )

________________________________________
## 2. ASE Power
P_ASE=2n_sp (G-1)hνB_o

where:
	n_sp= spontaneous emission factor 
	G= amplifier gain (linear) 
	h= Planck's constant 
	ν= optical frequency 
	B_o= optical bandwidth 
________________________________________
## 3. Noise Figure
Noise Factor:
F=(SNR_in)/(SNR_out )

For EDFA:
F=2n_sp  (G-1)/G

Noise Figure in dB:
NF=10〖log⁡〗_10 (F)

For high-gain EDFAs (G≫1):
NF≈10〖log⁡〗_10 (2n_sp)

Typical commercial EDFAs have:
NF≈4"-" 6" dB"

________________________________________
## Typical Practical Values
Parameter	Typical Value
Pump wavelength	980 nm / 1480 nm
Signal wavelength	1530–1565 nm
Peak gain	25–40 dB
Saturation output power	10–23 dBm
Noise figure	4–6 dB
Fiber length	5–20 m

## Sample Output
   	Graph: Gain spectrum curve peaking near 1550 nm.
<img width="528" height="388" alt="image" src="https://github.com/user-attachments/assets/15e6aaff-d3f3-42d1-aa76-66bb575b6c93" />
<img width="518" height="469" alt="image" src="https://github.com/user-attachments/assets/cce70c57-34f5-4634-a90e-df47c4e45b62" />
<img width="561" height="461" alt="image" src="https://github.com/user-attachments/assets/0f298da2-0dc1-43fd-bab6-0641a5210748" />

## Python Code
```
import numpy as np
import matplotlib.pyplot as plt

# Constants
h = 6.626e-34
c = 3e8
lambda_s = 1550e-9
nu = c / lambda_s

# Parameters
n_sp = 1.2
B = 50e9
Pin = 1e-6

# Gain vs Pump Power
pump_power = np.linspace(0.01, 0.2, 50)

G_linear = 1 + 50 * (
    pump_power / (pump_power + 0.05)
)

G_dB = 10 * np.log10(G_linear)

# Gain Spectrum
wavelength = np.linspace(1525, 1565, 100)

G_spec = 30 * np.exp(
    -((wavelength - 1535) / 10)**2
)

# Noise Figure
F = 2 * n_sp * (G_linear - 1) / G_linear

NF_dB = 10 * np.log10(F)

# ASE Power
P_ASE = (
    2 * n_sp *
    (G_linear - 1) *
    h * nu * B
)

# Plot 1: Gain vs Pump Power
plt.figure()
plt.plot(pump_power, G_dB)

plt.xlabel("Pump Power (W)")
plt.ylabel("Gain (dB)")
plt.title("Gain vs Pump Power")
plt.grid()
plt.show()

# Plot 2: EDFA Gain Spectrum
plt.figure()
plt.plot(wavelength, G_spec)

plt.xlabel("Wavelength (nm)")
plt.ylabel("Gain (dB)")
plt.title("EDFA Gain Spectrum")
plt.grid()
plt.show()

# Plot 3: Noise Figure vs Gain
plt.figure()
plt.plot(G_dB, NF_dB)

plt.xlabel("Gain (dB)")
plt.ylabel("Noise Figure (dB)")
plt.title("Noise Figure vs Gain")
plt.grid()
plt.show()
```

## Output
<img width="563" height="455" alt="image" src="https://github.com/user-attachments/assets/6d17253f-af7f-4d0a-a121-dbc0135c7f6f" />

<img width="562" height="455" alt="image" src="https://github.com/user-attachments/assets/c4a02a6d-0b9c-44f1-9065-eea84e6891bd" />

<img width="576" height="455" alt="image" src="https://github.com/user-attachments/assets/9afd0349-0e12-42f1-b86d-6a44e708f5a2" />

## Result
The EDFA performance was successfully analyzed using Python simulation. The amplifier gain and noise performance were studied, and the relationship between input power, output power, gain, and noise figure was observed.
