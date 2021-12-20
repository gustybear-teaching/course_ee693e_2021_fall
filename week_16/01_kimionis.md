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
- Demonstrated a bit rate of 2 Gbps of backscatter transmission at 24–28 GHz
- Possible Upgradation to 28 GHz using existing the 2.4 GHz electronics
- Possible reduction of total production cost of mobile devices

### Weaknesses
- Parasitics
- The paper lacks to mention a detailed cost analysis to support the claim their system to be cost effective. 


### Detailed Comments
Backscatter has been used in commercial radio frequency applications in the sub-GHz range. In 2.4 GHz, backscatter is limited to hundreds of megabit per second. By using mmWave communication in a single high frequency transistor, backscatter can reach gigabit rate speeds. The backscatter communicator consists of antenna array and single RF transistor.  By controlling the gate voltage of the transistor, the reflection coefficient can be varied which can digitally encode information in the same way complex baseband communication signal encode information in a conventional transmitter. Even though using multiple transistors can generate multiple reflection coefficients in different topologies, increasing the number of transistors decrease performance due to device parasitics limiting scalability. Modern communication devices push signal processing to the baseband IC, instead of the multiple mixer stages in RF front end hardware, which makes radios to be software defined. This enables the use of generic RF front end and antennas with communication protocol upgrades and modulation schemes to support multiple applications. Mixing the base signal digitally using only one transistor regardless of the signal dimension allows scalability of the architecture. Not doing this in hardware offers the flexibility of selecting any bias intermediate frequency without needing any additional mixers in the communicator or transceiver. The advantage of this heterodyne backscatter is any baud rate, IF, constellation size and modulation format can be supported.

### Implementation

The range of backscatter communication systems such as RFID systems assuming free-space propagation is estimated by the value of R which is proportional to the waveleght time rootover transmit and receive gain. Compared to a typical UHF RFID scenario, their prototype introduces an increase in the combined transmit and receive gain of 200 or 23 dB. The frequency scaling from 915 MHz to 24.5 GHz is 26.8 or 14.3 dB. This translates to an ~3-dB reduction in the achievable range. The system prototype comprises a transmit antenna with 20 dB of gain and a receive antenna with 10 dB of gain. The prototype introduces an increase in the combined transmit and receive gain of 200 or 23 dB.The frequency scaling from 915 MHz to 24.5 GHz is 26.8 dB or 14.3 dB.

All printing was performed with a Dimatix DMP-2831 material deposition inkjet printer Four layers of SNP ink were printed at a 20-$m drop-to-drop spacing and with a 600-s inter-layer delay.The printer’s print table was heated to a maximum of 60 °C to promote solvent evaporation between layers.Vias were formed manually with a Dremel rotary tool driving a 0.5 mm drill bit. For the bias signal excitation port, a screw-on end-launch SMA connector was used (Southwest 292-06A-6); this provided a coaxial-to-microstrip transition. For the simulations, the Keysight Advanced Design System (ADS) solver was used. A full electromagnetic analysis with the method of moments was applied to the backscatter modulator and 5 × 1-antenna array to estimate the losses from the LCP substrate and SNP, the fringing fields and the electromagnetic coupling between ports. 

### Experimentation

In principle, any antenna array can be used for mmWave backscattering. A series-fed patch antenna array was designed for demonstration purposes. It has a structure of a bandpass microstripstepped-impedance filter. The antenna array is circularly polarized and circular polarization is achieved by appropriatelytruncating two corners. The integrated backscatter communicator was implemented on a 0.1778-mm-thick flexible liquid-crystal polymer (LCP) substrate.

One side of the substrate was used for inkjet-printing the antenna array. Because of the good adhesion of the SNP ink on the thin LCP substrate, the entire structure is flexible. A custom mmWave transceiver with off-the-shelf modules was set up, with a transmitter set up to emit a 24.5 GHz continuous wave. The spectrum of the receiver covered the whole 24–28 GHz band while discarding the 22.5 GHz region. The main-lobe spectrum has been demodulated with a BPSK waveform that was pulse-shaped with square-root raised cosine (SRRC) pulses.

The AWG was set up to generate a QPSK waveform, digitally upconverted to a 2 GHz IF subcarrier. The real-valued analogue signal output was used to drive the mmWave communicator. This work demonstrates gigabit-per-second-level data rates for backs catterradio with extremely low-energy front-end consumptions.

### Audience Questions
1.	What is the between PSK and QPSK? 

The simplest form of PSK is BPSK, so we are assuming you are asking the difference between BPSK and QPSK. QPSK uses 4 constellation points which allows it to encode two bits per symbol. This can let the data rate sent over the same bandwidth to be doubled or send the same data rate over half the bandwidth of a BPSK modulation. 

2.	Do you know the cost for using single-transisiter front-ends for backscatter instead of active mixers?

Active mixer allows more flexibility to design the communication systems. There could be possibly two types of systems design depending on how the mixer is connected. In one set up two separate mixures can be used to connect the transmitter and the receiver. While on the other hand, a more of a Radar like system can be designed using a single mixer and connecting the transmit and the receiving antenna from to the same mixure and using an active mixer in the set up allows the synchronizaion of the modulated signal afterwards. The cost of the system is driven by the trade-off between the design drivers and complexity to implement the system and also cost vs. utility. The paper lacks to present a detailed cost analysis for the proposed system. However, in the paper they mentions about if an active mixer costs 10 USD then a using a single transitor will cost 1 USD. From that notion, we can assume that if we use a single transistor it will reduce the overall system cost at least one or two orders of magnatude. 

4.	Is the LCP substrate the only/best option for them?

The LCP substrates are widely used for medical devices/application because of their excellent thermal properties. An alernative sustrate could be polymide but since polymide needs adhessive and for this particular application higher dielectric contract and higher thermal resistivity is assumed to be the driving factor for choosing LCP substrate. The LCP substrate is capable of supporting upto 60 degrees temeparture which is one of the strongest facor to choose LCP substate.   
