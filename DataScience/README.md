# 📘 Le Processus Data Driven


*(Du brut à la décision actionnable)*

Une entreprise **data-driven** place la donnée au cœur de toutes ses décisions.
👉 Le processus suit 6 étapes clés, où les **4 types d’analyses** (Descriptive, Diagnostique, Prédictive, Prescriptive) prennent place comme **moteur de valeur**.

---

## 🔄 Les 6 étapes du processus Data Driven

1️⃣ **Collecter & Centraliser**

* Sources : ERP, CRM, capteurs IoT, applications, réseaux sociaux, open data.
* Objectif : disposer de données variées, en temps réel si possible.
* Bonnes pratiques : API, ETL, Data Lake, Data Warehouse.
  💡 Sans collecte fiable, pas de pilotage possible.

---

2️⃣ **Gouverner & Sécuriser**

* Règles de qualité, conformité (RGPD, ISO 27001), cybersécurité.
* Objectif : instaurer la **confiance dans la donnée**.
* Bonnes pratiques : Master Data Management (MDM), IAM/SSO, politiques de sécurité.
  💡 Une entreprise data-driven est aussi “trust-driven”.

---

3️⃣ **Préparer & Enrichir**

* Nettoyage, normalisation, suppression des doublons, enrichissement externe.
* Outils : Python (Pandas), R, Talend, dbt.
* Objectif : obtenir une donnée prête à l’analyse.
  💡 80% du travail d’un Data Scientist = préparation de la donnée.

---

4️⃣ **Analyser & Comprendre** (Cœur du Data Driven)
C’est ici que s’appliquent les **4 types d’analyse** :

* **Descriptive** → *Quoi ?* → Reporting, Dashboards.
* **Diagnostique** → *Pourquoi ?* → Recherche de causes racines.
* **Prédictive** → *Et après ?* → Machine Learning, anticipation.
* **Prescriptive** → *Que faire ?* → Optimisation, recommandations actionnables.

💡 Chaque niveau augmente la **maturité data** et la valeur métier.

---

5️⃣ **Diffuser & Rendre Accessible**

* Objectif : que chaque décisionnaire ait accès aux bons insights.
* Outils : Power BI, Tableau, Metabase, API data, reporting automatisé.
* Bonnes pratiques : Data Storytelling, démocratisation des dashboards.
  💡 Une donnée qui dort dans un rapport non consulté n’a aucune valeur.

---

6️⃣ **Agir & Améliorer en continu**

* Mise en œuvre des recommandations (CRM, ERP, automatisation).
* Tests A/B, suivi des KPIs, boucle de rétroaction.
* Objectif : transformer la donnée en **impact business mesurable**.
  💡 Data Driven = Action Driven.

---

## 🔗 Synthèse Data Science & Data Driven

| Étape Data Driven | Rôle Data Science                   | Types d’analyses mobilisés                          | Livrables                                    |
| ----------------- | ----------------------------------- | --------------------------------------------------- | -------------------------------------------- |
| Collecter         | Automatiser l’ingestion des données | -                                                   | Pipelines ETL, Data Lake                     |
| Gouverner         | Assurer qualité et conformité       | -                                                   | Catalogue de données, règles de gouvernance  |
| Préparer          | Nettoyer et transformer             | -                                                   | Jeux de données propres, feature engineering |
| Analyser          | Explorer et modéliser               | Descriptive, Diagnostique, Prédictive, Prescriptive | Rapports, modèles, scoring, recommandations  |
| Diffuser          | Visualiser et vulgariser            | Descriptive, Diagnostique                           | Dashboards, Data Stories                     |
| Agir              | Déployer et mesurer l’impact        | Prescriptive                                        | Plans d’action, API, intégration CRM/ERP     |

---

## 🎯 Exemple concret – Retail Data Driven

1. **Collecte** : Données caisse + appli mobile + météo locale.
2. **Gouvernance** : Vérification RGPD (pas de données personnelles sensibles non anonymisées).
3. **Préparation** : Nettoyage des ventes journalières, enrichies par météo.
4. **Analyse** :

   * Descriptive : CA en baisse 10% vs mois dernier.
   * Diagnostique : corrélation avec pluies + baisse fréquentation magasin.
   * Prédictive : modèle prévoit -15% si météo pluvieuse continue.
   * Prescriptive : booster les promos en ligne + livraison gratuite quand il pleut.
5. **Diffusion** : Dashboard accessible aux managers régionaux.
6. **Action** : Campagne promo déployée, résultats mesurés en temps réel.

👉 Résultat : **+12% de ventes en ligne** compensant la baisse en magasin.

---

## 🏆 À retenir

* Le **processus Data Driven** transforme la donnée en **avantage compétitif**.
* Les **4 types d’analyses** sont au cœur de la phase **Analyse** mais irriguent aussi la diffusion et l’action.
* La **Data Science** est le moteur technique (statistiques, IA, ML, optimisation).
* Une entreprise réellement **data-driven** ne se contente pas de **reporter le passé**, elle **pilote son futur** grâce à la donnée.


----------
# 📘 Guide Pratique des 4 Types d’Analyse de Données

*(Descriptive, Diagnostique, Prédictive, Prescriptive)*

La donnée brute ne vaut rien si elle n’est pas exploitée intelligemment. Pour en tirer de la valeur, il existe **4 grands types d’analyse**, qui forment une véritable **pyramide de maturité data**.

👉 Chaque étape répond à une question :

1. **Descriptive** – Quoi ?
2. **Diagnostique** – Pourquoi ?
3. **Prédictive** – Et après ?
4. **Prescriptive** – Que faire ?

---

## 1️⃣ Analyse Descriptive – **“Que s’est-il passé ?”**

### Définition

C’est la **photo de la situation** : on décrit les faits observés.

