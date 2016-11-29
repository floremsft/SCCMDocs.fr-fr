---
title: "Prérequis pour les sites | System Center Configuration Manager"
description: "Découvrez les différents prérequis liés à l’installation des différents types de sites System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bf3b1e4d87a972f530590bf94e38a5ec66c4fc9a

---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>Prérequis à l’installation de sites System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Les sections suivantes fournissent des informations sur les différents prérequis liés à l’installation des différents types de sites System Center Configuration Manager.



## <a name="primary-sites-and-the-central-administration-site"></a>Sites principaux et site d’administration centrale
Les prérequis suivants s’appliquent à l’installation d’un site d’administration centrale en tant que premier site d’une hiérarchie, site principal autonome ou site principal enfant. Si vous installez un site d’administration centrale dans le cadre d’un scénario d’extension de hiérarchie, consultez [Développement d’un site principal autonome](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand
) dans cette rubrique.

####  <a name="a-namebkmkprereqpria-prerequisites-to-install-a-primary-site-or-central-administration-site"></a><a name="bkmk_PrereqPri"></a> Prérequis à l’installation d’un site principal ou d’un site d’administration centrale  

-   Pour installer le site, l’utilisateur doit disposer des autorisations suivantes :  

    -   **Administrateur local** sur l’ordinateur serveur de site  

    -   **Administrateur local** sur chaque ordinateur devant héberger la **base de données du site** ou une instance de **SMS_Provider** pour le site  

    -   **Sysadmin** sur l’instance de SQL Server qui héberge la base de données du site  

        > [!IMPORTANT]  
        >  Une fois l'installation terminée, le compte d'utilisateur qui exécute le programme d'installation et le compte d'ordinateur du serveur de site doivent tous deux conserver des droits d'administrateur système sur SQL Server. La suppression des droits d'administrateur système de ces comptes n'est pas prise en charge.  

-   Lors de l’installation d’un site principal, les autorisations supplémentaires suivantes sont nécessaires :  
    -  **Administrateur local** sur les autres ordinateurs où vous allez installer le point de gestion initial et le point de distribution (si ce n’est pas sur le serveur de site)  

-   Pour installer un nouveau site principal enfant sous un site d’administration centrale, les autorisations supplémentaires suivantes sont nécessaires :  

    -   **Administrateur local** sur l’ordinateur hébergeant le site d’administration centrale  

    -   Autorisations d’administration basée sur des rôles dans Configuration Manager, qui équivalent au rôle de sécurité **Administrateur d’infrastructure** ou **Administrateur complet**.  

-   Vous devez utiliser le média d’installation correct (fichiers sources) et exécutez le programme d’installation à partir de cet emplacement. Pour plus d’informations sur les fichiers sources adéquats à utiliser pour installer différents sites, consultez [Options d’installation des différents types de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) dans la rubrique [Préparer l’installation des sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md).

-   L’ordinateur serveur de site doit avoir accès aux fichiers d’installation mis à jour de Microsoft :
    -  Avant de commencer l’installation, vous pouvez télécharger et stocker une copie de ces fichiers sur votre réseau local à l’aide du [téléchargeur d’installation](../../../../core/servers/deploy/install/setup-downloader.md).
    -  Si une copie locale de ces fichiers n’est pas disponible, le serveur de site doit avoir accès à Internet afin de pouvoir télécharger ces fichiers depuis Microsoft lors de l’installation.

  - Pour pouvoir étendre un site principal autonome ayant un rôle de système de site Point de connexion de service installé, vous devez désinstaller le point de connexion de service. Une seule instance de ce rôle est autorisée dans une hiérarchie, et uniquement sur le site de niveau supérieur de la hiérarchie. Vous avez la possibilité de réinstaller le rôle lors de l’installation du site d’administration centrale.
  - Le serveur de site et les ordinateurs de base de données du site doivent présenter toutes les configurations prévues dans les conditions préalables. Avant de démarrer l’installation, vous pouvez [exécuter manuellement l’outil de vérification de la configuration requise](../../../../core/servers/deploy/install/prerequisite-checker.md) pour identifier et résoudre les problèmes.  


## <a name="a-namebkmkexpanda-expanding-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Développement d’un site principal autonome
Un site principal autonome doit remplir les conditions préalables suivantes pour pouvoir être développé dans une hiérarchie constituée d'un site d'administration centrale :


-   **Vous devez installer le nouveau site d’administration centrale à l’aide du support d’installation (fichiers sources) qui correspond à la version du site principal autonome :**  
     Pour garantir la correspondance de la version, installez le nouveau site en utilisant les fichiers sources figurant dans le [dossier CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) sur le site principal autonome.

     Pour plus d’informations sur les fichiers sources adéquats à utiliser pour installer différents sites, consultez [Options d’installation des différents types de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) dans la rubrique [Préparer l’installation des sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md).


