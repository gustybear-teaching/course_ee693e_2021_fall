---
title: "02: Predictive Adaptive Streaming to Enable Mobile
360-degree and VR Experiences"
date: 2021-10-18
type: journal
commentable: true
# Provide the name of the presenter
summary: "Presenter(s): Alemayehu Beemnet, Banh Nguyen, Tahmid Tasmia"
# Provide other tags that describe the paper
tags:
- teaching
- ee693e
- virtual reality
---
***
## Paper Summary
In order to deliver 360-degree videos and cloud/edge-based virtual reality applications, a high level of bandwidth and low latency is required, both of which are difficult to achieve over mobile networks. The practice of streaming only the field of view is a common way to reduce bandwidth consumption (FOV). While extracting and transmitting the FOV in response to user head motion can reduce latency significantly, it can have a negative impact on the user experience. A predictive adaptive streaming approach is proposed in this paper, in which the predicted view with a high predictive probability is encoded in relatively high quality according to bandwidth conditions and transmitted in advance, based on the findings of the paper. This method uses Long Short Term Memory variation of neural network trained on a large dataset to predict the next viewpoint a user will see. The use of edge devices reduces the latency compared to a cloud using system, but also keeps the head mounted displays (HMD) lighter because the computation is done outside the displays. Predicting head movement and streaming the viewpoint in advance reduces the latency, while streaming only the field of view with high quality reduces the bandwidth. This approach works on any existing network infrastructure.
***
## Presentation
{{< youtube ynD_kXCivFE >}}
***
## Review
### Strengths
- The proposed LSTM model outperforms the other methods
-  The Predictive adaptive streaming algorithm can run in real-time
-  Works on existing network infrastructures

### Weaknesses
- Need to test the predictive model to real users
- The performance difference in different type of video content
- The video content needs to be encode before streaming
- Tends to be computationally expensive

### Detailed Comments
360?? videos and cloud/edge-based virtual reality applications require extremely high bandwidth and low latency. The method of predictive adaptive streaming is based on a model of viewpoint prediction developed using deep learning. It predicts the user's gaze in a 360-degree view based on previous head movements. They examine how to develop mobile (wireless and lightweight) head-mounted displays (HMDs) and how to enable VR experiences on mobile HMDs while operating on bandwidth-constrained mobile networks while meeting ultra-low latency requirements in this article. The paper's approach overcomes both bandwidth and latency constraints by predicting head motion.

They present a real-time predictive long-term memory (LSTM) model for 360-degree video streaming in this article. Additionally, they demonstrate significant quality, bandwidth, and network capacity benefits over current state-of-the-art streaming without bitrate adaptation (BTVR). We investigate the problem of sequence prediction in this article, which is defined as predicting the next value(s) given a historical sequence. At this stage in their respective fields, conventional machine learning and deep learning approaches to sequence prediction are not considered very effective. They are the first to suggest a method for 360-degree video streaming prediction.


This method, which relies solely on head motion data, is more efficient and concise in addressing the ultra-low latency challenge in our current video-streaming scenarios. Because most HMDs are incapable of tracking gaze, the gaze-prediction technique cannot be implemented directly. The edge device can be a Mobile Edge Computing (MEC) node embedded within the mobile radio access or core network, or it can be a. Local Edge Computing (LEC) nodes can be located on the user's premises or even on his or her mobile device. Utilization of cloud servers for predictive view generation is also a possibility.



In each time point, a viewpoint can occur in up to K unique tiles (e.g., every 200ms). The entire predictive adaptive streaming method is decomposed into two subtasks: viewpoint prediction and adaptive streaming. Over 80% of videos have a duration of a few seconds and approximately 85% have a viewing time of several thousand hours. Head pose data for 19 online virtual reality videos are included in the dataset.



