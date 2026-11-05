# Cours Kubernetes — ENSAI 3A

Thomas Bossard — promo 2026

## TP 1 · Conteneurisation

Compte rendu : [`tp1/TP1_compte_rendu_BOSSARD.odt`](tp1/TP1_compte_rendu_BOSSARD.odt)

### Exercice 1 — API Python

[`tp1/python-api/`](tp1/python-api) — FastAPI, build simple avec optimisation du cache
de layers (dépendances installées avant la copie du code) et exécution en utilisateur
non root.

```bash
cd tp1/python-api
docker build -t python-api:1.0 .
docker run -d -p 8000:8000 python-api:1.0
curl localhost:8000/hello
```

Image publiée : `thomasbossard/python-api:1.0`

### Exercice 2 — API Java

[`tp1/java-api/`](tp1/java-api) — Spring Boot 3.2 / Java 21, multi-stage build
(JDK + Maven pour le build, JRE Alpine pour le run).

```bash
cd tp1/java-api
docker build -t java-api:multi .
docker run -d -p 8080:8080 java-api:multi
curl localhost:8080/hello
```

Image publiée : `thomasbossard/java-api:1.0`

`Dockerfile.mono` est la version mono-stage, conservée uniquement pour la comparaison
de tailles demandée par l'énoncé :

| Image | Disk usage | Content size |
|---|---|---|
| `java-api:mono` | 932 Mo | 302 Mo |
| `java-api:multi` | 326 Mo | 91,9 Mo |
