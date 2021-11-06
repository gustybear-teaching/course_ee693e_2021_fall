---
title: "01: They Can Hear Your Heartbeats: Non-Invasive Security for
Implantable Medical Devices
Shyamnath Gollakota, Haitham Hassanieh,
Benjamin Ransford, Dina Katabi, Kevin Fu"
date: 2021-10-25
type: book
commentable: true

# Provide the name of the presenter
summary: "Presenter(s): Saige Dacuycuy, Tasmia Tahmid, Beemnet Alemayehu"

# Provide other tags that describe the paper
tags:
- teaching
- ee693e
- Full-duplex
- Implanted Medical Devices

---

***
## Paper Summary
Implantable medical devices are widespread and have been helping patients for decades. However, the recent works have shown that IMDs are vulnerable to attack. The biggest challenge arises from the difficulty of modifying an already implanted devices for security enhancements. The paper proposes to the use of a physical device called the shield, in which the security of the IMD is delegated to. The shield uses a novel radio design that can act as a jammer-cum-receiver. This design allows it to jam the IMD’s messages, preventing others from decoding them while being able to decode them itself. This design was evaluated using a software radio and was able to effectively provide confidentiality and protection from outside attacks.
***

## Presentation
{{< youtube h7mzwFhR_M0 >}}

***

## Review
### Strengths
- Shield prevents the IMDs' transmission and other incoming transmission
- Provide protection for existing IMD without any modifications	
- Can coexist with other devices
- First full-duplex radio without strict antenna positioning


### Weaknesses
- High turn-around time
- Full-duplex radio is very difficult to implment
- Shield has a transmission power limit, which is dependent on the position of the adversary

### Detailed Comments
The wireless connectivity of implantable medical devices (IMDs) leaves IMDs exploited to compromised confidentiality of transmitted data or unauthorized commands. An external device called a shield is worn on the body and near the IMD to jam the IMDs’ transmissions and other incoming transmissions. This helps prevent adversaries from decoding any information from the IMD and encoding unauthorized commands into the IMDs. Since the shield can be carried around as an external device to protect existing IMDs, this is useful since it eliminates the concept of surgically removing IMDs to perform cryptographic mechanisms. This work also presents this shield as the full-duplex radio without any strict antenna positioning. The jamming antenna and the receive antenna in the radio can be placed next each other, and hence can be built as a small wearable device capable of providing security. In addition to the compatibility with existing IMDs, shields can also coexist with meteorological devices that are users in the medical implant communication services (MICS) band. The shield does detect all packets, but it does not jam any of the cross-traffic packets. This means that the only packets it jams is those that were addressed to the IMD. 

Although the shield can jam all packets address to the IMD, the software radio implementation of the shield showed high turn-around times. A high turn-around time results into longer exposure of an IMDs’ transmissions after the shield stops an adversary’s transmission. Typically, a hardware implementation of the shield would be more efficient and give a turn-around time of tens of microseconds. In terms of design of the full-duplex radio, the jammer-cum-receiver shows low practicality. When jamming or transmitting signals, relying on the digital domain and the baseband to cancel signals out is not very dependable. Thus, it is not practical to use this device. Another performance issue with the shield is that it has a transmission power limit. Although the shield is capable of jamming signals at a distance, when the adversary is too far, the device would need more power to continue its operations.

### Implementation

### Experimentation
In order to evaluate Clicktok, the authors of the paper, used the click traffic obtained, filtered it and exposed it to a testbed with malicious apps and click malware. Through this they were able to get a click traffic that contained both legitimate and fake clicks.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_10/images/Fig5_Gollakota.png" title="Fig. 1: Antenna cancellation" width="320" >}}


{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_10/images/Fig6_Gollakota.png" title="Fig. 2: Packet loss at the shield" width="320" >}}


{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_10/images/Fig7_Gollakota.png" title="Fig. 3: Tradeoff between BER at the eavesdropper and reliable decoding at the shield" width="320" >}}


{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_10/images/Fig8_Gollakota.png" title="Fig. 4: Depletion of the IMD battery without the shield" width="320" >}}


{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_10/images/Fig9_Gollakota.png" title="Fig. 5: Sending unauthorized commands to the IMD without the shield" width="320" >}}

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_10/images/Fig10_Gollakota.png" title="Fig. 6: Adversary transmission 100 times the shield's power" width="320" >}}

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_10/images/Table1_Gollakota.png" title="Table 1: Coexistance of the shield with other devices" width="320" >}}


### Discussion
The authors had to calibrate the shield parameters to set the component bench marks. The shield was doing two tasks, send a random signal to the jammer and an antidote to the receiver antenna. The antenna calibration evaluates the performance of the antidote signal at the receiver. To evaluate this, the shield transmitted 100 Kb without the antidote followed by 100 Kb with the antidote. The difference in the power received at the receiver shows how much the antidote was able to block. This value averaged at 32 dB. The shield needs to balance how much to jam the eavesdropper and how much error to tolerate when decoding the IMD signal. 

To evaluate the shield protection against adversaries, the authors did two measurements. The first one was against passive adversaries where eavesdroppers try to intercept messages, and the second one is against active adversaries where they try to issue unauthorized commands to the IMD. The shield repeatedly triggers the IMD to transmit the same 1000 packets to evaluate shield’s jamming against passive adversaries. All the adversary locations had nearly 50% BER showing the effectiveness of the shield. 

Active adversaries were further divided into two based on the equipment they use. Those that use off-the-shelf IMD programmer and those that use custom hardware that transmits with higher power. The location distances varied from 20 cm to 30 m from the shield. Each adversary ran the same command 100 times with both the shield on and shield off. The shield was able to block all the attacks by the off-the-shelf IMD programmers, but the sophisticated IMD programmers that were closer than 5m were able to get a response from the IMD. Without the shield IMD programmers up to 27 m away was able to elicit a response. This shows the shield offers valuable protection to the IMD. An additional feature of the shield is to raise an alarm when an attempt is made regardless of the success/failure of the attacker.

### Audience Questions

1.	Is there some power loss that we need to consider for this system? Power delivered to an attacker from the IMD-shield combo? 
      
      Distance and RF environments do play a role here. In the experiment, not all the adversaries were able to send their commands to the IMD. For example, off-the-shelf IMD programmers who were placed further than 14m were not able to get any response even without the shield, and the custom hardware adversaries further than 27m were similarly unsuccessful.

2.	There is always a cost-benefit analysis when it comes to security and convenience. What is the cost of this system?

      In terms of pricing, it is not very clear on what parts were used for a full-duplex radio, especially since the design has to be a small wearable device. Hence, this product could be very expensive to create and implement. In the paper, the MICS band is partitioned into multiple channels of 300 KHz width, for a total bandwidth of 3 MHz. This means that the system doesn't require a high-speed analog-to-digital converter, which lowers the cost and power consumption.

3.	What are the limitations for this experiment?

      The limitations of this system is the transmission power limit of the jammer. In order to prevent an attack at immensely far distances, the shield requires more power to transmit a jamming signal. In addition, the functionality of the shield is only applicable to digital and software security. If an adversary were to ever be in close, physical proximity to the patient's IMD, the attacker can trigger a reaction that even the shield is unable to prevent.
      
