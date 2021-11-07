---
title: "02: Heart-to-Heart(H2H): 
Authentication for Implanted Medical Devices
M. Rostami, A. Juels, F. Koushanfar"

date: 2021-10-27
type: book
commentable: true
# Provide the name of the presenter
summary: "Presenter(s): Clyde James Felix, Jeana Wadsack-Myers and Banh Nguyen "
# Provide other tags that describe the paper
tags:
- teaching
- ee693e
- Cryptography
- ECG
---
***
## Paper Summary
Implantable Medical Device (IMD) applies continuous monitoring therapies for chronic medical disordered patients. Patients have been implanted with IMDs to assess vital signs. To reprogram the IMD and to extract its data, a Commercial Device Programmers is a device that can perform these tasks wirelessly. A problem with this technology is the security risk that can harm patients. Hackers can seize unauthorized control of the IMDs. This paper proposes Heart-to-Heart (H2H) that establishes a novel access-control policy between the programmer and the IMD. H2H utilizes Electrocardiogram signals to generate random key sources to authorize control to IMDs. This paper further discusses the validity of ECG signals for authentication by examining their entropy. This paper also described the cryptographic pairing protocol between the programmer and the IMD and tested it on an adversarial model. Lastly, this paper describes the full implementation of H2H while displaying code size and power consumption analysis.
***
## Presentation
{{< youtube cQj1CtbFsMI >}}
***
## Review
### Strengths
- Provides greater security for the IMDs
- Provides a protocol for crucial cases (i.g. patient ECG goes flat)

### Weaknesses
- Limitation of having to touch the patient for authentication.

### Detailed Comments
This paper considers the system of using the IMD and the programmer. In this system, programmers can wirelessly extract data and reprogram the IMDs. The IMD system brings security risks that can potentially harm patients. While implementing security to the system, IMDs must offer permissive access control policies for life-threatening events. By balancing between the two challenges, implementing a security protocol for this application can be difficult. Heart-to-Heart is the proposed solution that uses touch-to-access to gain access to the IMD. For this proposal, the programmer and the IMD must measure ECG signals. The ECG signals then generate random key sources for authentication. If ECG signals are closely similar to each other, programmers gain access from the IMDs.

In this paper, the authors had to examine whether ECG signals are capable of producing pure random numbers for authentication. The approach of the validation is to investigate the entropies of the ECG signals. The result from this experiment is that ECGs are capable of producing 4 bits of random numbers with high entropies for authentication.

One advantage of H2H is that it protects from attackers by providing touch-to-access security. H2H provides protocols for different scenarios (i.g. when a patient ECG signal goes flat). A disadvantage of this proposal is the limitation of having touch-to-access between the programmer and the IMD. 

### Implementation
H2H was implemented into an IMD prototype consisting of three boards which can be seen from Figure 6. The ARM board was chosen to be the Leopard Gecko EFM-32 microcontroller (EFM32LG-DK3650) with a 32-bit ARM Cortex-M3 processor. This board communicates with the ECG analog front end (TI ADS1298) and the wireless board (TI CC430F5137). It has convenient power debugging tools and can extract the ECG features and communicate with the Programmer using TLS all while having a good power consumption profile.

TLS is used to establish the secure channel implementation between the Programmer and H2H. It is designed to provide an encrypted and authenticated channel between the two parties, usually comparing the Programmer certificate to PKI. However, the authors chose to forgo that for the ECG PV comparison which is more forgiving to the noise typical in ECG signals. RSA encryption for key exchange is chosen since it is the fastest exchange option for TLS in this application which has a small public exponent of 216 + 1. The RSA follows the NIST key length recommendation of modulus and message length set to 2048 bits and is also MISRA-C standard compliant. 

A NIST-recommended pseudo-random number generator or PRNG is used to allow certain actions such as RSA ciphertext padding and key generation and commitment. The initial random seed is generated offline and stored in the IMD’s non-volatile memory. As for ECG parameter extraction, the prototype annotates the ECG R-peaks by using an open source algorithm called WQRS to apply a simple length transformation to the ECG waveform.


### Experimentation
<!-- {{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/responsetime.jpg" title="Response Time" width="300" >}}

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/successrate.jpg" title="Success Rate with One Round" width="300" >}}

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/multipleattempts.jpg" title="Success Rate with Multiple Rounds" width="300" >}} -->

### Discussion
There are three broad technical approaches other papers have explored with comparison to H2H. The first is distance bounding which focuses on acoustic transmission of a random key. Halperin et al. tested authentication with a piezo device while Rasmussen et al. tested a similar ultrasound-based approach. However, it was found that this security model was too fragile and also comes with added energy cost and RF shielding requirements. 
The next technical approach is called shielding which is the idea of blocking inappropriate access to an IMD. There are two comparisons made with a wearable device called IMDGuard  and the works of Gollakota et al. In the end, the external burdens of a wearable device plus an increase in system failures make it an inferior method. 
Lastly, PV based authentication is mentioned in numerous works. However, none have done a rigorous security analysis like H2H and have been exposed to serious issues. 
Overall, the H2H prototype implementation confirms the promise of security, practicality and low overhead of H2H for current and future generations of IMDs.


### Questions
(1) Do you think other biometrics can be used for H2H? Something other than PV?

- Respiration measurements can be also used for authentication. The proposal of this paper might have a different approach. The entopies of the biometrics have to be investigated to decide whether those are good for authentication.

(2) Would there be a noticable difference in running time for the algorithm shown? Is it worth improving the n4logn time complexity?
- It is possible to improve time complexity of the algorithm by using another sorting algorithm. Further research has to be conducted. 

(3) Would x86 or other CISC architecture offer a better performance in place of the ARM architecture?
- Any processor can be used for the IMD. Although the choice of using ARM processor is not explained in the paper, It should be best to choose a processor that consumes less power.

