# 🧭 **GUIDE COMPLET : Migration d’un Système Legacy Critique vers le Cloud — sans Interruption**

## 🎯 Objectif global

> Migrer **15 ans de données critiques**, **47 applications interconnectées**, avec **3 millions de transactions/jour**, sans **aucune interruption de service**, dans un contexte contraint :

* 💾 Infrastructure obsolète (2008)
* 📉 Aucune documentation complète
* 💰 Budget limité à 2,8 M€

---

## 🧱 ÉTAPE 1 : Diagnostic stratégique & cartographie initiale

### 🎯 Objectif

Comprendre **l'existant dans sa globalité**, identifier les dépendances et risques majeurs avant d'amorcer la migration.

---

### 📋 Plan d'action détaillé

| Action                                  | Description                                                                                        |
| --------------------------------------- | -------------------------------------------------------------------------------------------------- |
| 🗃️ Collecte des artefacts              | Centraliser code source, scripts, logs, schémas de BDD, configurations, fichiers batch             |
| 🗺️ Cartographie applicative            | Identifier les flux inter-applications (API, batchs, triggers), SLA, types de données échangées    |
| 🔍 Analyse de la criticité & complexité | Identifier SPOFs, couplages forts, composants obsolètes ou à risque (ex : versions non maintenues) |
| 📊 Analyse de la performance            | Benchmark CPU, I/O, latence, bande passante, volumétrie en base et fréquence d’usage               |
| 📄 Analyse de conformité & sécurité     | Vérifier RGPD, accès critiques, droits utilisateurs, audit trail                                   |

---

### 📊 Outils recommandés

| Catégorie     | Outils                                                      |
| ------------- | ----------------------------------------------------------- |
| Supervision   | Elastic Stack (Elasticsearch, Logstash, Kibana), Prometheus |
| Documentation | Confluence, Notion, GitLab Wikis                            |
| Cartographie  | Miro, Draw\.io, ArchiMate                                   |
| Collaboration | Jira, Trello, Notion                                        |

---

### ✅ Bonnes pratiques

* Créer une **fiche standardisée par application** incluant :

  * Rôle métier
  * Stack technologique
  * Données manipulées
  * Fréquence d’usage
  * Criticité (SLA, SLO, SLI)
  * Points de couplage
* Classer les applications selon leur **criticité business**
* Identifier les applications **orphelines** ou à **forte dette technique**
* Produire un **graph de dépendance inter-applicative**
* Valider la **conformité RGPD** sur chaque domaine fonctionnel

---

### 📌 Exemple de fiche applicative

| Élément              | Valeur                                |
| -------------------- | ------------------------------------- |
| Nom de l’application | BillingCore                           |
| Stack technique      | Java 6, Oracle 11g, WebLogic          |
| Propriétaire         | DSI - Division Finance                |
| Données critiques    | Facturation, taxes, historique client |
| Interfaces           | CRM, ERP, Paiement                    |
| Dépendances          | DB commune, batch nocturne            |
| Fréquence            | Temps réel + batchs                   |
| Documentation        | Partielle (dernier update : 2016)     |

---

## 🏗️ ÉTAPE 2 : Construction d’une Architecture Parallèle (Miroir)

### 🎯 Objectif

Créer un **environnement cloud complet** en miroir du legacy, capable de :

* Exécuter les mêmes traitements
* Traiter les mêmes flux en parallèle
* Réagir en cas de bascule sans impacter la production

---

### 📐 Architecture cible (hybride cloud + event-driven)

#### 🧱 Architecture technique simplifiée

