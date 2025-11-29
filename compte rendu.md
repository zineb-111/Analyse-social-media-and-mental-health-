# ZINEB EL MEJDOUBI
**Numéro d'étudiant** : 24010156
**Classe** : CAC2


# Compte rendu

📊 Analyse de l'Équilibre entre Usage des Réseaux Sociaux et Santé Mentale 

**Date :** 29 Novembre 2025



## Introduction
Ce projet vise à analyser les facteurs influençant l'indice de bonheur à partir d'un jeu de données relatif à la santé mentale et l'équilibre des médias sociaux. L'objectif est de construire et d'évaluer plusieurs modèles de régression pour prédire cet indice, ainsi qu'un modèle de classification pour catégoriser le niveau de bonheur. L'analyse mettra en lumière les variables clés ayant un impact significatif sur le bien-être.

## Exploration et Préparation des Données
Le jeu de données initial contient 500 entrées et 10 colonnes. Aucune valeur manquante n'a été détectée, ce qui a simplifié la phase de prétraitement. La colonne `User_ID`, étant un identifiant unique, a été supprimée. Les variables catégorielles comme `Gender` et `Social_Media_Platform` ont été transformées en variables numériques à l'aide de l'encodage One-Hot, préparant ainsi le jeu de données pour l'entraînement des modèles.

## Analyse de Corrélation
L'analyse de corrélation a révélé des relations importantes entre les variables et l'indice de bonheur :
- **Stress_Level(1-10)** : Forte corrélation négative (-0.74). Plus le niveau de stress est élevé, plus l'indice de bonheur tend à être bas.
- **Daily_Screen_Time(hrs)** : Forte corrélation négative (-0.71). Un temps d'écran quotidien plus élevé est associé à un indice de bonheur plus faible.
- **Sleep_Quality(1-10)** : Forte corrélation positive (0.68). Une meilleure qualité de sommeil est liée à un indice de bonheur plus élevé.

Ces corrélations suggèrent que la santé mentale et les habitudes de vie jouent un rôle prépondérant dans l'indice de bonheur.

## Modèles de Régression
Nous avons entraîné et évalué plusieurs modèles de régression pour prédire l'indice de bonheur. Voici un aperçu de chaque modèle et de ses performances.

### 1. Régression Linéaire Simple
- **Mise en œuvre** : Utilisant uniquement `Stress_Level(1-10)` comme prédicteur.
- **Performance** : R-carré = {r2_simple:.2f}, MSE = {mse_simple:.2f}, MAE = {mae_simple:.2f}.
- **Forces** : Très simple et facile à interpréter. Bonne base pour comprendre l'impact d'une seule variable.
- **Faiblesses** : Limité aux relations linéaires, ne capture pas la complexité des données.

### 2. Régression Linéaire Multiple
- **Mise en œuvre** : Inclut toutes les caractéristiques prédictives.
- **Performance** : R-carré = {r2_multiple:.2f}, MSE = {mse_multiple:.2f}, MAE = {mae_multiple:.2f}.
- **Forces** : Interprétable, prend en compte plusieurs facteurs simultanément.
- **Faiblesses** : Suppose une relation linéaire, sensible à la multicolinéarité.

### 3. Régression Polynomiale
- **Mise en œuvre** : Utilise des caractéristiques polynomiales de degré 2.
- **Performance** : R-carré = {r2_poly:.2f}, MSE = {mse_poly:.2f}, MAE = {mae_poly:.2f}.
- **Forces** : Peut capturer des relations non linéaires.
- **Faiblesses** : Augmente la complexité du modèle et le risque de surapprentissage. Moins performant que la régression linéaire multiple dans ce cas.

### 4. Régression Ridge (L2)
- **Mise en œuvre** : Régression linéaire avec pénalité L2 pour la régularisation (`alpha=1.0`).
- **Performance** : R-carré = {r2_ridge:.2f}, MSE = {mse_ridge:.2f}, MAE = {mae_ridge:.2f}.
- **Forces** : Aide à prévenir le surapprentissage et gère la multicolinéarité en réduisant les coefficients.
- **Faiblesses** : Ne réalise pas de sélection de caractéristiques (les coefficients ne sont pas réduits à zéro).

### 5. Régression Lasso (L1)
- **Mise en œuvre** : Régression linéaire avec pénalité L1 pour la régularisation (`alpha=0.1`).
- **Performance** : R-carré = {r2_lasso:.2f}, MSE = {mse_lasso:.2f}, MAE = {mae_lasso:.2f}.
- **Forces** : Réalise la sélection de caractéristiques en réduisant certains coefficients à zéro, simplifiant le modèle.
- **Faiblesses** : Son efficacité dépend fortement du choix de `alpha`.

