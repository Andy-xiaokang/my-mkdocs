---
comments: true
---

# Chapter1 Introduction
## 1.1 what is Internet? What is a protocal
Internet: ==**Network of Networks**==  
protocals define the **format**, **order** of **messages sent and received** among network entities, and **actions taken** on message transmission, receipt.  
## 1.2 Network edge
approximate speeds  

|access network| speeds|
|:--:|:--:|
|Ethenet|Wired. Up to 100's Gbps per link|
|802.11 WiFi|Wireless. 10’s to 100’s of Mbps per device.|
|Cable access Network|Wired. Up to 10’s to 100’s of Mbps downstream per user.|
|Digital subscriber Line|Wired. Up to 10’s of Mbps downstream per user.|  
|4G cellular|Wireless. Up to 10’s Mbps per device.|

## 1.3 The network core: packet/circuit switching, internet structure 
## 1.4 performance: delay, loss, throughput  
delay: processing delay, queueing delay, transmission delay, propagation delay  
## 1.5 layering, encapsulation, sevice models
layered Internet protocal stack  
![20231124171819](https://s2.loli.net/2023/11/24/cedPxGOqnpyRoBv.png)

1. ***application***: supporting network applications
    * http, IMAP, SMTP, DNS 
2. ***transport***: process-process data transfer  
    * TCP, UDP  
3. ***network***: routing of datagrams from source to destination
    * IP, Routing protocals 
4. ***link***: data transfer between neighboring network elements  
    * Ethenet, 802.11(WiFi), PPP  
5. ***physical***: bits "on the wire"  

|layer|||
|:--:|:--:|:--:|
|application|message|M|
|transport|  segment | H~t~M |
|network|datagram|H~n~H~t~M|
|link|frame|H~l~H~n~H~t~M|
|pysical|bit||





