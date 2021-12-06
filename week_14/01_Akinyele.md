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
The paper very well addresses some major problem areas triggering the requirements of an effective systems: 1) EMR systems’ reliance on transport security; 2) Access control is online only; 3) Most hospital systems today require online access control decisions; 4) Records are not well protected today; 5) Provider-centric environment and 6) Complexity of access policies. The records transmitted among institutions are usually protected by transport-level protocols only. The access control decisions might get hindered in the absence of access to the server or database. Today’s EMR systems patients have little or no access to their medical records. The medical systems lacks adequate protection for records despite the high level of regulation regarding EMR use. The state of the art access control matrix is very complex, expensive, and sometimes it is prone to system error. Therefore, in this paper, the author proposed a a self protecting EMRs system for mobile devices using recent developments in attribute-based encryption (ABE). The paper highlights on Role-based and Content-based Access Control and focuses on their proposed Automated policy generation techniques including a a high-level overview of the system.

### Implementation

The paper describes a high-level overview of how medical institutions provide an encrypted CCR to users, and how cloud-based storage is implemented via Google Health (Fig. 1). Before medical information is released to the user, an access policy is implemented into the nodes of the CCR. Here, an attribute-based encryption (ABE) is implemented into the CCR. The policies are initially specified by the medical provider and may consider attributes of the patient such as the age of the patient, the sensitivity of the data, and the identity of the authoring agent. 

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_14/images/Akinyele_Fig1.png" title="Figure 1: Implementation of Attribute-Based Encryption" width="250" >}}

The paper uses a mobile application called "iHealthEMR" that interface with the provider's server and, optionally, with cloud-based storage by Google Health. The primary function of the application is to browse, update, and secure CCRs. There are two interfaces with the application. One of them is to interact with the web service provided by the hospital. The user can read encrypted CCRs downloaded on their phones by decrypting it using ABE private keys stored on the user's phone's keychain. The second interface interacts with Google Health, a cloud-based storage. This interface allows users to read and write any of their records and be given the option to store it on the cloud server.

In the mobile application, the authors implement a "lazy" decryption, which only performs decryptions of records on an as-needed basis. This results into using less memory and less processing power, thus preserving battery life. Eventually the usability can be improved by selecting decryption once, and it allows for all other entries to be decrypted in the background. Other functions from the application are the supporting of caching encrypted medical records for when network connectivity is unavailable. Finally, one of the main highlights is that the application allows users to choose whether to trust Google with the privacy of their records. Even if the records cannot be uploaded to Google Health, the system's architecture supports other cloud-based EMR systems as well.

### Experimentation
In order to evaluate the ABE techniques on medical records, the authors conducted several experiments using their implementation.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_14/images/Akinyele_Fig2.png" title="Figure 2: CP-ABE and KP-ABE Encryption and Decryption Times" width="250" >}}
In their experimentation, the authors measured time required for encryption and decryption under various scenarios and tested it on their Intel-based workstations and mobile devices.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_14/images/Akinyele_Fig3.png" title="Figure 3: Storage Overhead Incurred by ABE Encryption of Medical Records" width="250" >}}
To also show that the techniques induce an acceptable cost in record storage, the authors measured the ciphertext size overhead incurred by their encryption solution.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_14/images/Akinyele_Table1.png" title="Table 1: Policy Complexity" width="250" >}}
This table summarize the sample polcies, its types of timestamps, the number of leaves required to compute each policy in a binary tree. 

### Discussion
The first test to evaluate the efficiency of ABE encryption and decryption was done with a workstation and an Apple mobile device. To calculate their CP-ABE micro benchmarks, they took values of N from 1 to 100 and encrypted a message under a policy consisting of a single AND gate with N distinct attribute leaves. After that, a key was generated containing all N attributes and they instrumented both encryption and decryption processes to determine the time required for each operation. They did a similar methodology for the KP-ABE as well but placed the access policy within the generated key. The results of the tests on their Intel based platform and their ARM-based platform in the experimentation section. The x-axis is the number of leaf nodes or attributes in the access policy and the y-axis is the time required for encryption and decryption. Throughout all the trials, it is apparent that processing time linearly increases with policy complexity. The CP-lite variant is also depicted to be significantly better than the standard CP at complex policies. This result was expected for decryption time. However, it was not expected in the encryption results since there are no pairing operations like in decryption. They noted that it may be due to a side effect of the algebraic group assignments made during the implementation of the scheme. Overall, it was determined that encryption using any of the schemes is practical on an Intel-based platform. They also noted that decryption is a little more expensive with the CP-ABE scheme on mobile devices. Although the “lite” scheme requires a larger private key size, it is strongly recommended to support future applications. As long as the policy size is under 30 leaves, the scheme will have acceptable performance.

The next test they did was to determine storage overhead sustained from their ABE implementation. The results of the storage overhead test are shown in the experimentation section. The storage overhead added from ABE encryption is very dependent on attribute policy complexity. The worst case is with the treatment of minors ciphertext size increasing from 8.3 MB all the way to 46 MB with all nodes encrypted which was probably due to the ‘less than’ and ‘greater than’ operators that add 32 additional attributes to the policy tree. Also, due to metadata required by the CP-ABE scheme, each encryption of a node adds 68 bytes of overhead per encryption and about 250 bytes per policy attribute. Overall, the minor policy requires 9,183 bytes of overhead per encryption which is large compared to other cryptographic schemes. However, even though it is a lot larger, it shows a potential upper bound for a fully encrypted record that they believe is still acceptable.
Overall, the authors have demonstrated a proof of concept mobile app that allows offline access to encrypted records and a way to securely export those records to other cloud-based EMR providers.


### Audience Questions
1. Is there a reason 128 bit size was used in the AES over other larger bit sizes?

  We believe that there is no reason for why the authors used 128-bit keys for AES other than a simple implementation and for a proof-of-concept. A 128-bit size key is usually the less secured type of AES encryption. Having more bits, a 192-bit or a 256-bit AES encryption, would progressively give more rounds of encryption and improve the security of the one used in the paper. 

2. Do you think this proposal is still secure as of today?

  We believe that this proposal will not be secured when compared to today’s standards. It was discussed earlier that a 128-bit size AES encryption showed less encrypted security. It could be argued that the minimal action needed to break into a 128-bit size AES encryption is the same for a 256-bit size AES encryption. We believe that due to this paper being published in 2011 and the advancement of quantum computing, AES will soon become obsolete.

3. Along with the ciphertext, ABE requires the sender to provide information about the receiver's required attributes. Is this system capable of preventing that?

  We are not sure about the meaning of your question. To elaborate on the concept of the ABE approach used in this paper, the nodes in the CCR are encrypted using key- or ciphertext-policy ABE under an access policy. These policies are then initialized with the attributes of the user such as age, name of physician, etc.
