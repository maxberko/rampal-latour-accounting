# Hypothèses & suppositions — Diagnostic automatisation Rampal / CDP

> Document de traçabilité. Chaque hypothèse doit être confirmée ou infirmée avant de passer en phase de recommandation opérationnelle.

---

## 1. Hypothèses sur le document source

| # | Hypothèse | Type | Statut | À vérifier avec |
|---|---|---|---|---|
| H1 | Les éléments labellisés "Automatisé" dans le diagnostic sont des **propositions**, pas l'état actuel | Interprétation — **confirmée par le client** | ✅ Confirmée | — |
| H2 | Les éléments labellisés "Manuel" décrivent l'état actuel réel des flux | Interprétation | ❓ À confirmer | Aurélie / Gaëlle |
| H3 | Le document couvre l'intégralité des flux comptables — aucun flux secondaire n'est omis | Périmètre | ❓ À confirmer | Aurélie / Gaëlle |

---

## 2. Hypothèses sur l'organisation

| # | Hypothèse | Type | Statut | À vérifier avec |
|---|---|---|---|---|
| H4 | Aurélie et Gaëlle sont les **seules personnes** qui maîtrisent les flux comptables de leur entité respective | Risque RH | ❓ À confirmer | PDG / DRH |
| H5 | Il n'existe **aucune procédure écrite** ni documentation des flux actuels | Risque opérationnel | ❓ À confirmer | Aurélie / Gaëlle |
| H6 | Le cabinet comptable externalisé (expert-comptable) n'est **pas impliqué** dans les flux quotidiens pré-comptables | Périmètre | ❓ À confirmer | Cabinet / PDG |

---

## 3. Hypothèses sur les systèmes

| # | Hypothèse | Type | Statut | À vérifier avec |
|---|---|---|---|---|
| H7 | Un connecteur natif ou un pont applicatif entre **Prestashop et Sage Compta** existe et est compatible avec les versions utilisées par CDP | Faisabilité technique | ❓ À confirmer | Intégrateur / éditeur Sage |
| H8 | Les interfaces de programmation de **Stripe, Paypal et Amazon** sont accessibles dans le contexte CDP (pas de restriction contractuelle ou technique) | Faisabilité technique | ❓ À confirmer | CDP / prestataire technique |
| H9 | Un flux direct **Odoo → LSI** est techniquement faisable sans refonte majeure | Faisabilité technique | ❓ À confirmer | Intégrateur LSI |
| H10 | Les deux entités utilisent des **versions à jour** de leurs logiciels (Sage, LSI, Quadra, Odoo, Prestashop) | Compatibilité | ❓ À confirmer | DSI / prestataire |
| H11 | LSI et Quadra chez Rampal sont deux logiciels **distincts et non intégrés nativement** | Architecture | ❓ À confirmer | Aurélie / prestataire |

---

## 4. Hypothèses sur les volumes et le ROI

| # | Hypothèse | Type | Statut | À vérifier avec |
|---|---|---|---|---|
| H12 | Le gain estimé de **1,5 équivalent temps plein / semaine** est un ordre de grandeur non étayé — aucune mesure du temps passé par tâche n'a été réalisée | Estimation | ⚠️ Non étayée | Aurélie / Gaëlle (chrono des tâches) |
| H13 | Le volume de commandes B2B CDP est **suffisant** pour justifier une automatisation de la saisie (item 8 de la matrice) | Rentabilité | ❓ À confirmer | Julia / CDP |

---

## 5. Hypothèses sur la conformité réglementaire

| # | Hypothèse | Type | Statut | À vérifier avec |
|---|---|---|---|---|
| H14 | La facturation électronique obligatoire s'applique aux deux entités dès **2026** (hypothèse basée sur le calendrier réglementaire français en vigueur à mars 2025) | Réglementaire | ⚠️ À actualiser | Expert-comptable / site impots.gouv.fr |
| H15 | Aucune des deux entités n'a déjà engagé de démarche de sélection d'une **plateforme de dématérialisation partenaire** | Avancement | ❓ À confirmer | PDG / cabinet |

---

## 6. Hypothèses sur Pennylane (analyse complémentaire)

| # | Hypothèse | Type | Statut | À vérifier avec |
|---|---|---|---|---|
| H16 | Le cabinet comptable externalisé n'est **pas encore utilisateur de Pennylane** ou n'a pas manifesté de préférence pour cet outil | Compatibilité partenaire | ❓ À confirmer | Cabinet |
| H17 | Le volume et la complexité des flux CDP (B2B, sous-traitance, matières premières) **ne dépassent pas** les capacités de Pennylane | Adéquation produit | ❓ À confirmer | Test / démo Pennylane |

---

## Légende

| Symbole | Signification |
|---|---|
| ✅ Confirmée | Validée par le client ou une source fiable |
| ❓ À confirmer | Non vérifiée — à investiguer avant toute décision |
| ⚠️ Non étayée | Estimation ou hypothèse de travail — à quantifier |
