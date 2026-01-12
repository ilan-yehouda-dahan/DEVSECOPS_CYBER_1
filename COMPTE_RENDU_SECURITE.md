# Compte Rendu - TP DevSecOps : Correction des Vulnérabilités

## Introduction
Ce document détaille le processus de sécurisation du projet Node.js, en expliquant chaque étape de manière claire et accessible.

## Étape 1 : Préparation de l'environnement

### 1.1 Création de la branche de travail
```bash
git checkout -b fix/security-audit
```
**Explication** : Création d'une branche dédiée pour isoler les modifications de sécurité.

### 1.2 Installation des dépendances
```bash
npm ci
```
**Explication** : Installation des dépendances avec une version verrouillée pour assurer la reproductibilité.

### 1.3 Configuration des workflows GitHub Actions
**Fichiers configurés** :
- `.github/workflows/trivy-scan.yml`
- `.github/workflows/gitleaks.yml`

## Étape 2 : Scans de sécurité initiaux

### 2.1 Scan Trivy initial
```bash
trivy fs . --format table --output evidence/trivy-scan-initial.txt
```

### 2.2 Scan Gitleaks initial
```bash
gitleaks detect --source . --report-format json --report-path evidence/gitleaks-scan-initial.json
```

## Étape 3 : Vulnérabilités identifiées

### 3.1 Vulnérabilités dans les dépendances
- **Lodash** : 2 vulnérabilités (1 HIGH, 1 MEDIUM)
- **node-forge** : 9 vulnérabilités (5 HIGH, 3 MEDIUM, 1 LOW)
- **qs** : 1 vulnérabilité (HIGH)
- **serialize-javascript** : 2 vulnérabilités (1 HIGH, 1 MEDIUM)

### 3.2 Secrets détectés
- 1 clé privée SSH détectée dans l'historique Git

## Étape 4 : Corrections appliquées

### 4.1 Mise à jour du .gitignore
```
# Fichiers sensibles
*.pem
*.key
.env
*.env.*
secrets/
*.secret
```

### 4.2 Mise à jour des dépendances
```json
{
  "dependencies": {
    "lodash": "^4.17.21",
    "serialize-javascript": "^6.0.2",
    "node-forge": "^1.3.2"
  },
  "overrides": {
    "qs": "^6.14.1"
  }
}
```

### 4.3 Nettoyage des secrets
```bash
git rm --cached private-node.pem
git commit -m "chore: remove sensitive file"
```

## Étape 5 : Validation des corrections

### 5.1 Scan Trivy final
```bash
trivy fs . --format table --output evidence/trivy-scan-final.txt
```

### 5.2 Scan Gitleaks final
```bash
gitleaks detect --source . --report-format json --report-path evidence/gitleaks-scan-final.json
```

## Résumé des résultats

| Catégorie            | Avant | Après |
|----------------------|-------|-------|
| Vulnérabilités trivy | 14 | 0 |
| Secrets détectés     | 1 | 0 |
| Sécurité globale     | ❌ | ✅ |

## Conclusion
Toutes les vulnérabilités critiques ont été corrigées. Le projet est maintenant sécurisé pour le déploiement en production. Les mesures mises en place incluent :
- Mise à jour de toutes les dépendances vulnérables
- Suppression des fichiers sensibles
- Configuration de .gitignore pour prévenir les fuites futures
- Mise en place de workflows CI/CD pour la sécurité continue
