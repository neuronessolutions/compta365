# Compta365 version 2023.10.02.2
Comptabilité générale Open source créée avec Microsoft PowerApps et les outils de la powerplatforme

# Introduction
**Compta365** a été développé avec la plateforme Low Code Microsoft PowerApps et la "Power Plateforme" ! Ce projet est open source et est utilisé aussi pour un évènement 2023 HackTogether, "the Power Platform Global AI Hack" pour utiliser des parties IA intégrées dans la solution avec Azure OpenAI et Copilot. Il s'agit d'une PowerApps de type "model-driven". Donc, comme Microsoft Dynamics 365 Sales par exemple !
Il sert de tutoriel ou de base à qui voudrait se lancer dans la création de solutions destinées aux entreprises.

Pour la base, nous avons commencé par développer une comptabilité générale d'entreprise multicompagnie simple. Au fur et à mesure, nous y ajouterons des fonctionnalités régulièrement.
Vous pouvez l'utiliser comme comptabilité générale pour votre compagnie. On pourrait aussi faire une interface grâce à Powerautomate pour générer les écritures comptables dans Compta365 à partir d'un logiciel externe de facturation ou des factures issues de Dynamics 365 Sales par exemple.

Nous utiliserons Copilot pour bâtir automatiquement des rapports PowerBI :)

Les sources sont disponibles sous forme de solution non managée. Ainsi, vous pourrez utiliser la solution dans votre environnement de développement PowerApps, puis l'exporter en solution managée pour votre environnement de production !

Vous trouverez ci-dessous la documentation détaillée de la solution et les fonctionnalités par version.

En premier lieu, nous décrivons le modèle de données Dataverse ainsi que les liens entre les entités. 
Puis, pour chaque table, la structure détaillée des données et description des différents objets par table (formulaires, vues, ...)
Ensuite, nous donnons les fonctionnalités par version, puis la documentation détaillée sur l'utilisation de cette comptabilité générale !

# Version de documentation et fonctionnalités
>Version 2023.10.02.2 :
>* Ajout d'une entité "Transactions" qui sert d'entête à l'entité "Détails transactions". Ajout des liens entre ces 2 entités et modification des formulaires et vues.
>* Ajout de champs "Total débit" et "Total crédit" dans la nouvelle entité "Transactions" et création d'un workflow pour cumuler les montants débits et crédits de l'entité "Détails transactions". Total débit doit être égal au Total crédit pour pouvoir poster la transaction (future fonctionnalité)
>* Ajout d'une entité "Periode fiscale" par compagnie pour contrôler plus tard la saisie des écritures dans une période autorisée
>* Ajout de 2 champs (taxes sur achats et taxes sur ventes) dans l'entité "Plan comptable" pour indiquer qu'un compte de GL concerne une taxe. Va servir à notre futur module de déclaration de taxes.
>* Mise à jour de la solution non managée et des sources de la solution
>* Mise à jour du modèle des données
>* Ajout des descriptions des nouvelles entités et champs ajoutés !

>Version 2023.09.27.1 :
>* Ajout de 2 champs dans la table "Plan comptable" pour gérer plus facilement les rapports annuels. (Regroupement Bilan et Regroupement compte de résultat)
>* Mise à jour du modèle de données pour "Plan comptable"
>* Ajout des icônes pour chaque table custom
>* Ajout de la solution non managée et des sources de la solution

>Version 2023.09.26 :
>* Mise à jour du modèle de base, des liens entre différentes entités et de la documentation des tables :
>* Ajout des champs montant débit et crédit de type devise. Simplification du modèle pour les transactions.

>Version 2023.09.23 :
>* Mise à jour du modèle de base, des liens entre différentes entités et de la documentation des tables :
>* Ajout du champ devise dans la table "Détails transactions"

>Version 2023.09.16 :
>* Création du modèle de base
>* Création des liens du modèle de base
>* Structure détaillée des tables du modèle de base
  
# Description du modèle de données et liens entre les données