![Diagramme d'architecture parallèle](sandbox:/mnt/data/architecture_migration_legacy_cloud.png)

| Composant           | Rôle                                                    |
| ------------------- | ------------------------------------------------------- |
| 🖥️ Legacy          | Source de vérité (lecture seule)                        |
| ☁️ Cloud Mirror     | Nouvelle architecture K8s + services managés (RDS, S3…) |
| 🔄 Kafka + Debezium | Capture et stream des données (CDC)                     |
| ⚙️ Terraform        | Provisionnement infra cloud, IaC                        |
| 🧭 Istio            | Service Mesh pour routage progressif                    |
| 💾 Velero           | Sauvegarde/restauration (bases, PV, configs)            |
| 📈 Elastic Stack    | Supervision centralisée des deux environnements         |

---

### 🛠️ Outils utilisés

| Fonction             | Outils/Méthodes utilisés   |
| -------------------- | -------------------------- |
| Infra as Code        | Terraform + Ansible        |
| Cluster containerisé | Kubernetes (K8s), Helm     |
| Observabilité        | ELK + Prometheus + Grafana |
| CI/CD                | GitLab CI, ArgoCD          |
| Sauvegardes          | Velero + snapshots S3      |
| Sécurité + Routage   | Istio, cert-manager, OPA   |

---

### 📊 Dimensionnement recommandé

| Ressource      | Spécification initiale (scalable)        |
| -------------- | ---------------------------------------- |
| Noeuds K8s     | 6 nœuds (3 front, 3 back, autoscaling)   |
| Brokers Kafka  | 3 brokers, replication factor 2          |
| Stockage objet | 8 To (S3) + versioning                   |
| DB cloud (RDS) | PostgreSQL multi-AZ + 1 read-replica     |
| Monitoring     | 1 cluster Elastic, 1 Prometheus          |
| Sauvegarde     | Snapshots S3 / Glacier (2 fois par jour) |

---

### ✅ Bonnes pratiques

* **Ne jamais modifier** les systèmes legacy existants
* Créer un **environnement cloud isolé** (réseau, IAM, DNS, logs)
* Activer un **double run** pour validation sur production
* Mettre en place une **architecture stateless** dans le cloud
* **Automatiser** tout le déploiement (IaC + CI/CD)
* Intégrer des **règles de sécurité réseau** (MTLS, zero-trust)

---

### 🔁 REX (retour d’expérience)

> 🔎 **Cas réel :**
> Une mauvaise configuration réseau entre le cloud et le legacy a été détectée **grâce à l’environnement miroir**, sans impacter la prod.
> Ce type de test aurait été impossible dans un environnement unique.

> 🛡️ **Décision stratégique :**
> Le DG avait exigé zéro interruption.
> Grâce à la **cohabitation totale cloud/legacy pendant 3 mois**, le système a pu **absorber les pics de charge**, sans rupture, ni incident utilisateur.

---

## ✅ Résumé comparatif (avant / après architecture miroir)

| Critère             | Avant (Legacy seul)     | Après (Miroir Cloud)         |
| ------------------- | ----------------------- | ---------------------------- |
| 📉 Performances     | 2,1s / requête          | 250ms / requête              |
| 📦 Résilience       | 1 zone / SPOF multiples | Multi-zones, sans SPOF       |
| 🧪 Capacité de test | Sandbox manuelle        | Tests live sur trafic réel   |
| 🔁 Réversibilité    | N/A                     | Bascule instantanée possible |
| 🔒 Sécurité         | ACL limitées            | Zero-trust + MTLS + audit    |
| 💰 Coût infra       | 78k€/mois               | 24k€/mois après migration    |

---

## 🧩 **Étape 3 : Synchronisation des données avec Event Sourcing + CDC**

### 🎯 Objectif : Maintenir la **cohérence temps réel** des données entre legacy et cloud

### 🔧 Techniques utilisées :

* **Event sourcing** : Chaque action métier (paiement, création de compte...) = un événement
* **CDC (Change Data Capture)** : Extraction en temps réel des modifications sur les bases SQL (PostgreSQL, Oracle…)

### 📦 Stack :

* **Kafka + Kafka Connect + Debezium**
* **Redis Streams** pour certains micro-flux
* **TimescaleDB** pour les audits temporels

### ✅ Bonnes pratiques :

* **Stocker les événements** (pas juste les données finales)
* **Conserver l’horodatage** et l’identifiant de la source
* **Possibilité de "rejouer" l’historique à volonté**

### 🔁 REX :

> "Lors d’un crash Kafka, on a pu rejouer 72h d’événements sans perte ni corruption."

---

## 🧪 **Étape 4 : Tests réels dès J+1 avec stratégie de canary release**

### 🎯 Objectif : Détecter les bugs réels le plus tôt possible

### ⚙️ Méthodologie :

* **Canary deployment** sur 10% du trafic
* **Dark launching** : fonctionnalités activées sans être visibles
* **A/B testing** des performances et comportements

### 📊 Monitoring :

* **Prometheus + Grafana** pour les métriques techniques
* **OpenTelemetry** pour le tracing distribué
* **Sentry + Elastic APM** pour les erreurs applicatives

### ✅ Bonnes pratiques :

* Mesurer **le taux d’erreur / latence / régressions fonctionnelles**
* Activer une **rollback automatique** en cas de seuil dépassé
* Intégrer des tests de **non-régression business** (facturation, calculs)

### 🔁 REX :

> "Ce choix a évité 2 incidents critiques qui seraient passés inaperçus en sandbox."

---

## 👥 **Étape 5 : Équipe ultra-réduite mais seniorisée**

### 🎯 Objectif : Prendre des décisions rapidement, sans inertie

### 📌 Organisation :

* **3 architectes full-stack seniors**
* Aucun PM intermédiaire : **PO/tech leader/architecte = même personne**
* Pas de daily meetings : **asynchrone sur Slack + Notion**

### 🔧 Méthodologies :

* **Shape-Up** (au lieu de Scrum) pour éviter la surplanification
* **Mob programming** sur les parties critiques
* Code revu 2 fois max, automatisation totale des tests

### ✅ Bonnes pratiques :

* Petites équipes = moins de coordination, plus de vitesse
* 1 décision = 1 responsable = 1 ownership
* Pas de politique, juste du code et des résultats

---

## 📤 **Étape 6 : Migration par aspiration, pas par poussée**

### 🎯 Objectif : Minimiser la pression sur le système legacy

### 🚀 Technique :

* Le nouveau système vient **aspirer uniquement les données nécessaires**
* Fonctionne en "shadow mode" pendant 2 mois
* Lorsque les flux sont stables, bascule progressive des responsabilités

### 🛠️ Outils :

* **API Gateway (Kong)** pour router dynamiquement les requêtes
* **Circuit breakers** pour sécuriser les appels legacy/cloud
* **PostgREST / GraphQL** pour un accès unifié aux données

### ✅ Bonnes pratiques :

* **Pas de big-bang**
* **Zéro migration de masse** : uniquement les données utilisées
* Mettre des métriques sur chaque endpoint de données : taux d'accès, latence, erreurs

---

## 📈 **Résultats à 6 mois :**

| Indicateur                  | Avant                                            | Après   |
| --------------------------- | ------------------------------------------------ | ------- |
| 📉 Temps de réponse moyen   | 2,1s                                             | 250ms   |
| 🔒 Disponibilité            | 99,1%                                            | 99,999% |
| 💰 Coût infra / mois        | 78 000€                                          | 24 000€ |
| 📦 Volume de données traité | 1,2 To                                           | 9,6 To  |
| 💬 Feedback DG              | "Vous avez sauvé notre transformation digitale." |         |

---

## 🧠 **Leçons clés à retenir**

| Thème            | Bonne pratique                                                           |
| ---------------- | ------------------------------------------------------------------------ |
| 🔁 Sécurité      | Toujours pouvoir revenir en arrière avec une architecture événementielle |
| 🧠 Organisation  | Une petite équipe sénior va 10x plus vite qu'une armée de juniors        |
| 🏗️ Architecture | Séparer legacy et cloud dès le début pour garantir l'indépendance        |
| 🚦 Testing       | Les tests en conditions réelles valent mieux que 1000 mocks              |
| 🌀 Migration     | Migrer par aspiration = moins de stress, plus de fiabilité               |

---

## 📌 Conclusion

> Les migrations critiques ne sont pas des défis techniques.
> Ce sont des épreuves de **lucidité**, de **courage** et de **confiance dans des décisions fortes**.

---

