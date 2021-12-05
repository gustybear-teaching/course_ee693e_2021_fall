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


The paper uses an app called "iHealthEMR" that interfaces with the provider's server and, optionally, with cloud-ase storage by Google Health. The primary functions of the app is to browse, update, and secure CCR.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/ClicktokSystemArchitecture.png" title="System Architecture" width="320" >}}

They then use a moving window function to reduce sensitivity to synchronization errors from timing misalignments.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/ClicktokSystemPartitioning.png" title="Traffic Partitioning" width="300" >}}

Afterwards by examining the weight matrix, they can determine which patterns are repeated and are potentially fraudulent clicks, as patterns matrices that are repeated can be attributed to organic click spam (fake clicks imitating user inputs). They cluster the closely related patterns matrices, to then determine inorganic click spam by finding clusters with a higher entropy, characteristic of clicks generated from a randomized/constant time offsets. The remaining clicks can then be attributed to real users.

Another technique Clicktok applies is bait clicks (active defense), where ad networks inject bait clicks, so any malicious users that may try to imitate these bait clicks are identified with Clicktok's algorithm and flagged as fraudulent.

### Experimentation
In order to evaluate Clicktok, the authors of the paper, used the click traffic obtained, filtered it and exposed it to a testbed with malicious apps and click malware. Through this they were able to get a click traffic that contained both legitimate and fake clicks.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/ClicktokTable1.png" title="Table 1: Passive Detection" width="320" >}}
In their experimentation, they consider *stealthy* attackers to be under 5 clicks a day per device, *sparse* to be 5-15 clicks, and *firehose* to be over 15 clicks. From Table 1, it can be seen that Clicktok with a passive defense is effective in identifying click fraud. With a longer ad network duration, leads to better inference, especially against stealth attacks.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/ClicktokTable2.png" title="Table 2: Detection Across Multiple Clickstreams" width="320" >}}
They also categorized and analyzed different click categories, where sponsored are advertisements displayed by search engines, contextual are ads displayed on a webpage based on keywords present in the webpage, and mobile are ads exclusively present on mobile devices. From the results in Table 2, it is shown that the Clicktok is able to identify fraudulent clicks across the ad categories at a high true positive rate of ~90%, and a low false positive rate at around ~0.004%.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/ClicktokTable3.png" title="Table 3: Active Defense" width="320" >}}
When applying the active defense with bait clicks, it can be seen in Table 3, that it improves detection rates. With both the increase in true positive rates, and decrease in false positive rates, show that an active defense may be important in identifying fake clicks.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/ClicktokTable4.png" title="Table 4: Comparation of Clicktok" width="320" >}}
Lastly, Clicktok gives an comparation between their implementation compared to other defenses, with Clicktok providing vastly lower false positive rates comparatively, and similar or better true positive rates.

### Audience Questions
1. Is there a reason 128 bit size was used in the AES over other larger bit sizes?

2. Do you think this proposal is still secure as of today?

3. Along with the ciphertext, ABE requires the sender to provide information about the receiver's required attributes. Is this system capable of preventing that?