![Compta365 Modèle de données (3)](https://github.com/nuage365/compta365/assets/102873102/02781fca-844d-4db3-9a74-cf3bd0370b89)


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

## Entité / table "Période fiscale"
- Nom de la table : nuage365_Periodefiscale
  
| Nom d'affichage|Nom de colonne|Type de colonne|Remarques |
| --- | --- | --- | --- |
| Compagnie | nuage365_Compagnie | Rechercher (Compagnie) |  |
| Date de début d'exercice | nuage365_Datededebutdexercice | Date uniquement |  |
| Date de fin d'exercice | nuage365_Datedefindexercice | Date uniquement |  |
| Nom période  | nuage365_Nomperiode  | Une seule ligne de texte (100 caractères)  |   |

## Entité / table "Plan comptable"
- Nom de la table : nuage365_Plancomptable
  
| Nom d'affichage|Nom de colonne|Type de colonne|Remarques |
| --- | --- | --- | --- |
| GL No | nuage365_GLNo | Une seule ligne de texte (40 caractères) |  |
| Description  | nuage365_Description  | Une seule ligne de texte (100 caractères)  |   |
| Type de compte| nuage365_Typedecompte | Option (Bilan, Résultat)  |   |
| Sous type de compte| nuage365_Soustypedecompte | Option (Charges, Produits) |   |
| Regroupement Bilan | nuage365_RegroupementBilan  | Une seule ligne de texte (150 caractères)  |   |
| Regroupement compte de résultat  | nuage365_Regroupementcomptederesultat  | Une seule ligne de texte (150 caractères)  |   |
| Taxes sur achats| nuage365_Taxessurachats  | Oui/Non  | Valeur Non par défaut  |
| Taxes sur ventes| nuage365_Taxessurachats  | Oui/Non  | Valeur Non par défaut  |

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

## Entité / table "Transactions"
- Nom de la table : nuage365_Transactions
  
| Nom d'affichage|Nom de colonne|Type de colonne|Remarques |
| --- | --- | --- | --- |
| Transactions | nuage365_TransactionsId | Identificateur unique |  |
| Code journal | nuage365_Codejournal | Rechercher (Journaux comptables) |  |
| Compagnie | nuage365_Compagnie | Rechercher (Compagnie) |  |
| Date écriture | nuage365_Dateecriture | Date uniquement |  |
| Description transaction| nuage365_Name  | Une seule ligne de texte (100 caractères)  |   |
| Devise | TransactionCurrencyId | Rechercher (Devise) |   |
| Taux de change | ExchangeRate | Décimal |   |
| Total débit  | nuage365_Totaldebit  | Devise  |   |
| Total crédit  | nuage365_Totalcredit  | Devise  |  |
| Total débit (de base)  | nuage365_totaldebit_Base  | Devise  |   |
| Total crédit (de base)  | nuage365_totalcredit_Base  | Devise  |  |
| Transaction postée| nuage365_Transactionpostee  | Oui/Non  | Valeur Non par défaut  |

## Entité / table "Détails Transactions"
- Nom de la table : nuage365_Detailstransactions
  
| Nom d'affichage|Nom de colonne|Type de colonne|Remarques |
| --- | --- | --- | --- |
| Numéro écriture | nuage365_NumeroEcriture | Rechercher (Journaux comptables) |  |
| Code journal | nuage365_Codejournal | Rechercher (Journaux comptables) |  |
| Compagnie | nuage365_Compagnie | Rechercher (Compagnie) |  |
| Date écriture | nuage365_Dateecriture | Date uniquement |  |
| Numéro de compte GL | nuage365_NumerodeGL | Rechercher (Plan comptable) |  |
| Référence écriture  | nuage365_Referenceecriture  | Une seule ligne de texte (150 caractères)  | Peut représenter le numéro de document, facture, ...  |
| Tiers | nuage365_Tiers | Rechercher (Tiers) |   |
| Devise | TransactionCurrencyId | Rechercher (Devise) |   |
| Taux de change | ExchangeRate | Décimal |   |
| Montant débit  | nuage365_Montantdebit  | Devise  |   |
| Montant crédit  | nuage365_Montantcredit  | Devise  |  |
| Montant débit (de base)  | nuage365_Montantdebit_Base  | Devise  |   |
| Montant crédit (de base)  | nuage365_Montantcredit_Base  | Devise  |  |
| Description | nuage365_Description  | Une seule ligne de texte (150 caractères)  |   |
| Ecritures postées| nuage365_Ecriturespostees  | Oui/Non  | Valeur Non par défaut  |

# Documentation de la solution Compta365

![Capture d’écran, le 2023-09-27 à 22 49 01](https://github.com/nuage365/compta365/assets/102873102/8d385e12-a59f-49a9-8d33-28c82cdc60f2)


Documentation détaillée par module à venir :)
