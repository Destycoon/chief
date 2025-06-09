# Cahier des charges – Application de gestion de recettes de cuisine (Android)

## 1. Contexte du projet

Ce projet vise à développer une application mobile Android de gestion de recettes de cuisine, à usage personnel et familial. L’application permettra de consulter, modifier et organiser des recettes partagées entre plusieurs utilisateurs identifiés, avec un accès en ligne et en hors-ligne.

## 2. Objectifs

* Centraliser et organiser des recettes de cuisine accessibles à tous les utilisateurs autorisés.
* Permettre à chacun d'ajouter, modifier ou supprimer des recettes.
* Pouvoir consulter les recettes sans connexion, avec synchronisation différée à la reconnexion.
* Identifier l’auteur ou le modificateur d’une recette.
* Proposer une navigation fluide, une interface adaptative et une expérience utilisateur moderne.

## 3. Fonctionnalités principales

### 3.1. Gestion des utilisateurs

* Authentification via Firebase Authentication (email/mot de passe ou Google).
* Attribution automatique de l’auteur lors de l’ajout ou la modification d’une recette.

### 3.2. Gestion des recettes

* Ajouter, modifier, supprimer une recette.
* Affichage sous forme de liste scrollable.
* Tri possible (par temps, nom, auteur, etc.).
* Filtrage par catégorie ou ingrédients.

### 3.3. Gestion des favoris

* Possibilité de marquer une recette comme favorite (stockée localement).

### 3.4. Fonctionnement hors-ligne

* Sauvegarde locale automatique des données (Room ou fichier JSON).
* Synchronisation automatique avec Firestore à la reconnexion.

### 3.5. Mise à jour en temps réel

* Les modifications faites par un utilisateur sont propagées automatiquement aux autres utilisateurs connectés via Firestore.

## 4. Modèle de données

### 4.1. Recette

```json
{
  "nom": "Tarte aux pommes",
  "categorie": "Dessert",
  "tempsPreparation": 45,
  "instructions": "Éplucher les pommes, les couper, etc.",
  "ingredients": [
    {"nom": "pomme", "quantite": 3, "unite": "pièce"},
    {"nom": "sucre", "quantite": 100, "unite": "g"}
  ],
  "auteur": "uidFirebase",
  "timestampModification": "2025-06-09T14:00:00"
}
```

### 4.2. Ingrédient

* Nom (String)
* Quantité (Float ou Int selon le type)
* Unité (g, mL, cuil., etc.)

## 5. Architecture technique

* **Modèle MVC** :

  * **Modèle** : gestion des données (recettes, ingrédients) + communication Firestore
  * **Vue** : interface en Jetpack Compose (responsive)
  * **Contrôleur** : logique métier et communication entre les composants

* **Base de données** :

  * En ligne : Firebase Firestore (temps réel)
  * En local : Room ou cache JSON pour accès hors-ligne

* **Services Firebase** :

  * Firestore (NoSQL Cloud DB)
  * Firebase Auth (authentification utilisateur)
  * Firestore Sync (écoute en temps réel des données)

## 6. Interface utilisateur

### 6.1. Écrans principaux

* Connexion / inscription
* Liste des recettes (filtrable / triable)
* Détail d’une recette
* Ajout / modification d’une recette
* Favoris

### 6.2. Responsivité

* Adaptation smartphone et tablette
* Thème clair / sombre basé sur les préférences système

## 7. Contraintes techniques

* Kotlin + Jetpack Compose
* Pas d’emoji dans les chaînes de caractères
* Support du mode hors-ligne (via cache local)
* UTF-8 sans caractères spéciaux non pris en charge
* Authentification obligatoire pour modifier les recettes

## 8. Planning

* Projet personnel, sans échéance stricte
* Avancement par fonctionnalités prioritaires :

  1. Authentification
  2. Affichage des recettes (lecture)
  3. Ajout / modification / suppression
  4. Favoris hors-ligne
  5. Synchronisation Firestore
  6. Tri / filtrage

## 9. Maintenance et évolutions possibles

* Ajout d’un moteur de recherche
* Ajout de photos ou d’illustrations
* Partage de recettes via lien ou QR code
* Export PDF ou impression
