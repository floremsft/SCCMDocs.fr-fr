---
title: "Changements par rapport à Configuration Manager 2012 | System Center Configuration Manager "
description: "Identifiez les changements et les nouvelles fonctionnalités de System Center Configuration Manager par rapport à System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: 51
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f3b68fb17920b0abacc1428c8763ec8c06e6b22


---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>Changements dans System Center Configuration Manager par rapport à System Center 2012 Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 La branche CB (Current Branch) de System Center Configuration Manager présente des changements importants par rapport à System Center 2012 Configuration Manager. Les informations contenues dans cette rubrique identifient les changements les plus importants et les nouvelles fonctionnalités dans la version de base de référence 1511 de System Center Configuration Manager. Pour en savoir plus sur les autres changements introduits dans les mises à jour suivantes pour System Center Configuration Manager, consultez [Nouveautés dans les versions incrémentielles de System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).



 La version de décembre 2015 de System Center Configuration Manager (version 1511) est la dernière version du produit Configuration Manager de Microsoft.   Elle est généralement désignée sous le nom de « Current Branch » de System Center Configuration Manager. *Current Branch* indique qu’il s’agit d’une version qui prend en charge les mises à jour incrémentielles apportées au produit et peut représenter une distinction importante entre cette version et les versions précédentes de Configuration Manager.  

 Avec cette version, System Center Configuration Manager :  

-   N’utilise pas d’identificateur d’année ni de produit dans le nom du produit, comme c’était le cas dans les versions précédentes telles que Configuration Manager 2007 ou System Center 2012 Configuration Manager.

-   Prend en charge les mises à jour incrémentielles dans le produit, aussi appelées versions de mise à jour. La version initiale est la version 1511. Les versions suivantes sont publiées plusieurs fois par an comme mises à jour dans la console, telles que la version 1602 ou 1606.




##  <a name="a-namebkmkupdatesa-in-console-updates-for-configuration-manager"></a><a name="bkmk_updates"></a> Mises à jour dans la console pour Configuration Manager  
 System Center Configuration Manager utilise une méthode de service dans la console appelée **Mises à jour et maintenance** qui facilite la localisation et l’installation des mises à jour recommandées pour Configuration Manager.  

 Certaines versions disponibles uniquement comme mises à jour pour des sites existants (à partir de la console Configuration Manager) ne peuvent pas être utilisées pour installer de nouveaux sites Configuration Manager.   
Par exemple, la mise à jour 1602 est disponible uniquement à partir de la console Configuration Manager, et utilisée pour mettre à jour un site exécutant une version de base de référence 1511 vers la version 1602.  

Régulièrement, une version de mise à jour sera également disponible comme nouvelle version de base de référence (par exemple, la mise à jour 1606) qui peut être utilisée pour installer une nouvelle hiérarchie sans avoir à démarrer avec une ancienne version de base de référence (comme 1511) et à effectuer une mise à niveau vers la version la plus récente.


 Pour plus d’informations sur l’utilisation des mises à jour, consultez [Mises à jour pour System Center Configuration Manager](../../../core/servers/manage/updates.md).  

##  <a name="a-namebkmkservicepointa-service-connection-point-replaces-microsoft-intune-connector"></a><a name="bkmk_servicepoint"></a> Le point de connexion de service en remplacement du connecteur Microsoft Intune  
 Le **connecteur Microsoft Intune** est remplacé par un nouveau rôle de système de site qui offre des fonctionnalités supplémentaires, à savoir le **point de connexion de service**. Le point de connexion de service :  

-   remplace le connecteur Microsoft Intune quand vous intégrez Intune à la gestion des appareils mobiles locale System Center Configuration Manager  

-   est utilisé comme point de contact pour les appareils que vous gérez avec  

-   charge des données d’utilisation relatives à votre déploiement sur le service cloud Microsoft  

-   met des mises à jour qui s’appliquent à votre déploiement à disposition à partir de la console Configuration Manager  