### 6. Arbre de Décision
- **Mise en œuvre** : Modèle basé sur un seul arbre de décision.
- **Performance** : R-carré = {r2_dt:.2f}, MSE = {mse_dt:.2f}, MAE = {mae_dt:.2f}.
- **Forces** : Facile à comprendre et à visualiser (pour des arbres simples).
- **Faiblesses** : Très sensible au surapprentissage, souvent moins performant que les méthodes d'ensemble.

### 7. Forêt Aléatoire
- **Mise en œuvre** : Ensemble de plusieurs arbres de décision.
- **Performance** : R-carré = {r2_rf:.2f}, MSE = {mse_rf:.2f}, MAE = {mae_rf:.2f}.
- **Forces** : Très robuste, gère les relations non linéaires et les interactions, réduit le surapprentissage.
- **Faiblesses** : Moins interprétable que les modèles linéaires, peut être coûteux en calcul.

## Tableau Récapitulatif des Performances des Modèles de Régression
```
{performance_df.round(2).to_string()}
```

## Analyse de Régression Logistique (Classification)
Pour explorer les catégories de bonheur, la variable cible `Happiness_Index(1-10)` a été discrétisée en trois catégories : 'faible' (0-6), 'moyen' (7-8) et 'élevé' (9-10). Un modèle de régression logistique multiclasse a été entraîné.

### Performance du Modèle de Régression Logistique
- **Précision (Accuracy)** : {model_lr.score(X_test_clf, y_test_clf):.2f}
- **Rapport de Classification** :
```
{classification_report(y_test_clf, y_pred_clf, target_names=['faible', 'moyen', 'élevé'])}
```
- **Matrice de Confusion** :
```
{conf_matrix}
```

### Interprétation des Résultats de Classification
Le modèle de régression logistique a une précision globale de {model_lr.score(X_test_clf, y_test_clf):.2f}. Il excelle dans la prédiction de la catégorie 'élevé' (Rappel de {classification_report(y_test_clf, y_pred_clf, output_dict=True)['élevé']['recall']:.2f}) mais peine avec la catégorie 'faible' (Rappel de {classification_report(y_test_clf, y_pred_clf, output_dict=True)['faible']['recall']:.2f}), la confondant souvent avec la catégorie 'moyen'. Cela est probablement dû au déséquilibre des classes et à la complexité de distinguer les catégories adjacentes. Des techniques de rééquilibrage de classes pourraient améliorer la performance sur la catégorie 'faible'.

## Découvertes Clés
- Le **Stress_Level**, la **Sleep_Quality** et le **Daily_Screen_Time** sont les facteurs les plus influents sur l'indice de bonheur.
- Le **modèle de Forêt Aléatoire** est le plus performant pour prédire l'indice de bonheur, indiquant des relations complexes et non linéaires entre les variables.
- La régression linéaire multiple et les modèles régularisés (Ridge, Lasso) offrent des performances solides, soulignant l'importance de plusieurs caractéristiques simultanément.
- Le modèle d'Arbre de Décision seul est moins efficace que les modèles d'ensemble, suggérant que l'agrégation d'arbres est bénéfique.
- La régression logistique permet de classer les niveaux de bonheur, mais la prédiction des catégories minoritaires ('faible') reste un défi.

## Conclusions Générales
Cette analyse a démontré l'importance des facteurs liés au mode de vie et à la santé mentale dans la détermination de l'indice de bonheur. La capacité de la Forêt Aléatoire à gérer la complexité des relations en fait le modèle le plus adapté pour cette tâche. Les interventions visant à améliorer le bonheur devraient cibler la gestion du stress, l'amélioration du sommeil et la modération du temps d'écran.

## Prochaines Étapes
- **Optimisation des hyperparamètres** : Utiliser des techniques comme la recherche par grille (Grid Search) ou la recherche aléatoire (Random Search) pour affiner les modèles, en particulier la Forêt Aléatoire et l'Arbre de Décision.
- **Rééquilibrage des classes** : Appliquer des méthodes de rééquilibrage (SMOTE, sur/sous-échantillonnage) pour améliorer la performance du modèle de régression logistique sur les classes minoritaires.
- **Exploration d'autres modèles** : Tester d'autres algorithmes d'apprentissage automatique comme XGBoost ou LightGBM pour la régression et la classification.
- **Analyse d'interactions** : Étudier plus en profondeur les interactions entre les caractéristiques pour affiner la compréhension des relations non linéaires.
- **Collecte de données supplémentaires** : Un jeu de données plus vaste ou incluant d'autres variables pourrait renforcer la robustesse et la généralisabilité des modèles.
"""

print(readme_content)
