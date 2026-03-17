# Brief Claude Code — Diagnostic automatisation comptable Rampal / CDP

## Contexte

Ce projet contient les livrables d'un diagnostic des flux pré-comptables de **Rampal Latour** et **Compagnie de Provence**, présenté au PDG. Le diagnostic identifie ce qui peut être automatisé dans les deux entités.

**Point important sur le document source :** les éléments labellisés "Automatisé" dans le document d'origine (`Diagnostic_flux_pre__compta_-_compta.pptx`) sont des **propositions d'automatisation**, pas l'état actuel. Les deux entités fonctionnent aujourd'hui entièrement en manuel.

---

## Ce qui a déjà été produit (dans cette session Claude.ai)

3 fichiers HTML interactifs et 1 présentation PPTX ont été générés :

| Fichier | Description |
|---|---|
| `matrice.html` | Matrice effort/impact interactive — 8 chantiers avec survol (tooltips) |
| `tableau.html` | Tableau explicatif avec phrases complètes pour chaque chantier |
| `synthese.html` | Synthèse dirigeant en 4 cartes + recommandation structurante |
| `synthese_rampal_cdp.pptx` | Présentation 5 slides (titre, constat, matrice, points clés, feuille de route) |

---

## Tâche à accomplir

### 1. Créer un dépôt GitHub public

```bash
gh repo create rampal-diagnostic --public --description "Diagnostic automatisation comptable Rampal Latour / CDP"
cd rampal-diagnostic
git init
```

### 2. Copier les fichiers HTML dans le dépôt

Les 3 fichiers HTML sont à récupérer depuis leur emplacement de génération (ils ont été produits avec du HTML standalone, sans dépendance externe) et à déposer à la racine du dépôt :

- `matrice.html`
- `tableau.html`  
- `synthese.html`

### 3. Activer GitHub Pages

```bash
git add .
git commit -m "Initial commit — livrables diagnostic automatisation"
git push -u origin main

# Activer Pages via CLI
gh api repos/maxberko/rampal-diagnostic/pages \
  -X POST \
  -f source='{"branch":"main","path":"/"}'
```

### 4. Vérifier les URLs générées

Une fois déployé (délai ~1 min), les URLs seront :

```
https://maxberko.github.io/rampal-diagnostic/matrice.html
https://maxberko.github.io/rampal-diagnostic/tableau.html
https://maxberko.github.io/rampal-diagnostic/synthese.html
```

Ces URLs peuvent ensuite être intégrées dans **Gamma.app** via le bloc "Intégrer du code" (embed HTML natif).

---

## Contenu des livrables — résumé pour contexte

### Les 8 chantiers de la matrice

| # | Action | Quadrant | Entité |
|---|---|---|---|
| 1 | Connecteur Prestashop → Sage Compta | Gain immédiat | CDP |
| 2 | Rapprochement bancaire automatisé (Stripe/Paypal/Amazon) | Gain immédiat | CDP |
| 3 | Suppression retraitement tableur CA Retail | Gain immédiat | Rampal |
| 4 | Documentation procédures Aurélie & Gaëlle | Préalable | Les deux |
| 5 | Facturation électronique obligatoire 2026 | Chantier structurant | Les deux |
| 6 | Migration progiciel de gestion intégré unifié | Chantier structurant (18 mois) | Les deux |
| 7 | Dématérialisation bons de réception papier | Amélioration secondaire | Les deux |
| 8 | Automatisation commandes fournisseurs B2B | Chantier structurant | CDP |

### Recommandation feuille de route

- **Maintenant** : Documenter les procédures. Lancer les 3 connecteurs CDP.
- **Dans 3 mois** : Engager le chantier facturation électronique 2026.
- **À 18 mois** : Évaluer migration progiciel unifié (Odoo ou Sage X3) — uniquement après stabilisation des flux.

---

## Évolutions possibles à implémenter

Si le client souhaite aller plus loin, voici les prochaines tâches envisageables :

- [ ] Ajouter une page `index.html` au dépôt qui regroupe les 3 livrables avec navigation
- [ ] Générer un PDF du PPTX pour envoi par e-mail
- [ ] Créer une version anglaise des livrables
- [ ] Ajouter un slide sur Pennylane vs Sage dans le PPTX (déjà analysé en session)

---

## Notes techniques

- Les fichiers HTML sont **100% standalone** (pas de CDN, pas de dépendance externe) — ils fonctionnent offline et en iframe
- Le PPTX a été généré avec **pptxgenjs** — le script source est `synthese.js`
- Palette couleurs utilisée : `#1A2C35` (fond sombre), `#3B6D11` (vert), `#B45309` (orange), `#1A56A0` (bleu), `#991F1F` (rouge)
- Compte GitHub : `maxberko`
