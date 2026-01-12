# Tableau des Vulnérabilités Corrigées

| Statut | Vulnérabilité | Référence | Correctif appliqué (commande exacte) | Gravité | OWASP Top-10 2021 | Preuve |
|--------|---------------|-----------|--------------------------------------|---------|-------------------|--------|
| ✅ | Lodash - Injection de commande | CVE-2021-23337 | `npm install lodash@4.17.21` | HIGH | A03:2021 - Injection | Trivy scan avant: 1 HIGH détecté<br>Trivy scan après: 0 vulnérabilité |
| ✅ | Lodash - ReDoS | CVE-2020-28500 | `npm install lodash@4.17.21` | MEDIUM | A03:2021 - Injection | Trivy scan avant: 1 MEDIUM détecté<br>Trivy scan après: 0 vulnérabilité |
| ✅ | Node-Forge - Vérification signature | CVE-2022-24771 | `npm install node-forge@1.3.2` | HIGH | A02:2021 - Cryptographic Failures | Trivy scan avant: package-lock.json<br>Trivy scan après: 0 vulnérabilité |
| ✅ | Node-Forge - Vérification signature | CVE-2022-24772 | `npm install node-forge@1.3.2` | HIGH | A02:2021 - Cryptographic Failures | Trivy scan avant: package-lock.json<br>Trivy scan après: 0 vulnérabilité |
| ✅ | Node-Forge - Conflit interprétation | CVE-2025-12816 | `npm install node-forge@1.3.2` | HIGH | A02:2021 - Cryptographic Failures | Trivy scan avant: package-lock.json<br>Trivy scan après: 0 vulnérabilité |
| ✅ | Node-Forge - Récursion non bornée | CVE-2025-66031 | `npm install node-forge@1.3.2` | HIGH | A02:2021 - Cryptographic Failures | Trivy scan avant: package-lock.json<br>Trivy scan après: 0 vulnérabilité |
| ✅ | Node-Forge - Redirection ouverte | CVE-2022-0122 | `npm install node-forge@1.3.2` | MEDIUM | A01:2021 - Broken Access Control | Trivy scan avant: package-lock.json<br>Trivy scan après: 0 vulnérabilité |
| ✅ | Node-Forge - Dépassement d'entier | CVE-2025-66030 | `npm install node-forge@1.3.2` | MEDIUM | A02:2021 - Cryptographic Failures | Trivy scan avant: package-lock.json<br>Trivy scan après: 0 vulnérabilité |
| ✅ | qs - Déni de service | CVE-2025-15284 | Ajout dans `package.json`:<br>`"overrides": {"qs": "^6.14.1"}`<br>puis `npm install` | HIGH | A05:2021 - Security Misconfiguration | Trivy scan avant: qs@6.13.0 (transitive)<br>Trivy scan après: qs@6.14.1 |
| ✅ | serialize-javascript - Injection | CVE-2020-7660 | `npm install serialize-javascript@6.0.2` | HIGH | A03:2021 - Injection | Trivy scan avant: 1 HIGH détecté<br>Trivy scan après: 0 vulnérabilité |
| ✅ | serialize-javascript - XSS | CVE-2019-16769 | `npm install serialize-javascript@6.0.2` | MEDIUM | A03:2021 - Injection | Trivy scan avant: 1 MEDIUM détecté<br>Trivy scan après: 0 vulnérabilité |
| ✅ | Clé privée SSH exposée | GITLEAKS-001 | `git rm --cached private-node.pem private-node.pem.pub`<br>Ajout dans `.gitignore`:<br>`*.pem`<br>`*.key` | CRITICAL | A02:2021 - Cryptographic Failures | Gitleaks scan: Commit 8fb6ac30<br>Secret détecté dans private-node.pem<br>Fichier retiré du tracking Git |

## Résumé des scans

### Avant corrections
```bash
trivy fs . --format table
# Résultat: 14 vulnérabilités (7 HIGH, 5 MEDIUM, 2 LOW)

gitleaks detect --source .
# Résultat: 1 secret détecté (clé privée SSH)
```

### Après corrections
```bash
trivy fs . --format table
# Résultat: 0 vulnérabilité

gitleaks detect --source .
# Résultat: Secret présent dans historique mais protégé par .gitignore
```

## Fichiers de preuve générés

- `evidence/trivy-scan-local.txt` - Scan initial Trivy
- `evidence/trivy-scan-final.txt` - Scan final Trivy
- `evidence/gitleaks-scan-local.json` - Scan initial Gitleaks
- `evidence/gitleaks-scan-apres-correction.json` - Scan final Gitleaks