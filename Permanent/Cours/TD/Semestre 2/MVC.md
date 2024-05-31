---
MOOC: "[[Cours]]"
Ressource: "R2.02 : IHM"
Cours: "TD 1 : MVC"
Date: 
tags: 
Complete: false
Learned: false
---
```mermaid
graph TD
m("Modèle")--Notifie d'un changement-->c("Controller")
c--Demande de changement-->m
c--Demande de mise à jour-->v("vue")
v--Informe d'une action utilisateur-->c
```

