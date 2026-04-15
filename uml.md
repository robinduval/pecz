Modèle Conceptuel de Données (ACOO) - Projet PECz (Version Simple Stylée)

Auteur : Jean-Guy Mauve (revu par l'Équipe d'Architecture)
Note de conception : Application de la nomenclature "Ez" pour le style, et de la notation hongroise majuscule pour les attributs.

Ce diagramme de classes représente le modèle du domaine simplifié. Il met en évidence l'encapsulation (attributs privés -, méthodes publiques +), l'héritage, ainsi que les relations fortes (composition *--) et faibles (agrégation o-- ou association simple --).

Note technique pour GitHub : Ce diagramme utilise la syntaxe Mermaid. Il sera automatiquement rendu de manière visuelle par l'interface GitHub.

```mermaid
classDiagram
direction TB

%% ==========================================
%% PACKAGE UTILISATEURS
%% ==========================================
class UtilisateurEz {
    <<abstract>>
    -int INT_id
    -String STR_pseudo
    -String STR_email
    -String STR_motDePasseHash
    -DateTime DATETIME_dateInscription
    +seConnecter() bool
    +seDeconnecter() void
}

class AcheteurEz {
    -float FLOAT_soldeCredits
    +acheterCredits(float montant) void
    +debiterCredits(float montant) bool
}

class VendeurCertifieEz {
    -String STR_clePubliqueCrypto
    -String STR_adresseFiscale
    -boolean BOOLEAN_identiteVerifiee
    +soumettrePreuveBounty(PreuveAuthenticiteEz preuve) void
    +creerEnchere(ExemplaireCarteEz carte) EnchereEz
}

class AdministrateurEz {
    -int INT_niveauPrivilege
    +bannirUtilisateur(UtilisateurEz u) void
    +validerPreuve(PreuveAuthenticiteEz p) void
}

%% Héritage (Un Vendeur EST UN Acheteur qui a été certifié)
UtilisateurEz <|-- AcheteurEz
AcheteurEz <|-- VendeurCertifieEz
UtilisateurEz <|-- AdministrateurEz

%% ==========================================
%% PACKAGE CATALOGUE & CARTES
%% ==========================================
class CarteReferenceEz {
    <<Catalogue Global>>
    -int INT_id
    -String STR_nom
    -String STR_jeuTCG
    -String STR_extension
    -String STR_rarete
    +getValeurEstimee() float
}

class ExemplaireCarteEz {
    <<Objet Physique Unique>>
    -int INT_id
    -int INT_gradeEtat
    -String STR_numeroCertification
    -String STR_hashBlockchain
    +mettreAJourGrade(int nouveauGrade) void
}

%% ==========================================
%% PACKAGE TRANSACTIONS (ENCHÈRES & BOUNTIES)
%% ==========================================
class EnchereEz {
    -int INT_id
    -DateTime DATETIME_dateHeureDebut
    -DateTime DATETIME_dateHeureFin
    -float FLOAT_prixDepart
    -float FLOAT_prixActuel
    -String STR_statut
    +ajouterMise(MiseEnchereEz mise) void
    +cloturer() void
}

class MiseEnchereEz {
    <<Pay-to-Bid Transaction>>
    -int INT_id
    -DateTime DATETIME_dateMise
    -float FLOAT_coutEnCredit
    -float FLOAT_incrementPrixEuro
}

class DemandeBountyEz {
    -int INT_id
    -DateTime DATETIME_dateCreation
    -float FLOAT_recompenseProposee
    -String STR_statutDemande
    +accepterPreuve(PreuveAuthenticiteEz p) void
}

class PreuveAuthenticiteEz {
    -int INT_id
    -String STR_cheminFichierVideo
    -DateTime DATETIME_dateSoumission
    -boolean BOOLEAN_estValidee
    -String STR_commentaireJuge
}

%% ==========================================
%% RELATIONS ET MULTIPLICITÉS
%% ==========================================

%% Un exemplaire appartient physiquement à un vendeur (Agrégation)
VendeurCertifieEz "1" o-- "*" ExemplaireCarteEz : détient

%% Un exemplaire référence une carte générique du catalogue
CarteReferenceEz "1" *-- "*" ExemplaireCarteEz : est instanciée en >

%% Gestion des enchères
VendeurCertifieEz "1" -- "*" EnchereEz : organise >
ExemplaireCarteEz "1" -- "0..1" EnchereEz : est mise en vente dans >

%% Composition pure : Une enchère est composée de mises qui n'existent pas sans elle
EnchereEz "1" *-- "*" MiseEnchereEz : contient >
AcheteurEz "1" -- "*" MiseEnchereEz : place >

%% Gestion des Bounties
AcheteurEz "1" -- "*" DemandeBountyEz : publie >
CarteReferenceEz "1" -- "*" DemandeBountyEz : cible >

%% Composition : Les preuves sont attachées à une demande spécifique
DemandeBountyEz "1" *-- "*" PreuveAuthenticiteEz : reçoit >
VendeurCertifieEz "1" -- "*" PreuveAuthenticiteEz : fournit >

%% Une preuve valide un exemplaire physique précis
PreuveAuthenticiteEz "0..*" -- "1" ExemplaireCarteEz : authentifie >


```
