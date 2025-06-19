
# Behavioral Model of an Analog Front-End FM-UWB Using CppSim Virtuoso "" *ID:9750* ""



This repository contains the simulation codes for a behavioral model of an FM-UWB transceiver, implemented and evaluated using CppSim and Virtuoso.

The corresponding paper is titled:  
**Behavioral Model of an Analog Front-End FM-UWB Using CppSim Virtuoso**

---

## 📄 File Descriptions

The repository includes various functional blocks used in the system-level simulation:

- **`add2`**: Two-input adder block  
- **`BPF_BUTTERWORTH`**: Band-pass filter with a Butterworth response  
- **`Comparator`**: Signal comparator (binary output)  
- **`constant`**: Constant value generator  
- **`gain`**: Signal gain amplifier  
- **`LPF_BUTTERWORTH`**: Low-pass Butterworth filter  
- **`lpf_first_order`**: First-order low-pass filter  
- **`noise`**: Noise source (e.g., thermal or Gaussian noise)  
- **`PA`**: Power amplifier block  
- **`Rectifier`**: Signal rectifier (half or full-wave)  
- **`signal_source`**: General-purpose signal source (e.g., sinusoidal or pulse)  
- **`Sub_Carrier`**: Sub-carrier generator for modulation  
- **`sub2`**: Subtractor (version 2)  
- **`vco`**: Voltage Controlled Oscillator  
- **`vco_noise`**: VCO with noise modeling (phase noise or jitter)

---

## 🔧 Description of `BPF_BUTTERWORTH` Block

### Module: `BPF_BUTTERWORTH`

This module implements a Butterworth band-pass filter using a Laplace-domain transfer function.

### Parameters
- `wo` (double): Center angular frequency in radians/second  
- `in` (double): Input signal  
- `out` (double): Filtered output signal

### Transfer Function

- **Numerator**: (W × 2π / 0.7) × s  
- **Denominator**: s² + ((2πW)/0.7) × s + (2πW)²

Where:
- *s*: Complex Laplace variable  
- *W*: Center frequency  
- *Ts*: Integration or sampling time constant

The 1/0.7 factor adjusts the filter bandwidth to achieve a smooth Butterworth response.

### Functionality
1. Receives input signal `in`
2. Applies the defined band-pass filtering
3. Outputs the filtered signal as `out`

### Core Code

```c
module: BPF_BUTTERWORTH
description: 
timing_sensitivity: 
parameters:  double wo
inputs:  double in
outputs:  double out
classes:  Filter filt("(W*2*pi/0.7)*s","s^2 + ((2*pi*W)/0.7)*s + (2*pi*W)^2","W,Ts",wo,Ts);
static_variables:  
init:  
end:  
code:  

filt.inp(in);
out = filt.out;
electrical_element:  
functions:  
custom_classes_definition:  
custom_classes_code:  
```

---

## ✍️ Authors

### Juan C. Garcia Gutierrez (ORCID: [0009-0003-0434-2841](https://orcid.org/0009-0003-0434-2841)

Born in Puebla in 1997. He earned his B.Sc. in Mechatronics Engineering from BUAP in 2021. He collaborated on chip characterization at the Circuits and Systems Characterization Laboratory, Faculty of Electronics. Currently pursuing his M.Sc. at BUAP, his interests include RF system design for wireless communications.

### Victor R. Gonzalez Diaz (ORCID: [0000-0002-2931-8368](https://orcid.org/0000-0002-2931-8368))

Born in Mexico. He received M.Sc. and Ph.D. degrees from INAOE in 2005 and 2009, respectively. He was a Postdoctoral Fellow at the University of Pavia, Italy (2009–2010). He is a full-time Professor at BUAP and leads the Circuits and Systems Characterization Lab. His research includes ADCs, frequency synthesizers, and micropower circuits. Associate Editor for IEEE TCAS-II.

### Luis A. Sanchez Gasparino (ORCID: [0000-0002-3899-0746](https://orcid.org/0000-0002-3899-0746))

He obtained his Ph.D. in Electronics Sciences from INAOE in 2011, specializing in CMOS Power Amplifiers for wireless systems. He was a visiting scholar at the University of Twente in 2009. He led the Electronics group at Universidad Politécnica de Puebla (2011–2017). Currently a professor at BUAP and member of the Photonics and Nanooptics Systems group. Member of Mexico’s SNI (level-1), with over 60 publications. His work focuses on EDA tools, analog/RF design, and future wireless systems (IoT, 5G).

---

## 🛠️ About CppSim

CppSim is a simulation environment for analog and digital systems. It is particularly well-suited for developing and testing communication front-ends and circuit-level blocks.

To install CppSim:
1. Visit [cppsim.com](https://www.cppsim.com/download.html)
2. Download and unzip the package
3. Follow the platform-specific installation guide
4. Ensure you have a C++ compiler and required dependencies

### Integrating a Custom Block
To add your own block:
1. Create a new C++ file containing your logic
2. Add it to the CppSim project and connect via signal definitions
3. Compile and run the simulation to validate functionality
