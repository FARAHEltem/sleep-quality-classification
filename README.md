# 😴 Classification de la qualité du sommeil

Projet de **Machine Learning** qui prédit la **qualité du sommeil** d'une personne à partir de son mode de vie et de ses indicateurs de santé (durée de sommeil, stress, activité physique, IMC, fréquence cardiaque…).

Le projet couvre tout le cycle d'un projet de Data Science : **exploration des données, nettoyage, préparation, entraînement de modèles et évaluation**.

---

## 🎯 Objectif

Le sommeil a un impact direct sur la santé et la productivité. L'objectif est de :

- **comprendre** quels facteurs du mode de vie influencent la qualité du sommeil ;
- **construire un modèle** capable de prédire la qualité du sommeil d'une personne à partir de ces facteurs.

## 📊 Données

**Source :** [Sleep Health and Lifestyle Dataset](https://www.kaggle.com/) sur Kaggle *(remplacez ce lien par l'adresse exacte de la page Kaggle)*

Le jeu de données contient **374 personnes** et **13 colonnes** :

| Colonne | Description |
|---|---|
| `Person ID` | Identifiant de la personne |
| `Gender` | Genre |
| `Age` | Âge (années) |
| `Occupation` | Profession |
| `Sleep Duration` | Durée de sommeil (heures par jour) |
| `Quality of Sleep` | **Qualité du sommeil, note de 1 à 10 (variable cible)** |
| `Physical Activity Level` | Activité physique (minutes par jour) |
| `Stress Level` | Niveau de stress (1 à 10) |
| `BMI Category` | Catégorie d'IMC |
| `Blood Pressure` | Tension artérielle (systolique/diastolique) |
| `Heart Rate` | Fréquence cardiaque au repos (bpm) |
| `Daily Steps` | Nombre de pas par jour |
| `Sleep Disorder` | Trouble du sommeil (aucun, insomnie, apnée du sommeil) |

## 🔍 Démarche

### 1. Analyse exploratoire (`Analyse_du_dataset_sommeil.ipynb`)

- Distribution de l'âge des participants
- Répartition de la qualité du sommeil
- Relations entre la qualité du sommeil et les autres variables (stress, durée de sommeil, activité physique…)

### 2. Nettoyage et préparation des données

- Vérification des valeurs manquantes et des doublons
- Harmonisation des catégories d'IMC
- Séparation de la tension artérielle en deux variables numériques (systolique et diastolique)
- Encodage des variables catégorielles (genre, profession, IMC, trouble du sommeil)
- Mise à l'échelle des variables numériques
- Découpage en ensembles d'entraînement et de test

### 3. Modélisation et évaluation (`Classification_de_la_qualité_du_sommeil.ipynb`)

Plusieurs modèles de classification ont été entraînés et comparés :

| Modèle | Accuracy | F1-score |
|---|---|---|
| *Modèle 1 (ex. Régression logistique)* | … | … |
| *Modèle 2 (ex. Random Forest)* | … | … |
| *Modèle 3 (ex. …)* | … | … |

**Meilleur modèle :** *à compléter*

## 💡 Principaux enseignements

*À compléter avec vos observations, par exemple :*

- *Le niveau de stress est fortement lié à une mauvaise qualité de sommeil.*
- *La durée de sommeil est l'un des facteurs les plus déterminants.*
- *…*

## 🛠️ Technologies

- **Python**
- **Pandas**, **NumPy** : manipulation des données
- **Matplotlib**, **Seaborn** : visualisation
- **Scikit-learn** : préparation des données, modèles et évaluation
- **Google Colab** : environnement de travail

## 📁 Structure du projet

```
sleep-quality-classification/
├── Analyse_du_dataset_sommeil.ipynb               # Analyse exploratoire
├── Classification_de_la_qualité_du_sommeil.ipynb  # Préparation, modèles et évaluation
├── Sleep_health_and_lifestyle_dataset.csv         # Jeu de données
└── README.md
```

## 🚀 Utilisation

**Dans Google Colab (le plus simple) :** ouvrez un notebook sur GitHub et cliquez sur le badge **« Open in Colab »** en haut du fichier. Envoyez le fichier CSV dans l'espace de fichiers de Colab, puis exécutez les cellules dans l'ordre.

**En local :**

```bash
git clone https://github.com/FARAHEltem/sleep-quality-classification.git
cd sleep-quality-classification
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
jupyter notebook
```

Dans les notebooks, adaptez le chemin du fichier CSV (`/content/...` dans Colab) en `Sleep_health_and_lifestyle_dataset.csv`.

## 🔭 Améliorations possibles

- Optimisation des hyperparamètres (GridSearchCV)
- Validation croisée pour des résultats plus robustes
- Analyse de l'importance des variables
- Déploiement du modèle dans une petite application (Streamlit ou API FastAPI)

## 👤 Auteur

**Farahe El-Montaser** – [GitHub](https://github.com/FARAHEltem) · [LinkedIn](https://www.linkedin.com/in/votre-profil)
