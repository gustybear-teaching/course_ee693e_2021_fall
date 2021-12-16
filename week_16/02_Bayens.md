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
{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_16/images/Bayens_Fig12.png" title="Figure 1: Mean Measured of Raman Scattering" width="250" >}}

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_16/images/Bayens_Fig13.png" title="Figure 2: Classifcation Using Mean and Standard Deviation" width="250" >}}

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_16/images/Bayens_Fig15.png" title="Figure 3: Comparison of Rectilinear 60% Fill vs. Malicious 20% Honeycomb Fill" width="250" >}}

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_16/images/Bayens_Fig16.png" title="Figure 4: Comparison of Frequency Response Between Different Printings" width="250" >}}

### Discussion
As we can see from the first figure, we can see all of the variations in timings that 2FA-PP observes, whether it being a normal login, to a phishing attack which modifies the obfuscated code. Although phishing attacks are able to successfully modify the obfuscated code, the round trip and modification takes a considerable amount of time, where we can set our threshold to contain the vast majority of our baseline timing, while preventing a majority of phishing attacks.

As from the second figure, by setting the threshold accordingly, we see that attackers within a different locality as the user have a difficult time successfully attacking 2FA-PP. However, if they are in the same locality, such as the same Wi-Fi or Hotspot, the success rate is significantly higher. We could reduce the success rate by tightening our threshold, but this is at the cost of false positives, where legitimate logins are deemed suspicious.

For the third figure, as this is a scalable implementation, we can send multiple challenges to the client. This lessens the chance for an attacker to successfully complete all of the challenges within the given time frame, therefore securing the login from phishing attacks. We find that at about 5 challenges, gives the best chance of preventing phishing attacks, even with local adversaries.

### Questions
(1) Why did they choose acoustic classification over other classification techniques such as image classification?

(2) Does the paper mentions about making the MySQL database faster/more efficient as their proposed system introduced more overheads because of choosing identity-based encryption scheme?

(3) Would changing the material the printer is made of or installing additional acoustic device that emits random noise to throw of the side channel attacks work?