Ce rôle de système de site prend en charge à la fois un mode en ligne et hors connexion de fonctionnement qui peut affecter ses autres usages. Pour plus d’informations, consultez [À propos du point de connexion de service dans System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

##  <a name="a-namebkmkusagea-usage-data-collection"></a><a name="bkmk_usage"></a> Collecte des données d’utilisation  
 System Center Configuration Manager collecte des données d’utilisation sur vos sites et votre infrastructure. Ces informations sont compilées et transmises au service cloud Microsoft par le point de connexion de service (nouveau rôle de système de site). Configuration Manager en a besoin pour télécharger les mises à jour applicables à la version de Configuration Manager que vous utilisez pour votre déploiement. Au moment de configurer le point de connexion de service, vous pouvez définir le niveau des données collectées et si celles-ci sont envoyées automatiquement (mode en ligne) ou manuellement (mode hors connexion).  

 Pour plus d'informations, consultez [Paramètres et niveaux de données d’utilisation](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

##  <a name="a-namebkmkamta-support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Prise en charge de la technologie Intel AMT (Active Management Technology)  
 Avec System Center Configuration Manager, la prise en charge native des ordinateurs AMT à partir de la console Configuration Manager est supprimée.  

-   Les ordinateurs AMT restent entièrement gérés quand vous utilisez le [module complémentaire Intel SCS pour Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html).  

-   Ce module complémentaire vous permet d’accéder aux dernières fonctionnalités pour gérer AMT tout en supprimant les limitations introduites jusqu’à ce que Configuration Manager puisse intégrer ces changements  

-   La gestion hors bande dans System Center 2012 Configuration Manager n’est pas affectée par cette modification.  

La suppression de la technologie AMT intégrée pour System Center Configuration Manager a la conséquence suivante :  

-   Le rôle de système de site de point de gestion hors bande n’est plus utilisé, ni disponible.  

##  <a name="a-namebkmkouta-deprecated-functionality"></a><a name="bkmk_out"></a> Fonctionnalités déconseillées  
 Avec System Center Configuration Manager, certaines fonctionnalités, telles que la [Prise en charge de la technologie Intel AMT (Active Management Technology)](#bkmk_AMT), sont retirées de la console Configuration Manager, alors que d’autres comme la Protection d’accès réseau sont entièrement retirées. Par ailleurs, certains produits Microsoft plus anciens comme Windows Vista, Windows Server 2008 et SQL Server 2008 ne sont plus pris en charge.  

 Pour obtenir la liste des fonctionnalités dépréciées, consultez [Fonctionnalités supprimées et déconseillées dans System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 Pour plus d’informations sur les produits, les systèmes d’exploitation et les configurations pris en charge, consultez [Configurations prises en charge pour System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md).  

## <a name="client-deployment"></a>Déploiement des clients  
 System Center Configuration Manager inaugure une nouvelle fonctionnalité visant à tester les nouvelles versions du client Configuration Manager avant la mise à niveau du reste du site avec le nouveau logiciel.  Cette nouvelle fonctionnalité vous permet de configurer un regroupement de préproduction dans lequel piloter un nouveau client. Dès lors que vous êtes satisfait du nouveau logiciel client en préproduction, vous pouvez le promouvoir pour mettre automatiquement à niveau le reste du site avec la nouvelle version.  

 Pour plus d’informations sur le test des clients, consultez [Comment tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation  

-   Un nouveau type de séquence de tâches est disponible dans l’Assistant Création d’une séquence de tâches, à savoir  **Mettre à niveau un système d’exploitation à partir du package de mise à niveau**. Celle-ci permet de créer la procédure de mise à niveau des ordinateurs Windows 7, Windows 8 ou Windows 8.1 vers Windows 10.  Pour plus d’informations, voir [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Le cache d’homologue Windows PE est désormais disponible pendant le déploiement de systèmes d’exploitation. Les ordinateurs qui exécutent une séquence de tâches pour le déploiement d’un système d’exploitation peuvent utiliser le cache d’homologue Windows PE pour obtenir le contenu d’un homologue local (source de cache d’homologue) au lieu de télécharger du contenu auprès d’un point de distribution. Cela permet de réduire le trafic du réseau étendu dans les scénarios de succursale où il n'existe aucun point de distribution local. Pour plus d'informations, voir [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

-   Vous pouvez désormais afficher l’état de Windows sous forme de service dans votre environnement, créer des plans de maintenance pour former des boucles de déploiement et vérifier que les ordinateurs CB de Windows 10 sont tenus à jour quand de nouvelles builds sont publiées. Par ailleurs, vous pouvez être alerté quand la prise en charge de la build Current Branch (CB) ou Current Branch for Business (CBB) des clients Windows 10 touche à sa fin. Pour plus d'informations, voir [Gérer Windows as a Service (WaaS) à l’aide de System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

## <a name="application-management"></a>Gestion des applications  

-   System Center Configuration Manager vous permet de déployer des applications de la plateforme Windows universelle pour les appareils exécutant Windows 10 et des versions ultérieures. Consultez [Création d’applications Windows avec System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Le Centre logiciel a été modernisé et les applications qui figuraient uniquement dans le catalogue d’applications (applications accessibles à l’utilisateur) apparaissent désormais dans le Centre logiciel sous l’onglet Applications. Ces déploiements sont ainsi plus identifiables pour les utilisateurs qui n’ont plus besoin d’utiliser le catalogue d’applications. De plus, un navigateur Silverlight n’est plus nécessaire. Consultez [Planifier et configurer la gestion des applications dans System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   Par l’intermédiaire du type d’application MDM, le nouveau Windows Installer vous permet de créer et déployer des applications Windows Installer sur les PC inscrits qui exécutent Windows 10. Consultez [Création d’applications Windows avec System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Quand vous créez une application pour une application iOS interne, vous devez seulement spécifier le fichier d’installation (.ipa) de l’application. Vous n’avez plus besoin de spécifier de fichier de liste de propriétés (.plist) correspondant. Consultez [Création d’applications iOS avec System Center Configuration Manager](../../../apps/get-started/creating-ios-applications.md).  

-   Dans Configuration Manager 2012, pour spécifier un lien vers une application du Windows Store, vous pouviez soit spécifier directement le lien, soit accéder à un ordinateur distant sur lequel l’application était installée. Dans System Center Configuration Manager, vous pouvez toujours entrer directement le lien mais, au lieu d’accéder à un ordinateur de référence, vous pouvez maintenant rechercher l’application directement dans le Store à partir de la console Configuration Manager.  

## <a name="software-updates"></a>Mises à jour logicielles  

-   System Center Configuration Manager peut désormais faire la distinction entre un ordinateur Windows 10 qui se connecte à WUfB (Windows Update for Business) pour la gestion des mises à jour logicielles et les ordinateurs qui se connectent à WSUS à cette même fin. **UseWUServer** est un nouvel attribut qui indique si l’ordinateur est géré avec WUfB. Vous pouvez utiliser ce paramètre dans un regroupement pour retirer ces ordinateurs de la gestion des mises à jour logicielles. Pour plus d'informations, voir [Intégration avec Windows Update for Business dans Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   Vous pouvez maintenant planifier et exécuter la tâche de nettoyage WSUS à partir de la console Configuration Manager.  
    Vous pouvez désormais exécuter manuellement la tâche de nettoyage WSUS à partir des propriétés du composant du point de mise à jour logicielle. Quand vous choisissez d’exécuter la tâche de nettoyage WSUS, elle s’exécute à la prochaine synchronisation des mises à jour logicielles. Les mises à jour logicielles qui ont expiré présentent un état refusé sur le serveur WSUS et l’Agent Windows Update ne les analyse plus. Pour plus d'informations, voir [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md).  

## <a name="compliance-settings"></a>Paramètres de compatibilité  

-   System Center Configuration Manager introduit un flux de travail amélioré pour créer les éléments de configuration. Désormais, quand vous créez un élément de configuration et que vous sélectionnez une plateforme prise en charge, seuls les paramètres correspondant à cette plateforme vous sont proposés. Consultez [Prise en main des paramètres de compatibilité dans System Center Configuration Manager](../../../compliance/get-started/get-started-with-compliance-settings.md).  

-   L’Assistant Création d’élément de configuration vous permet désormais de choisir plus facilement le type d’élément de configuration à créer. De plus, les éléments de configuration nouveaux et mis à jour sont disponibles pour :  

    -   Les appareils Windows 10 gérés avec le client Configuration Manager  

    -   Les appareils Mac OS X gérés avec le client Configuration Manager  

    -   Les ordinateurs de bureau et serveur Windows gérés avec le client Configuration Manager  

    -   Les appareils Windows 8.1 et Windows 10 gérés sans le client Configuration Manager  

    -   Les appareils Windows Phone gérés sans le client Configuration Manager  

    -   Les appareils iOS et Mac OS X gérés sans le client Configuration Manager  

    -   Les appareils KNOX Android et Samsung gérés sans le client Configuration Manager  

     Consultez [Comment créer des éléments de configuration dans System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items.md).  

-   Prise en charge de la gestion des paramètres sur les ordinateurs Mac OS X inscrits avec Microsoft Intune ou gérés à l’aide du client Configuration Manager. Consultez [Comment créer des éléments de configuration pour des appareils iOS et Mac OS X gérés sans le client System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md).  

## <a name="protect-data-and-site-infrastructure"></a>Protéger l’infrastructure de site et les données  
-   System Center Configuration Manager vous permet d’adopter Windows Hello Entreprise (anciennement Microsoft Passport for Work), qui est une méthode de connexion alternative qui utilise Active Directory ou un compte Azure Active Directory en remplacement d’un mot de passe, d’une carte à puce ou d’une carte à puce virtuelle sur les appareils exécutant Windows 10. Consultez [Paramètres Windows Hello Entreprise dans System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md).

## <a name="mobile-device-management-with-microsoft-intune"></a>Gestion des appareils mobiles avec Microsoft Intune  
 System Center Configuration Manager propose des améliorations en matière de gestion des appareils mobiles, avec notamment :  

-   Une limitation du nombre d’appareils qu’un utilisateur peut inscrire  

-   La possibilité de spécifier des conditions générales que les utilisateurs du portail d’entreprise doivent accepter avant de pouvoir inscrire ou utiliser l’application  

-   L’ajout d’un rôle de gestionnaire d’inscription d’appareil pour faciliter la gestion d’un grand nombre d’appareils  

Pour plus d’informations sur les fonctionnalités de gestion des appareils mobiles avec Configuration Manager et Intune, consultez [Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md).  

## <a name="on-premises-mobile-device-management"></a>Gestion des appareils mobiles locale  
 System Center Configuration Manager vous permet désormais de gérer les appareils mobiles au moyen d’une infrastructure Configuration Manager locale. La gestion des appareils et les données associées sont traitées localement et ne font pas partie de Microsoft Intune ni d’autres services cloud. Ce type de gestion d’appareils ne fait appel à aucun logiciel client, car les fonctionnalités dont se sert Configuration Manager pour gérer les appareils sont intégrées aux systèmes d’exploitation des appareils.  

 Pour en savoir plus, consultez [Gérer des appareils mobiles avec une infrastructure locale dans System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).



<!--HONumber=Nov16_HO1-->