-   **Le site principal autonome ne peut pas être configuré pour faire migrer les données d’une autre hiérarchie Configuration Manager :**  

     Vous devez arrêter la migration active vers le site principal autonome, depuis d’autres hiérarchies Configuration Manager, puis supprimer toutes les configurations pour la migration. Sont incluses les tâches de migration qui ne sont pas terminées, la collecte des données et la configuration de la hiérarchie source active.  

     En effet, les opérations de migration sont effectuées par le site de niveau supérieur de la hiérarchie et les configurations à faire migrer ne sont pas transférées au site d’administration centrale quand vous développez un site principal autonome.  

     Après avoir développé le site principal autonome, si vous reconfigurez la migration sur le site principal, c'est le site d'administration centrale qui assure les opérations liées à la migration. Pour plus d’informations sur la configuration de la migration, consultez [Configuration des hiérarchies sources et des sites sources pour la migration vers System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **Le compte de l’ordinateur appelé à héberger le nouveau site d’administration centrale doit être membre du groupe Administrateurs sur le site principal autonome :**  

     Pour développer correctement le site principal autonome, le compte d'ordinateur du nouveau site d'administration centrale doit être membre du groupe **Administrateurs** du site principal autonome. Cela est nécessaire uniquement pendant le développement du site. Le compte peut être supprimé du groupe du site principal dès lors que le développement du site est terminé.  

-   **Le compte d’utilisateur qui exécute le programme d’installation pour installer le nouveau site d’administration centrale doit disposer des autorisations d’administration basée sur les rôles au niveau du site principal autonome :**  

     Pour installer un site d'administration centrale dans le cadre d'un scénario d'extension de site, le compte d'utilisateur qui exécute le programme d'installation pour installer le site d'administration centrale doit être défini dans une administration basée sur les rôles sur le site principal autonome en tant que **Administrateur complet** ou **Administrateur d'infrastructure**.  

-   **Pour pouvoir développer le site, vous devez désinstaller les rôles système de site suivants du site principal autonome :**  

    -   Point de synchronisation Asset Intelligence  

    -   Point Endpoint Protection  

    -   point de connexion de service  

     Ces rôles de système de site sont pris en charge uniquement sur le site de niveau supérieur de la hiérarchie. Par conséquent, vous devez désinstaller ces rôles système de site avant de développer le site principal autonome. Une fois le site développé, vous pouvez réinstaller ces rôles de système de site sur le site d'administration centrale.  

    Tous les autres rôles de système de site peuvent rester installés sur le site principal.  

-   **Le port pour SQL Server Service Broker doit être ouvert entre le site principal autonome et l’ordinateur qui va installer le site administration centrale :**  

     Pour répliquer correctement des données entre un site d’administration centrale et un site principal, Configuration Manager requiert qu’un port qui sera utilisé par SQL Server Service Broker soit ouvert entre les deux sites. Lorsque vous installez une administration centrale et développez un site principal autonome, la vérification des prérequis n'établit pas que le port que vous spécifiez pour SQL Server Service Broker est ouvert sur le site principal.  


## <a name="a-namebkmksecondarya-secondary-sites"></a><a name="bkmk_secondary"></a> Sites secondaires
Voici les prérequis à l’installation des sites secondaires :
-   L’utilisateur administratif qui configure l’installation du site secondaire dans la console Configuration Manager doit posséder des droits d’administration basés sur des rôles qui équivalent au rôle de sécurité **Administrateur d’infrastructure** ou **Administrateur complet**.  

-   Le compte d’ordinateur du site principal parent doit avoir des droits **Administrateur local** sur l’ordinateur serveur du site secondaire.  

-   Lorsque le site secondaire utilise une instance précédemment installée de SQL Server pour héberger la base de données du site secondaire :  

    -   Le **compte d’ordinateur** du site principal parent doit disposer des droits d’administrateur système ( **sysadmin** ) sur l’instance de SQL Server exécutée sur l’ordinateur serveur de site secondaire.  

    -   Le compte **Système local** de l’ordinateur serveur de site secondaire doit disposer des droits d’administrateur système ( **sysadmin** ) sur l’instance de SQL Server exécutée sur cet ordinateur.  

        > [!IMPORTANT]  
        >  Une fois l’installation terminée, les deux comptes doivent conserver les droits d’administrateur système (sysadmin) sur SQL Server. La suppression des droits d'administrateur système de ces comptes n'est pas prise en charge.  

-   L’ordinateur serveur de site secondaire doit présenter toutes les configurations requises, ce qui inclut SQL Server et les rôles de système de site par défaut du point de gestion et du point de distribution.  



<!--HONumber=Nov16_HO1-->


