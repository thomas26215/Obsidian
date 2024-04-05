---
MOOC: "[[Autre]]"
Sujet: Entreprise
Type: 
tags:
  - status_finish
  - note_permanent
---
La fonction étude a pour vocation la mise au point de produits nouveaux et l'amélioration des produits existants, en vue de leur production par l'entreprise
Ses rôles : Innovation dans les procédés, Préparation technique du travail, Amélioration des postes de travail, Mise à jour des données scientifiques

[[Les fonctions de production]]

**Capacité =** Capacité théorique vs capacité réelle (cf [[Définition - Capacité]])
**Charge =** Quantité de travail à réaliser sur une poste de travail, pendant une certaine période (cf [[Définition - Charge]])

Capacité = je peux (machine, ouvriers, heures annueles de dispo pour une machine), charge = je dois (⇒ Planning, en heures machine

# 2 - Notion de capacité
1. → On commence par calculer la capacité :
   50 semaines, 5 jours par semaine, 8h / jour, 2 équipes
   ⇒ $50*5*8*2=4000h$ ⇒ **Capacité théorique**
   On enlève la réserve de capacité qui est de 5% :
   $4000*0.95=3800h$ ⇒ **Capacité réelle**
	→  Il faut maintenant calculer la production possible
	**80000 paires pour hommes**
	Prepa → 240 paires → Prepa → 240 → ...
	80000 paires → $80000*0,05$ (Traitement) + $\frac{80000}{240}*0.5$ (Préparation) = $4167h$
	 ⇒ $\frac{80000}{240}$ = Nombre de lots
	60000 paires → $60000*0,10+\frac{60000}{180}=6734$
	...                                                    $=3667$
	Total = $14568h$
	Nombre de machines = $\frac{14568}{3800}=3,8$ machines
	On arrondit à 4 machines mais on augmente le planning
	Si on reste à 3 machines, on diminue le planning, ou heures supp pour équipe

# Les flux poussés : Le MRP

|       |                      | A   | B   | C   | D   | E   | F   | G   | H   |
| ----- | -------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| Niv 0 | Besoins bruts        | 100 |     |     |     |     |     |     |     |
| Niv 0 | Stock dispo          | 15  |     |     |     |     |     |     |     |
| Niv 0 | En cours de prod     | 0   |     |     |     |     |     |     |     |
| Niv 0 | En cours de commande | 0   |     |     |     |     |     |     |     |
| Niv 0 | Besoins nets         | 85  |     |     |     |     |     |     |     |

|       |                         | A   | B   | C   | D   | E   | F   | G   | H   |
| ----- | ----------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| Niv 0 | Besoins nets            | 85  |     |     |     |     |     |     |     |
| Niv 1 | Besoins bruts           |     | 170 | 255 |     |     |     |     |     |
| Niv 1 | Stock dispo             |     | 5   | 0   |     |     |     |     |     |
| Niv 1 | En cours de fabrication |     | 0   | 20  |     |     |     |     |     |
| Niv 1 | En cours de commande    |     | 0   | 0   |     |     |     |     |     |
| Niv 1 | Besoins nets            |     | 165 | 235 |     |     |     |     |     |


|       |                         | A   | B   | C   | D   | E   | F   | G   | H   |
| ----- | ----------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| Niv 1 | Besoins nets            |     | 165 | 235 |     |     |     |     |     |
| Niv 2 | Besoins bruts           |     |     |     | 660 | 330 | 235 | 235 | 470 |
| Niv 2 | Stock dispo             |     |     |     | 45  | 20  | 20  | 20  | 50  |
| Niv 2 | En cours de fabrication |     |     |     | 0   | 0   | 0   | 0   | 0   |
| Niv 2 | En cours de commande    |     |     |     | 0   | 180 | 20  | 200 | 0   |
| Niv 2 | Besoins nets            |     |     |     | 615 | 130 | 195 | 5   | 420 |

**Attention :** Le stock affecté est retiré du stock dispo

**Calendrier prévisionnel :**

|     | 0   | -1  | -2  | -3  | -4  | -5  | -6  | -7  | -8  | -9  | -10 | -11 | -12 | -13 | -14 |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A   | X   | X   | X   |     |     |     |     |     |     |     |     |     |     |     |     |     |
| B   |     |     |     | X   | X-. |     |     |     |     |     |     |     |     |     |     |     |
| C   |     |     |     |     | .-X | X   |     |     |     |     |     |     |     |     |     |     |
| D   |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |
| E   |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |
| F   |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |
| H   |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |
|     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |

# 4 - Toyota production system
1. **Exemple du métier à tisser** : Dès que il y a un prblm, tout arrête. Pour ne pas produire mal
2. **Supermarché objectifs :** Jamais vides et se remplissaient rapidement
3. **Juste à temps** : Processus de production lancé juste après demande de client. Pièces fournis en fonction de nécessité exacté de demande
   Cadence de production parfaitement piloté. Fait en sotr epour ne pas surcharger employés ou machines pour fournir qualité supérieures
4. **Jidoka** : Chaque travailleur autorisé à arrêté machine si dysfonctinonement. Prblm affiché sur tableau. Assure produits de bonne qualité
5. **Kaisen** : Amélioration continue. Processus et philosophie. Salarié donne aupinions dans réunions. 3k par an. TPS présents partout dans le travail. Rôle actif avec 5 S

# 5 - Production agile
1. Victimes de leur succès. Travailler avec le moins de stocks car ca a un coût. Tout le monde veut le même modèle au même moment

---
**Questions :**
1. Définir la notion de charge
2. Définir la notion de capacité
3. Répondre aux questions ,n- n,b