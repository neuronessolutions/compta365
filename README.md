# Compta365 version 2023.09.16
Comptabilité générale Open source créée avec Microsoft PowerApps et les outils de la powerplatforme

# Introduction
**Compta365** a été développé avec la plateforme Low Code Microsoft PowerApps et la "Power Plateforme" ! Ce projet est open source et est utilisé aussi pour un évènement 2023 HackTogether, "the Power Platform Global AI Hack" pour utiliser des parties IA intégrées dans la solution avec Azure OpenAI et Copilot. Il s'agit d'une PowerApps de type "model-driven". Donc, comme Microsoft Dynamics 365 Sales par exemple !
Il sert de tutoriel ou de base à qui voudrait se lancer dans la création de solutions destinées aux entreprises.

Pour la base, nous avons commencé par développer une comptabilité générale d'entreprise multicompagnie simple. Au fur et à mesure, nous y ajouterons des fonctionnalités régulièrement.
Vous pouvez l'utiliser comme comptabilité générale pour votre compagnie. On pourrait aussi faire une interface grâce à Powerautomate pour générer les écritures comptables dans Compta365 à partir d'un logiciel externe de facturation ou des factures issues de Dynamics 365 Sales par exemple.

Les sources (Disponible dans la semaine du 25 septembre) seront disponibles sous forme de solution non managée et managée. Ainsi, vous pourrez utiliser la solution dans votre environnement de développement PowerApps ou dans votre environnement de production !

Vous trouverez ci-dessous la documentation détaillée de la solution et les fonctionnalités par version.

En premier lieu, nous décrivons le modèle de données Dataverse ainsi que les liens entre les entités. 
Puis, pour chaque table, la structure détaillée des données et description des différents objets par table (formulaires, vues, ...)
Ensuite, nous donnons les fonctionnalités par version, puis la documentation détaillée sur l'utilisation de cette comptabilité générale !

# Version de documentation et fonctionnalités
>Version 2023.09.23 :
>* Mise à jour du modèle de base, des liens entre différentes entités et de la documentation des tables :
>* Ajout du champ devise dans la table "Détails transactions"

>Version 2023.09.16 :
>* Création du modèle de base
>* Création des liens du modèle de base
>* Structure détaillée des tables du modèle de base
  
# Description du modèle de données

![1](https://github.com/nuage365/compta365/assets/102873102/e821a274-dd19-4639-9135-bdf9488c1d4c)

# Liens entre les différentes entités du modèle

![2](https://github.com/nuage365/compta365/assets/102873102/5f7c8dbe-3a5b-459e-b072-b3d05473b9ae)

# Structure détaillée des données et des objets par table

## Entité / table "Compagnie"
- Nom de la table : nuage365_Compagnie
  
| Nom d'affichage|Nom de colonne|Type de colonne|Remarques |
| --- | --- | --- | --- |
| Nom | nuage365_Name | Une seule ligne de texte (100 caractères) |  |
| Adresse  | nuage365_Adresse  | Zone de texte (400 caractères)  |   |
| Numéro de taxe fédérale| nuage365_Numerodetaxefederale | Une seule ligne de texte (50 caractères)  |   |
| Numéro de taxe provinciale| nuage365_Numerodetaxeprovinciale | Une seule ligne de texte (50 caractères) |   |
| Numéro de taxe autre| nuage365_Numerodetaxeautre | Une seule ligne de texte (50 caractères) |   |
| Devise par défaut| nuage365_Devisepardefaut | Rechercher (Devise) |   |

## Entité / table "Plan comptable"
- Nom de la table : nuage365_Plancomptable
  
| Nom d'affichage|Nom de colonne|Type de colonne|Remarques |
| --- | --- | --- | --- |
| GL No | nuage365_GLNo | Une seule ligne de texte (40 caractères) |  |
| Description  | nuage365_Description  | Une seule ligne de texte (100 caractères)  |   |
| Type de compte| nuage365_Typedecompte | Option (Bilan, Résultat)  |   |
| Sous type de compte| nuage365_Soustypedecompte | Option (Charges, Produits) |   |

## Entité / table "Journaux comptables"
- Nom de la table : nuage365_Journauxcomptables
  
| Nom d'affichage|Nom de colonne|Type de colonne|Remarques |
| --- | --- | --- | --- |
| Code journal | nuage365_Codejournal | Une seule ligne de texte (20 caractères) |  |
| Description  | nuage365_Description  | Une seule ligne de texte (80 caractères)  |   |

## Entité / table "Tiers"
- Nom de la table : nuage365_Tiers
  
| Nom d'affichage|Nom de colonne|Type de colonne|Remarques |
| --- | --- | --- | --- |
| Nom du tiers | nuage365_Nomdutiers | Une seule ligne de texte (150 caractères) |  |
| Adresse  | nuage365_Adresse  | Zone de texte (400 caractères)  |   |
| Type de tiers  | nuage365_Typedetiers  | Option (Client, Fournisseur, Banque)  |   |

## Entité / table "Transaction"
- Nom de la table : nuage365_Transaction
  
| Nom d'affichage|Nom de colonne|Type de colonne|Remarques |
| --- | --- | --- | --- |
| Numéro Lot journal | nuage365_NumeroLotjournal | Numérotation automatique (Personnalisé : LOT{SEQNUM:8}) |  |
| Compagnie | nuage365_Compagnie | Rechercher (Compagnie) |  |
| Date de journal  | nuage365_Datedejournal  | Date uniquement  |   |
| Code journal  | nuage365_Codejournal  | Rechercher (Journaux comptables)  |   |
| Description  | nuage365_Description  | Une seule ligne de texte (100 caractères)  |   |
| Transaction postée | nuage365_Transactionpostee  | Oui/Non  | Valeur Non par défaut  |

## Entité / table "Détails Transactions"
- Nom de la table : nuage365_Detailstransactions
  
| Nom d'affichage|Nom de colonne|Type de colonne|Remarques |
| --- | --- | --- | --- |
| Numéro Lot journal | nuage365_NumeroLotjournal | Rechercher (Transaction) |  |
| Numéro de compte GL | nuage365_NumerodeGL | Rechercher (Plan comptable) |  |
| Référence écriture  | nuage365_Referenceecriture  | Une seule ligne de texte (150 caractères)  | Peut représenter le numéro de document, facture, ...  |
| Devise | nuage365_Devisepardefaut | Rechercher (Devise) |   |
| Montant débit  | nuage365_Montantdebit  | Décimal (2)  | Valeur minimale : -100 000 000 000 valeur maximale : 100 000 000 000  |
| Montant crédit  | nuage365_Montantcredit  | Décimal (2)  | Valeur minimale : -100 000 000 000 valeur maximale : 100 000 000 000  |
| Description | nuage365_Description  | Une seule ligne de texte (150 caractères)  |   |
| Ecritures postées| nuage365_Ecriturespostees  | Oui/Non  | Valeur Non par défaut  |

# Documentation de la solution Compta365
