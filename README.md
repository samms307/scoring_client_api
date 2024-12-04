# Projet de Scoring de Crédit avec FastAPI et Streamlit  

## Description des Données  
Les données utilisées dans ce projet proviennent du dataset **Home Credit Default Risk**, disponible sur [Kaggle](https://www.kaggle.com/c/home-credit-default-risk). Ce dataset contient des informations financières et personnelles sur les clients et permet de prédire la probabilité qu’un client fasse défaut sur son crédit.

Le dataset se compose de plusieurs fichiers. Cependant pour ce projet nous avons choisi de travailler uniquement avec les deux fichiers suivants :  
- **application_train.csv** : Données d’entraînement avec les informations des clients (âge, revenu, statut familial) et la variable cible **TARGET** (1 = défaut, 0 = non défaut).  
- **application_test.csv** : Données utilisées pour tester le modèle après l'entraînement sur de nouvelles données en production.

## Objectifs du Projet  
- Créer un modèle de classification supervisé pour prédire le risque de défaut de paiement des clients.  
- Exposer le modèle via une **API FastAPI** afin de pouvoir l'utiliser pour des prédictions en ligne.  
- Créer une interface **Streamlit** interactive pour faciliter l'utilisation du modèle.  
- Déployer l’API et l’application Streamlit sur Render pour une utilisation facile et en ligne.

## Fonctionnalités  
Ces fonctionnalités sont accessibles via [l'application déployée sur Render](https://scoring-client-dashboard.onrender.com) :

### API  
L'API permet de :  
- **Retourner la probabilité** qu'un client rembourse son crédit.  
- **Afficher l'interprétabilité** de la prédiction (variables les plus contributives).  

### Dashboard  
Le tableau de bord interactif permet de :  
- **Sélectionner un client** via une liste déroulante.  
- **Visualiser les détails** du client sélectionné (âge, revenu, statut familial).  
- **Comparer les données** du client avec celles des autres clients.  
- **Exécuter une prédiction** via le bouton "Run Prediction" pour afficher la probabilité de remboursement.

## Installation des Dépendances  
 Liste des dépendances nécessaires pour exécuter le projet spécifiés dans le fichier requirements.txt
  

## Structure du Projet

- **app/** : Contient les fichiers liés à l'application et à l'API.
  - `basic_app.py` : Application principale utilisant FastAPI.
  - `user_interface.py` : Interface utilisateur Streamlit.
  - `utils_ui.py` : Fonctions utilitaires pour l'interface Streamlit.

- **data/** : Données brutes et prétraitées.
  - `application_train.csv` : Données d'entraînement initiales.
  - `application_test.csv` : Données de test initiales.
  - `final_train.csv` : Données d'entraînement après prétraitement.
  - `final_test.csv` : Données de test après prétraitement.

- **notebooks/** : Notebooks Jupyter pour le prétraitement et la modélisation.
  - `final_pretraitement.ipynb` : Étapes de nettoyage et prétraitement des données.
  - `final_modelisation.ipynb` : Construction et évaluation du modèle.

- **models/** : Contient le modèle entraîné.
  - `model_finale.pkl` : Modèle final sauvegardé.

- **reports/** : Rapports générés.
  - `data_drift.html` : Rapport d'analyse de dérive des données.

- **clients_api.csv** : Données des clients utilisées pour l'API.
- **client_dashboard.csv** : Données des clients utilisées pour le tableau de bord.









