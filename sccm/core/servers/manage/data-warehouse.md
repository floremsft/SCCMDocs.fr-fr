---
title: "Entrepôt de données | Microsoft Docs"
description: "Base de données et point de service de l’entrepôt de données pour System Center Configuration Manager"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: eedbf12d3bf628666efc90c85a8dfab37e4dc9ab
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>Point de service de l’entrepôt de données pour System Center Configuration Manager
*S’applique à : System Center Configuration Manager (Current Branch)*

Depuis la version 1702, vous pouvez utiliser le point de service de l’entrepôt de données pour stocker des données d’historique à long terme et créer des rapports sur celles-ci pour votre déploiement de Configuration Manager.

> [!TIP]
> Le point de service de l’entrepôt de données est une fonctionnalité en préversion introduite dans la version 1702. Pour savoir comment l’activer, voir [Fonctionnalités en préversion dans System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

> À compter de la version 1706, cette fonctionnalité n’est plus une fonctionnalité en préversion.

L’entrepôt de données prend en charge jusqu’à 2 To de données, avec des horodatages pour le suivi des modifications. Pour stocker des données, vous utilisez des synchronisations automatisées entre la base de données du site Configuration Manager et la base de données de l’entrepôt de données. Ces informations sont ensuite accessibles à partir de votre point de Reporting Services. Les données qui sont synchronisées avec la base de données de l’entrepôt de données sont conservées pendant trois ans. Périodiquement, une tâche intégrée supprime les données datant de plus de trois ans.

Les données synchronisées incluent les éléments suivants, qui proviennent des groupes des données de site et des données globales :
- Intégrité de l’infrastructure
- Sécurité
- Compatibilité
- Programme malveillant   
- Déploiements de logiciels
- Détails d’inventaire (toutefois, l’historique d’inventaire n’est pas synchronisé)

Une fois installé, le rôle de système de site installe et configure la base de données de l’entrepôt de données. Il installe également plusieurs rapports, afin que vous puissiez facilement rechercher ces données et créer des rapports les concernant.



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>Conditions préalables pour le point de service de l’entrepôt de données
- Le rôle de système de site d’entrepôt de données est pris en charge uniquement sur le site de niveau supérieur de la hiérarchie. (Un site d’administration centrale ou site principal autonome.)
- L’ordinateur sur lequel vous installez le rôle de système de site nécessite .NET Framework 4.5.2 ou version ultérieure.
- Le compte de l’ordinateur sur lequel vous installez le rôle de système de site est utilisé pour synchroniser les données avec la base de données de l’entrepôt de données. Ce compte nécessite les autorisations suivantes :  
  - des autorisations de niveau **administrateur local** sur l’ordinateur qui hébergera la base de données de l’entrepôt de données ;
  - des autorisations **DB_owner** la base de données de l’entrepôt de données.
  - des autorisations **DB_reader** et **execute** sur la base de données des sites de niveau supérieur.
- La base de données de l’entrepôt de données nécessite l’utilisation de SQL Server 2012 ou version ultérieure. L’édition peut être Standard, Entreprise ou Datacenter.
- Les configurations de SQL Server suivantes sont prises en charge pour héberger la base de données de l’entrepôt :  
  - Une instance par défaut
  - Instance nommée
  - Groupe de disponibilité SQL Server AlwaysOn
  - Cluster de basculement SQL Server
-   Quand la base de données de l’entrepôt de données ne se trouve pas au même emplacement que la base de données du serveur de site, vous devez disposer d’une licence distincte pour chaque instance de SQL Server qui héberge la base de données.
- Si vous utilisez des [vues distribuées](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews), le rôle de système de site de point de service de l’entrepôt de données doit être installé sur le serveur qui héberge la base de données de site des sites d’administration centrale.



> [!IMPORTANT]  
> L’entrepôt de données n’est pas pris en charge lorsque l’ordinateur qui exécute le point de service de l’entrepôt de données ou qui héberge la base de données de l’entrepôt de données exécute l’une des langues suivantes :
> - JPN – Japonais
> - KOR – Coréen
> - CHS – Chinois simplifié
> - CHT – Chinois traditionnel Ce problème sera résolu dans une version à venir.


## <a name="install-the-data-warehouse"></a>Installer l’entrepôt de données
Chaque hiérarchie prend en charge une seule instance de ce rôle, sur n’importe quel système de site du site de niveau supérieur. L’instance SQL Server qui héberge la base de données de l’entrepôt peut être locale ou distante par rapport au rôle de système de site. Bien que l’entrepôt de données fonctionne avec le point de Reporting Services installé sur le même site, il n’est pas nécessaire d’installer les deux rôles de système de site sur le même serveur.   

Pour installer le rôle, vous pouvez utiliser deux assistants : **l’Assistant Ajout des rôles de système de site** ou **l’Assistant Création d’un serveur de système de site**. Pour plus d’informations, consultez [Installer des rôles de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles).  

Quand vous installez le rôle, Configuration Manager crée la base de données de l’entrepôt de données pour vous sur l’instance de SQL Server que vous spécifiez. Si vous spécifiez le nom d’une base de données existante (comme vous le feriez si vous [déplaciez la base de données de l’entrepôt de données vers un nouveau serveur SQL Server](#move-the-data-warehouse-database)), Configuration Manager ne crée pas une base de données, mais utilise à la place celle que vous spécifiez.

### <a name="configurations-used-during-installation"></a>Configurations utilisées lors de l’installation
Page **Sélection du rôle système** :  

Page **Général** :
-   **Paramètres de connexion de la base de données de l’entrepôt de données Configuration Manager** :
 - **Nom de domaine complet de SQL Server** :  
 spécifiez le nom de domaine complet (FQDN) du serveur qui héberge le point de service de l’entrepôt de données et la base de données.
 - **Nom d’instance SQL Server, le cas échéant** :   
 si vous n’utilisez pas une instance par défaut de SQL Server, vous devez spécifier l’instance utilisée.
 - **Nom de la base de données** :   
 indiquez le nom de la base de données de l’entrepôt de données. Le nom de la base de données ne doit pas dépasser 10 caractères. (La longueur du nom prise en charge sera augmentée dans une version ultérieure.)
 Configuration Manager crée la base de données de l’entrepôt de données en lui donnant ce nom. Si vous spécifiez un nom de base de données qui existe déjà sur l’instance de SQL Server, Configuration Manager utilise cette base de données.
 - **Port SQL Server utilisé pour la connexion** :   
 spécifiez le numéro de port TCP/IP configuré pour l’instance SQL Server qui héberge la base de données de l’entrepôt de données. Ce port est utilisé par le service de synchronisation de l’entrepôt de données pour se connecter à la base de données de ce dernier.  

Page **Calendrier des synchronisations** :   
- **Calendrier des synchronisations** :
 - **Heure de début** :  
 indiquez l’heure de début de la synchronisation de l’entrepôt de données.
 - **Périodicité** :
    - **Tous les jours** : permet d’indiquer que la synchronisation doit s’exécuter chaque jour.
    - **Hebdomadaire** : permet de spécifier une seule journée chaque semaine ainsi qu’une périodicité hebdomadaire pour la synchronisation.

## <a name="reporting"></a>Rapports
Une fois que vous avez installé un point de service de l’entrepôt de données, plusieurs rapports sont disponibles sur le point de Reporting Services installé sur le même site. Si vous installez le point de service de l’entrepôt de données avant d’installer un point de Reporting Services, les rapports sont automatiquement ajoutés lorsque vous installez le point de Reporting Services.

Le rôle de système de site de l’entrepôt de données inclut les rapports suivants, qui appartiennent à la catégorie **Entrepôt de données** :
 - **Déploiement de l’application - Historique** :   
 Affiche les détails du déploiement d’application pour une application et un ordinateur spécifiques.
 - **Endpoint Protection et Compatibilité des mises à jour logicielles - Historique** : affiche les ordinateurs sur lesquels des mises à jour logicielles n’ont pas été effectuées.  
 - **Inventaire matériel général - Historique** :   
 Affiche tout l’inventaire matériel pour un ordinateur spécifique.
 - **Inventaire logiciel général - Historique** :   
 Affiche tout l’inventaire logiciel pour un ordinateur spécifique.
 - **Vue d'ensemble de l'intégrité de l'infrastructure - Historique** :  
 affiche une vue d’ensemble de l’intégrité de votre infrastructure Configuration Manager.
 - **Liste des programmes malveillants détectés - Historique** :    
 Affiche les programmes malveillants qui ont été détectés dans l’organisation.
 - **Résumé de la distribution de logiciels - Historique** :   
 Synthèse de la distribution de logiciels pour une publication et un ordinateur spécifiques.


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>Étendre un site principal autonome existant vers une hiérarchie
Avant d’installer un site d’administration centrale pour développer un site principal autonome existant, vous devez désinstaller le rôle de point de service de l’entrepôt de données. Après avoir installé le site d’administration centrale, vous pouvez installer le rôle de système de site sur ce site.  

Contrairement au déplacement de la base de données de l’entrepôt de données, cette modification entraîne une perte des données historiques que vous avez synchronisées sur le site principal. La sauvegarde de la base de données depuis le site principal et sa restauration sur le site d’administration centrale ne sont pas prises en charge.




## <a name="move-the-data-warehouse-database"></a>Déplacer la base de données de l’entrepôt de données
Procédez comme suit pour déplacer la base de données de l’entrepôt de données vers un nouveau serveur SQL Server :

1.  Utilisez SQL Server Management Studio pour sauvegarder la base de données de l’entrepôt de données. Ensuite, restaurez cette base de données sur un serveur SQL Server sur le nouvel ordinateur qui héberge l’entrepôt de données.   
> [!NOTE]     
> Après avoir restauré la base de données sur le nouveau serveur, vérifiez que les autorisations d’accès à la base de données sont les mêmes sur la nouvelle base de données de l’entrepôt de données que sur la base de données de l’entrepôt de données d’origine.  

2.  Utilisez la console Configuration Manager pour supprimer du serveur actuel le rôle de système de site du point de service de l’entrepôt de données.
3.  Réinstallez le point de service de l’entrepôt de données et spécifiez le nom du nouveau serveur SQL Server et de l’instance qui héberge la base de données de l’entrepôt de données que vous avez restaurée.
4.  Une fois le rôle de système de site installé, le déplacement est terminé.

## <a name="troubleshooting-data-warehouse-issues"></a>Résolution des problèmes relatifs à l’entrepôt de données
**Fichiers journaux** :  
utilisez les journaux suivants pour examiner les problèmes d’installation du point de service de l’entrepôt de données ou de synchronisation des données :
 - *DWSSMSI.log* et *DWSSSetup.log* : utilisez ces journaux pour examiner les erreurs survenues lors de l’installation du point de service de l’entrepôt de données.
 - *Microsoft.ConfigMgrDataWarehouse.log* : utilisez ce journal pour examiner la synchronisation des données entre la base de données de site et la base de données de l’entrepôt de données.

**Échec d’installation**  
 L’installation du point de service de l’entrepôt de données échoue sur un serveur de système de site distant quand le premier rôle de système de site installé sur cet ordinateur est celui de l’entrepôt de données.  
  - **Solution** :   
    Assurez-vous que l’ordinateur sur lequel vous installez le point de service de l’entrepôt de données héberge au moins un autre rôle de système de site.  


**Problèmes de synchronisation connus**   
La synchronisation échoue et génère le message suivant dans le fichier *Microsoft.ConfigMgrDataWarehouse.log* : **« Impossible de remplir des objets de schéma ».**  
 - **Solution** :  
    Assurez-vous que le compte de l’ordinateur qui héberge le rôle de système de site est bien **db_owner** sur la base de données de l’entrepôt de données.

Les rapports de l’entrepôt de données ne s’ouvrent pas lorsque la base de données de l’entrepôt de données et le point de Reporting Services se trouvent sur des systèmes de site différents.  

 - **Solution** :  
    Accordez au **compte du point de Reporting Services** l’autorisation d’accès **db_datareader** à la base de données de l’entrepôt de données.

Lorsque vous ouvrez un rapport de l’entrepôt de données, l’erreur suivante est renvoyée :

*Une erreur s’est produite lors du traitement du rapport. (rsProcessingAborted) Impossible de créer une connexion à la source de données 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection) Une connexion a été établie avec le serveur, mais une erreur s’est ensuite produite pendant la négociation préalable à l’ouverture de session. (Fournisseur : fournisseur SSL, erreur : 0 - La chaîne de certificats a été fournie par une autorité qui n’est pas approuvée.)*

- **Solution** : procédez comme suit pour configurer les certificats.

  1. Sur l’ordinateur qui héberge la base de données de l’entrepôt de données :

    1. Ouvrez IIS, cliquez sur **Certificats de serveur**, puis cliquez avec le bouton droit sur **Créer un certificat auto-signé** et spécifiez le « nom convivial » du nom du certificat en tant que **certificat d’identification SQL Server de l’entrepôt de données**. Sélectionnez le magasin de certificats en tant que **Applications personnelles**.
    2. Ouvrez le **Gestionnaire de configuration SQL Server**. Sous **Configuration du réseau SQL Server**, cliquez avec le bouton droit pour sélectionner **Propriétés** sous **Protocoles pour MSSQLSERVER**. Ensuite, sur l’onglet **Certificat**, sélectionnez le **certificat d’identification SQL Server de l’entrepôt de données** et enregistrez les modifications.  
    3. Ouvrez le **Gestionnaire de configuration SQL Server**. Sous **Services SQL Server**, redémarrez le **service SQL Server** et le **Reporting Service**.
    4.  Ouvrez la console MMC (Microsoft Management Console) et ajoutez le composant logiciel enfichable relatif aux **certificats**, puis sélectionnez la gestion du certificat pour le **compte d’ordinateur** de la machine locale. Ensuite, dans la console MMC, développez le dossier **Applications personnelles** > **Certificats** et exportez le **certificat d’identification SQL Server de l’entrepôt de données** en tant que fichier **Binaire codé DER X.509 (.cer)**.    
  2.    Sur l’ordinateur qui héberge SQL Server Reporting Services, ouvrez la console MMC et ajoutez le composant logiciel enfichable **Certificats**. Ensuite, sélectionnez la gestion du certificat pour le **Compte d’ordinateur**. Sous le dossier **Autorités de certification racine reconnues**, importez le **certificat d’identification SQL Server de l’entrepôt de données**.


## <a name="data-warehouse-dataflow"></a>Flux de données de l’entrepôt de données   
![Flux_entrepôtdedonnées](./media/datawarehouse.png)

**Synchronisation et stockage des données**

| Étape   | Détails  |
|:------:|-----------|  
| **1**  |  Le serveur de site transfère et stocke les données dans la base de données de site.  |  
| **2**  |      Selon sa planification et de sa configuration, le point de service de l’entrepôt de données obtient des données de la base de données de site.  |  
| **3**  |  Le point de service de l’entrepôt de données transfère et stocke une copie des données synchronisées dans la base de données de l’entrepôt de données. |  
**Rapports**

| Étape   | Détails  |
|:------:|-----------|  
| **A**  |  Via des rapports intégrés, un utilisateur demande des données. La demande est transmise au point de Reporting Services à l’aide de SQL Server Reporting Services. |  
| **B**  |      La plupart des rapports concernent des informations actuelles et ces demandes sont exécutées sur la base de données de site. |  
| **C**  | Quand un rapport demande des données d’historique, à l’aide de l’un des rapports avec la *Catégorie* **Entrepôt de données**, la demande s’exécute sur la base de données de l’entrepôt de données.   |  
