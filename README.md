# compta365
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
>Version 2023.09.16 :
>* Création du modèle de base
>* Création des liens du modèle de base
>* Structure détaillée des tables du modèle de base
  
# Description du modèle de données

![Modèle de données](https://github.com/nuage365/compta365/assets/102873102/71659a8a-e4d0-469f-b8a5-bde782029a21)

# Liens entre les différentes entités du modèle

![2](https://github.com/nuage365/compta365/assets/102873102/308e7cb0-cae7-4230-b0b1-4f538936fdc7)

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

# Documentation de la solution Compta365
