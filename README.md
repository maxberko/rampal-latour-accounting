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

### Gains immédiats — avec réserves

**1. Connecteur Prestashop → Sage Compta (CDP)**
Gaëlle ressaisit manuellement dans Sage Compta chaque vente issue de Prestashop. Un connecteur natif ou un pont applicatif supprimerait cette double saisie quotidienne.

> **Réalité terrain.** Le label "effort faible" suppose qu'un connecteur compatible existe pour les versions exactes de Prestashop et Sage Compta utilisées par CDP. Ce n'est pas vérifié. L'écosystème des connecteurs Prestashop → Sage est fragmenté : les modules tiers du marketplace Prestashop ont des taux de maintenance inégaux et des limitations sur les plans comptables personnalisés. Si les versions sont anciennes ou si le plan comptable de Gaëlle comporte des spécificités, il faudra un développement sur mesure via un intégrateur Sage. Le "gain immédiat" peut donc prendre 2 à 4 mois entre le cadrage, le choix du connecteur, les tests et la mise en production. Prévoir aussi un temps de validation comptable post-migration où Gaëlle fait la double saisie en parallèle. **Fourchette de coût : d'un module marketplace à quelques centaines d'euros (cas favorable, versions compatibles) à une prestation intégrateur Sage de plusieurs milliers d'euros (développement sur mesure). Non chiffrable précisément sans audit des versions en place.**

**2. Rapprochement bancaire automatisé (CDP)**
Les encaissements CDP transitent par quatre canaux (carte bancaire, Paypal, Amazon, Stripe), tous réconciliés à la main. Ces plateformes disposent d'API documentées.

> **Réalité terrain.** Dire que "les API existent" ne suffit pas. Chaque plateforme a sa propre logique de remontée des transactions (Stripe raisonne en paiements, Amazon en settlements avec des décalages de 14 jours, Paypal mélange les devises). Le rapprochement automatisé ne consiste pas à brancher quatre API — il faut un outil de réconciliation intermédiaire (ou un développement spécifique) capable de normaliser les formats, gérer les décalages temporels, les frais de commission, les remboursements et les litiges. Le gain de "3 à 4 h/semaine" est une estimation non mesurée : il faudrait d'abord chronométrer le temps réel passé par Gaëlle sur cette tâche. Un outil type Bridge, Qonto ou un module Sage dédié peut couvrir une partie du besoin, mais rarement les quatre canaux d'un coup. Le rapprochement 100% automatique est un objectif rarement atteint — viser 80% de lettrage automatique serait déjà un bon résultat. **Fourchette de coût : d'un abonnement outil SaaS à quelques dizaines d'euros/mois (si un seul canal, outil existant compatible) à plusieurs milliers d'euros de développement sur mesure (si les quatre canaux doivent être couverts avec réconciliation spécifique). Dépend de la stack exacte et du volume de transactions.**

**3. Suppression du retraitement tableur CA Retail (Rampal)**
Aurélie passe par un fichier tableur intermédiaire pour intégrer le CA des boutiques depuis Odoo vers LSI.

