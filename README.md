# 😴 Classification de la qualité du sommeil

Projet de **statistique et de Machine Learning** qui identifie les facteurs influençant la **qualité du sommeil** et prédit si une personne a une **bonne ou une mauvaise qualité de sommeil** à partir de son mode de vie et de ses indicateurs de santé.

Projet réalisé dans le cadre du **Master Web Intelligence and Data Science**, module *Statistiques Exploratoires Multidimensionnelles* (encadré par Pr. AbdElkamel ALAJ, 2024-2025).

📄 **[Lire le rapport complet (PDF)](Rapport_regression_logistique_sommeil.pdf)**

---

## 🎯 Problématique

> Dans quelle mesure les habitudes de sommeil et le mode de vie influencent-ils la qualité du sommeil ?

- Quels sont les facteurs les plus déterminants pour un sommeil de qualité ?
- Comment le stress, l'activité physique ou l'IMC affectent-ils le sommeil ?
- Peut-on quantifier et hiérarchiser l'impact de chaque facteur ?

## 📊 Données

**Source :** [Sleep Health and Lifestyle Dataset](https://www.kaggle.com/datasets/uom190346a/sleep-health-and-lifestyle-dataset) (Kaggle, Laksika Tharmalingam, licence CC0)

- **374 participants** âgés de 27 à 59 ans, **13 variables**
- Aucune valeur manquante, aucune valeur aberrante problématique
- Données **synthétiques**, construites à des fins pédagogiques et de recherche

| Colonne | Description |
|---|---|
| `Gender`, `Age`, `Occupation` | Caractéristiques démographiques |
| `Sleep Duration` | Durée de sommeil (heures par jour) |
| `Quality of Sleep` | Qualité du sommeil, note de 1 à 10 |
| `Physical Activity Level` | Activité physique (minutes par jour) |
| `Stress Level` | Niveau de stress (1 à 10) |
| `BMI Category` | Catégorie d'IMC |
| `Blood Pressure` | Tension artérielle (systolique/diastolique) |
| `Heart Rate` | Fréquence cardiaque au repos (bpm) |
| `Daily Steps` | Nombre de pas par jour |
| `Sleep Disorder` | Trouble du sommeil (aucun, insomnie, apnée du sommeil) |

**Variable cible :** la qualité du sommeil a été **binarisée** :

| Classe | Règle | Effectif |
|---|---|---|
| **Good** | note ≥ 7 | 255 (68,2 %) |
| **Bad** | note < 7 | 119 (31,8 %) |

## 🔍 Démarche

### 1. Analyse exploratoire

- Distributions des variables numériques et catégorielles, détection des valeurs aberrantes (boxplots)
- Matrice de corrélation : **Stress Level (r = −0,90)** et **Sleep Duration (r = 0,88)** sont très fortement liés à la qualité du sommeil
- Contrôle de la multicolinéarité avec le **VIF** (toutes les valeurs < 5)
- Analyse bivariée : qualité du sommeil selon l'IMC, le trouble du sommeil, le stress…

### 2. Modélisation

- Création de la variable cible binaire (Good / Bad)
- Découpage **stratifié 80 / 20** (entraînement / test)
- **Régression logistique** (estimation par maximum de vraisemblance), interprétation des coefficients et des odds ratios
- Comparaison avec **Random Forest** et **SVM** (noyau radial)
- Évaluation : accuracy, sensibilité, spécificité, précision, F1-score, **courbe ROC et AUC**

## 📈 Résultats

### Notebook Python : régression logistique

| Métrique | Résultat |
|---|---|
| Accuracy | **93,75 %** |
| Sensibilité (rappel) | 94,79 % |
| Spécificité | 91,43 % |
| Précision | 96,05 % |
| F1-score | **95,42 %** |
| AUC | **0,982** |
| Pseudo R² de McFadden | 0,846 |

### Rapport R : comparaison de trois modèles (ensemble de test, n = 74)

| Modèle | Accuracy | AUC | Temps |
|---|---|---|---|
| Régression logistique | 98,65 % | 1,000 | 21 ms |
| Random Forest (500 arbres) | 98,65 % | 1,000 | 101 ms |
| SVM (noyau radial) | 98,65 % | 1,000 | 20 ms |

Les trois modèles ne font **qu'une seule erreur sur 74** prédictions. La **régression logistique** est retenue comme modèle final pour son **interprétabilité** (coefficients et odds ratios), ses tests de significativité et sa rapidité.

### Facteurs les plus importants (Random Forest, Mean Decrease Gini)

| Rang | Variable | Importance |
|---|---|---|
| 1 | **Stress Level** | 50,67 |
| 2 | **Sleep Duration** | 38,54 |
| 3 | **Heart Rate** | 21,42 |
| 4 | Age | 6,09 |
| 5 | Daily Steps | 4,77 |

Ces résultats convergent avec la régression logistique, où le stress, la durée de sommeil, la fréquence cardiaque, l'activité physique et les troubles du sommeil sont statistiquement significatifs.

## 💡 Principaux enseignements

- **Le stress est le facteur dominant** : plus il est élevé, plus la qualité du sommeil se dégrade.
- **La durée de sommeil** est le deuxième facteur majeur (7,5 h en moyenne pour un bon sommeil, contre 6,3 h pour un mauvais).
- **Stress, durée de sommeil et fréquence cardiaque** représentent à eux seuls près de **87 %** de l'importance prédictive.
- Les personnes **obèses** ont environ 50 % de mauvaise qualité de sommeil, contre 20 % pour un poids normal.

## ⚠️ Limites

Les performances très élevées (AUC proche de 1) s'expliquent en partie par la **nature synthétique** des données, qui présentent des relations très régulières, et par la **petite taille** de l'ensemble de test. Sur des données cliniques réelles, les performances seraient vraisemblablement plus modestes. La **hiérarchie des facteurs** reste toutefois cohérente avec la littérature scientifique.

## 🛠️ Technologies

- **Python** (Google Colab) : Pandas, Matplotlib, Seaborn
- **R** (RStudio) : tidyverse, caret, car, pROC, randomForest, e1071, MASS, corrplot, ggplot2

## 📁 Structure du projet

```
sleep-quality-classification/
├── Analyse_du_dataset_sommeil.ipynb                 # Analyse exploratoire (Python)
├── Classification_de_la_qualité_du_sommeil.ipynb    # Régression logistique (Python)
├── comparaison_modeles_sommeil.ipynb                # Comparaison LR / Random Forest / SVM (Python)
├── Sleep_health_and_lifestyle_dataset.csv           # Jeu de données
├── Rapport_regression_logistique_sommeil.pdf        # Rapport complet (analyse sous R)
└── README.md
```

## 🚀 Utilisation

Ouvrez les notebooks directement dans Google Colab :

- Analyse exploratoire : [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/farahe-elmontaser/sleep-quality-classification/blob/main/Analyse_du_dataset_sommeil.ipynb)
- Classification : [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/farahe-elmontaser/sleep-quality-classification/blob/main/Classification_de_la_qualit%C3%A9_du_sommeil.ipynb)
- Comparaison des modèles : [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/farahe-elmontaser/sleep-quality-classification/blob/main/comparaison_modeles_sommeil.ipynb)

Envoyez ensuite le fichier CSV dans l'espace de fichiers de Colab, puis exécutez les cellules dans l'ordre.

## 👤 Auteure

**Farahe El-Montaser** – [LinkedIn](https://www.linkedin.com/in/farahe-el-montaser-30a422368) · [GitHub](https://github.com/farahe-elmontaser)
