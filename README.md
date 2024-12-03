project_scoring/
├── api/                     # API pour les prédictions
│   └── basic_app.py         # Point d'entrée pour l'API
├── data/                    # Données brutes et prétraitées
│   ├── raw/                 # Données brutes (non modifiées)
│   │   ├── application_train.csv
│   │   └── application_test.csv
│   └── processed/           # Données après prétraitement
│       ├── final_train.csv
│       └── final_test.csv
├── models/                  # Modèle final et scripts d'entraînement
│   ├── model_finale.pkl     # Modèle entraîné sauvegardé
│   └── train_model.py       # Script Python pour l'entraînement
├── notebooks/               # Notebooks pour exploration et modélisation
│   ├── final_pretraitement.ipynb  # Prétraitement des données
│   └── final_modelisation.ipynb   # Modélisation et entraînement
├── ui/                      # Interface utilisateur
│   ├── user_interface.py    # Fichier principal de l'interface
│   └── utils_ui.py          # Fonctions utilitaires pour l'interface
├── tests/                   # Tests unitaires
│   └── test_api.py          # Tests pour l'API
├── requirements.txt         # Dépendances du projet
└── README.md                # Documentation du projet
