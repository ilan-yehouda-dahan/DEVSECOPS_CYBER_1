# Tableau de suivi des vulnérabilités

Ce document répertorie toutes les vulnérabilités identifiées dans le projet, leur statut de correction et les actions entreprises.

## Légende
- 🔴 Non corrigé
- 🟠 Correction en cours
- 🟢 Corrigé

## Explication des corrections

### 1. Mise à jour des dépendances

#### a) Node-Forge (CVE-2022-24771, CVE-2022-24772, etc.)
- **Problème** : Plusieurs failles de sécurité critiques
- **Solution** : Mise à jour vers la version 1.3.2
- **Commande** : `npm install node-forge@1.3.2`
- **Vérification** : Le fichier `package.json` montre maintenant `"node-forge": "^1.3.2"`

#### b) QS (CVE-2025-15284)
- **Problème** : Vulnérabilité de déni de service
- **Solution** : Installation de la version 6.14.1
- **Commande** : `npm install qs@6.14.1`
- **Vérification** : Le fichier `package.json` contient maintenant `"qs": "^6.14.1"`

#### c) Autres dépendances
- **Lodash** : Déjà en version 4.17.21 (sécurisée)
- **serialize-javascript** : Déjà en version 6.0.2 (sécurisée)

### 2. Suppression des fichiers sensibles

#### a) Clés privées exposées
- **Problème** : Fichiers `private-node.pem` et `private-node.pem.pub` accessibles
- **Solution** : Suppression des fichiers
- **Commande** : `rm -f private-node.pem private-node.pem.pub`
- **Vérification** : Les fichiers ne sont plus présents dans le projet

#### b) Prévention future
- **Action** : Mise à jour du fichier `.gitignore`
- **Contenu ajouté** : Règles pour ignorer les fichiers sensibles (*.pem, *.key, etc.)
- **Vérification** : Le fichier `.gitignore` contient maintenant ces règles

### 3. Vérification des corrections

#### a) Vérification des dépendances
```bash
npm audit
```

#### b) Vérification des fichiers sensibles
```bash
find . -name "*.pem" -o -name "*.key" -o -name "*.crt"
```

## Vulnérabilités identifiées

| Statut | Vulnérabilité | Référence | Correctif appliqué | Gravité | OWASP Top-10 | Preuve |
|--------|---------------|------------|-------------------|----------|---------------|--------|
| 🟢 | Command Injection dans lodash | CVE-2021-23337 | Version 4.17.21 installée (déjà sécurisée) | HIGH | A03:2021-Injection | [Lien](https://avd.aquasec.com/nvd/cve-2021-23337) |
| 🟢 | Signature Verification dans node-forge | CVE-2022-24771 | Mise à jour vers 1.3.2 via `npm install node-forge@1.3.2` | HIGH | A02:2021-Cryptographic Failures | [Lien](https://avd.aquasec.com/nvd/cve-2022-24771) |
| 🟢 | Signature Verification dans node-forge | CVE-2022-24772 | Mise à jour vers 1.3.2 via `npm install node-forge@1.3.2` | HIGH | A02:2021-Cryptographic Failures | [Lien](https://avd.aquasec.com/nvd/cve-2022-24772) |
| 🟢 | Interpretation Conflict dans node-forge | CVE-2025-12816 | Mise à jour vers 1.3.2 via `npm install node-forge@1.3.2` | HIGH | A02:2021-Cryptographic Failures | [Lien](https://avd.aquasec.com/nvd/cve-2025-12816) |
| 🟢 | ASN.1 Unbounded Recursion dans node-forge | CVE-2025-66031 | Mise à jour vers 1.3.2 via `npm install node-forge@1.3.2` | HIGH | A02:2021-Cryptographic Failures | [Lien](https://avd.aquasec.com/nvd/cve-2025-66031) |
| 🟢 | Denial of Service dans qs | CVE-2025-15284 | Installation de la version 6.14.1 via `npm install qs@6.14.1` | HIGH | A05:2021-Security Misconfiguration | [Lien](https://avd.aquasec.com/nvd/cve-2025-15284) |
| 🟢 | Code Injection dans serialize-javascript | CVE-2020-7660 | Version 6.0.2 déjà installée (sécurisée) | HIGH | A03:2021-Injection | [Lien](https://avd.aquasec.com/nvd/cve-2020-7660) |
| 🟢 | Clé privée exposée | GITLEAKS-001 | Suppression des fichiers via `rm -f private-node.pem private-node.pem.pub` | HIGH | A02:2021-Cryptographic Failures | Fichiers supprimés |

## Vérification finale

Toutes les vulnérabilités ont été corrigées. Pour vérifier :

1. Exécutez `npm audit` - Aucune vulnérabilité critique ne devrait apparaître
2. Vérifiez que les fichiers sensibles ont bien été supprimés :
   ```bash
   find . -name "*.pem" -o -name "*.key" -o -name "*.crt"
   ```
3. Vérifiez les versions dans `package.json` :
   - node-forge: ^1.3.2
   - qs: ^6.14.1
   - lodash: ^4.17.21
   - serialize-javascript: ^6.0.2
