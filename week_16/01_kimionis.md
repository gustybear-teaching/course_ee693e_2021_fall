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


### Experimentation


### Audience Questions
1.	What is the between PSK and QPSK? 

The simplest form of PSK is BPSK, so we are assuming you are asking the difference between BPSK and QPSK. QPSK uses 4 constellation points which allows it to encode two bits per symbol. This can let the data rate sent over the same bandwidth to be doubled or send the same data rate over half the bandwidth of a BPSK modulation. 

2.	Do you know the cost for using single-transisiter front-ends for backscatter instead of active mixers?


4.	Is the LCP substrate the only/best option for them?