The attention map is defined as a series of probabilities that a viewpoint is contained within a tile for n viewers over the time period cts1 to cts2. Figure 1 illustrates an attention map, illustrating how users' attention was distributed during a one-second period within the Kong VR video's high-motion sequence. For viewpoint feature representation, we employ a tile-based format. Each grid is 30??30?? in size, which divides the 360-degree view into 72 tiles. They chose 2s as the prediction window because it outperforms 3s, 4s, and 5s in terms of performance.

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/blob/main/week_08/images/fig%206.png" title="Fig. 1: Attention Map" width="320" >}}


Given the previous sequence of viewpoint tiles, their LSTM model predicts which tile will contain the viewpoint. The proposed model optimizes parameters by minimizing cross-entropy, and was trained using 30 mini-batches and 128 LSTM units. Predictive FOV streaming can help meet the ultra-low latency requirement of an immersive 360-degree or VR experience. However, wireless network bandwidth may not always be sufficient to transmit with high accuracy the predicted FOV (that is, considering a high enough number of "m" tiles). They examine how viewpoint prediction can be used to develop an adaptive streaming technique for 360-degree and virtual reality videos. They can find an optimal solution that maximizes user experience (minimizes impairment) given a bandwidth constraint BW(t) for the time slot t.



Next, they present the experimental results and experimental setup for the proposed LSTM model. This approach is implemented in Python using Keras on an Intel Core i7 Quad-Core processor with 32GB RAM. Up to one hour of training is required for state-of-the-art methods. As the number of tiles m increases, the accuracy of the FOV prediction increases while the number of pixels saved decreases.



Their LSTM model can predict the FOV with an accuracy of approximately 95% when only four tiles (i.e., m = 4) are used, resulting in FOV and pixel savings of approximately 70% for Fashion Show and Roller Coaster, and 66.8 percent for Whale Encounter. They use an adaptive streaming technique known as viewport-driven rate distortion optimized streaming. This method enables adaptive video streaming based on heatmaps that quantify the probability of navigating various spatial segments of a 360-degree video over time. We calculate the P(QHigh), P(QMedium), P(QLow), and PSNR in actual user FOV under various bandwidth conditions using 1000 head motion traces from a video sequence called Fashion Show.



Their predictive adaptive streaming algorithm VR-PAS achieves an average P(QHigh) of approximately 98 percent while using 25Mbps, whereas a typical HDTV stream requires 57.6Mbps in total bandwidth. When compared to conventional streaming, predictive adaptive streaming (VR-PAS) can save up to 53.3 percent on network bandwidth (i.e., non-adaptive streaming). The method achieves a PSNR of 50dB when operating within a range of fixed bandwidth limits.



The predictive adaptive streaming algorithm VR-PAS can run in real time with a runtime of less than 70 milliseconds. With a round-trip transmission latency of less than 25ms and the additional delays associated with viewpoint prediction and decoding, their algorithm can be executed in real time approximately every 100ms. We present a multilayer LSTM model that is capable of learning general head motion patterns and forecasting future viewpoints. Their method outperforms state-of-the-art methods on a real-world dataset of head motion traces and demonstrates significant potential for bandwidth reduction while maintaining a positive user experience (i.e., high PSNR).

### Questions
(1) What is the normal range of bandwidth needed for gaming?

Normally, this demand varies based on the game you are playing. For online games, it is recommended that you have a connection speed of between 3 and 8 megabits per second. However, we believe that your question is related to the amount of video streaming bandwidth required for 360-degree video transmissions. A minimum of 25 megabits per second is required for 4K streaming.

https://help.netflix.com/en/node/306

(2) What is the reason why LSTM is used for this research?

Due to the fact that there can be lags between important events in a time series that are unknown in terms of duration, the use of LSTM networks for time series data classification, processing, and prediction is particularly advantageous in time series data classification, processing, and prediction. When training traditional RNNs, the LSTM algorithm was developed in order to deal with the vanishing gradient problem that can occur.

(3) What do you think is the next step for FOV probability?

In order to improve prediction accuracy even further, they intend to investigate and develop more comprehensive models for viewpoint prediction that take into account the type of video content being viewed in the future research. Also on the agenda is the investigation and development of more comprehensive models for joint head and body motion in order to provide immersive experiences with six degrees of freedom.