> **Réalité terrain.** Un "flux direct Odoo → LSI" suppose que les deux systèmes peuvent communiquer. LSI est un progiciel de gestion industrielle dont les capacités d'import/export varient fortement selon la version et le paramétrage. Il faudra probablement un développement d'interface (fichier plat, API si disponible, ou script d'import). Le risque principal : le tableur intermédiaire d'Aurélie ne fait peut-être pas que transférer des données — il peut aussi appliquer des retraitements, des regroupements ou des corrections que le flux direct ne reproduira pas sans spécification précise. Avant de supprimer le tableur, il faut documenter exactement ce qu'il fait. **Fourchette de coût : de quelques jours d'intégrateur (si LSI dispose d'un import standard compatible) à un développement d'interface complet (si les retraitements du tableur sont complexes). Dépend de l'intégrateur LSI et de ce que le tableur fait réellement.** Délai : 1 à 3 mois minimum.

### Préalable indispensable

**4. Documentation des procédures d'Aurélie et de Gaëlle**
Aucune procédure écrite n'existe. Documenter les flux est un prérequis à toute automatisation.

> **Réalité terrain.** C'est le chantier le moins cher et le moins risqué, mais aussi celui qui a le plus de chances de ne jamais aboutir. Documenter ses propres procédures est une tâche ingrate que les opérationnels repoussent indéfiniment. Il faut un tiers (consultant, stagiaire, collègue) qui s'assoit à côté d'Aurélie et Gaëlle pendant quelques jours chacune et rédige pour elles. Sans cette contrainte externe, la documentation restera une ligne dans un plan d'action. **Coût : quasi nul si réalisé en interne, quelques jours de prestation si externalisé.**

### Chantiers structurants

**5. Facturation électronique obligatoire 2026**
Mise en conformité légale non négociable. Impose le choix d'une plateforme de dématérialisation partenaire (PDP) agréée par l'État.

> **Réalité terrain.** Le calendrier réglementaire a déjà glissé plusieurs fois (initialement prévu en 2024). L'obligation de réception est effective au 1er septembre 2026 pour toutes les entreprises ; l'obligation d'émission est échelonnée selon la taille. Il faut vérifier dans quelle catégorie tombent Rampal et CDP. Le choix d'une PDP est un sujet à part entière : le marché est encore jeune, les offres évoluent vite, et le risque est de s'engager avec un acteur qui n'obtiendra pas ou ne maintiendra pas son agrément. L'expert-comptable est le premier interlocuteur pour ce choix — pas l'éditeur de logiciel. **Fourchette de coût : de quelques dizaines d'euros/mois par entité (PDP entrée de gamme, faible volume) à plusieurs centaines d'euros/mois (volume élevé, intégration poussée avec l'outil comptable). Dépend du prestataire choisi et du volume de factures.** Délai de mise en conformité : 3 à 6 mois.

**6. Migration vers un progiciel de gestion intégré unifié**
Cible logique à 18 mois (Odoo complet ou Sage X3).

> **Réalité terrain.** C'est le chantier le plus risqué et le plus coûteux de la liste. Une migration ERP pour deux entités avec des flux industriels, c'est un projet à 6–12 mois de mise en œuvre réelle (pas 18 mois de "cible" — 18 mois c'est le début du projet, pas la fin). Le taux d'échec ou de dérapage des projets ERP en PME est bien documenté : les délais doublent fréquemment. Ce chantier ne doit être engagé que si le groupe a la capacité managériale et financière de le porter — et surtout pas en même temps que les autres chantiers. La recommandation "après stabilisation des flux" est correcte mais insuffisante : il faut aussi un sponsor interne fort et un budget validé. **Fourchette de coût : de plusieurs dizaines de milliers d'euros (périmètre restreint, intégrateur local) à bien au-delà de cent mille euros (périmètre complet deux entités, migration de données, formation). Non chiffrable sans cahier des charges et appel d'offres intégrateur.**

**8. Automatisation des commandes fournisseurs B2B (CDP)**
Les commandes B2B sont saisies manuellement à réception (messagerie, téléphone). Un portail en ligne ou un EDI réduirait ce travail.

> **Réalité terrain.** L'EDI suppose que les clients B2B de CDP soient équipés et volontaires pour changer leurs habitudes. Pour une PME, c'est rarement le cas — les clients commandent par email ou téléphone parce que ça leur convient. Un portail de commande en ligne est possible mais ne sera adopté que si les clients y trouvent un intérêt (historique, suivi, tarifs). Le ROI dépend entièrement du volume : si CDP traite 10 commandes B2B par semaine, l'automatisation ne se justifie pas. Si c'est 50+, la question se pose. Ce volume n'est pas connu. **Fourchette de coût : d'un portail de commande simple (quelques milliers d'euros) à une intégration EDI complète avec Sage (plusieurs dizaines de milliers d'euros). Dépend du volume de commandes et du niveau d'équipement des clients. Ne pas engager avant d'avoir mesuré le besoin réel.**

### Amélioration secondaire

**7. Dématérialisation des bons de réception papier**
Les réceptions logistiques sont confirmées sur papier. Un bon de réception numérique améliorerait la fluidité.

> **Réalité terrain.** Chantier simple en apparence, mais qui touche aux habitudes terrain (magasiniers, logistique). L'adoption dépend de l'équipement (tablettes, scanners) et de la formation. Peut s'intégrer naturellement dans le projet ERP (item 6) plutôt que d'être traité isolément. Ne pas en faire un projet à part.

---

## Question ouverte — Pennylane

L'hypothèse d'une migration vers Pennylane a été analysée :

- **Pour CDP** : pertinent comme remplacement de Sage Compta sur les flux simples (ventes, e-commerce, fournisseurs transport). L'outil intègre nativement la TVA française, la liasse fiscale et une interface partagée client/expert-comptable.
- **Pour Rampal** : inadapté. Les flux industriels (sous-traitance, matières premières, rapprochement BL/facture, logistique intégrée) dépassent les capacités du produit.
- **Contrainte externe** : le cabinet comptable doit être partant pour adopter Pennylane comme outil de travail, ce qui n'est pas acquis.

**Verdict** : Pennylane n'est ni rejeté ni prioritaire. Le problème du groupe n'est pas un problème de logiciel — c'est un problème de processus non documentés, de dépendance humaine et de dette tableur. Changer d'outil sans avoir résolu ça revient à migrer le chaos.

---

## Feuille de route recommandée — version réaliste

| Horizon | Actions | Risque principal |
|---|---|---|
| **Mois 1–2** | Documenter les procédures Aurélie & Gaëlle (avec un tiers dédié, pas en auto-documentation). | Ne sera pas fait si personne ne le porte. |
| **Mois 2–4** | Cadrer le connecteur Prestashop → Sage (audit versions, choix module, test). | Incompatibilité de versions, plan comptable non standard. |
| **Mois 3–6** | Rapprochement bancaire : choisir un outil de réconciliation, brancher les canaux un par un. Viser 80% de lettrage auto. | Complexité des formats Amazon/Paypal, gestion des écarts. |
| **Mois 3–6** | Facturation électronique : travailler avec l'expert-comptable sur le choix d'une PDP. | Marché jeune, risque de mauvais choix de prestataire. |
| **Mois 4–6** | Flux Odoo → LSI : documenter les retraitements du tableur d'Aurélie, puis spécifier l'interface. | Le tableur cache peut-être des retraitements non documentés. |
| **Mois 12–24** | Migration ERP unifiée — uniquement si les flux sont stabilisés, les procédures documentées, et le budget validé. | Projet structurant à fort risque de dérapage. |

**Note sur les coûts** : les fourchettes de coût sont indiquées dans l'analyse détaillée de chaque chantier (section précédente). Ce sont des ordres de grandeur larges — les coûts réels dépendent des versions logicielles, des intégrateurs disponibles, du volume de transactions et de la complexité des flux. Chaque chantier nécessite un cadrage et un devis avant engagement. Le gain de "1,5 ETP/semaine" annoncé dans la synthèse est un ordre de grandeur optimiste et non mesuré — le gain réel ne sera quantifiable qu'après mise en production de chaque brique.

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
