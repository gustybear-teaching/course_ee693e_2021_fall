---
title: "02: See No Evil, Hear No Evil, Feel No Evil, Print No Evil? Malicious Fill Patterns Detection in Additive Manufacturing
Christian Bayens, Tuan Le, Raheem Beyah, Mehdi Javanmard"
date: 2021-12-15
type: book
commentable: true
# Provide the name of the presenter
summary: "Presenter(s): Clyde James Felix, Saige Dacuycuy, Jeanalyn Wadsack-Myers"
# Provide other tags that describe the paper
tags:
- teaching
- ee693e
- additive manufacturing
---
***
## Paper Summary
Two factor authentication (2FA) schemes help provide a strong user authentication alongside the traditional password. However, many 2FA schemes are still vulnerable to phishing attacks, where the 2FA can be phished along with the password. This is where the paper proposes 2nd Factor Phishing Prevention, 2F-PP, which uses the browser’s API to communicate with an external device, such as a mobile phone, and lets the phone check what domain the browser is connected to. With this domain check, the phone can decide whether to authenticate the log-in or reject it and alert the user of an attempted attack.
***
## Presentation
{{< youtube PH9HPmnIK24 >}}
***
## Review
### Strengths
- 2FA-PP requires little user interaction to set up, and no user interaction per login once set up.
- Time added by 2FA-PP is negligible, adding about less than a seconds worth towards the login time.
- Utilizes currently available software and hardware used in current 2FA schemes, such as bluetooth and browser APIs, so implementation into current systems is feasible.

### Weaknesses
- As 2FA-PP is timing based, attackers within the same locality as the user (such as on the same Hotspot or Wi-Fi) has a significantly higher chance at success than other attackers
### Detailed Comments
2FA-PP is a novel 2FA scheme which helps mitigate phishing attacks. Although it has a poor time preventing phishing attacks on the same network, with an attacker success rate having a worse case scenario of 35% success rate if not tuned correctly, it is more than likely that the phishing attack will occur from a proxy server, moving its location far from the user, meaning it would be able to prevent a majority of phishing attacks. Since 2FA-PP only requires the user to set up an application and the server to set up a database to handle interactions with the application, it is a user friendly scheme which is easy to implement into existing structures, using current generation browser APIs to communicate with the phone’s BLE, which is readily available to a majority of users who use 2FA. Some worries for 2FA-PP stems from the use of the browser’s API to communicate with BLE, as this can be a vector for attack by the phishing user where they can take over communication and report a real domain as opposed to the phishing domain, but this is circumvented by the use of obfuscation techniques, such that the report of the domain will be unobfuscated in a certain way, preventing a phishing user from figuring out and using this obfuscation technique within the given time frame.

### Implementation
To implement 2FA-PP, there are two components: the smartphone application and the server. The smartphone application will act as the software token, and will communicate with the server to keep a set of tokens up to date. The smartphone application requires minimal permissions from the user, only needing Bluetooth access, which is used to communicate with the browser. As for the server, it will handle the registration of the 2FA device, or our smartphone application,  and each instance of a login which requires a 2FA.

Although these are the two main components to be implemented, there are also some intermediate steps that are taken. The client side, which would be the computer logging onto the server, needs Bluetooth functionality, and the ability to run JavaScript, the two of which are widely available on a majority of laptops and desktops.

Once the smartphone application is registered as a 2FA device, the flow of authentication is as follows. When a client logs into the server, the server will request the 2FA device, or smartphone in our case, a token. To get this token, a challenge is sent in a form of a JavaScript file, which is encrypted with a key which only the server and smartphone have. The smartphone knows the answer to this JavaScript file, which is used to verify the URL. Once the smartphone sends the decryption key to the client, it will start a timer, where the browser will execute the JavaScript file to unobfuscate the ciphertext it contains. The obfuscation process contains references to the legitimate URL, which is obtained through the browser’s reference to the URL, window.location, which cannot be modified by a phishing user. Once the challenge is completed, the answer is sent to the smartphone for verification. If correct and within the timing threshold, the smartphone will send the token to verify the login.

### Experimentation
The authors wanted to embed contrast agents or markers at precise Cartesian coordinates within the 3D printed modes. For 3D printing filament, the authors would produce three types of filaments. One that was made using ABS pills that provides extremely durable thermoplastic, and other variants of ABS that is coated with GNRs or DTTCI. These types of filaments were implemented by embedding and coating the objects, then evaluating using Raman spectroscopy and CT scans.

