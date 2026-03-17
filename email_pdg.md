Objet : Diagnostic comptable Rampal / CDP — analyse et prochaines étapes

---

Le diagnostic réalisé par la DAF est un bon travail de cartographie. Il pose clairement les flux des deux entités, ce qui est manuel, ce qui pourrait ne plus l'être. Ce qui suit est une lecture critique de ce diagnostic, avec les questions qu'il faut se poser avant d'aller plus loin.

---

### Ce que le diagnostic montre bien

Rampal et CDP fonctionnent sur deux architectures logicielles séparées (LSI/Quadra d'un côté, Sage 100/Sage Compta de l'autre). Elles ne se parlent pas. La majorité des flux est manuelle, surtout côté CDP où Gaëlle ressaisit à la main ce qui sort de Prestashop dans Sage Compta.

Il y a des gains possibles — connecter Prestashop à Sage, automatiser une partie des rapprochements bancaires, supprimer le tableur intermédiaire du CA Retail chez Rampal. Tout ça est identifié dans le diagnostic et c'est juste.

### Ce que le diagnostic ne dit pas

**1. La facturation électronique obligatoire n'est pas mentionnée.**

La dématérialisation des factures inter-entreprises devient obligatoire en France à partir de 2026. Ce calendrier a déjà glissé plusieurs fois (initialement prévu en 2024), mais l'obligation arrive. Ça concerne les deux entités. Ça impose de choisir une plateforme de dématérialisation partenaire agréée par l'État. C'est le seul sujet qui a une deadline externe — tout le reste peut attendre, pas celui-là.

Le premier interlocuteur sur ce sujet, c'est l'expert-comptable. Pas un éditeur de logiciel.

**2. On ne sait pas si les automatisations proposées sont faisables.**

Le diagnostic identifie ce qu'il faudrait automatiser. Il ne dit pas si c'est techniquement possible avec les versions de logiciels en place, ni combien ça coûte, ni combien de temps ça prend. C'est normal — ce n'est pas son rôle. Mais ça veut dire qu'on ne peut pas passer directement du diagnostic à l'action sans une phase de vérification.

**3. La dépendance sur deux personnes n'est pas traitée comme un risque.**

Aurélie porte Rampal, Gaëlle porte CDP. Si l'une des deux est absente un mois, qu'est-ce qui se passe ? Le diagnostic cartographie leurs flux, ce qui est déjà bien — mais la question de la continuité n'est pas posée explicitement.

---

### Pennylane

La question a été soulevée. Réponse courte :

- Pour CDP, c'est envisageable. Pennylane couvre bien les flux simples (e-commerce, fournisseurs, TVA française) et propose une interface partagée avec l'expert-comptable.
- Pour Rampal, non. Les flux industriels (matières premières, sous-traitance, rapprochement BL/facture, logistique) dépassent ce que Pennylane sait faire.
- Dans tous les cas, le cabinet comptable doit être d'accord pour basculer dessus. Si ce n'est pas le cas, la discussion s'arrête là.

Mais surtout : Pennylane ou pas Pennylane, ça ne change rien au problème de fond. Le problème, c'est que les processus ne sont pas documentés au-delà du diagnostic, que deux personnes portent tout, et que les deux stacks ne communiquent pas. Changer de logiciel sans avoir résolu ça, c'est déplacer le problème.

---

### Les 10 questions à poser avant de décider quoi que ce soit

Tant que ces réponses n'existent pas, tout chiffrage ou planning est prématuré.

**Organisation :**
1. Aurélie et Gaëlle sont-elles réellement les seules à maîtriser les flux de leur entité ? Y a-t-il un suppléant, même partiel ?
2. Le cabinet comptable intervient-il dans les flux quotidiens pré-comptables, ou uniquement en fin d'exercice ?

**Faisabilité technique :**
3. Quelles versions exactes de Prestashop et Sage Compta sont utilisées par CDP ? Un connecteur compatible existe-t-il ?
4. Les API de Stripe, Paypal et Amazon sont-elles accessibles dans le contexte CDP (pas de restriction contractuelle) ?
5. Un flux direct Odoo → LSI est-il techniquement faisable avec les versions en place chez Rampal ?
6. Les logiciels des deux entités sont-ils à jour, ou sur des versions anciennes ?
7. LSI et Quadra chez Rampal sont-ils intégrés nativement ou fonctionnent-ils comme deux outils séparés ?

**Dimensionnement :**
8. Quel est le volume réel de commandes B2B chez CDP ? (Si c'est 10 par semaine, automatiser ne se justifie pas. Si c'est 50+, la question se pose.)

**Conformité :**
9. Une démarche de sélection d'une plateforme de facturation électronique a-t-elle déjà été engagée ?

**Pennylane :**
10. Le cabinet comptable est-il utilisateur de Pennylane ou ouvert à le devenir ?

---

### Ce qu'on recommande, dans l'ordre

**Étape 1 — Répondre aux questions ci-dessus.** Ça prend quelques coups de fil à l'intégrateur, au cabinet comptable, à Aurélie et Gaëlle. Pas un projet, pas un budget — juste des réponses.

**Étape 2 — Facturation électronique.** En parler avec l'expert-comptable maintenant. C'est le seul sujet avec une contrainte de calendrier externe.

**Étape 3 — Connecteur Prestashop → Sage (CDP).** Si les versions sont compatibles, c'est le gain le plus direct. Sinon, c'est un projet à cadrer avec un intégrateur.

**Étape 4 — Rapprochement bancaire (CDP).** Commencer par un seul canal (Stripe, par exemple), voir ce que ça donne, puis élargir. Le 100% automatique n'existe pas — 80% de lettrage automatique serait déjà un très bon résultat.

**Étape 5 — Tableur CA Retail (Rampal).** Comprendre d'abord ce que le tableur d'Aurélie fait exactement — il applique peut-être des retraitements qu'un flux direct ne reproduirait pas.

**Étape 6 — ERP unifié.** Pas avant d'avoir fait tout le reste. C'est un projet lourd, coûteux, qui dérape souvent en PME. À n'engager que si le groupe a la capacité managériale et financière de le porter.

---

Les visuels interactifs du diagnostic sont consultables ici :
- Synthèse dirigeant : https://maxberko.github.io/rampal-latour-accounting/synthese.html
- Matrice effort / impact : https://maxberko.github.io/rampal-latour-accounting/matrice.html
- Tableau détaillé : https://maxberko.github.io/rampal-latour-accounting/tableau.html
