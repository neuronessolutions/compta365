# Compta365 version 2023.10.19.1
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
>Version 2023.10.19.1 :
>* Ajout d'un rapport "Déclarations de taxes" créé avec PowerBI
>* Ajout des copies écrans des modules existants et début de documentation

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

![Compta365 Modèle de données](https://github.com/neuronessolutions/compta365/assets/102873102/bc950026-07df-487d-a348-a9a54307fd86)


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
### Menu général
![compta365_Mainmenu](https://github.com/neuronessolutions/compta365/assets/102873102/1cf0cf1d-b732-44d6-b212-61fa7c725bbe)

### Module Compagnies
![compta365_Mainmenu](https://github.com/neuronessolutions/compta365/assets/102873102/7eba3be6-1aa2-4715-b911-f4cd8d962c5c)


![compta365_compagnies_details](https://github.com/neuronessolutions/compta365/assets/102873102/0fba538c-ef85-420d-b5b3-c5775889209e)

### Module Périodes fiscales
![compta365_periodefiscale_liste](https://github.com/neuronessolutions/compta365/assets/102873102/74d15ff2-8706-493a-9863-19688855780f)


![compta365_Periodefiscale_details](https://github.com/neuronessolutions/compta365/assets/102873102/042d670a-9446-4f8b-8227-042c51481a35)

### Module Plans comptables
![compta365_plancomptable_liste](https://github.com/neuronessolutions/compta365/assets/102873102/2461530f-ef8a-4fa9-98cf-8f81e6fd04d7)


![compta365_plancomptable_details](https://github.com/neuronessolutions/compta365/assets/102873102/20a5d07a-e803-4f80-884f-af090b7d332c)

### Module Journaux comptables
![compta365_journauxcomptables_liste](https://github.com/neuronessolutions/compta365/assets/102873102/fb4c7854-adcb-4f80-bb0d-69671c9a3100)


![compta365_journauxcomptables_details](https://github.com/neuronessolutions/compta365/assets/102873102/337328a1-f679-41b5-bc05-9092b4c717b2)

### Module Tiers
![compta365_tiers_client_liste](https://github.com/neuronessolutions/compta365/assets/102873102/7718d615-0e67-431c-bff5-3c10af0a90b6)


![compta365_Tiers_autres_liste](https://github.com/neuronessolutions/compta365/assets/102873102/bcf503b0-262e-4c71-9e05-38fc03d3717f)

### Module Transactions
![compta365_transactions_liste](https://github.com/neuronessolutions/compta365/assets/102873102/7614fcdc-50a6-427d-9480-998b9ff7b50e)


![compta365_transactions_details](https://github.com/neuronessolutions/compta365/assets/102873102/55692f23-fcc3-453d-8e09-6a073326dcc1)

### Module Rapports
#### Rapport "Déclarations des taxes"
![compta365_powerbi_declarationtaxes](https://github.com/neuronessolutions/compta365/assets/102873102/00807c27-578e-402f-9c5c-0fc7413140fd)