Figure 1 is given by evaluating the Raman spectra of the blank or unmodified 3D printed disk, a 3D coated with GNRs or DTTCI, or a 3D printed disk with GNRs or DTTCI embedded filament. To achieve the embedding of the filaments, a C++ program was written to allow users to embed filament at desired locations by modifying the G-code. In this case, the 3D printer would switch between a nozzle with normal filament to a nozzle with GNR or DTTCI filament. When using Raman spectroscopy on the disk the 3D disk is first exited with a 785 nm light for 20s per accumulation of data.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_16/images/Bayens_Fig12.png" title="Figure 1: Mean Measured of Raman Scattering" width="250" >}}

To differentiate between the three types of disks, the authors would use the mean and standard deviation of the spectra to distinguish the cluster of data set (Figure 2).

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_16/images/Bayens_Fig13.png" title="Figure 2: Classifcation Using Mean and Standard Deviation" width="250" >}}

To demonstrate Figure 3 and Figure 4, the authors evaluated their approach on a tibial prothesis. Since prosthetics differ slightly between patients, the authors assume that they need to perform a malicious print identification periodically on the prosthetic. Acoustic error detection was used to identify malicious prints in the early parts of the printing stage, and an FFT analysis was performed to compare malicious prints against target and training prints.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_16/images/Bayens_Fig15.png" title="Figure 3: Comparison of Rectilinear 60% Fill vs. Malicious 20% Honeycomb Fill" width="250" >}}


{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_16/images/Bayens_Fig16.png" title="Figure 4: Comparison of Frequency Response Between Different Printings" width="250" >}}

In Figure 5, the G-Code of the intended print was compared to a CT scan at 15-micron/voxel resolution. To demonstrate a proof-of-concept, steel particles were injected into the tibial knee implant prints in order visualize its inner structure. Steel particles would produce similar responses to GNRs by exhibiting high X-ray density.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_16/images/Bayens_Fig16.png" title="Figure 5: Comparison of G-code Simulation vs CT Scan of the Printed Model" width="250" >}}

### Discussion
Figure 1 shows the mean measurements of Raman scattering of 3D printed disk. The spectrum of the 3D printed disk coated with DTTCI has huge photon counts across the spectrum. This is also true with the embedded filament design, which falls between the control experiment and the fully coated experiment. The challenge with Raman scattering for analyzing the model is that this does not reflect he approximate distribution of contrast agent embedded in the filament, since it might be a cluster or sparse of contrast agents of markers. Although the figure only shows results with DTTCI, it was concluded that a similar response can be made with using GNRs as well. 

Figure 2 helps with the idea of classification of the three types of disks: ABS; GNRs embedded disks; and DTTCI embedded disks. The authors trained a logistic regression model, and the classification using mean and standard deviation shows 100% accuracy against the blank ABS (226 samples) filament for both GNRs (179 samples) and DTTCI (71 samples) embedded filaments.

Figure 3 shows the confident value of both the target print and the malicious print. By setting the confidence threshold to zero, a positive error classification can be made within the first 360s of the print. The threshold value may be set to anything less than 18 without causing a false positive. Overall, the acoustic error detection saves over 2 hours of print time and prevents potentially harmful prints. 

Figure 4 is the FFT of a target print and a malicious print compared to a training print. The malicious print shows a different frequency response near 0.2 Hz as highlighted by the lower box. The upper box highlights the closeness of the peaks between the training and target prints while differentiating from the malicious print. The significance of this figure is that during the printing of a 3D object with 111 layers, it takes less than 1% of the total print time to identify the error.

Figure 5 is the comparison between the target design and the printed model under a CT scan. With larger structures like a tibial prosthesis, Raman spectroscopy cannot be used as the sole analyzer for structural integrity. For designs as large as 30-mm, a CT scan approach can be used to see physical changes in the structure. In this case, since the steel particles have high X-ray density, the inner structure of the tibial prosthesis can be analyzed. The idea of using steel particles can further introduce the use of GNRs into post-production evaluation.

### Questions
(1) Why did they choose acoustic classification over other classification techniques such as image classification?



(2) Does the paper mentions about making the MySQL database faster/more efficient as their proposed system introduced more overheads because of choosing identity-based encryption scheme?

(3) Would changing the material the printer is made of or installing additional acoustic device that emits random noise to throw of the side channel attacks work?

