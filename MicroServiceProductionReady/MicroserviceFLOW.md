# 🚦 Microservice Architecture Flow — Comment les apps modernes tournent fluide

## 🧭 Vue d’ensemble

Contrairement au **monolithe**, une app en **microservices** découpe le domaine en petits services autonomes (User, Product, Order, Payment…). Chaque service est **indépendant** pour le build, le déploiement et la montée en charge, et communique via **API synchrones** (REST/GraphQL) et **événements asynchrones** (Kafka/RabbitMQ/NATS).

![Flow Microservices](https://github.com/sanogotech/transformationdigitalebooster/blob/main/MicroServiceProductionReady/MicroServiceProductionFLOW.jpg)

---

## 1) 👤 Client Interaction (Web/Mobile)

* **Rôle** : Point de départ (ex. “Place Order”).
* **Bonnes pratiques**

  * Utiliser des **SDK** alignés avec les contrats d’API (OpenAPI/GraphQL schema).
  * Propager un **Correlation ID** dès le client (header `X-Correlation-ID`) 🔗.
  * Activer **retry** avec **exponential backoff** pour les lectures idempotentes.
* **Métriques**

  * **TTI/TTFB** côté front, taux d’échec (4xx/5xx), **Apdex**.

---

## 2) 🚪 API Gateway (Front Door)

* **Rôle** : AuthN/AuthZ, routage, rate-limiting, **load balancing**.
* **Bonnes pratiques**

  * **OAuth2/OIDC** (JWT) 🔐, **mTLS** côté est-ouest via service mesh.
  * **Rate limiting** (ex. 100 req/s par token), **WAF** & IP allow/deny.
  * **Circuit breaker** & **timeouts** (p95 < 300–500 ms).
* **Métriques**

  * Latence p50/p95/p99, QPS, 4xx/5xx, taux de **throttling**.

---

## 3) 🧩 Microservices Layer (Business)

* **Rôle** : Chaque service = **Single Responsibility** (User, Product, Order, Payment).
* **Bonnes pratiques**

  * **API versioning** (v1/v2), **Contract tests** (Pact), **Twelve-Factor**.
  * **Idempotency** (clé `Idempotency-Key`) pour POST sensibles (paiement).
  * **Sagas** pour transactions distribuées, **Outbox pattern** pour fiabilité event.
* **Métriques**

  * Taux de succès, latence par endpoint, **error budget** consommé.

---

## 4) 💾 Independent Databases

* **Rôle** : **Database-per-service** (évite le couplage).
* **Bonnes pratiques**

  * Schémas privés, **no foreign key cross-service**.
  * **Backups** + **PITR**, **read replicas**, chiffrement **at rest**.
  * Stratégies d’**éventuelle cohérence** via événements (CQRS/Materialized views).
* **Métriques**

  * Latence requêtes, locks/deadlocks, réplication en retard, taille/IOPS.

---

## 5) 🔄 Service-to-Service Communication

* **Synchrones** : REST/GraphQL (besoin temps-réel).
* **Asynchrones** : Kafka/RabbitMQ/NATS (événements, intégrations, emails).
* **Bonnes pratiques**

  * **Timeouts** stricts (ex. 200–800 ms selon route) + **retries** bornés.
  * **DLQ** (Dead Letter Queue) & **poison message handling**.
  * **Schema registry** (Avro/JSON Schema) ✅.
* **Métriques**

  * **Consumer lag**, débit (msg/s), taux d’échecs, retries, âge des messages.

---

## 6) ⚡ Caching Layer (Redis/Memcached)

* **Rôle** : Réduire la charge DB, accélérer les réponses.
* **Bonnes pratiques**

  * **TTL** appropriés, **cache-aside** pattern, invalidation ciblée.
  * Ne pas stocker de secrets en cache, éviter les **stampedes** (lock/penalty).
* **Métriques**

  * **Hit ratio**, latence, mémoire utilisée, taux d’évictions.

---

## 7) 🧭 Service Discovery

* **Rôle** : Résout dynamiquement les endpoints (scaling, rolling updates).
* **Bonnes pratiques**

  * **Health checks** (liveness/readiness), **self-registration**.
  * Haute disponibilité du registre (pas de **SPOF**).
* **Métriques**

  * Services **UP/DOWN**, latence heartbeat, erreurs de résolution.

---

## 8) 👀 Observability = Logs + Metrics + Traces

* **Logs** : ELK/EFK, **structured logging** (JSON) + correlation ID.
* **Metrics** : Prometheus + Grafana (RED/USE method).
* **Traces** : Jaeger/Zipkin (**OpenTelemetry** partout).
* **Bonnes pratiques**

  * **Sampling** intelligent (p.ex. 1% OK, 100% erreurs).
  * Dashboards **SLO** (latence, erreurs, disponibilité), **Alerting** par **SLI**.
* **Métriques (exemples SLO)**

  * **Availability** ≥ 99.9%, p95 latence API < 300 ms, **5xx** < 0.5%.

---

## 9) ☸️ Orchestration & Deployment (Docker + Kubernetes)

* **Rôle** : Scheduling, **auto-scaling**, self-healing, HA.
* **Bonnes pratiques**

  * **Probes** (readiness/liveness), **HPA** (CPU/RAM/QPS), **PodDisruptionBudget**.
  * **Blue-Green/Canary**, **resource requests/limits** propres.
* **Métriques**

  * Pods prêts, taux d’échec de déploiement, utilisation CPU/RAM, **MTTR**.

---

### 🧪 Bonus cruciaux (recommandés en prod)

* **CI/CD** (GitLab/Jenkins/ArgoCD), **Secrets Management** (Vault/K8s Secrets),
* **Service Mesh** (Istio/Linkerd) pour **mTLS**, **traffic shaping**,
* **Feature Flags** (Unleash/Flagsmith), **Chaos Engineering** (Litmus/Gremlin).

---

## 🔗 Comparatif rapide Sync vs Async

| Critère        | Synchrone (REST/GraphQL) ⚡          | Asynchrone (Kafka/RabbitMQ/NATS) 📬 |
| -------------- | ----------------------------------- | ----------------------------------- |
| Latence perçue | Faible, immédiate                   | Décorrélée, variable                |
| Couplage       | Plus fort (disponibilité requise)   | Faible (découplé)                   |
| Patterns       | **Circuit breaker**, retries courts | **Outbox**, **DLQ**, reprocess      |
| Idéal pour     | Lecture temps réel, commandes       | Événements métiers, intégrations    |
| Risques        | Cascade de timeouts                 | Messages dupliqués / ordre          |

---

## 🗂️ Datastores par besoin

| Besoin        | Type      | Exemples            | Pourquoi             |
| ------------- | --------- | ------------------- | -------------------- |
| Transactions  | SQL       | PostgreSQL/MySQL    | ACID, cohérence      |
| Catalogue/Doc | NoSQL     | MongoDB             | Flexibilité schéma   |
| Analytics     | Columnar  | ClickHouse/BigQuery | Requêtes analytiques |
| Cache         | In-Memory | Redis/Memcached     | Vitesse, TTL         |
| Streams       | Log       | Kafka               | Événements ordonnés  |

---

# 🧵 Exemple End-to-End “Place Order” (de A à Z)

### 0) Pré-requis (contrats & sécurité)

* **OpenAPI** pour Order API, **Avro** pour `order.created` & `payment.authorized`.
* **Scopes OAuth** : `orders:create`, `payments:charge`.
* **mTLS** entre services via **service mesh**.

### 1) Le client envoie `POST /orders`

* En-têtes : `Authorization: Bearer <JWT>`, `X-Correlation-ID`, `Idempotency-Key`.
* **Gateway** : AuthN/AuthZ ✅, **rate limit** OK, routage → `order-service`.

### 2) Order Service (synchrone + cache)

* Vérifie le **cache Redis** (stock niveau/price snapshot).
* Réserve les items (DB locale Postgres), **statut=“PENDING\_PAYMENT”**.
* Écrit en **Outbox** l’événement `order.created` (transaction locale) 🧾.
* **Publisher** lit Outbox → publie sur **Kafka** (`topic: order.created`).

### 3) Payment Service (asynchrone)

* Consomme `order.created`, crée un **payment intent**, débite via PSP.
* Gère **idempotence** (clé = `Idempotency-Key`).
* Publie `payment.authorized` (ou `payment.failed`) sur Kafka.

### 4) Order Service (réaction au paiement)

* Consomme `payment.authorized` → statut `CONFIRMED`, déclenche **saga step** :

  * Envoie `inventory.reserve` (ou annule si `payment.failed`).
* En cas d’échec de réserve : publie `order.cancelled`, **refund** via événement compensatoire.

### 5) Notification / Email

* **Notification service** consomme `order.confirmed` → envoie email/SMS (asynchrone).
* **Eventual consistency** : l’email peut arriver après la réponse API.

### 6) Réponse au client (synchrone)

* Dès la création initiale, l’API renvoie `202 Accepted` + `orderId`.
* Le client **poll** `GET /orders/{id}` ou s’abonne **WebSocket/SSE** pour l’état en temps réel.

### 7) Observability & Traçage

* Chaque hop propage `X-Correlation-ID`.
* **Metrics RED** par service (Rate, Errors, Duration), **traces** (Jaeger).
* **Logs** structurés (JSON) dans EFK, requêtables par `correlation_id`.

---

## 🧩 Extraits “prêts à l’emploi”

### 🔐 Idempotency (pseudo-code)

```pseudo
if exists store.get(idempotencyKey):
  return store.get(idempotencyKey).response
resp = process_business()
store.put(idempotencyKey, resp, ttl=24h)
return resp
```

### 📦 K8s HPA (autoscaling sur CPU)

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: order-svc-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: order-svc
  minReplicas: 3
  maxReplicas: 15
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 60
```

### ❤️ Probes (readiness/liveness)

```yaml
livenessProbe:
  httpGet: { path: /health/live, port: 8080 }
  periodSeconds: 10
readinessProbe:
  httpGet: { path: /health/ready, port: 8080 }
  initialDelaySeconds: 5
```

### 📈 Règle d’alerte (Prometheus)

```yaml
- alert: HighErrorRate
  expr: sum(rate(http_server_errors_total[5m])) / sum(rate(http_requests_total[5m])) > 0.02
  for: 10m
  labels: { severity: "page" }
  annotations:
    summary: "Taux d'erreurs > 2% (5m)"
```

### 🧾 Log structuré (ex.)

```json
{
  "timestamp":"2025-08-25T09:00:00Z",
  "service":"order-svc",
  "level":"INFO",
  "correlation_id":"c-9f12...",
  "event":"order.created",
  "order_id":"o-123",
  "user_id":"u-789"
}
```

---

## 📊 Métriques & SLO recommandés (exemples)

| Domaine       | SLI                    | SLO conseillé                       |
| ------------- | ---------------------- | ----------------------------------- |
| Gateway       | p95 latence            | < 300 ms                            |
| Services      | Taux 5xx               | < 0.5%                              |
| Disponibilité | Uptime                 | ≥ 99.9%                             |
| Messaging     | Consumer lag max       | < 2 s (critiques)                   |
| DB            | p95 requêtes           | < 20 ms (cache), < 100 ms (lecture) |
| Cache         | Hit ratio              | > 85%                               |
| Sécurité      | JWT échecs injustifiés | < 0.1%                              |

---

## 🧯 Anti-patterns à éviter

* **DB partagée** entre services ❌
* **Appels synchrones en chaîne** sans timeout/circuit breaker (effet domino) ❌
* **Événements sans schéma/version** ❌
* **Logs non corrélés** (pas de `correlation_id`) ❌
* **Manque d’idempotence** sur les opérations financières ❌

---

## ✅ Checklist de mise en prod (express)

* [ ] OpenAPI/GraphQL **versionné** + **contract tests**
* [ ] **Idempotency-Key** pour POST critiques
* [ ] **Sagas + Outbox** pour fiabilité event
* [ ] **Probes** + **HPA** + **PDB** sur K8s
* [ ] **mTLS + OAuth2/OIDC** + **secrets** gérés (Vault)
* [ ] **Dashboards SLO** + **alertes** RED/USE
* [ ] **Chaos test** (petit scope) + **runbook** incident

---

