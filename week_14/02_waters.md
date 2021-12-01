---
title: "02: Building an Encrypted and Searchable Audit Log 

B. Waters, D. Balfanz, G. Durfee, D. Smetters"
date: 2021-11-24
type: book
commentable: true
# Provide the name of the presenter
summary: "Presenter(s): Clyde James Felix, Banh Nguyen, Beemnet Alemayehu"
# Provide other tags that describe the paper
tags:
- teaching
- ee693e
- Audit Log
- Cryptography
---
***
## Paper Summary

***
## Presentation
{{< youtube A2pjPfPfrRE >}}
***
## Review
### Strengths
- Secured audit log encryption with search feature.

### Weaknesses
- Must require audit agents to create search capabilities.
- Introduces considerable overhead on the proposed ID-based schemes.

### Detailed Comments
Most server software requires secured audit logs against attacks. A secure audit log is important in telehealth field due to the sensitive data hospitals contain. A secured audit log must be tamper resistant, verifiable, has data access control, and has search capabilities. This paper proposes an approach to build a secured audit log based on Identity-Based Encryption (IBE). In this approach, the master secret is held by trusted authority to issue keyword search capabilities. Audit log entries are encrypted with public keys corresponding to keywords. In this scheme, the adversary cannot tell which public keys was used for each ciphertexts.



### Implementation
A database audit log system that creates asymmetrically encrypted and searchable entries was implemented for testing. The proxy server was a MySQL server developed on a multi-threaded linux platform that allows multiple users to run the system in parallel. The IBE operations were based on a Stanford Identity-Based Encryption library and the symmetric encryption was based on Cryptlib library. The IBE parameter values include a p = 1024 and q = 160. A 128-bit AES key was used for the symmetric encryption. The server has a cache to implement reuse pairing and random reuse. The performance measurements were taken on a Pentium IV processor machine running RedHat Linux 9.0 with 2GB of memory. The speed of the processor is 2.8GHz. The cost of encryption for each keyword with the pairing computation, modular exponentiation, and look up in the cache totals 180ms. However, if the keyword is in the cache, it only takes 5ms to execute modular exponentiation. So, the use of cache has sped up the process with a huge margin. As a reference, a 100MB cache can hold upto 800,000 keywords. 

### Experimentation
<!-- {{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/responsetime.jpg" title="Response Time" width="300" >}}

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/successrate.jpg" title="Success Rate with One Round" width="300" >}}

{{< figure src="https://github.com/gustybear-teaching/course_ee693e_2021_fall/raw/main/week_02/images/multipleattempts.jpg" title="Success Rate with Multiple Rounds" width="300" >}}
 -->
### Discussion


### Questions
(1) So to reduce overhead, the authors plan to implment the indexing algorithm in the future?

There were two bottlenecks defined for optimization process. The first one was the computations of the pairing and the other one was the modular exponentiations for each keyword w. Indexing optimizes by creating an index of keywords at periodic intervals in the log, instead of storing IBE encryptions with each log entry. This increases performance because the pairing and modular exponentiation would only need to be done once per keyword and reusing a key would only require a lookup in the log. To reduce overhead, indexing can be paired with a pairing reuse or randomness reuse, which will increase the advantages of using indexing due to the keyword repetition employed by the other steps. 

(2) Some literature mentions that, identity based crypotography causes identity recovation problem, does this paper cover this aspect?

(3) Are there any tradeoffs with optimizing the asymmetric scheme?

There is a tradeoff when trying to optimize the performance of the asymmetric scheme. When you gain performance in terms of computation time reduction, you will use extra space/memory you would not need originally. So, whenever you are optimizing you will have to consider this time/space tradeoff and the tipping point would depend on the case at hand. For example, when using indexing in the asymmetric scheme, the extra memory used for the buffer was worth the time gain because the buffer did not demand that much space and the time gain was noticeably different. 