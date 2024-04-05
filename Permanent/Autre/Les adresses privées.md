---
MOOC: "[[Autre]]"
Sujet: Systèmes d'exploitation
Type: Adresses IP
tags:
---
Les adresses privées sont utilisées en interne au sein d'un site et ne sont pas routées à l'extérieur de ce site. Cette approche permet à un site d'avoir plus de stations que d'adresses IP publiques attribuées. Ces adresses privées sont couramment utilisées par les stations Linux et nécessitent l'utilisation de mécanismes de traduction d'adresses, tels que NAT (Network Address Translation), PAT (Port Address Translation) ou masquerading, pour permettre l'accès à Internet tout en préservant la connectivité des applications réseau. Les adresses privées sont classées en trois catégories, chacune définissant un intervalle d'adresses.

| Classe | Intervalle d'adresses       |
| ------ | --------------------------- |
| A      | 10.x.y.z                    |
| B      | 172.16.x.y à 172.31.x.y     |
| C      | 192.168.0.x à 192.168.255.x | 

---
**Links :**
[[L'utilité des adresses IP]]
[[La configuration d'une adresse]]