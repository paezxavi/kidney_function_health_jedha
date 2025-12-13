# Modèles de Prédiction de la Santé Rénale

## Objectif du Projet

Ce projet explore l'utilisation de modèles de machine learning pour prédire des indicateurs de santé rénale à partir du jeu de données `kidney_dataset.csv`. L'analyse est menée en deux parties distinctes :
1.  **Classification :** Prédire le statut binaire de la Maladie Rénale Chronique (MRC).
2.  **Régression :** Prédire le Débit de Filtration Glomérulaire (DFG), une mesure continue essentielle de la fonction rénale.

---

## Pipeline de Traitement des Données

Les deux notebooks suivent une méthodologie similaire pour la préparation des données :

1.  **Chargement des données :** Le fichier `kidney_dataset.csv` est chargé dans un DataFrame pandas.
2.  **Nettoyage des données :** Les valeurs manquantes (`NaN`) dans la colonne `Medication` sont remplacées par la chaîne de caractères 'None', considérant l'absence de médicament comme une catégorie à part entière.
3.  **Ingénierie de fonctionnalités (Feature Engineering) :**
    *   Une nouvelle colonne `uACR` (rapport albumine/créatinine urinaire) est créée. Elle est calculée en divisant `Protein_in_Urine` par `Creatinine`, ajoutant ainsi un indicateur clinique pertinent.
4.  **Prétraitement et Encodage :**
    *   Un `ColumnTransformer` est utilisé pour appliquer un prétraitement différencié :
        *   **Variables Numériques :** Les caractéristiques numériques sont standardisées avec `StandardScaler`.
        *   **Variables Catégorielles :** Les caractéristiques catégorielles (`Diabetes`, `Hypertension`, `Medication`) sont encodées avec `OneHotEncoder(drop='first')` pour éviter la multicolinéarité.

---

## Analyse et Modèles

### 1. Classification : Prédire le statut de la MRC (`kidney_function_health_multi_classification_algo.ipynb`)

*   **Objectif :** Ce notebook construit et évalue des modèles pour classifier si un patient est atteint de Maladie Rénale Chronique (`CKD_Status`).
*   **Modèles Évalués :**
    *   Régression Logistique
    *   Arbre de Décision (Classification)
    *   Forêt Aléatoire (Classification)
*   **Conclusion :** Le **Random Forest Classifier** est le modèle recommandé pour ce contexte médical. Bien que la Régression Logistique ait une précision (accuracy) globale légèrement supérieure, le modèle Random Forest atteint un score de **Rappel (Recall) de 1.0**. C'est un avantage crucial en diagnostic, car cela signifie que le modèle identifie tous les vrais positifs, minimisant le risque de passer à côté d'un patient malade (faux négatif). De plus, son analyse d'importance des caractéristiques est la plus pertinente et équilibrée.

### 2. Régression : Prédire le score DFG (`kidney_function_health_multi_regression_algo.ipynb`)

*   **Objectif :** Ce notebook vise à prédire la valeur du Débit de Filtration Glomérulaire (`GFR`), un indicateur clé de la fonction rénale.
*   **Modèles Évalués :**
    *   Régression Linéaire
    *   Arbre de Décision (Régression)
    *   Forêt Aléatoire (Régression)
*   **Conclusion :** Le **Random Forest Regressor** s'avère être le meilleur modèle. Il surpasse les autres avec les métriques de performance les plus élevées (R² de **0.9956**) et l'erreur la plus faible. De plus, son analyse d'importance des caractéristiques est la plus robuste et équilibrée, ce qui en fait le choix le plus fiable et le plus performant pour ce cas d'usage.

---

## Principales Conclusions sur l'Importance des Caractéristiques

À travers les deux analyses (classification et régression), les modèles les plus robustes (Random Forest) ont constamment mis en évidence l'importance d'un groupe de caractéristiques clés pour prédire la santé rénale :

1.  **`Creatinine`** et **`BUN`** (Azote uréique sanguin) : Les deux indicateurs les plus forts.
2.  **`Urine_Output`** (Débit urinaire) : Fortement corrélé à la fonction rénale.
3.  **`Protein_in_Urine`** : Indicateur important de dommages rénaux.
