---
title: "Préparer l’installation de sites | Microsoft Docs"
description: "Lisez les informations ci-dessous pour gagner du temps durant l’installation de plusieurs sites et éviter des erreurs."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 0534d1eb587cb01f35d811d72ddfe6ceb07e5b7c

---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>Préparer l’installation de sites System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour préparer dans les meilleures conditions le déploiement d’un ou plusieurs sites System Center Configuration Manager, prenez connaissance des informations contenues dans cet article. Ces étapes peuvent vous faire gagner du temps durant l’installation de plusieurs sites et vous éviter des faux pas qui pourraient vous contraindre à réinstaller un ou plusieurs sites.
 > [!TIP]
 >  Bien que similaires, les scénarios suivants se distinguent de l’installation d’un site System Center Configuration Manager Current Branch :
 > -  **Mise à niveau** : installez System Center Configuration Manager pour effectuer une **mise à niveau** à partir de System Center 2012 Configuration Manager (consultez [Effectuer une mise à niveau vers System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)).
 > -  **Mise à jour** : utilisez les mises à jour dans la console pour installer une nouvelle **version de mise à jour** sur un site System Center Configuration Manager existant (consultez [Mises à jour pour System Center Configuration Manager](../../../../core/servers/manage/updates.md)).
 > -  **Migration** : pour **migrer des données** d’une autre hiérarchie Configuration Manager vers une hiérarchie System Center Configuration Manager active, consultez [Planification de la migration vers System Center Configuration Manager](../../../../core/migration/planning-for-migration.md).



## <a name="a-namebkmkoptionsa-options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a> Options d’installation de différents types de sites
Quand vous installez une nouvelle version de Configuration Manager, la version des fichiers sources que vous pouvez utiliser dépend de la version des sites qui se trouvent déjà dans la hiérarchie (le cas échéant), et les méthodes d’installation disponibles dépendent du type de site que vous souhaitez installer.  

