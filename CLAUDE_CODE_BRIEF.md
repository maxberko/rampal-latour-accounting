# Diagnostic automatisation comptable — Rampal Latour · Compagnie de Provence

## Contexte

**Rampal Latour** et la **Compagnie de Provence (CDP)** sont deux entités d'un même groupe, spécialisées dans la fabrication et la distribution de savons et cosmétiques en Provence. Le PDG a commandé un diagnostic des flux pré-comptables et comptables des deux entités pour identifier ce qui peut être automatisé, rationalisé ou supprimé.

Le document source (`Diagnostic_flux_pre__compta_-_compta.pptx`) cartographie l'ensemble des flux comptables des deux entités. **Point critique d'interprétation** : les éléments labellisés "Automatisé" dans ce document sont des *propositions* d'automatisation, pas l'état actuel. Les deux entités fonctionnent aujourd'hui majoritairement en saisie manuelle.

### Les deux entités

| | Rampal Latour | Compagnie de Provence |
|---|---|---|
| **Activité** | Fabrication industrielle + retail | E-commerce + B2B |
| **Stack comptable** | LSI (gestion) → Quadra (compta), protocole EBICS | Sage 100 (gestion) + Sage Compta, Prestashop (e-commerce) |
| **Personne clé** | Aurélie | Gaëlle |
| **Niveau d'automatisation** | Partiellement automatisé (flux LSI → Quadra) | Quasi entièrement manuel |

---

## Executive summary

Le groupe souffre de trois problèmes structurels :

1. **Dépendance humaine critique.** L'intégralité des flux comptables repose sur deux personnes (Aurélie et Gaëlle), sans suppléant ni procédure documentée. Un départ ou une absence prolongée compromettrait la continuité d'activité.

2. **Dette tableur.** Les prévisions matières premières, le suivi des impayés et les retraitements du chiffre d'affaires transitent par des fichiers tableur non audités, non versionnés. Ce sont des points de fragilité invisibles.

3. **Deux architectures logicielles incompatibles.** LSI/Quadra d'un côté, Sage 100/Sage Compta de l'autre — aucune vision consolidée du groupe n'est possible en l'état.

À cela s'ajoute un **angle mort réglementaire** : la facturation électronique obligatoire (2026 en France) n'est pas dans le radar du diagnostic, alors qu'elle impose des choix techniques structurants immédiats.

---

## Analyse détaillée — Les 8 chantiers identifiés

### Gains immédiats (effort faible, impact élevé)

**1. Connecteur Prestashop → Sage Compta (CDP)**
Gaëlle ressaisit manuellement dans Sage Compta chaque vente issue de Prestashop. Un connecteur natif ou un pont applicatif supprimerait cette double saisie quotidienne sans remise en cause de l'architecture existante.

**2. Rapprochement bancaire automatisé (CDP)**
Les encaissements CDP transitent par quatre canaux (carte bancaire, Paypal, Amazon, Stripe), tous réconciliés à la main. Ces plateformes disposent d'API documentées. Gain estimé : 3 à 4 h/semaine.

**3. Suppression du retraitement tableur CA Retail (Rampal)**
Aurélie passe par un fichier tableur intermédiaire pour intégrer le CA des boutiques depuis Odoo vers LSI. Un flux direct Odoo → LSI est techniquement accessible et supprimerait ce point de fragilité.

### Préalable indispensable

**4. Documentation des procédures d'Aurélie et de Gaëlle**
Aucune procédure écrite n'existe. Documenter les flux est un prérequis à toute automatisation et un investissement de faible coût face à un risque opérationnel élevé.

### Chantiers structurants (effort moyen à élevé, impact élevé)

**5. Facturation électronique obligatoire 2026**
Mise en conformité légale non négociable. Impose le choix d'une plateforme de dématérialisation partenaire (PDP) agréée par l'État. Ce sujet doit être engagé immédiatement.

