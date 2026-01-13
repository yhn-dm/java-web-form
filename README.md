# Exercice Spring Boot JPA MySQL – Gestion des Produits (Boutique de thés)

Ce projet est une application Spring Boot simple qui permet de gérer une boutique de thés. Il a été réalisé dans le cadre d’un exercice pour pratiquer Spring Boot, JPA, MySQL et Thymeleaf, avec une approche volontairement claire et lisible.

L’objectif est de mettre en place une application complète (backend + frontend) autour d’une seule entité : **Produit**.

---

## Technologies utilisées

* Java
* Spring Boot
* Spring Web
* Spring Data JPA
* Thymeleaf
* MySQL
* HTML / Tailwind CSS

---

## Configuration du projet

Le projet utilise une base de données MySQL locale.

Paramètres de connexion (dans `application.properties`) :

* Base de données : `boutique_thes`
* URL : `jdbc:mysql://localhost:3306/boutique_thes`
* Utilisateur : `root`
* Mot de passe : à définir selon votre configuration locale

---

## Modèle de données

Une seule table est utilisée : `produit`.

Champs principaux :

* `id` : identifiant (auto-incrémenté)
* `nom` : nom du thé (obligatoire)
* `typeThe` : type de thé (Vert, Noir, Oolong, Blanc, Pu-erh)
* `origine` : pays d’origine
* `prix` : prix du produit (entre 5 et 100)
* `quantiteStock` : quantité disponible (minimum 0)
* `description` : description du produit
* `dateReception` : date de réception du produit

La date de réception est automatiquement initialisée lors de l’insertion si elle n’est pas fournie.

---

## Architecture

Le projet suit une architecture classique Spring Boot :

* **Entity** : `Produit`
* **Repository** : `ProduitRepository` (extends JpaRepository)
* **Service** : `ProduitService` (logique métier)
* **Controller** : `ProduitController` (gestion des routes web)
* **Templates Thymeleaf** : interface utilisateur

---

## Fonctionnalités

### Gestion des produits

* Affichage de la liste des produits
* Ajout d’un nouveau produit
* Modification d’un produit existant
* Suppression d’un produit

### Interface utilisateur

* Tableau des produits avec informations détaillées
* Boutons Modifier / Supprimer
* Formulaire unique pour l’ajout et la modification
* Validation côté serveur
* Message de confirmation avant suppression

### Pagination

* Pagination côté backend avec Spring Data
* Navigation entre les pages depuis l’interface
* Nombre de produits par page configurable

### Export CSV

* Export de la liste complète des produits
* Génération d’un fichier CSV téléchargeable
* Compatible avec Excel / LibreOffice

---

## Templates Thymeleaf

### `index.html`

* Affiche les produits dans un tableau
* Bouton pour ajouter un nouveau thé
* Bouton pour exporter en CSV
* Pagination en bas de page

### `formulaire-produit.html`

* Formulaire de création / modification
* Champs correspondant au modèle Produit
* Validation des champs obligatoires

---

## Lancement du projet

1. Créer la base de données `boutique_thes`
2. Vérifier les paramètres MySQL dans `application.properties`
3. Lancer l’application Spring Boot
4. Accéder à l’application via :

   [http://localhost:8080/](http://localhost:8080/)

