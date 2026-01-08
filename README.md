# Projet MRR : Prédiction de Popularité d'Animes & Système de Recommandation 
Auteurs : Arnaud GRASSIAN & Vithuson VAITHILINGAM Date : Décembre 2025 Formation : ENSIIE

Ce projet a été réalisé dans le cadre du cours de **Modèles de Régression (MRR)** à l'**ENSIIE** (Décembre 2025). Il vise à analyser une large base de données d'animes pour prédire les notes globales des œuvres et recommander des contenus aux utilisateurs via des modèles d'apprentissage statistique.

## 📋 Description

L'objectif de cette étude est double : comprendre les facteurs qui influencent la note moyenne d'un animé (régression) et développer un moteur de recommandation capable de prédire si un utilisateur spécifique aimera une œuvre donnée (classification). Nous avons mis en œuvre une approche rigoureuse comparant plusieurs techniques de régularisation pour éviter le surapprentissage.

## 💾 Source des Données

Les données utilisées proviennent de la plateforme **Kaggle**. Le dataset regroupe des informations issues de *MyAnimeList*, comprenant :
* Les métadonnées des animes (genre, studio, type, source).
* Les profils utilisateurs et leurs historiques de visionnage.
* Les notes (ratings) et favoris.

Vous pouvez retrouver le dataset original ici : [Lien vers le Dataset Kaggle](https://www.kaggle.com/datasets/neelagiriaditya/anime-dataset-jan-1917-to-oct-2025)

## ⚙️ Workflow et Fonctionnalités

### 1. Traitement et Préparation des Données (Data Engineering)
Fusion et nettoyage de multiples sources de données CSV (`anime`, `profiles`, `reviews`, `staff`, etc.) :
* **Nettoyage avancé :** Gestion des valeurs manquantes et parsing des colonnes "listes" (genres, studios).
* **Feature Engineering :**
    * Création de matrices **One-Hot** et **Multi-Hot** pour les variables catégorielles.
    * Extraction de features temporelles et calcul d'indicateurs utilisateurs (âge, taux de rewatch).
* **Échantillonnage :** Travail sur un sous-ensemble représentatif pour optimiser les temps de calcul.

### 2. Prédiction de la note d'un animé (Régression)
Objectif : Prédire le score global (`Y_score_global`) d'un animé sur une échelle de 1 à 10.
* **Modèles testés :**
    * OLS (Moindres Carrés Ordinaires).
    * Ridge (Pénalité $L_2$).
    * Lasso (Pénalité $L_1$).
    * Elastic Net (Combinaison $L_1 + L_2$).
* **Méthodologie :** Validation croisée pour l'optimisation des hyperparamètres ($\lambda$ et $\alpha$).
* **Résultats :** Analyse des résidus et comparaison via RMSE et $R^2$ pour identifier les facteurs clés de succès.

### 3. Recommandation d'un animé (Classification)
Objectif : Prédire si un utilisateur spécifique va "Aimer" (Note $\ge$ 7) un animé donné.
* **Approche :** Classification binaire (Aimé / Pas aimé).
* **Modélisation :** Régression logistique pénalisée.
* **Application :** Simulation pour trouver le **Top 30 des utilisateurs** les plus susceptibles d'aimer une œuvre donnée (Calcul d'un score de compatibilité).

## 🛠️ Prérequis Techniques

Pour exécuter ce projet, vous avez besoin de **R** et **RStudio**. Les scripts sont fournis au format R Markdown (`.Rmd`).

### Packages R nécessaires

Le code dépend des librairies suivantes. Assurez-vous de les installer via la console R avant de lancer les scripts :

```r
install.packages(c("data.table", "dplyr", "glmnet", "caret", "formatR", "knitr"))
