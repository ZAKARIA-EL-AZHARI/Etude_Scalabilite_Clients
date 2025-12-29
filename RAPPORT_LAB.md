# Rapport de Lab : Clients Synchrones

## Partie G — Récapitulatif des résultats

### Tableau 1 — Performance (latence et débit)

**Configuration Eureka**

| Méthode | Temps Moyen (ms) | Débit (req/s) | P95 (ms) |
| :--- | :--- | :--- | :--- |
| **RestTemplate**  |95 |310 | 150|
| **Feign**  |85 | 350|135 |
| **WebClient**  |60 | 420|100 |

**Configuration Consul**

| Méthode | Temps Moyen (ms) | Débit (req/s) | P95 (ms) |
| :--- | :--- | :--- | :--- |
| **RestTemplate** |90 |330 |140 |
| **Feign** |80 |360 |125 |
| **WebClient** |55 |450 | 90|

### Tableau 2 — CPU / Mémoire

| Méthode | Eureka CPU% | Eureka RAM (MB) | Consul CPU% | Consul RAM (MB) |
| :--- | :--- | :--- | :--- | :--- |
| **RestTemplate** |45% |320 |42% |310 |
| **Feign** |40% |300|38% |295 |
| **WebClient** |35% |280 |33% |270 |

### Tableau 3 — Résilience (Scénarios de panne)

| Scénario | Observation (Comportement) | Temps de reprise | Taux d'échec (%) |
| :--- | :--- | :--- | :--- |
| **Panne Service-Client** |retries → fallback correct |4s | 25%|
| **Panne Service-Voiture** |erreurs 503 jusqu'au retour |6s | 40%|
| **Panne Discovery** |résolution DNS cache → latence haute |12s |60% |

### Tableau 4 — Simplicité et Maintenabilité

| Méthode | Configuration Initiale (Facile/Moyen/Difficile) | Lignes de Code (approx) | Complexité |
| :--- | :--- | :--- | :--- |
| **RestTemplate** |Facile | 90| Moyenne|
| **Feign** |Facile |50 | Faible|
| **WebClient** |Moyenne | 110|Elevée |

---

## Partie H — Analyse et Discussion

### 1. Performance en charge
*Quelle méthode donne la meilleure latence ?*
> WebClient offre la meilleure latence

*Le débit maximal observé ?*
> 450 req/s avec Consul

### 2. Maintenabilité
*Quelle méthode est la plus simple à maintenir ?*
> Feign est le plus simple à coder

### 3. Impact du Discovery
*Comparaison Eureka vs Consul sur la latence/stabilité :*
> Consul améliore légèrement la latence

### 4. Résilience
*Comportement observé lors des pannes :*
> Sans service de discovery, les clients perdent la localisation des services

### Conclusion Générale
> WebClient + Consul = meilleur combo Performance
 Feign = meilleur choix maintenabilité / rapidité de dev
