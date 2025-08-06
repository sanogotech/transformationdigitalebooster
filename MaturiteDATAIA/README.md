# 🧭 **Diagnostic Complet de Maturité Data : 12 Niveaux pour Piloter Votre Transformation**

## De l’Excel Sauvage à l’Entreprise Data-First

---

## 🟠 **CATÉGORIE 1 – SURVIE**

### *Des données non maîtrisées, fragmentées, dangereuses.*

---

### 🔹**Niveau 1 – Excel Sauvage**

📉 *"On navigue à vue, chaque fichier est une bombe à retardement."*

✅ **Objectif :** Identifier les sources critiques, éviter les pertes de données.
📌 **Symptômes :**

* Données sur des clés USB, postes individuels.
* Copie manuelle entre fichiers.
* Formules cassées, erreurs fréquentes, aucune traçabilité.

🧩 **Risques :**

* Décisions sur des données erronées,
* Dépendance à des utilisateurs clés,
* Blocages fréquents.

🛠️ **Actions :**

* Centraliser les fichiers sur Google Drive / OneDrive,
* Modéliser les fichiers critiques,
* Former les utilisateurs à des modèles réutilisables.

🧠 **Compétences :** Excel avancé, gestion documentaire, sensibilisation à la qualité.

---

### 🔹**Niveau 2 – Collaboration Manuelle**

📋 *"On commence à partager… mais mal."*

✅ **Objectif :** Structurer la collaboration autour des fichiers partagés.
📌 **Symptômes :**

* Fichiers partagés mais dupliqués,
* Absence de droits d’accès clairs,
* Multiples versions : v1\_final\_v3\_final\_final.xlsx.

🧩 **Risques :**

* Données divergentes,
* Perte de temps à comparer les versions,
* Méconnaissance des sources fiables.

🛠️ **Actions :**

* Mettre en place des conventions de nommage,
* Définir les rôles d’accès,
* Utiliser les commentaires, les historiques de modification.

🧠 **Outils recommandés :** Google Sheets, Microsoft 365, Notion.

---

### 🔹**Niveau 3 – BI Orphelin**

📊 *"On a des dashboards, mais personne ne s’en sert."*

✅ **Objectif :** Rétablir la confiance et l’usage autour des rapports.
📌 **Symptômes :**

* Rapports Power BI/Tableau existent mais non mis à jour,
* Personne n’en connaît le périmètre,
* Les métiers préfèrent exporter et recalculer.

🧩 **Risques :**

* Décisions en doublon ou erronées,
* Perte de temps et démotivation,
* Échec des projets BI.

🛠️ **Actions :**

* Désigner un owner pour chaque dashboard,
* Documenter les indicateurs,
* Créer un planning de maintenance.

🧠 **Outils recommandés :** Power BI, Tableau, Looker Studio, notion de data literacy.

---

## 🟡 **CATÉGORIE 2 – STRUCTURATION**

### *La donnée devient accessible, propre, documentée, partagée.*

---

### 🔹**Niveau 4 – Data Ad Hoc**

🛠️ *"Des scripts utiles… mais dépendants de héros isolés."*

✅ **Objectif :** Assurer la pérennité des traitements de données.
📌 **Symptômes :**

* Scripts en local, pas versionnés,
* Zéro documentation,
* Dépendance à 1 ou 2 développeurs data.

🧩 **Risques :**

* Défaillance si une personne quitte l’entreprise,
* Reproductibilité impossible,
* Dette technique croissante.

🛠️ **Actions :**

* Centraliser les scripts sur Git,
* Créer des environnements standardisés (Conda, Docker),
* Faire des revues de code.

🧠 **Compétences :** Python, Git, Jupyter, Airflow (notions), collaboration technique.

---

### 🔹**Niveau 5 – Data Structurée**

🗂️ *"On commence à construire une base fiable."*

✅ **Objectif :** Disposer d’un entrepôt de données fiable et maintenu.
📌 **Symptômes :**

* Sources identifiées, entrepôt en place (Snowflake, BigQuery, etc.),
* Extraction planifiée,
* Début d’usage transverse.

🧩 **Risques :**

* Défauts de qualité non détectés,
* Surcharge de pipelines manuels,
* Défaillance si la structure change.

🛠️ **Actions :**

* Mettre en place un schéma source → destination,
* Instaurer un contrôle de qualité sur les pipelines,
* Consolider les usages métiers autour du DWH.

🧠 **Outils :** DWH, dbt, Fivetran, Talend, Airbyte.

---

### 🔹**Niveau 6 – Gouvernance Définie**

⚖️ *"On sait ce que signifient les données et comment les utiliser."*

✅ **Objectif :** Fiabiliser la compréhension et l’usage des données.
📌 **Symptômes :**

* Catalogue de données en cours,
* Indicateurs documentés,
* Métiers impliqués.

🧩 **Risques :**

* KPIs contradictoires entre services,
* Méfiance des utilisateurs,
* Non-conformité RGPD.

🛠️ **Actions :**

* Mettre en place un data catalog (ex : DataHub),
* Définir les indicateurs clés par département,
* Créer un comité gouvernance mensuel.

