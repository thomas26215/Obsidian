# Apix Analytics — Présentation Entreprise

---

## 🏢 Qui est Apix Analytics ?

Apix Analytics est une entreprise spécialisée dans le développement de **logiciels embarqués pour analyseurs de gaz chromatographiques** (CHROMPIX, GREENPIX). Elle conçoit et maintient l'ensemble de la suite logicielle **PixL Suite**, qui pilote ces analyseurs industriels depuis la collecte des données jusqu'à la présentation des résultats aux utilisateurs finaux.




## 📦 Les logiciels de la PixL Suite — Détail

### 🔵 PixL Core

**Rôle :** Orchestrateur général de l'analyseur.

- Gère la communication avec les cartes électroniques de l'analyseur
- Pilote le processing des chromatogrammes (traitement des signaux)
- Assure la coordination entre tous les modules internes
- Déployé directement sur Debian 13 (PC embarqué)

---

### 🟢 PixL Console

**Rôle :** Interface web complète pour les utilisateurs avancés.

- Application web accessible depuis un navigateur (local ou distant)
- Donne accès aux commandes, configurations et résultats de l'analyseur
- Permet la calibration semi-automatique, la gestion des méthodes, la visualisation des chromatogrammes
- Disponible en **français, anglais et polonais**
- En cours de refonte vers **PixL Expert** (interface nouvelle génération basée sur Vue.js)


---

### 🔴 PixL Api

**Rôle :** API REST sécurisée (HTTPS).

- Accessible en interne (par les autres logiciels Apix) et en externe (par les clients via API)
- Permet l'accès sécurisé à la base de données
- Documentée via **Swagger**
- Sert de passerelle entre PixL Core et les applications tierces

---

### 🟣 PixL Modbus

**Rôle :** Communication protocole Modbus.

- Expose les données de l'analyseur via le protocole **Modbus** (série et TCP/IP simultanément)
- Permet l'intégration avec des systèmes industriels tiers (automates, SCADA…)
- Déployé dans un conteneur Docker

### Librairies communes (Apix Tools)

Plusieurs logiciels partagent des **librairies communes** pour éviter la duplication de code :

- **Apix Tools** : code utilitaire partagé entre tous les logiciels de la suite
- **Apix Database** : librairie dédiée à la gestion des modèles de base de données, partagée entre PixL Api et PixL Console

---

## 🏗️ Infrastructure technique

| Composant            | Technologie                                       |
| -------------------- | ------------------------------------------------- |
| Conteneurisation     | **Docker**                                        |
| Base de données      | **PostgreSQL**                                    |
| Signature logicielle | **SHA-256** (tous les logiciels PixLSuite 2026.X) |
