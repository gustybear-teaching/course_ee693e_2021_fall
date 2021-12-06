---
title: "01: Securing Electronic Medical Records Using Attribute-Based Encryption On Mobile Devices
Joseph Akinyele, Matthew Pagano, Matthew Green, Christoph Lehmann, Zachary Peterson, Aviel Rubin"
date: 2021-11-28
type: book
commentable: true

# Provide the name of the presenter
summary: "Presenter(s): Saige Dacuycuy, Tasmia Tahmid, Jeanalyn Wadsack-Myers"

# Provide other tags that describe the paper
tags:
- attribute-based encryption
- security

---

***
## Paper Summary
This paper delves into the creation and testing of a new protocol, Clicktok, in an attempt to detect fraudulent clicks from real clicks where ad companies may pay money per click on their ads. There are various attack methods used to generate these clicks whether it comes from a bot farm, or from malicious apps installed on a normal user's device, detecting inorganic clicks from organic clicks is a concern to prevent adversaries from profiting off from ad companies. Clicktok attempts to classify these clicks by utilizing the fact that fake generated click spam imitates user traffic in an attempt to stay stealthy. By analyzing repeating patterns in a user's click history, Clicktok aims to identify these false clicks from real clicks.
***

## Presentation
{{< youtube rKlSd3DZfkY >}}

***

## Review
### Strengths
- This paper offers a method of detecting fraudulent clicks that does not rely on a threshold based defense.
- By taking advantage that click fraud often uses previous user traffic in order to fabricate fake clicks, Clicktok is able to identify click fraud even though the attacker may be imitating organic clicks.

### Weaknesses
- Although Clicktok seems promising in detecting fraudulent clicks at various rates of attack, it seem it may be possible for an adversary to create a method that is able to bypass Clicktok's detection system.
- It may be difficult to keep track of malicious clicks with IP aggregation and churn. As some networks may try to avoid exposing IP addresses, it makes attributing fraudulent clicks to a certain source more difficult.

### Detailed Comments
By detecting the timing characteristics of click traffic feed received at ad networks, one can detect fraudulent clicks that attempt to be stealthy by sending a low amount of clicks. This is useful as farming clicks is becoming more economical with advances in technology, meaning that more attackers can have the luxury of sending a low amount of fraudulent clicks in an attempt to not be flagged as fake. Then even with a wide range of rates which an attacker can send fake clicks, whether the adversary decides to imitate previous user clicks or generate random clicks, Clicktok is able to identify repeating patterns of the imitation clicks, or the randomness of the clicks as not being attributed to real clicks.

As for the potential weakness in Clicktok, a more advanced click randomization/generation scheme may make detecting fraudulent clicks from real organic clicks difficult. If an attacker is able to uncover how Clicktok determines fraudulent clicks, they may be able to generate a workaround towards Clicktok's defenses. Then addressing the IP aggregation and churn, as some networks may aggregate IPs, it makes identifying individual user's clicks all the more difficult which would result in a lower efficacy when identifying false clicks.

### Implementation

The paper describes a high-level overview of how medical institutions provide an encrypted CCR to users, and how cloud-based storage is implemented via Google Health (Fig. 1). Before medical information is released to the user, an access policy is implemented into the nodes of the CCR. Here, an attribute-based encryption (ABE) is implemented into the CCR. The policies are initially specified by the medical provider and may consider attributes of the patient such as the age of the patient, the sensitivity of the data, and the identity of the authoring agent. 

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_14/images/Akinyele_Fig1.png" title="Figure 1: Implementation of Attribute-Based Encryption" width="250" >}}

The paper uses a mobile application called "iHealthEMR" that interface with the provider's server and, optionally, with cloud-based storage by Google Health. The primary function of the application is to browse, update, and secure CCRs. There are two interfaces with the application. One of them is to interact with the web service provided by the hospital. The user can read encrypted CCRs downloaded on their phones by decrypting it using ABE private keys stored on the user's phone's keychain. The second interface interacts with Google Health, a cloud-based storage. This interface allows users to read and write any of their records and be given the option to store it on the cloud server.

In the mobile application, the authors implement a "lazy" decryption, which only performs decryptions of records on an as-needed basis. This results into using less memory and less processing power, thus preserving battery life. Eventually the usability can be improved by selecting decryption once, and it allows for all other entries to be decrypted in the background. Other functions from the application are the supporting of caching encrypted medical records for when network connectivity is unavailable. Finally, one of the main highlights is that the application allows users to choose whether to trust Google with the privacy of their records. Even if the records cannot be uploaded to Google Health, the system's architecture supports other cloud-based EMR systems as well.

### Experimentation
In order to evaluate the ABE techniques to medical records, the authors conducted several experiments using their implementation.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_14/images/Akinyele_Fig2.png" title="Figure 1: CP-ABE and KP-ABE Encryption and Decryption Times" width="250" >}}
In their experimentation, they consider *stealthy* attackers to be under 5 clicks a day per device, *sparse* to be 5-15 clicks, and *firehose* to be over 15 clicks. From Table 1, it can be seen that Clicktok with a passive defense is effective in identifying click fraud. With a longer ad network duration, leads to better inference, especially against stealth attacks.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_14/images/Akinyele_Fig3.png" title="Figure 1: Implementation of Attribute-Based Encryption" width="250" >}}
They also categorized and analyzed different click categories, where sponsored are advertisements displayed by search engines, contextual are ads displayed on a webpage based on keywords present in the webpage, and mobile are ads exclusively present on mobile devices. From the results in Table 2, it is shown that the Clicktok is able to identify fraudulent clicks across the ad categories at a high true positive rate of ~90%, and a low false positive rate at around ~0.004%.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_14/images/Akinyele_Table1.png" title="Figure 1: Implementation of Attribute-Based Encryption" width="250" >}}
When applying the active defense with bait clicks, it can be seen in Table 3, that it improves detection rates. With both the increase in true positive rates, and decrease in false positive rates, show that an active defense may be important in identifying fake clicks.

### Audience Questions
1. Is there a reason 128 bit size was used in the AES over other larger bit sizes?

  We believe that there is no reason for why the authors used 128-bit keys for AES other than a simple implementation and for a proof-of-concept. A 128-bit size key is usually the less secured type of AES encryption. Having more bits, a 192-bit or a 256-bit AES encryption, would progressively give more rounds of encryption and improve the security of the one used in the paper. 

2. Do you think this proposal is still secure as of today?

  We believe that this proposal will not be secured when compared to today’s standards. It was discussed earlier that a 128-bit size AES encryption showed less encrypted security. It could be argued that the minimal action needed to break into a 128-bit size AES encryption is the same for a 256-bit size AES encryption. We believe that due to this paper being published in 2011 and the advancement of quantum computing, AES will soon become obsolete.

3. Along with the ciphertext, ABE requires the sender to provide information about the receiver's required attributes. Is this system capable of preventing that?

  We are not sure about the meaning of your question. To elaborate on the concept of the ABE approach used in this paper, the nodes in the CCR are encrypted using key- or ciphertext-policy ABE under an access policy. These policies are then initialized with the attributes of the user such as age, name of physician, etc