**6. Migration vers un progiciel de gestion intégré unifié**
Cible logique à 18 mois (Odoo complet ou Sage X3). Ne doit être engagée qu'après stabilisation des flux actuels et documentation des procédures.

**8. Automatisation des commandes fournisseurs B2B (CDP)**
Les commandes B2B sont saisies manuellement à réception (messagerie, téléphone). Un portail en ligne ou un EDI réduirait ce travail. L'opportunité dépend du volume B2B.

### Amélioration secondaire

**7. Dématérialisation des bons de réception papier**
Les réceptions logistiques sont confirmées sur papier. Un bon de réception numérique améliorerait la fluidité, sans être prioritaire.

---

## Question ouverte — Pennylane

L'hypothèse d'une migration vers Pennylane a été analysée :

- **Pour CDP** : pertinent comme remplacement de Sage Compta sur les flux simples (ventes, e-commerce, fournisseurs transport). L'outil intègre nativement la TVA française, la liasse fiscale et une interface partagée client/expert-comptable.
- **Pour Rampal** : inadapté. Les flux industriels (sous-traitance, matières premières, rapprochement BL/facture, logistique intégrée) dépassent les capacités du produit.
- **Contrainte externe** : le cabinet comptable doit être partant pour adopter Pennylane comme outil de travail, ce qui n'est pas acquis.

**Verdict** : Pennylane n'est ni rejeté ni prioritaire. Le problème du groupe n'est pas un problème de logiciel — c'est un problème de processus non documentés, de dépendance humaine et de dette tableur. Changer d'outil sans avoir résolu ça revient à migrer le chaos.

---

## Feuille de route recommandée

| Horizon | Actions |
|---|---|
| **Maintenant** | Documenter les procédures Aurélie & Gaëlle. Lancer les 3 automatisations CDP (connecteur Prestashop, rapprochements bancaires, flux Odoo → LSI). |
| **Dans 3 mois** | Engager le chantier facturation électronique 2026 (sélection PDP). |
| **À 18 mois** | Évaluer la migration vers un progiciel unifié (Odoo complet ou Sage X3) — uniquement après stabilisation des flux et résolution de la dette tableur. |

---

## Hypothèses et points à vérifier

Ce diagnostic repose sur 17 hypothèses documentées dans `HYPOTHESES.md`. Les principales :

- **H1 ✅** Les éléments "Automatisé" du diagnostic source sont des propositions, pas l'état actuel (confirmé par le client).
- **H4 ❓** Aurélie et Gaëlle sont les seules personnes maîtrisant les flux de leur entité (à confirmer avec PDG/DRH).
- **H5 ❓** Il n'existe aucune procédure écrite (à confirmer avec Aurélie/Gaëlle).
- **H7 ❓** Un connecteur Prestashop → Sage Compta existe et est compatible avec les versions CDP (à confirmer avec intégrateur).
- **H12 ⚠️** Le gain estimé de 1,5 ETP/semaine est un ordre de grandeur non étayé — aucune mesure du temps par tâche n'a été réalisée.
- **H14 ⚠️** Le calendrier facturation électronique 2026 est basé sur la réglementation en vigueur à mars 2025 (à actualiser).

---

## Livrables produits

| Fichier | Description | URL GitHub Pages |
|---|---|---|
| `synthese.html` | Synthèse dirigeant en 4 cartes + section Pennylane | `https://maxberko.github.io/rampal-latour-accounting/synthese.html` |
| `matrice.html` | Matrice effort/impact interactive (8 chantiers, tooltips au survol) | `https://maxberko.github.io/rampal-latour-accounting/matrice.html` |
| `tableau.html` | Tableau explicatif détaillé de chaque chantier | `https://maxberko.github.io/rampal-latour-accounting/tableau.html` |
| `synthese_rampal_cdp.pptx` | Présentation PowerPoint 5 slides | — |
| `HYPOTHESES.md` | Liste des 17 hypothèses avec statut et responsable de vérification | — |
