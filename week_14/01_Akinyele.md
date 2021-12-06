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
The paper present a prototype system to protect EMRs when outside of the trusted domain of a hospital. Authors use Access based encryption (ABE) to provide fine-grained, policy-based encryption. To facilitate the implementation of the proposed system, the authors have developed a software library to support different modes of ABE. The paper focuses to develop meaningful techniques for protecting the privacy of records and targets to address 5 major issues focusing to establish the importance of offline access to the emergency medical records. The paper also presents how the proposed system enables realistic use cases for example treatment of minors and advanced directives. To ensure as smooth and secure access to the EMRs systems the authors also came up with appropriate policies which are quite complex policies in nature. The paper describes a policy engine providing automated support for policy generation. Finally, the paper also presents a a proof-of-concept mobile app allowing patients to access the encrypted records on their mobile phone (iPhone) offline and also explains the mechanism to securely export EMR records to other cloud-based EMR providers.

***

## Presentation
{{< youtube rKlSd3DZfkY >}}

***

## Review
### Strengths
- This paper focuses to develop effective techniques for protecting the privacy of emergency medical records and targets to address 5 major issues or problem areas. 
- The paper very well addresses various complexity of access policies to ensure information security. 
- In this paper, the author describes  efforts to provide self protecting EMRs on mobile devices using recent developments in attribute-based encryption (ABE).
- The paper scrutizes the importance of offline access thoroghly which eventually puts some light on understanding the importance of emergency access to medical records during massive catastropic failures or similar disaster situations.  

### Weaknesses
- A 128-bit size key is usually the less secured type of AES encryption.
- The paper mentions about Attribute-Based Encryption (ABE) system to protect EMRs against cyber threat but recent development in this area offers a hint that this system might not be completely full proved to protect various types of cyber threats. 

### Detailed Comments
The paper very well addresses some major problem areas triggering the requirements of an effective systems: 1) EMR systems’ reliance on transport security; 2) Access control is online only; 3) Most hospital systems today require online access control decisions; 4) Records are not well protected today; 5) Provider-centric environment and 6) Complexity of access policies.
When records are transmitted among institutions, they are typically protected only by transport-level protocols. When the server or database is unavailable, access control decisions cannot be made. Today’s EMR systems patients have little or no access to their medical records. Despite the high level of regulation surrounding EMR use, medical systems do not adequately protect records. The state of the art access control matrix is overly complex, costly, and error prone. Therefore, in this paper, the author describes  efforts to provide self protecting EMRs on mobile devices using recent developments in attribute-based encryption (ABE). The paper highlights on Role-based and Content-based Access Control and focuses on their proposed Automated policy generation techniques including a a high-level overview of the system.

### Implementation

The paper describes a high-level overview of how medical institutions provide an encrypted CCR to users, and how cloud-based storage is implemented via Google Health (Fig. 1). Before medical information is released to the user, an access policy is implemented into the nodes of the CCR. Here, an attribute-based encryption (ABE) is implemented into the CCR. The policies are initially specified by the medical provider and may consider attributes of the patient such as the age of the patient, the sensitivity of the data, and the identity of the authoring agent. 

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_14/images/Akinyele_Fig1.png" title="Figure 1: Implementation of Attribute-Based Encryption" width="250" >}}

The paper uses a mobile application called "iHealthEMR" that interface with the provider's server and, optionally, with cloud-based storage by Google Health. The primary function of the application is to browse, update, and secure CCRs. There are two interfaces with the application. One of them is to interact with the web service provided by the hospital. The user can read encrypted CCRs downloaded on their phones by decrypting it using ABE private keys stored on the user's phone's keychain. The second interface interacts with Google Health, a cloud-based storage. This interface allows users to read and write any of their records and be given the option to store it on the cloud server.

In the mobile application, the authors implement a "lazy" decryption, which only performs decryptions of records on an as-needed basis. This results into using less memory and less processing power, thus preserving battery life. Eventually the usability can be improved by selecting decryption once, and it allows for all other entries to be decrypted in the background. Other functions from the application are the supporting of caching encrypted medical records for when network connectivity is unavailable. Finally, one of the main highlights is that the application allows users to choose whether to trust Google with the privacy of their records. Even if the records cannot be uploaded to Google Health, the system's architecture supports other cloud-based EMR systems as well.

### Experimentation
In order to evaluate Clicktok, the authors of the paper, used the click traffic obtained, filtered it and exposed it to a testbed with malicious apps and click malware. Through this they were able to get a click traffic that contained both legitimate and fake clicks.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_14/images/Akinyele_Fig2.png" title="Figure 1: Implementation of Attribute-Based Encryption" width="250" >}}
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