Avant d’installer des sites, veillez à élaborer le plan de votre hiérarchie et à déterminer le type de site que vous voulez installer. Pour plus d’informations, consultez [Concevoir une hiérarchie de sites](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### <a name="first-site"></a>Premier site
Le premier site que vous installez pour une hiérarchie doit être un site principal autonome ou un site d’administration centrale.

**Média d’installation** : pour installer un site d’administration centrale ou un site principal autonome comme premier site d’une nouvelle hiérarchie, vous devez [utilisent une version de référence](../../../../core/servers/manage/updates.md#bkmk_Baselines) de Configuration Manager. N’installez pas le premier site d’une nouvelle hiérarchie en utilisant les fichiers sources mis à jour extraits du [dossier CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) d’un site quelconque.

**Méthode d’installation** : vous pouvez installer l’un ou l’autre de ces types de site en vous aidant de l’[Assistant Installation de Configuration Manager](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md). Vous pouvez aussi configurer un script à utiliser avec une [installation scriptée en ligne de commande](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Sites supplémentaires
Après avoir installé le site initial, vous pouvez à tout moment ajouter d’autres sites. Les options suivantes permettent d’ajouter des sites supplémentaires (jusqu’aux [limites autorisées](../../../../core/plan-design/configs/size-and-scale-numbers.md)) :

Site existant          |Autres sites pouvant être installés  
---------                   |---------
Site d'administration centrale |   Site principal enfant            
Site principal enfant          |   Installer un site secondaire        
Site principal autonome    |   Installer un site secondaire<br />Développez le site principal, qui convertit le site principal autonome en site principal enfant

**Média d’installation** : quand vous installez un site d’administration centrale pour étendre un site principal autonome, ou que vous installez un nouveau site principal enfant dans une hiérarchie existante, vous devez utiliser le média d’installation (fichiers sources) qui correspondent à la version du ou des sites existants.
> [!IMPORTANT]
> Si vous avez installé des mises à jour dans la console qui ont changé la version des sites installés précédemment, n’utilisez pas le média d’installation d’origine et utilisez à la place les fichiers sources du [dossier CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) d’un site mis à jour.  Configuration Manager vous impose d’utiliser des fichiers sources qui correspondent à la version du site existant auquel votre nouveau site doit se connecter.


Un site secondaire doit être installé à partir de la console Configuration Manager et s’installe donc toujours en utilisant les fichiers sources du site principal parent.

**Méthode d’installation** : la méthode que vous utilisez pour installer des sites supplémentaires dépend du type de site que vous voulez installer.
-   **Ajout d’un site d’administration centrale** :  
Vous pouvez utiliser l’Assistant Installation de Configuration Manager ou une ligne de commande scriptée pour installer le nouveau site d’administration centrale comme site parent de votre site principal autonome existant.  Pour plus d’informations, consultez [Étendre un site principal autonome](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
-   **Ajout d’un site principal enfant** :  
Vous pouvez utiliser l’Assistant Installation de Configuration Manager ou une installation en ligne de commande pour ajouter un site principal enfant sous un site d’administration centrale.
-   **Ajout d’un site secondaire** :   
Vous devez utiliser la console Configuration Manager pour installer un site secondaire comme site enfant sous un site principal. Les autres méthodes ne sont pas prises en charge pour les sites secondaires.



## <a name="a-namebkmktasksa--common-tasks-to-complete-before-starting-an-install"></a><a name="bkmk_tasks"></a>  Tâches courantes à effectuer avant de démarrer une installation
-   Déterminer la topologie de la hiérarchie que vous allez utiliser pour votre déploiement    
     (voir [Concevoir une hiérarchie de sites pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md))  

-   Préparer et configurer des serveurs individuels pour respecter lesprérequis et les configurations prises en charge en vue d’une utilisation avec Configuration Manager (voir [Prérequis des sites et systèmes de site](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md))  

-   Installer et configurer SQL Server pour héberger la base de données du site (voir    
    [Prise en charge des versions de SQL Server pour System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md))  

-   Préparer votre environnement réseau pour prendre en charge Configuration Manager (voir [Configurer les pare-feu, les ports et les domaines à préparer pour Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains))  

-   Si vous prévoyez d’utiliser une infrastructure à clé publique (PKI), préparer votre infrastructure et vos certificats (voir [Configuration requise des certificats PKI pour Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md))

-   Installer les dernières mises à jour de sécurité sur les ordinateurs que vous devez utiliser comme serveurs de site ou serveurs de système de site et les redémarrer si nécessaire



## <a name="a-namebkmksitecodesa--about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a>  À propos des noms de site et des codes de site
Les codes de site et les noms de site permettent d’identifier et de gérer les sites dans une hiérarchie Configuration Manager. Dans la console Configuration Manager, le code de site et le nom de site s’affichent au format &lt;code de site\> - &lt;nom de site\>. Chaque code de site que vous utilisez dans votre hiérarchie doit être unique. Si le schéma Active Directory est étendu pour Configuration Manager et que des sites publient des données, les codes de site utilisés dans une forêt Active Directory doivent être uniques, même s’ils sont utilisés dans une autre hiérarchie Configuration Manager ou s’ils ont été utilisés dans des installations précédentes de Configuration Manager. Veillez à planifier correctement vos codes et noms de site avant de déployer votre hiérarchie.

### <a name="specify-a-site-code-and-site-name"></a>Spécifier un code de site et un nom de site
Pendant l’installation de Configuration Manager, vous devez indiquer un code de site et un nom de site pour le site d’administration centrale et pour l’installation de chaque site principal et secondaire. Le code de site est destiné à identifier chaque site de façon unique dans la hiérarchie. Comme le code de site est utilisé dans les noms de dossier, n’utilisez jamais les noms suivants en guise de code de site, notamment les noms réservés à Configuration Manager et à Windows :
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> Le programme d’installation de Configuration Manager ne vérifie pas que le code de site que vous spécifiez n’est pas déjà utilisé.



Pour entrer le code de site pour un site pendant l’installation de Configuration Manager, vous devez entrer trois caractères alphanumériques. Les caractères valides pour les codes de site sont les lettres de A à Z et les chiffres de 0 à 9, ou une combinaison de ces chiffres et lettres. La séquence de lettres ou de chiffres n'influe en rien sur la communication entre les sites. Par exemple, il n'est pas nécessaire de nommer un site principal ABC et un site secondaire DEF.

Le nom du site est un identificateur de nom convivial pour ce site. Utilisez uniquement les caractères standard, de A à Z, de a à z et de 0 à 9, ainsi que le tiret (-) dans les noms des sites.
> [!IMPORTANT]
> La modification du code de site ou du nom de site n'est pas autorisée.

### <a name="reuse-a-site-code"></a>Réutiliser un code de site
Les codes de site ne peuvent pas être utilisés plusieurs fois dans une hiérarchie Configuration Manager pour un site d’administration centrale ou un site principal, même si le site et le code de site d’origine ont été désinstallés. Si vous réutilisez un code de site, vous risquez d’avoir des conflits d’ID d’objet dans votre hiérarchie. Vous pouvez réutiliser le code de site d’un site secondaire si ce site secondaire et le code de site ne sont plus utilisés dans votre hiérarchie Configuration Manager ou dans la forêt Active Directory.


## <a name="limits-and-restrictions-for-installed-sites"></a>Limites et restrictions concernant les sites installés
Avant d’installer des sites, tenez compte des limitations suivantes qui s’appliquent aux sites et aux hiérarchies :
-   Une fois l’installation terminée, vous ne pouvez modifier les propriétés suivantes du site qu’en désinstallant le site et en le réinstallant avec les nouvelles valeurs :  
    -   Répertoire d’installation des fichiers programmes  
    -   Code de site  
    -   Description du site  
-   Si votre hiérarchie comprend un site d’administration centrale :  
    -   Configuration Manager ne permet pas de retirer un site principal enfant d’une hiérarchie pour en faire un site principal autonome ou pour le rattacher à une autre hiérarchie. Au lieu de cela, vous devez désinstaller le site principal enfant et le réinstaller comme nouveau site principal autonome ou enfant du site d’administration centrale d’une autre hiérarchie.  


## <a name="a-namebkmkoptionalstepsa--optional-steps-to-run-before-starting-setup"></a><a name="bkmk_optionalsteps"></a>  Étapes facultatives à exécuter avant de lancer l’installation
**Vous pouvez exécuter manuellement le [téléchargeur d’installation](../../../../core/servers/deploy/install/setup-downloader.md)** pour télécharger les fichiers d’installation mis à jour pour Configuration Manager.

Si l’ordinateur sur lequel vous voulez exécuter le programme d’installation n’est pas connecté à Internet, ou si vous prévoyez d’installer plusieurs serveurs de site, utilisez le téléchargeur d’installation pour télécharger les mises à jour requises des fichiers d’installation :

-  Par défaut, le programme d’installation se connecte à Internet pour télécharger les fichiers d’installation mis à jour.
-  Par défaut, les fichiers sont stockés dans un dossier nommé Redist.
-  Vous pouvez diriger le programme d’installation vers un emplacement sur votre réseau où vous avez précédemment stocké une copie de ces fichiers.


**Vous pouvez exécuter manuellement l’[outil de vérification des conditions préalables](../../../../core/servers/deploy/install/prerequisite-checker.md)** pour identifier et résoudre les problèmes avant d’exécuter le programme d’installation. Avant de démarrer le programme d’installation pour installer un site, et avant d’installer un rôle de système de site sur un serveur, vous pouvez exécuter l’outil de vérification des conditions préalables pour vous assurer que l’ordinateur présente la configuration requise pour héberger le site ou le rôle de système de site.
 -  Par défaut, le programme d’installation exécute l’outil de vérification des conditions préalables.
 -  En cas d’erreurs, le programme d’installation s’arrête jusqu’à ce que le problème soit résolu.


**Identifiez des ports facultatifs** à utiliser pour les clients et les systèmes de site.
 -  Par défaut, les systèmes de site et les clients utilisent des ports prédéfinis pour communiquer.
 -  Pendant l’installation, vous pouvez configurer d’autres ports.
 -  Pour plus d’informations, consultez [Ports utilisés dans System Center Configuration Manager](../../../../core/plan-design/hierarchy/ports.md).



<!--HONumber=Dec16_HO3-->


