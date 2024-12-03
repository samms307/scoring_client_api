# Projet de Scoring avec FastAPI et Streamlit

Ce projet permet de prédire la probabilité qu'un client rembourse son crédit à partir de données d'entrée, en utilisant un modèle de machine learning supervisé. Ce modèle est exposé via une API avec **FastAPI** et un tableau de bord interactif créé avec **Streamlit**, tous deux déployés sur **Render**.

## Objectifs

L'objectif de ce projet est de mettre en place un système de scoring des clients, avec :
- **API** : Prédire la probabilité de remboursement d'un crédit pour un client donné via l'API.
- **Dashboard** : Une interface graphique interactive pour sélectionner un client et afficher la probabilité de remboursement.

## Fonctionnalités

### 1. **API avec FastAPI**

L'API permet d'obtenir les prédictions du modèle à partir d'un identifiant client. Elle retourne :
- La probabilité que le client rembourse son crédit.
- L’interprétabilité du modèle (les variables les plus influentes dans la prédiction).

**URL de l'API** : [Lien vers l'API FastAPI sur Render](https://scoring-client-dashboard.onrender.com/)


