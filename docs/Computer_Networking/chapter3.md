---
comments: true
---

# Chapter 3 The transport layer
## 3.1 Introduction and transport-layer services  
TCP: transmission control protocol  

* reliable, in-order delivery
* congestion control  
* flow control
* connection setup  

UDP: User datagram protocol  

* unreliable, unordered delivery
* no-frills extension of "best-effort" IP
* service not available:  
    * delay guarantees
    * bandwith guarantees

## 3.2 Multiplexing and Demultiplexing
![20231203162315](https://s2.loli.net/2023/12/03/18CFrze9BGHWQ4q.png)  
![20231203162344](https://s2.loli.net/2023/12/03/cbr1qe9NJwtHW6X.png)  
![20231203162413](https://s2.loli.net/2023/12/03/jU9fFdZtqkxGAvo.png)  
![20231203162444](https://s2.loli.net/2023/12/03/cxi6TdpnmEaFtw9.png)  

## 3.3 Connectionless Transport UDP  
## 3.4 Principles of reliable data transfer  
### Principles of Reliable Data Transfer  
![20231203212241](https://s2.loli.net/2023/12/03/b8SLKUe9f4GzIwN.png)  
![20231203212338](https://s2.loli.net/2023/12/03/4k9FQTBtrAmSouy.png)  
### Pipelining increased utilization  
* Go-Back-N  
![20231209191836](https://s2.loli.net/2023/12/09/mcC9EangdtsDkoA.png)
![20231209191922](https://s2.loli.net/2023/12/09/TsD1HAFQPa3erYu.png)  
![20231209191944](https://s2.loli.net/2023/12/09/TI3PL4HMgA69v8u.png)

* Selective repeat  
![20231209192046](https://s2.loli.net/2023/12/09/RmOHteEl2LBbQgp.png)  
![20231209192116](https://s2.loli.net/2023/12/09/gGxDbWSaLfXecKm.png)  
![20231209192153](https://s2.loli.net/2023/12/09/fWE1oyQHVZDYeNl.png)  


## 3.5 connection-oriented transport: TCP
### tcp segment structure  
![20231209190516](https://s2.loli.net/2023/12/09/sbK7u1rqEToRvNQ.png)
* **sequence numbers:** byte stream "number" of first byte in segment's data  
* **acknowledgement number:** next byte expected from other side, **cumulative ACK**
### connection management 
![20231209190258](https://s2.loli.net/2023/12/09/tXuWTDkhGUEmcei.png)
### tcp fast retransmit  
![20231209191205](https://s2.loli.net/2023/12/09/DygLcYxlfCHG68W.png)  
### flow control  

## 3.6 congestion control  
### slow start  
initial cwnd = 1 then 2 4 8 ... exp  
### congestion avoidance  
* if timeout then cwnd reset to 1  
* if 3 ACK then cwnd = cwnd/2  

### quick restart  
TCP Reno: cwnd = cwnd/2 + 3, then linear add 1 MSS  
TCP AIMD (additive-increase multiplicative-decrease)  cwnd = cwnd / 2  
TCP CUBIC: cubic function  


