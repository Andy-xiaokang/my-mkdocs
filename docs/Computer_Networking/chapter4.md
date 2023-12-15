---
comments: true
---

# Network Layer: "data plane"
## 4.1 network layer: overview
![20231210145717](https://s2.loli.net/2023/12/10/TfO3XSPMDnexYiz.png)  
![20231210150024](https://s2.loli.net/2023/12/10/8WiNldCKmH3auf4.png)
![20231210153314](https://s2.loli.net/2023/12/10/1VEBmSIlTH3yKgO.png)
## 4.2 what's inside a router  
![20231212212142](https://s2.loli.net/2023/12/12/eqnmHMbs6vhdAy8.png)
### input ports  
![20231212212237](https://s2.loli.net/2023/12/12/HRiQCfceotPqDuY.png)  
![20231212212324](https://s2.loli.net/2023/12/12/BvrP8WEZ7OwtDy3.png)
![20231212212425](https://s2.loli.net/2023/12/12/XWYICUmdiQ1ATke.png)
### switching  
![20231212212726](https://s2.loli.net/2023/12/12/IKGzfklj1ycEbqW.png)
![20231212212743](https://s2.loli.net/2023/12/12/YJKNjEVASMktUFp.png)
![20231212212601](https://s2.loli.net/2023/12/12/riEePbsmh9VaF3X.png)
### output ports  
![20231212212841](https://s2.loli.net/2023/12/12/TO4L9saCqFQhePu.png)
### packet buffering, scheduling
![20231212213022](https://s2.loli.net/2023/12/12/sOLcGg8TmQxBr6Y.png)
![20231212213044](https://s2.loli.net/2023/12/12/fEGjCbo357viIaX.png)  
![20231212213108](https://s2.loli.net/2023/12/12/mxW2FSlQieuN5Ay.png)  

## 4.3 IP: the internet protocol  
### IPv4, addressing  
IP address: 32-bit identifier associated with each host or router interface  
![20231212213204](https://s2.loli.net/2023/12/12/bivWUR7stBh4rCx.png)
![20231212213237](https://s2.loli.net/2023/12/12/Mb5Ag14tm9C8epv.png)
### subnet
![20231212213437](https://s2.loli.net/2023/12/12/hpMJrZuY65n4iKg.png)
### CIDR 
![20231212213629](https://s2.loli.net/2023/12/12/WKQeUkVxjgSin3G.png)
### DHCP(host part)  
![20231212213738](https://s2.loli.net/2023/12/12/QXBcqRNV4onxpgM.png)
![20231212213808](https://s2.loli.net/2023/12/12/x6hzOK9bZ4ocuU7.png)
![20231212213828](https://s2.loli.net/2023/12/12/n6AXvVpRokN7OdF.png)
### (subnet part)
![20231212213956](https://s2.loli.net/2023/12/12/cZbtsTmj7VS6XJA.png)

### NAT, IPv6  
![20231212214112](https://s2.loli.net/2023/12/12/X4PbjKHI9v5oF7V.png)
![20231212214214](https://s2.loli.net/2023/12/12/3uZerv1noQgjkCV.png)
![20231212214259](https://s2.loli.net/2023/12/12/tKG8JEAefUMnszO.png)
![20231212214358](https://s2.loli.net/2023/12/12/GilewsxcCqHXSLD.png)  
![20231212214457](https://s2.loli.net/2023/12/12/qdUcnStygAuCE2r.png)
![20231212214521](https://s2.loli.net/2023/12/12/lDR5pBndsrzHvuL.png)  
![20231212214551](https://s2.loli.net/2023/12/12/kldo3tKvGmjXYEC.png)

## 4.4 Generalized Forwarding, SDN  
![20231212214634](https://s2.loli.net/2023/12/12/hgdq4F9DnVwG68Z.png)
![20231212214655](https://s2.loli.net/2023/12/12/pD6GxP2ingXJt5W.png)  
![20231212214751](https://s2.loli.net/2023/12/12/hkXmJODo29nexbL.png)  

## 4.5 Middle boxes
![20231212214935](https://s2.loli.net/2023/12/12/EtkTox1zdpnJr6A.png)  
![20231212215000](https://s2.loli.net/2023/12/12/FvNGpkjo5JCbT9K.png)
![20231212214841](https://s2.loli.net/2023/12/12/hVmFIBUaLvkNSP6.png)  
