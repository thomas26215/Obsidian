## 🧩 Structure générale de l’application

### 🎓 Rôles et permissions

- **Élève** : Rejoindre un groupe, réserver une salle, signaler un retard, consulter ses rendus et son historique.
- **Professeur** : Créer des groupes, inviter des élèves et référents, créer des salles, suivre les rendus, gérer les retards, attribuer des notes différenciées.
- **Référent / Admin** : Gérer les paramètres globaux, modérer les groupes, configurer les sanctions.

---

## 🧠 Fonctionnalités principales

### 👥 Gestion des groupes

- Création de groupes par les profs avec contraintes (ex. 5 élèves max, tags de compétences).
- Invitation par email, ou code d’accès.
- Suggestions automatiques de groupes équilibrés selon les tags.
- Feedback entre pairs en fin de projet.
- Messagerie interne : Chat entre membres d'un groupe ou avec le prof référent
- Planning de groupe : calendrier partagé pour organiser réunions, deadlines, rendus ...

### 🏢 Gestion des salles

- Création de salles avec créneaux disponibles.
- Réservation par les élèves parmis les salles mis à disposition par les enseignants en fonction des jours
- Vue calendrier des réservations.

### 📦 Suivi des rendus

- Upload de livrables par groupe ou par élève.
- Statut du rendu (en attente, rendu, corrigé).
- Feedback du prof (commentaire, note, badge).
- Historique des rendus par élève.

---

## ⏰ Gestion des retards en séance et vérification par les profs

### Signalement et présence

- Bouton “Je vais être en retard” dans l’app mobile, avec heure estimée et motif.
- Bouton vérification d'une salle avec la salle à vérifier. Si un groupe s'est mis présent dans une salle  ou que certains élèves ne sont pas présents alors qu'ils devraient l'être, sanction. Vérification par qr code : chaque élève à un qr code assigné et le prof scanne le qr code des élèves
- Horodatage automatique pour mesurer le retard.
- Historique des retards par élève.

### Sanctions et règles

- Paramètres configurables par le prof :
    - Nombre de retards tolérés
    - Type de sanction (baisse de note, exclusion temporaire, alerte)
    - Réinitialisation mensuelle ou par projet
- Sanctions automatiques ou manuelles selon préférence du prof.

---

## 📊 Suivi individuel et différenciation des notes

### Journal d’activité

- Actions enregistrées : rendus, réservations, messages, présence.
- Tâches assignées et réalisées.
- Feedbacks reçus des autres membres.

### Évaluation différenciée

- Vue prof : tableau comparatif des membres d’un groupe avec :
    - Taux de présence
    - Retards
    - Contributions
    - Feedbacks
- Attribution de notes personnalisées selon implication réelle.

---

## 📱 Différences Web / Mobile

| Fonctionnalité             | Web (desktop)                    | Mobile (app)                       |
| -------------------------- | -------------------------------- | ---------------------------------- |
| Création de groupes/salles | ✔️ Interface complète            | ❌ Consultation uniquement          |
| Réservation de salle       | ✔️                               | ✔️ Rapide via calendrier simplifié |
| Suivi des rendus           | ✔️ Vue détaillée, téléchargement | ✔️ Notifications, aperçu rapide    |
| Signalement de retard      | ✔️                               | ✔️ Formulaire rapide et push       |
| Check-in en séance         | ✔️                               | ✔️ QR code ou bouton               |
| Statistiques et exports    | ✔️ Tableaux, graphiques, CSV     | ❌ Résumé simple                    |
| Feedback entre pairs       | ✔️ Interface complète            | ✔️ Saisie rapide                   |

---

## 👜 Fourre-tout
- Système de notifications concernant les retards, les rendus en retard ...
- Chaque salle peut être attribué pour des besoins spécifiques (salle de réunion, salle "open-space" ...) et réservation des salles pour les travaux
- Possibilité pour les profs de laisser la possiblité aux élèves de travailler depuis chez eux ou réservation obligatoire d'une salle