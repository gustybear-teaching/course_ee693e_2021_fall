---
title: "01: Clicktok: Click Fraud Detection using Traffic Analysis
Shishir Nagaraja, Ryan Shah"
date: 2021-08-30
type: book
commentable: true

# Provide the name of the presenter
summary: "Presenter(s): Alvin Yang, Thomas Yang"

# Provide other tags that describe the paper
tags:
- teaching
- ee693e

---

***
## Paper Summary
This paper delves into the creation and testing of a new protocol, Clicktok, in an attempt to detect fraudulent clicks from real clicks where ad companies may pay money per click on their ads. There are various attack methods used to generate these clicks whether it comes from a bot farm, or from malicious apps installed on a normal user's device, detecting inorganic clicks from organic clicks is a concern to prevent adversaries from profiting off from ad companies. Clicktok attempts to classify these clicks by utilizing the fact that fake generated click spam imitates user traffic in an attempt to stay stealthy. By analyzing repeating patterns in a user's click history, Clicktok aims to identify these false clicks from real clicks.
***

## Presentation
{{< youtube C2LOWF_K-FM >}}

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
The paper provides an explanation into how they implemented their algorithm of Clicktok, as well as how they collected the data they used to train their model. The way they collected their data was by setting up traffic monitors on backbone routers of a university campus network. They collected a total of 217,334,190 unique clicks, between June 2015 and November 2017. The data was collected after obtaining ethical approval, and all stored data is encrypted. As for how they implemented their algorithm, they took the click traffic of each user (click stream), and attempted to decompose the click streams of each user into basic patterns by using a non-negative matrix factorization algorithm. This decomposes the click traces into pattern matrices, and weight matrices as to how often each pattern occurs.

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
Will this approach in telemedicine for medical education affect student performances?


We assumed that the questioner was curious about how much this approach may affect a student’s performance in course-related work, so we will answer the question considering this thought . Although not mentioned in the paper, a typical medical school program would have its students work on clinical rotations during their third year of medical school. The emphasis of using telemedicine for medical education is during the clinical training only. Hence, there should be no effect on a student’s performance in course-related work, since this is usually done during the first two years of medical school. 

What could be the biggest ethical concern relating to the tele-ICU concept?

The concept of the tele-ICU could jeopardize the American Medical Association’s (AMA) first principle of medical ethic, which is:

“A physician shall be dedicated to providing competent medical care, with compassion and respect for human dignity and rights.”
The idea of the tele-ICU can fragment the relationship between doctor and patient. Sometimes the decision of a patient’s life can only be made through on-site intervention, and the off-site physician may not be able to provide them assistance. A physician caring for a patient while distancing themselves could decrease the quality of competent medical care, especially since having an on-site intensivist was always the primary method.



Considering the size/maneuverability of sensation feedback technology for telesurgery, do you think this technology will actually be feasible for telesurgery teaching or just for very specific applications?

It’s still very hard to determine the outcome of sensation feedback technology in telesurgery or any other application, especially since the current technology is limited to virtual reality. Since the current technology can be used to simulate the weights of household objects, we believe that it can be applied for microscale objects as well. Eventually, we hope that this technology can be used in collaboration with the da Vinci system to achieve true telesurgery. 
