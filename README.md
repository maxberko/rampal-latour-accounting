# Diagnostic automatisation comptable — Rampal Latour · Compagnie de Provence

## Contexte

Deux entités d'un même groupe (savons et cosmétiques, Provence). La DAF a réalisé un diagnostic des flux pré-comptables et comptables. Ce document analyse ce diagnostic et identifie les suites possibles.

| | Rampal Latour | Compagnie de Provence |
|---|---|---|
| **Activité** | Fabrication industrielle + retail | E-commerce + B2B |
| **Logiciels** | LSI → Quadra, EBICS | Sage 100 + Sage Compta, Prestashop |
| **Personne clé** | Aurélie | Gaëlle |
| **Automatisation** | Partielle (flux LSI → Quadra) | Quasi aucune |

---

## Ce qu'on sait

- Les deux entités fonctionnent majoritairement en saisie manuelle.
- Rampal et CDP tournent sur deux stacks incompatibles — pas de vision consolidée possible.
- La facturation électronique obligatoire (2026) n'est pas abordée dans le diagnostic.
- Pennylane peut convenir pour CDP (flux simples), pas pour Rampal (flux industriels). Mais c'est secondaire : le problème est organisationnel, pas logiciel.

---

## Ce qu'on ne sait pas

À vérifier avant de décider quoi que ce soit :

| # | Question | À vérifier avec |
|---|---|---|
| 1 | Aurélie et Gaëlle sont-elles les seules à maîtriser les flux ? | PDG / DRH |
| 2 | Le cabinet comptable intervient-il dans les flux quotidiens ? | Cabinet / PDG |
| 3 | Un connecteur Prestashop → Sage compatible existe-t-il pour les versions CDP ? | Intégrateur Sage |
| 4 | Les API Stripe / Paypal / Amazon sont-elles accessibles pour CDP ? | CDP / prestataire |
| 5 | Un flux direct Odoo → LSI est-il faisable ? | Intégrateur LSI |
| 6 | Les logiciels sont-ils à jour ? | DSI / prestataire |
| 7 | LSI et Quadra sont-ils intégrés nativement ou non ? | Aurélie / prestataire |
| 8 | Le volume B2B de CDP justifie-t-il une automatisation ? | CDP |
| 9 | Une démarche facturation électronique a-t-elle été engagée ? | PDG / cabinet |
| 10 | Le cabinet comptable utilise-t-il déjà Pennylane ? | Cabinet |

Tant que ces questions n'ont pas de réponse, tout chiffrage ou planning est de la fiction.

---

## Ce qu'il faut faire, dans l'ordre

**1. Répondre aux questions ci-dessus.** Ça prend quelques coups de fil, pas un projet.

**2. Facturation électronique 2026.** Obligation légale, calendrier qui a déjà glissé. En parler avec l'expert-comptable maintenant — c'est lui qui sait quelle PDP choisir.

**3. Connecteur Prestashop → Sage (CDP).** Si les versions sont compatibles, c'est le gain le plus simple. Si elles ne le sont pas, c'est un projet à cadrer avec un intégrateur.

**4. Rapprochement bancaire (CDP).** Quatre canaux (CB, Stripe, Paypal, Amazon), chacun avec sa propre logique. Commencer par un seul canal, voir ce que ça donne. Le 100% automatique n'existe pas.

**5. Flux Odoo → LSI (Rampal).** Comprendre d'abord ce que le tableur d'Aurélie fait exactement avant de le supprimer.

**6. ERP unifié.** Pas avant d'avoir fait le reste. Projet lourd, coûteux, qui dérape souvent.

---

## Pennylane

- **CDP** : possible, sur les flux simples (e-commerce, fournisseurs).
- **Rampal** : non, les flux industriels dépassent le produit.
- **Condition** : le cabinet comptable doit être d'accord pour basculer.
- **Conclusion** : pas la priorité. Résoudre les problèmes de processus d'abord.

---

## Livrables

| Fichier | Description |
|---|---|
| `synthese.html` | [Synthèse dirigeant](https://maxberko.github.io/rampal-latour-accounting/synthese.html) |
| `matrice.html` | [Matrice effort / impact](https://maxberko.github.io/rampal-latour-accounting/matrice.html) |
| `tableau.html` | [Tableau détaillé](https://maxberko.github.io/rampal-latour-accounting/tableau.html) |
| `synthese_rampal_cdp.pptx` | Présentation PowerPoint 9 slides |
