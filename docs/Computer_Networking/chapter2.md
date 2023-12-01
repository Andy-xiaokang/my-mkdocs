---
comments: true
---

# Chapter2 Application layer
## 2.1 Principles of Applications  
### Processes communicating
process: program running within a host  

* within the same host, two processes communicate using ==***inter-process communication***==(defined by OS)
* processes in different hosts communicate by exchanging **messages**

client process: process that initiates communication  
sever process: process that waits to be contacted  
### Sockets
![20231125222508](https://s2.loli.net/2023/11/25/sBUAMw8DICbVjh3.png)  

## 2.2 Web and http  
![20231126142357](https://s2.loli.net/2023/11/26/rNVPhdZnKBXYpJU.png)  

### HTTP 
HTTP: hypertext transfer prototol  use port 80

* web's application-layer protocol
* client/server model:
  * client: browser that requests, receives, (using HTTP protocol) and "displays" Web objects
  * server: Web server sends (using HTTP protocol) objects in response to requests
* HTTP uses TCP  
* HTTP is "stateless": server maintains no infrmation about past client requests  

maintaining user/server state: cookies  
when initial http requests arrives at site, site creates:  

* unique ID(aka "cookie")  
* entry in backend database for ID 
* subsequent HTTP requests from user to this site will contain cookie ID value, allowing site to "identify" the user  

conditional get  `If-Modified-Since: Wed, 09 Sep 2020 16:06:01 -0700`  
**Goal: don't send object if browser has up-to-date cached version**(client have a cached copy of the object)  

## 2.3 Email, SMTP, IMAP  
### three major Components
* user agents  
* mail servers
* simple mail transfer protocol: SMTP

SMTP: simple mail transfer protocol, Pushes email from a mail client to a mail server(use port 25)  
IMAP: pull email from mail sever to mail client  

## 2.4 DNS (domain name system)  
**root name servers**: incredibly important internet function  
**Top-Level Domain servers**: responsible for .com .org, .net, .edu, .aero, .jobs, .museums, and all top-level country domains, e.g: .cn, .uk, .fr, .ca   
**authoritative DNS servers**: organization's own DNS server, providing authoritative hostname to IP mappings for organization's named hosts  
**local DNS name servers**: when host makes DNS query, it is sent to its local DNS server   
![20231126221420](https://s2.loli.net/2023/11/26/x9Xoan3NL4sm1JV.png)  
![20231126221720](https://s2.loli.net/2023/11/26/rKTzHA9gECG67pM.png)  
![20231201164719](https://s2.loli.net/2023/12/01/IGhz4klOoQNyv8Z.png)
`nslookup -NS domain_name` can return the authoritative DNS of the domain_name  
`nslookup domain_name` can return the ip of the domain_name  

## 2.5 Sockets programming
### socket programming with UDP  
UDP client:  
![20231129201350](https://s2.loli.net/2023/11/29/L1JYaNdqizkfrt6.png)  
UDP server:  
![20231129201457](https://s2.loli.net/2023/11/29/3bLkAWr1qFwRJsx.png)
UDP: no 'connection' between client and server  

* no handshaking before sending data  
* sender explictly attachs IP destination address and port to each packet  
* receiver extracts sender IP address and port from received packet  

`socket(AF_INET, SOCK_DGRAM)` creates this type of socket  
provides unreliable transfer of a groups of bytes (“a datagram”), from client to server  
data from different clients can be received on the same socket  
the application must explicitly specify the IP destination address and port number for each group of bytes written into a socket  

### socket programming with TCP 
TCP client:  
![20231129201624](https://s2.loli.net/2023/11/29/ojQxeTDKvACuMPG.png)  
TCP server:  
![20231129201731](https://s2.loli.net/2023/11/29/Ia6p8QdHiS1VYUl.png)

TCP:  
`socket(AF_INET, SOCK_STREAM)` creates this type of socket  
a server can perform an accept() on this type of socket  
when contacted, the server will create a new server-side socket to communicate with that client  
provides reliable, in-order byte-stream transfer (a “pipe”), from client to server  

What happens when a socket`connect()` procedure is called/invoked?  
This procedure creates a new socket at the client, and connects that socket to the specified server.