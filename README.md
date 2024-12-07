# Projet de Scoring de Crédit avec FastAPI et Streamlit  

## Description des Données  
Les données utilisées dans ce projet proviennent du dataset **Home Credit Default Risk**, disponible sur [Kaggle](https://www.kaggle.com/c/home-credit-default-risk). Ce dataset contient des informations financières et personnelles sur les clients et permet de prédire la probabilité qu’un client fasse défaut sur son crédit.

Le dataset se compose de plusieurs fichiers. Cependant pour ce projet nous avons choisi de travailler uniquement avec les deux fichiers suivants :  
- **application_train.csv** : Données d’entraînement avec les informations des clients (âge, revenu, statut familial) et la variable cible **TARGET** (1 = défaut, 0 = non défaut).  
- **application_test.csv** : Données utilisées pour tester le modèle après l'entraînement sur de nouvelles données en production.

## Objectifs du Projet  
Ce projet propose une solution complète pour évaluer le risque de défaut de crédit des clients, combinant l’analyse de données, l’apprentissage automatique, et une interface utilisateur interactive.
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
 Liste des dépendances nécessaires pour exécuter le projet dans le fichier requirements.txt
  

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




# 📈 **Étapes Clés du Projet**

### **1️⃣ Prétraitement des Données et Contrôle du Data Leakage**

Dans cette étape, l’objectif principal était de préparer les données et de garantir qu'aucune **fuite de données** (data leakage) ne se produise. Voici les actions effectuées :

#### **Contrôle du Data Leakage :**
- **Contamination des ensembles d’entraînement et de test :**  Le prétraitement a été effectué uniquement sur l'ensemble d'entraînement pour éviter que les données de test n'influencent le modèle. Ensuite, les mêmes transformations (nettoyage, encodage, équilibrage) ont été appliquées de manière identique sur les données de test, afin de garantir une évaluation impartiale du modèle.
  
- **Fuite de données (fuite cible) :**  Pour éviter ce risque, j’ai vérifié que les variables explicatives ne contiennent pas d’informations qui ne seraient pas disponibles lors de la prédiction. Cela inclut l’analyse des variables temporelles pour éviter l'inclusion de données futures, ainsi qu’une étude approfondie des relations entre les variables explicatives et la cible pour garantir la pertinence des variables sélectionnées.

#### **Prétraitement des Données :**
Résumé des étapes principales :
- **Nettoyage des données** J'ai éliminé les doublons, géré les valeurs manquantes et les valeurs aberrantes ou atypiques. Puis géré les modalités et encodé les variables catégorielles.
 
- **Équilibrage des classes :**  Pour traiter l'imbalancement des classes, j'ai utilisé `SMOTE` (Synthetic Minority Over-sampling Technique) pour créer des exemples synthétiques de la classe minoritaire, équilibrant ainsi la distribution des classes dans les données.
De plus, pour les modèles utilisés dans ce projet, j'ai intégré le `paramètre class_weight='balanced'`, ce qui permet d'ajuster automatiquement les poids des classes et d'assurer une meilleure prise en compte des classes minoritaires dans l'entraînement du modèle.
  

👉 **[ Voir plus de détails dans le notebook de prétraitement](https://github.com/samms307/scoring_client_api/blob/main/Final_pr%C3%A9traitement.ipynb)**



### 2️⃣ **Modélisation**  
Après avoir prétraité les données et éliminé tout risque de data leakage, le notebook suivant se concentre sur la construction et l’évaluation des modèles. Voici les points clés abordés dans cette phase :

- **Sélection du modèle :** Nous avons comparé plusieurs modèles, à commencer par la régression logistique et en incluant des modèles plus complexes comme Random Forest et LightGBM, adaptés aux données déséquilibrées. Les performances ont été évaluées via la métrique AUC-ROC, en calculant la moyenne des scores et l'écart-type pour mesurer la stabilité. Pour assurer une évaluation robuste, nous avons utilisé une validation croisée stratifiée, garantissant que la proportion des classes reste constante dans chaque pli, ce qui évite tout biais dans l'entraînement et permet au modèle de mieux généraliser.

- **Optimisation du seuil de décision :**  L’ajustement du seuil de probabilité a été effectué pour optimiser la classification des défauts de paiement, en tenant compte des erreurs de classification (faux négatifs et faux positifs), qui peuvent avoir un impact financier significatif pour l'entreprise.  
  Deux approches ont été explorées :  
  1. **Maximisation de la sensibilité et de la spécificité :** Trouver un seuil qui équilibre les faux positifs et faux négatifs pour améliorer la performance globale et minimiser les pertes.  
  2. **Optimisation de la précision et du rappel :** Prioriser la détection des clients risqués, en particulier pour minimiser les faux négatifs, afin de réduire les risques financiers et améliorer la gestion du crédit.

  
- **Explicabilité du modèle :**  Le modèle **LightGBM** a été utilisé pour les prédictions, et pour en comprendre les décisions, nous avons appliqué **LIME** pour expliquer chaque prédiction (ex : refus de prêt). L'**importance des caractéristiques** a permis d'identifier les variables influentes globalement (comme le revenu et l'historique de crédit). Ces méthodes assurent que les décisions du modèle sont compréhensibles et justifiables, répondant ainsi aux exigences réglementaires.


- **Détection du Data Drift :**
Pour assurer la performance continue du modèle en production, nous avons surveillé l'évolution des données avec la `bibliothèque Evidently`. Evidently permet de détecter le Data Drift en comparant les distributions des données d'entrée en production avec celles des données d’entraînement. Cette surveillance du drift des données aide à identifier des écarts significatifs dans les caractéristiques des données, garantissant ainsi que le modèle continue à fournir des prédictions fiables même lorsque les données changent avec le temps.

[Pour plus de détails sur la détection du data drift, vous pouvez consulter le rapport d'analyse de dérive des données ici](lien_vers_le_rapport)


👉 **[Voir le notebook de modélisation pour l'interprétation des résultats](https://github.com/samms307/scoring_client_api/blob/main/Final_Mod%C3%A9lisation.ipynb)**






