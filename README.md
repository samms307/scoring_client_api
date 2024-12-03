# Projet de Scoring de Crédit avec FastAPI et Streamlit

## Description des Données
Les données utilisées dans ce projet proviennent du dataset **Home Credit Default Risk**, disponible sur [Kaggle](https://www.kaggle.com/c/home-credit-default-risk). Ce dataset contient des informations financières et personnelles sur les clients et permet de prédire la probabilité qu’un client fasse défaut sur son crédit.

Le dataset se compose de plusieurs fichiers. Cependant pour ce projet nous avons choisi de travailler uniquement avec les deux fichiers suivants :
- **application_train.csv** : Ce fichier contient les données d’entraînement, incluant les informations des clients (âge, revenu, statut familial, etc.) ainsi que la variable cible **TARGET** (1 = défaut de paiement, 0 = non défaut).
- **application_test.csv** : - **application_test.csv** : Fichier utilisé pour tester le modèle après l'entraînement, afin d'évaluer ses performances sur de nouvelles données en production.

## Objectifs du Projet
- Créer un modèle de classification supervisé pour prédire le risque de défaut de paiement des clients.
- Exposer le modèle via une **API FastAPI** afin de pouvoir l'utiliser pour des prédictions en ligne.
- Créer une interface **Streamlit** interactive pour faciliter l'utilisation du modèle.
- Déployer l’API et l’application Streamlit sur Render pour une utilisation facile et en ligne.

### Dépendances
Les dépendances sont spécifiés dans le fichier requirements.txt

## Déployement
L'application est entièrement déployée sur **Render** et accessible en ligne via le lien suivant :  
[Accéder à l'application](https://scoring-client-dashboard.onrender.com)  








