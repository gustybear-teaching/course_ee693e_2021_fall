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
This paper presents a scheme to verify and detect intrusion within the additive manufacturing (AM)  printing process without the use of printer firmware and the controller PC. The 3D print is analysed through three layers of verification: side-channel verification of acoustic signatures, real-time spatial tracking of machine components, and post-production materials analysis. Each layer of verification is tested on simple 3D structures using three different types of printers and one CNC machine before the full scheme is evaluated. Lastly, to test the effectiveness of the scheme, a use case with a prosthetic tibial knee implant was done. The scheme proved to be very promising for mass production AM and for third-party AM producers.
***
## Presentation
{{< youtube 4Aezj_TOHoQ >}}
***
## Review
### Strengths
- Provides security in AM due to implementing malicious print detection.
- 100% accurate when predicting malicious prints.

### Weaknesses
- Materials verification system might be costly due to having Raman Spectroscopy/CT machines.
- It is possible there might be an error due to having small sample sizes.

### Detailed Comments
The paper focuses on preventing in 3D printing by implementing malicious fill pattern detection techniques. The design of this proposal is composed of verification of design parameters that utilize analysis of acoustic signals, spatial position of machine components, and embedded materials. The reason of using these parameters is to be able to get access to AM information process without accesing STL file of G-code instructions.

The authors contributed this paper on:
* Multi-layered design verifications in AM (design, manufacturing, and materials).
* Proposed implementations of approach for in-house and third-party AM producers.
* Prosthetic Tibial Implant case study.

### Implementation

This paper evaluates the identification of malicious prints, observation of the detected error, and the post-production materials verification. A logistic regression is used to detect whether there is a malicious print or not. The Area Under Receiver operating characteristic (AUROC) curve is a metric to determine the performance of the detection. In this experiment, small sample size is used because 3D printing takes long. This experiment is tested on using different printer models (TazMini, Orion Delta, Taz6). This experiment was also tested on a noisy environment. When visualizing malicious prints, researchers used spatial sensing to observe real-time.

For post-production materials veridication section, GNRs and DTTCI can be combined to be used as a contrast agent.

This experiment is tested on a specific use case on printing a prosthetic Tibial Implant. 

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

Acoustic classification is used to explore acoustic signals generated by the actuators and fans in a 3D printer. In a large-scale implementation, image classification may not be as useful since it would require larger sets of data to be analyzed. For the verification process, using the acoustic classification is more useful in comparing a single-file training set to a test set. In contrast, an image classification requires training of multiple sets of data.

(2) Does the paper mentions about making the MySQL database faster/more efficient as their proposed system introduced more overheads because of choosing identity-based encryption scheme?

We do not understand the question since a MySQL database was not mentioned in the paper. The database was used to store the confidence score of a classification result. Rectilinear filled structures had higher confidence values than Honeycomb filled structures. Thus, from the database, prints with a Rectilinear fill had more structural integrity than those with malicious prints or Honeycomb fill.

(3) Would changing the material the printer is made of or installing additional acoustic device that emits random noise to throw of the side channel attacks work?

We believe that changing the material of the case of the 3D printer may decrease side-channel attacks. Side-channel attacks commonly occur from attackers listening to noise from outside of the printer. If the 3D printer includes material that absorbs sound from the inside, or dampens audio signals, then this may be a simple solution to side-channel attacks. Another solution would be to make a noise generator and include a more directional microphone to record audio signals.
