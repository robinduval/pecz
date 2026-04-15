Grille d'evaluation ACOO - Contexte pour evaluation

Projet : PECz (Pablo EscoCardz) - Architecture ACOO

Objectif :Vérifier s'ils ont bien compris le besoin métier et s'ils ont su gérer les "contraintes" de Jean-Guy sans tomber dans le panneau technique.

1. Grille de Notation Globale (sur 20 points)

Le support fourni par les groupes (PDF, PPT, Word...) doit être autoporteur. 
S'il manque un élèment, je diminue la note.

A. Les 3 Diagrammes de Cas d'Utilisation (4 pts)

Rappel de ma consigne : 3 diagrammes regroupant au moins 4 comportements différents chacun, avec usage de extend ou use (include).

Mes critères de validation (à vérifier strictement) :
[ ] Le Piège du Micro-ondes : Ils ont dû modéliser la "Pause Temporelle" des enchères. Je dois vérifier qu'il y a bien un extend du type : (Enchérir) <..extend.. (Attendre fin du micro-ondes). Si c'est absent : -1 pt.
[ ] L'Acteur Kevin : Kevin (14 ans) DOIT apparaître comme acteur secondaire relié au cas d'utilisation (Certifier Carte).
[ ] Bonus Dédé : +1 pt s'ils ont pensé à mettre Dédé comme acteur de type "Administrateur" (même s'il est en prison, c'est métier).
[ ] Verifier qu'il y a bien 3 diagrammes et 4 comportements (+/- 1 point par comportement ou diag manquan)

B. Les 6 Spécifications de Cas d'Utilisations individuels (6 pts)

Rappel : 1 UC détaillé par membre du groupe (Nom, portée, acteur, scénario nominal, pré/post conditions...)

Ce que j'attends au tournant (exemple) :
[ ] Préconditions : Pour le cas d'utilisation "Créer une enchère", la précondition doit mentionner "La base Access fait moins de 1.9 Go". S'ils l'ont ignoré en disant "c'est de la technique, pas du fonctionnel", je leur rappellerai que Jean-Guy est le client et qu'il fait ce qu'il veut.
[ ] Scénario alternatif / Exigences spéciales : Pour le cas "Soumettre un Bounty", l'exigence spéciale DOIT stipuler la présence du Picsou Magazine. Si un groupe a oublié Picsou Magazine : 0 à cette sous-partie.

C. Diagrammes de Séquence et Classes d'Analyse individuels (5 pts)

Rappel : 1 Diagramme de séquence et 1 diagramme de classes d'analyse par personne.

Mes critères de validation :
[ ] Le Diagramme de Séquence de l'Enchère : Je veux voir le prélèvement "Pay-to-bid". Le diagramme doit montrer le flux vers l'objet Portefeuille (ou équivalent) pour prélever 1 crédit AVANT d'augmenter le prix de la carte.
[ ] Temps de réponse : Si leur diagramme de séquence ne montre pas un message asynchrone pour la validation Skype de Kevin, je les pénalise.
[ ] Le Piège de l'Architecture : S'ils ont modélisé la "Box internet" ou le "CPL" dans le diagramme de classes d'analyse : je mets un gros zéro. Le modèle d'analyse ne doit contenir que le métier ! (C'est le seul critère que je note très sérieusement, pour vérifier qu'ils n'ont pas recopié le mauvais schéma fourni en annexe).

D. Le Diagramme de Classes d'Analyse Unifié (5 pts)

Rappel : 1 réunification contenant les attributs, les opérations et les multiplicités.

[ ] La notation Ez : Pour qu'ils aient la totalité des points, leur diagramme final unifié doit impérativement utiliser la notation hongroise stylée que j'ai montrée en cours (ex: ajouter "Ez" à la fin des classes comme UtilisateurEz, 
[ ] La notation Hongroise : Typer les attributs en majuscule comme STR_pseudo.

2. Posture lors de la "préparation"

Si un étudiant me dit que MS Access n'est pas scalable : Je l'interromprai en disant "Jean-Guy a payé 4 Bitcoins pour ce projet, qui êtes-vous pour remettre en cause ses macros VBA de 2004 ?". Je veux évaluer leur capacité à défendre leur refonte technologique sans se démonter.

Si la solution est trop propre : Je leur demanderai avec un ton très sérieux comment ils ont intégré le script VBScript de Dédé pour la sécurité. S'ils disent qu'ils l'ont supprimé pour mettre de l'Argon2id ou du JWT, je ferai mine d'être extrêmement déçu par leur manque de respect pour le code hérité.