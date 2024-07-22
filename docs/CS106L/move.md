---
comments: true
---

# Move Semantics

## lvalues VS rvalues

How do we distinguish between when we **CAN** and **CANNOT** move?  
![20240711225604](https://s2.loli.net/2024/07/11/hLuJSNr6xcwjVB2.png)
![20240711225747](https://s2.loli.net/2024/07/11/9kv13wEFAea8KOr.png)
![20240711231541](https://s2.loli.net/2024/07/11/S7YiNhWf4PKcBL9.png)
![20240711230914](https://s2.loli.net/2024/07/11/8UsnaQXH6Rzl9Ji.png)
![20240711235603](https://s2.loli.net/2024/07/11/fkeqAcRoBmDUJsj.png)
![20240712001429](https://s2.loli.net/2024/07/12/BrEHdZXGMvFkVhc.png)
![20240712001459](https://s2.loli.net/2024/07/12/i6IePyn8LsUrYvC.png)
![20240712002350](https://s2.loli.net/2024/07/12/S5tCN1sWGTKrY4w.png)
![20240712004239](https://s2.loli.net/2024/07/12/BTfVxS7ojgGQCIi.png)
![20240712004323](https://s2.loli.net/2024/07/12/oG8pyWhuw69IkQt.png)
![20240712004411](https://s2.loli.net/2024/07/12/d1jKhJvuBAbWaDG.png)
![20240712005802](https://s2.loli.net/2024/07/12/wWdV2pkfXrK9Y6v.png)

## move constructor and assignment

How do we actually move?
![20240712011940](https://s2.loli.net/2024/07/12/58Vv3edtfwjJTxz.png)
![20240712013652](https://s2.loli.net/2024/07/12/mvhg6WMGoDfjYVE.png)
![20240712013756](https://s2.loli.net/2024/07/12/vqeKlbmHZT61MtC.png)
![20240712014946](https://s2.loli.net/2024/07/12/DUYo9dS812qyNaV.png)
![20240712015813](https://s2.loli.net/2024/07/12/pV2aPsYmefBdKg7.png)
![20240712015917](https://s2.loli.net/2024/07/12/SQIBm6OFabzVhcu.png)

## std::move  

Can we force a move to occur?
![20240712022546](https://s2.loli.net/2024/07/12/ikuRZs6In7KaTpW.png)
![20240712020715](https://s2.loli.net/2024/07/12/eAuYlbEWT7wFRIN.png)
![20240712020917](https://s2.loli.net/2024/07/12/baWR25jcf87HuMA.png)
![20240712021024](https://s2.loli.net/2024/07/12/C2T76kEvwFD4b1V.png)
![20240712021947](https://s2.loli.net/2024/07/12/nwV7fRba2rDemxJ.png)
![20240712022342](https://s2.loli.net/2024/07/12/3q8s5SEdrglyWbv.png)
![20240712023359](https://s2.loli.net/2024/07/12/rZUEO6WGI5RemLo.png)
![20240712023815](https://s2.loli.net/2024/07/12/ALclHINXPVoMw8d.png)
![20240712023930](https://s2.loli.net/2024/07/12/vFaVJI58iCSyz7q.png)


## swap and insert

How do we apply move?
![20240712030947](https://s2.loli.net/2024/07/12/d4Bjzuyc1vLiYsb.png)
![20240712031027](https://s2.loli.net/2024/07/12/NUTXI6j9ixacFQK.png)
![20240712031315](https://s2.loli.net/2024/07/12/yh4H8OZukBmCaQJ.png)
![20240712031341](https://s2.loli.net/2024/07/12/TeEtXZ58UIhqiKf.png)

## perfect forwarding  

Can we apply this to templates?
