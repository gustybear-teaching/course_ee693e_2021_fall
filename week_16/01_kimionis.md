---
title: "01: A printed millimetre-wave modulator and antenna 
array for backscatter communications at gigabit 
data rates
John Kimionis, Apostolos Georgiadis, Spyridon Nektarios Daskalakis, 
Manos M. Tentzeris"
date: 2021-12-06
type: book
commentable: true

# Provide the name of the presenter
summary: "Presenter(s): Beemnet Alemayehu, Tasmia Tahmid, Nguyen Banh"

# Provide other tags that describe the paper
tags:
- teaching
- ee693e
- mmWave
- backscatter

---

***
## Paper Summary
The increasing prevalence of IoT requires the use of scalable and robust communication systems that can deliver higher data rates with low power consumption. This paper investigates the novel technology to achieve this combination of high data rate and minimized energy consumption. By utilizing the wide bandwidth and large communication rates of mmWave technology, this paper uses backscattering to provide gigabit data rates with low-complexity approach. The low complexity front end reduces the cost and time it takes to fabricate this technology enabling it to be scalable.
***

## Presentation
{{<https://youtu.be/KCHre1Z_bFc >}}

***

## Review
### Strengths
- Scalable (no hardware mixer and oscillator)
- Low cost, low complexity, low power
- Support multiple modulation schemes

### Weaknesses
- parasitics


### Detailed Comments
Backscatter has been used in commercial radio frequency applications in the sub-GHz range. In 2.4 GHz, backscatter is limited to hundreds of megabit per second. By using mmWave communication in a single high frequency transistor, backscatter can reach gigabit rate speeds. The backscatter communicator consists of antenna array and single RF transistor.  By controlling the gate voltage of the transistor, the reflection coefficient can be varied which can digitally encode information in the same way complex baseband communication signal encode information in a conventional transmitter. Even though using multiple transistors can generate multiple reflection coefficients in different topologies, increasing the number of transistors decrease performance due to device parasitics limiting scalability. Modern communication devices push signal processing to the baseband IC, instead of the multiple mixer stages in RF front end hardware, which makes radios to be software defined. This enables the use of generic RF front end and antennas with communication protocol upgrades and modulation schemes to support multiple applications. Mixing the base signal digitally using only one transistor regardless of the signal dimension allows scalability of the architecture. Not doing this in hardware offers the flexibility of selecting any bias intermediate frequency without needing any additional mixers in the communicator or transceiver. The advantage of this heterodyne backscatter is any baud rate, IF, constellation size and modulation format can be supported.

### Implementation

The range of backscatter communication systems such as RFID systems assuming free-space propagation is estimated by the value of R which is proportional to the waveleght time rootover transmit and receive gain. Compared to a typical UHF RFID scenario, their prototype introduces an increase in the combined transmit and receive gain of 200 or 23 dB. The frequency scaling from 915 MHz to 24.5 GHz is 26.8 or 14.3 dB. This translates to an ~3-dB reduction in the achievable range. The system prototype comprises a transmit antenna with 20 dB of gain and a receive antenna with 10 dB of gain. The prototype introduces an increase in the combined transmit and receive gain of 200 or 23 dB.The frequency scaling from 915 MHz to 24.5 GHz is 26.8 dB or 14.3 dB.

All printing was performed with a Dimatix DMP-2831 material deposition inkjet printer Four layers of SNP ink were printed at a 20-$m drop-to-drop spacing and with a 600-s inter-layer delay.The printer’s print table was heated to a maximum of 60 °C to promote solvent evaporation between layers.Vias were formed manually with a Dremel rotary tool driving a 0.5 mm drill bit. For the bias signal excitation port, a screw-on end-launch SMA connector was used (Southwest 292-06A-6); this provided a coaxial-to-microstrip transition. For the simulations, the Keysight Advanced Design System (ADS) solver was used. A full electromagnetic analysis with the method of moments was applied to the backscatter modulator and 5 × 1-antenna array to estimate the losses from the LCP substrate and SNP, the fringing fields and the electromagnetic coupling between ports. 

### Experimentation


### Audience Questions
1.	What is the between PSK and QPSK? 

The simplest form of PSK is BPSK, so we are assuming you are asking the difference between BPSK and QPSK. QPSK uses 4 constellation points which allows it to encode two bits per symbol. This can let the data rate sent over the same bandwidth to be doubled or send the same data rate over half the bandwidth of a BPSK modulation. 

2.	Do you know the cost for using single-transisiter front-ends for backscatter instead of active mixers?


4.	Is the LCP substrate the only/best option for them?
