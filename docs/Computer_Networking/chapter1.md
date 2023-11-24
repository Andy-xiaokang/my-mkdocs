# Chapter1 Introduction
## what is Internet? What is a protocal
Internet: ==**Network of Networks**==  
protocals define the **format**, **order** of **messages sent and received** among network entities, and **actions taken** on message transmission, receipt.  
## Network edge
approximate speeds  

|access network| speeds|
|:--:|:--:|
|Ethenet|Wired. Up to 100's Gbps per link|
|802.11 WiFi|Wireless. 10’s to 100’s of Mbps per device.|
|Cable access Network|Wired. Up to 10’s to 100’s of Mbps downstream per user.|
|Digital subscriber Line|Wired. Up to 10’s of Mbps downstream per user.|  
|4G cellular|Wireless. Up to 10’s Mbps per device.|

## The network core: packet/circuit switching, internet structure 
## performance: delay, loss, throughput  
delay: processing delay, queueing delay, transmission delay, propagation delay  
## layering, encapsulation, sevice models
layered Internet protocal stack  

1. ***application***: supporting network applications
    * http, IMAP, SMTP, DNS 
2. ***transport***: process-process data transfer  
    * TCP, UDP  
3. ***network***: routing of datagrams from source to destination
    * IP, Routing protocals 
4. ***link***: data transfer between neighboring network elements  
    * Ethenet, 802.11(WiFi), PPP  
5. ***physical***: bits "on the wire"  