### Exemples

* CA du mois : 150K€
* Taux de churn : 5%
* Évolution des ventes sur 6 mois

### Bonnes pratiques

✅ Standardiser les KPI (mêmes définitions pour tous)
✅ Utiliser des visualisations simples (histogrammes, courbes, camemberts)
✅ Comparer dans le temps (MoM, YoY)
✅ Vérifier la qualité des données avant diffusion

### Mauvais usages

❌ Rapporter des chiffres bruts sans contexte
❌ Multiplier les KPI au point de noyer la direction
❌ Produire des rapports sans action derrière

### REX (Retour d’expérience)

Une banque publiait chaque mois le volume de crédits accordés. Mais faute de comparaison avec l’année précédente et de segmentation par région, elle a manqué un ralentissement préoccupant dans une zone clé.

### Outils & Méthodes

🔧 Excel / Google Sheets, SQL (SELECT, GROUP BY), Power BI, Tableau, Metabase, Python (Pandas, Matplotlib), R (ggplot2)

### Livrables

📑 Rapports mensuels / hebdos, Dashboards interactifs, Scorecards KPI, Data Quality Report

---

## 2️⃣ Analyse Diagnostique – **“Pourquoi cela s’est-il passé ?”**

### Définition

C’est **l’enquête** : on cherche les **causes racines** et corrélations.

### Exemple

* Pourquoi le churn a augmenté de 5% ?
  → 80% des clients perdus venaient de la région Sud
  → Ils étaient majoritairement sur l’offre “Start”

### Bonnes pratiques

✅ Segmenter les données (par région, produit, profil client)
✅ Identifier corrélations mais tester causalité
✅ Valider les hypothèses avec plusieurs sources
✅ Documenter le raisonnement pour éviter mauvaises interprétations

### Mauvais usages

❌ Confondre corrélation et causalité
❌ Se baser uniquement sur une intuition sans validation statistique
❌ Sur-analyser au point de bloquer l’action

### REX

Une startup e-commerce voyait ses ventes chuter. L’équipe marketing accusait la hausse des prix. L’analyse diagnostique a montré que 70% des abandons venaient d’un **bug mobile** → problème résolu, ventes revenues.

### Outils & Méthodes

🔧 SQL (jointures, cohortes), Python (scikit-learn pour corrélations), R (régressions), Power BI/Tableau (drill-down), RCA (Root Cause Analysis), Pareto

### Livrables

📑 Analyse des causes racines, Diagrammes Ishikawa/Pareto, Rapports de cohortes, Documentation d’investigation

---

## 3️⃣ Analyse Prédictive – **“Que va-t-il se passer ?”**

### Définition

C’est la **boule de cristal** : on utilise des modèles pour anticiper.

### Exemple

* Quels clients risquent de partir dans 3 mois ?
  → Moins d’activité sur l’appli
  → Revenus en baisse

### Bonnes pratiques

✅ Commencer simple (régression, scoring) avant ML avancé
✅ Toujours valider les modèles (train/test, cross-validation)
✅ Mettre à jour régulièrement les modèles (drift)
✅ Utiliser des méthodes explicables (SHAP, LIME)

### Mauvais usages

❌ Considérer une prédiction comme une certitude (elle reste probabiliste)
❌ Oublier d’actualiser le modèle
❌ Lancer du ML sans données propres et suffisantes

### REX

Un opérateur télécom avait déployé un modèle de churn. Six mois plus tard, les prédictions sont devenues fausses car la crise avait changé les comportements. Le modèle, non recalibré, a perdu toute fiabilité.

### Outils & Méthodes

🔧 Python (scikit-learn, TensorFlow, PyTorch), R (caret, forecast), SQL (time series), Azure ML, AWS SageMaker, Méthodes : régression, clustering, séries temporelles

### Livrables

📑 Modèles prédictifs (fichiers pickle/h5), Rapports de performance (ROC, AUC, RMSE), Tableaux de scoring, Documentation technique & métier

---

## 4️⃣ Analyse Prescriptive – **“Que devons-nous faire ?”**

### Définition

C’est la **boussole** : l’analyse mène à l’action concrète.

### Exemple

* Comment réduire le churn de 20% ?
  → Offres ciblées pour les clients à risque
  → Renforcement du service client dans le Sud

### Bonnes pratiques

✅ Définir contraintes métiers (budget, RH, légales)
✅ Tester les recommandations par A/B testing
✅ Intégrer les résultats dans les process (CRM, ERP)
✅ Toujours valider humainement les décisions automatiques

### Mauvais usages

❌ Proposer des actions impossibles à appliquer (coût, RH)
❌ Négliger l’adoption par les équipes métiers
❌ Penser que la machine décide seule sans validation humaine

### REX

Une banque a déployé un moteur de recommandations de crédit. Sans intégrer les contraintes réglementaires, certaines propositions étaient illégales → perte de confiance des conseillers et retour en arrière obligatoire.

### Outils & Méthodes

🔧 Python (scipy.optimize, OR-Tools), R (lpSolve), SAS, IBM Decision Optimization, CPLEX, Gurobi, Méthodes : A/B Testing, Monte Carlo, Algorithmes génétiques

### Livrables

📑 Plans d’action data-driven, Tableaux de recommandations, Rapports A/B Testing, Intégration CRM/ERP, Documentation métier

---

## 🎯 Résumé visuel & pratique

* **Descriptive = Photo** → Quoi ?
* **Diagnostique = Enquête** → Pourquoi ?
* **Prédictive = Boule de cristal** → Et après ?
* **Prescriptive = Boussole** → Que faire ?

💡 **Le saviez-vous ?**
👉 80% des entreprises s’arrêtent au descriptif.
👉 Passer au prescriptif, c’est multiplier par **3 l’impact business des données**.

---


