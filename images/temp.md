# TP – Conception Base de Données : Gestion Locative Immobilière

## Cahier des charges

---

## 1. Utilisateurs
Chaque utilisateur possède un compte personnel et gère ses propres données.  

**Champs :**
- Nom affiché / Société  
- Email (unique)  
- Téléphone 
- Adresse postale  

---

## 2. Bailleurs
**Champs (personne physique) :**  
- Prénom, Nom  
- Date et lieu de naissance  
- Adresse actuelle  
- Email, Téléphone 
- IBAN/BIC d’encaissement (plusieurs possibles)  

**Champs en plus pour les personnes morales :**  
- Capital social
- Type de société (SAS, SARL, etc.)
- Nom du représentant légal
- Numéro SIREN  
- Ville d’enregistrement du RCS

---

## 3. Locataires
**Champs principaux :**  
- Nom, Prénom  
- Date et lieu de naissance  
- Email, Téléphone  
- Profession et revenus  
- Statut (salarié, étudiant, indépendant, retraité)  
- Situation familiale (célibataire, couple, enfants)  

**Garant(s) :**  
- Identité et coordonnées  
- Revenus  
- Type de caution (simple / solidaire)  
- Durée  

**Aides :**  
- Numéro allocataire CAF  
- Garantie Visale (oui/non, référence)  

**Autres :**  
- Adresse de facturation/envoi (si différente)  
- Documents (pièce d’identité, 3 fiches de paie, attestation employeur, etc.)  

---

## 4. Biens immobiliers
**Champs :**  
- Nom du logement  
- Prix de location mensuel  
- Montant mensuel des charges  
- Impôts fonciers annuels  
- Assurance annuelle (+ numéro de contrat et assureur)  
- Surface en m², nombre de pièces  
- Type de bien (maison, appartement)  
- Accessibilité PMR  
- Description textuelle (annonce locative)  
- DPE et GES (+ dates)  
- Adresse complète  
- Numéro de lot / référence cadastrale  
- Présence de dépendances  
- Année de construction  
- RIB/IBAN associé par défaut 
- Bailleur par défaut

---

## 5. Articles de baux commerciaux
- Créés et gérés par **l’administrateur**  
- Réutilisables par les utilisateurs dans leurs baux  
- Historique conservé (pas d’écrasement des anciens articles)  

---

## 6. Dossiers de location
Chaque dossier regroupe **un bailleur, un ou plusieurs locataires, un bien immobilier** et génère les documents associés.  

### Documents d’entrée en location
- Bail (dates, dépôt de garantie, mode & périodicité de paiement, dernier loyer révisé, RIB choisi)  
- État des lieux  
- Caution + Annexe (optionnel)  
- Garantie Visale (optionnelle)  
- Attestation assurance habitation  
- Attestation règlement de copropriété  
- Remise de clés  
- Reçu dépôt de garantie  
- Reçu DPE  
- Quittance de loyer  
- Relevé compteurs (eau, gaz, électricité, multi-compteurs)  

### Documents pendant la location
- Notification révision de loyer  
- Quittance de loyer  

### Documents en sortie de location
- Restitution clés  
- Restitution dépôt de garantie  
- État des lieux  
- Relevé compteurs  

📄 Tous ces documents doivent être générés automatiquement, exportables en **PDF**, et archivés.  

---

## 7. Gestion documentaire
- Tous les documents liés à un contrat sont consultables directement (lecteur PDF intégré)  
- Téléchargement possible  
- Historique des versions conservé  
- Suivi : date de création, date de signature  

---

## 8. Gestion des paiements
- Suivi des loyers payés  
- Validation manuelle (ex : modale de confirmation)  
- Envoi automatique d’une quittance par email après validation  
- Régularisation des charges :  
  - Facture réelle enregistrée  
  - Déduction des montants déjà versés  
  - Calcul du solde à régulariser  
  - Validation paiement  

---

## 9. Administration
- Gestion des utilisateurs (activation, rôles)  
- Bibliothèque de modèles (baux, quittances, courriers types)  
- Paramètres globaux :  
  - IRL de référence par défaut  
  - Pénalité de retard par défaut  
  - Mentions légales  
- Journaux (audit log) : qui a fait quoi, quand  

## Travail à réaliser

- Dictionnaire de données (Nom de l’entité, Nom de l’attribut, Type, Taille, Contraintes, Commentaire)  
- MCD  
- MLD  
- MPD  
- Script SQL de création de tables 