🧠 **Compétences :** Data stewardship, data owner, RGPD, conformité, acculturation métier.

---

## 🟢 **CATÉGORIE 3 – INDUSTRIALISATION**

### *La donnée devient automatisée, exploitable, utile au quotidien.*

---

### 🔹**Niveau 7 – DataOps**

🔁 *"L’architecture est sous contrôle, les flux sont automatisés."*

✅ **Objectif :** Automatiser la chaîne de valeur de la donnée.
📌 **Symptômes :**

* Pipelines orchestrés,
* Tests de qualité automatisés,
* Déploiement contrôlé.

🧩 **Risques :**

* Latence dans les données,
* Bugs non détectés,
* Outils non alignés.

🛠️ **Actions :**

* Implémenter Airflow, dbt, tests unitaires,
* Mettre en place des alertes en cas d’échec,
* Formaliser le versioning des flux.

🧠 **Compétences :** Data Engineering, CI/CD, monitoring, orchestration.

---

### 🔹**Niveau 8 – Self-Service BI**

📈 *"Les métiers consomment les données en autonomie."*

✅ **Objectif :** Offrir des outils simples, compréhensibles, accessibles.
📌 **Symptômes :**

* Données accessibles via un portail,
* Dashboarding adapté aux utilisateurs,
* Moins de sollicitations à la DSI.

🧩 **Risques :**

* Utilisation sans interprétation correcte,
* Explosion de KPIs non validés,
* Saturation des outils.

🛠️ **Actions :**

* Créer une base de dashboards certifiés,
* Former les utilisateurs à la dataviz,
* Publier un guide d’usage.

🧠 **Compétences :** UX BI, formation interne, datavisualisation, gouvernance de KPI.

---

### 🔹**Niveau 9 – MLOps / IA en Production**

🤖 *"L’intelligence artificielle devient opérationnelle."*

✅ **Objectif :** Déployer, suivre et fiabiliser les modèles IA.
📌 **Symptômes :**

* Modèles déployés,
* Suivi des performances,
* Versions maîtrisées.

🧩 **Risques :**

* Modèles obsolètes ou biaisés,
* Dérive des données,
* Manque de documentation.

🛠️ **Actions :**

* Mettre en place MLflow, pipeline CI/CD IA,
* Définir un processus de validation métier,
* Monitorer les performances.

🧠 **Compétences :** MLOps, DevOps, data science appliquée, éthique IA.

---

## 🔵 **CATÉGORIE 4 – EXCELLENCE**

### *La donnée devient stratégie, culture et moteur d’innovation continue.*

---

### 🔹**Niveau 10 – AI Native**

🧠 *"L’IA est intégrée aux décisions quotidiennes."*

✅ **Objectif :** Intégrer l’IA dans la culture métier.
📌 **Symptômes :**

* IA dans les processus RH, finances, production, etc.,
* Scénarios A/B en cours permanent,
* Processus augmentés par l’IA.

🧩 **Risques :**

* IA mal comprise par les équipes,
* Fausses promesses,
* Réticence à l’adoption.

🛠️ **Actions :**

* Cadrer les cas d’usage stratégiques,
* Créer un Lab IA ouvert aux métiers,
* Renforcer la formation continue.

🧠 **Compétences :** Product Owner IA, business/data alignment, innovation.

---

### 🔹**Niveau 11 – Organisation Apprenante**

📚 *"La donnée alimente les boucles d’amélioration continue."*

✅ **Objectif :** Intégrer les données dans le pilotage de la performance.
📌 **Symptômes :**

* Culture du feedback,
* Apprentissage de l’erreur,
* Innovation data portée par les métiers.

🧩 **Risques :**

* Saturation informationnelle,
* Complexité dans l’interprétation,
* Manque d’alignement stratégique.

🛠️ **Actions :**

* Mettre en place des OKRs pilotés par la donnée,
* Organiser des revues data croisées,
* Intégrer l'analyse post-mortem des projets.

🧠 **Compétences :** Agilité data, pilotage par la valeur, continuous improvement.

---

### 🔹**Niveau 12 – Data-First by Design**

🌐 *"La donnée structure toute l’entreprise : stratégie, outils, RH."*

✅ **Objectif :** Concevoir l’entreprise autour de la donnée dès l’origine.
📌 **Symptômes :**

* L’architecture, les outils, les décisions sont data-centric,
* RH, produit, marketing : tout est co-conçu avec la data,
* Leadership convaincu et engagé.

🧩 **Risques :**

* Complexité de gouvernance,
* Dépendance aux systèmes,
* Nécessité d’alignement fort.

🛠️ **Actions :**

* Faire de la donnée un pilier stratégique,
* Fusionner roadmap produit + data + SI,
* Définir des indicateurs de valeur de la donnée.

🧠 **Compétences :** Leadership data, stratégie d’entreprise, transformation digitale.



* ✅ Un fichier PDF/Word structuré ?
* 📊 Une infographie ou poster visuel à afficher ?
* 📋 Un **outil d’auto-diagnostic interactif** (Excel ou Notion) ?

Je peux le faire immédiatement.
