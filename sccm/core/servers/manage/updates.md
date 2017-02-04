---
title: "Mises à jour | Microsoft Docs"
description: "Découvrez une méthode de service dans la console, appelée **Mises à jour et maintenance**, qui facilite la localisation et l’installation des mises à jour recommandées."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
caps.latest.revision: 51
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5314bcb434b5b540f80cdfe32002df7b8fed6195
ms.openlocfilehash: 52d5ad7a348e0489f43ac6cb46af930499ef6cf2


---
# <a name="updates-for-system-center-configuration-manager"></a>Mises à jour pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager utilise une méthode de service dans la console appelée **Mises à jour et maintenance** qui facilite la détection et l’installation des mises à jour recommandées pour votre infrastructure Configuration Manager. Cette méthode de maintenance dans la console est complétée par des mises à jour hors bande, telles que des correctifs logiciels, qui s’adressent aux clients qui ont besoin de résoudre des problèmes qui peuvent être propres à leur environnement.  

> [!TIP]
> Lors de la gestion de l’infrastructure de site et de hiérarchie System Center Configuration Manager, les termes *mise à niveau*, *mise à jour* et *installation* sont utilisés pour décrire trois concepts distincts. Pour connaître la signification et l’usage de chaque terme, consultez [À propos de la mise à niveau, de la mise à jour et de l’installation de l’infrastructure de site et de hiérarchie](/sccm/core/understand/upgrade-update-install).


 **Les rubriques suivantes peuvent vous aider à comprendre comment rechercher et installer les différents types de mise à jour pour System Center Configuration Manager :**  

-   [Installer des mises à jour dans la console pour System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  

-   [Utiliser l’outil de connexion de service pour System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [Importer des correctifs pour System Center Configuration Manager avec l’outil Inscription de la mise à jour](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [Utiliser le programme d’installation de correctif logiciel pour installer des mises à jour pour System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


Si vous utilisez l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview) pour plus d’informations sur cette édition.


##  <a name="a-namebkmkbaselinesa-baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> Versions de base et de mise à jour  
 La version initiale Current Branch de System Center Configuration Manager était la version 1511, une version de base de référence. Plus récemment, la version 1606 a été publiée comme base de référence :  

-   La dernière version de base est à utiliser quand il s’agit d’installer un nouveau site dans une nouvelle hiérarchie.  

-   Vous devez utiliser une version de base pour effectuer une mise à niveau à partir de System Center 2012 Configuration Manager.  

-   D’autres versions de base de référence seront régulièrement publiées. Quand vous utilisez la dernière version de base de référence pour installer une nouvelle hiérarchie, vous évitez d’installer une version obsolète de Configuration Manager, suivie d’une mise à niveau de votre infrastructure pour la mettre à jour.  

Après avoir installé une version de base, d’autres versions de Configuration Manager sont disponibles sous forme de mises à jour dans la console. Les mises à jour dans la console mettent à jour votre infrastructure vers la dernière version de Configuration Manager.  

-   L’installation des mises à jour dans la console visent à mettre à jour la version de votre site de niveau supérieur.  

-   Les mises à jour que vous installez sur le site d’administration centrale s’installent automatiquement sur les sites principaux enfants, sauf si elles sont bloquées par une fenêtre de maintenance que vous avez configurée sur le site principal.  

-   Vous devez mettre à jour manuellement les sites secondaires vers une nouvelle version de mise à jour à partir de la console.  

Quand vous installez une mise à jour, celle-ci stocke les fichiers d’installation de cette version sur le serveur du site dans un dossier nommé CD.Latest. Pour plus d’informations sur ces fichiers, consultez [Dossier CD.Latest pour System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md).  

-   Les fichiers contenus dans le dossier CD.Latest sont utilisés pendant la récupération de site et pour installer des sites supplémentaires dans une hiérarchie qui n’exécute plus une version de base.  

-   Vous ne pouvez pas vous servir des fichiers d’installation du dossier CD.Latest pour installer le premier site d’une nouvelle hiérarchie ni pour mettre à niveau un site à partir de System Center 2012 Configuration Manager.  

Certaines mises à jour de Configuration Manager sont disponibles à la fois comme version de mise à jour dans la console pour l’infrastructure existante et comme nouvelle version de base.  

Les versions suivantes de Configuration Manager sont disponibles sous forme de version de base, de mise à jour ou les deux à la fois :  

|Version|Date de disponibilité|De base|Mise à jour dans la console|  
|-------------|-----------------------|--------------|------------------------|  
|**1511**<br /><br /> 5.00.8325.1000|08/12/2015|Oui|Non|  
|**1602**<br /><br /> 5.00.8355.1000|11/03/2016|Non|Oui|
|**1606**<br /><br /> 5.00.8412.1000|7/22/2016|Non|Oui|
|**1606** avec le correctif cumulatif 1606 (KB3186654) </br></br>5.00.8412.1307 *(Note 1)* |10/12/2016|Oui|Non|
|**1610**<br /><br /> 5.00.8458.1000|11/18/2016|Non|Oui|
*(Note 1)* Ce support de la base de référence 1606 est disponible dans le cadre de Microsoft System Center 2016 ou de System Center Configuration Manager (Current Branch et Long-Term Servicing Branch 1606).

Pour vérifier la version de votre site Configuration Manager, dans la console, accédez à **À propos de System Center Configuration Manager** dans le coin supérieur gauche de la console où sont affichées la nouvelle version du site et de la console.  

##  <a name="a-namebkmkinconsolea-in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> Mises à jour et maintenance dans la console  
 Quand vous utilisez une installation de System Center Configuration Manager prête pour la production, aussi appelée « Current Branch », la plupart des mises à jour que vous installez sont disponibles via le canal Mises à jour et maintenance. Cette méthode identifie, télécharge et met à disposition les mises à jour qui s’appliquent à la version et à la configuration actuelles de votre infrastructure et propose uniquement les mises à jour que Microsoft recommande à tous les clients,   
 à savoir :  

-   Les nouvelles versions comme la version 1602  

-   Les mises à jour qui comprennent de nouveaux composants pour votre version actuelle  

-   Les correctifs logiciels pour votre version de Configuration Manager que tous les clients doivent installer  

Les mises à jour dans la console offrent une stabilité accrue et résolvent les problèmes courants. Elles remplacent les types de mise à jour déjà rencontrés pour les versions de produit précédentes de service packs, de mises à jour cumulatives et de correctifs logiciels applicables à tous les clients, et pour l’extension pour Microsoft Intune. Ces mises à jour peuvent s’appliquer à un ou plusieurs des éléments suivants :  

-   Serveurs de site principal et d’administration centrale  

-   Rôles de système de site et serveurs de système de site  

-   Instances du fournisseur SMS  

-   Consoles Configuration Manager  

-   Clients Configuration Manager  

Configuration Manager détecte automatiquement les nouvelles mises à jour au moment où vous synchronisez votre rôle système de site de point de connexion de service avec le service cloud et le centre de téléchargement Microsoft :  

-   Quand votre point de connexion de service est en mode en ligne, votre site se synchronise tous les jours avec Microsoft pour identifier automatiquement les nouvelles mises à jour qui s’appliquent à votre infrastructure.  Pour télécharger les mises à jour et fichiers de redistribution des mises à jour, l’ordinateur qui héberge le rôle système de site de point de connexion de service utilise le contexte **System** pour accéder aux emplacements Internet suivants : go.microsoft.com et download.microsoft.com. Pour plus d’informations sur les emplacements supplémentaires auxquels le point de connexion de service se connecte, consultez [Conditions requises pour l’accès Internet](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls) dans [À propos du point de connexion de service dans System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   Quand votre point de connexion de service est en mode hors connexion, vous utilisez l’outil de connexion de service pour opérer une synchronisation manuelle avec le cloud Microsoft. Pour plus d'informations, voir [Utiliser l’outil de connexion de service pour System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

-   Les mises à jour dans la console vous évitent d’avoir à localiser et à installer indépendamment les mises à jour, les service packs et les nouveaux composants.  

-   Vous installez uniquement les mises à jour dans la console que vous choisissez, et à l’occasion de l’installation de certaines mises à jour, vous pouvez sélectionner les composants individuels que vous voulez activer et utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](../../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Points à noter pendant l’installation d’une mise à jour dans la console :  

-   Elle procède automatiquement à une vérification de la configuration requise. Vous pouvez aussi effectuer cette vérification avant de démarrer l’installation.  

-   Elle s’installe automatiquement sur le site d’administration centrale (si vous en avez un) et sur les sites principaux. Vous pouvez contrôler à quel moment chaque serveur de site principal est autorisé à mettre à jour son infrastructure à l’aide des [fenêtres de service pour les serveurs de site](../../../core/servers/manage/service-windows.md).  

-   Après la mise à jour d’un serveur de site, tous les rôles de système de site affectés (notamment les instances du fournisseur SMS) se mettent automatiquement à jour. Par ailleurs, la console Configuration Manager invite son utilisateur à la mettre à jour, après que le site a installé la mise à jour.  

-   Si une mise à jour inclut le client Configuration Manager, possibilité vous est offerte de tester la mise à jour en préproduction ou d’appliquer tout de suite la mise à jour à tous les clients.  

-   Après la mise à jour d’un site principal, les sites secondaires ne sont pas mis à jour automatiquement. Vous devez en effet lancer leur mise à jour.  

> [!NOTE]  
>  La version de production de System Center Configuration Manager (Current Branch), la branche LTSB (Long Term Servicing Branch) et la préversion Technical Preview pour System Center Configuration Manager sont des versions différentes. Par conséquent, les mises à jour qui s’appliquent à une branche ne sont pas disponibles en tant que mises à jour dans la console pour les autres branches. Pour plus d’informations sur les branches disponibles, consultez [Quelle branche de Configuration Manager dois-je utiliser ?](/sccm/core/understand/which-branch-should-i-use)

##  <a name="a-namebkmkoutofbanda-out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> Correctifs logiciels hors bande  
Certains correctifs logiciels sont publiés pour une durée limitée dans le but de résoudre certains problèmes spécifiques, ou bien ils s’appliquent à tous les clients, mais ne peuvent pas être installés avec la méthode dans la console. Ces correctifs logiciels sont fournis hors bande et ne sont pas détectés à partir du service cloud Microsoft.  

En règle générale, quand vous cherchez à corriger ou à résoudre un problème lié à votre déploiement de Configuration Manager, vous apprenez l’existence de correctifs hors bande par l’intermédiaire des services clientèle de Microsoft, via un article de la Base de connaissances ou sur le [blog de l’équipe System Center Configuration Manager](https://blogs.technet.microsoft.com/configmgrteam).  

Pour installer ces correctifs manuellement, deux méthodes sont disponibles :  

-   **Outil Inscription de la mise à jour :** cet outil importe manuellement le correctif logiciel dans votre console Configuration Manager d’où vous pouvez ensuite installer la mise à jour comme des mises à jour dans la console qui seraient détectées automatiquement. Cette méthode est utilisée pour les mises à jour qui utilisent la structure de nom de fichier suivante : **.update.exe**.  Le nom de fichier complet de ce type de correctif logiciel se présente ainsi : **&lt;Produit\>-&lt;version du produit\>-&lt;ID d’article de la base de connaissances\>-ConfigMgr.Update.exe**.  

     Pour plus d’informations, consultez [Importer des correctifs pour System Center Configuration Manager avec l’outil Inscription de la mise à jour](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

-   **Programme d’installation de correctifs logiciels :** cet outil permet d’installer manuellement un correctif logiciel qui ne peut pas être installé via la méthode dans la console. Cette méthode s’applique aux correctifs qui utilisent la structure de nom de fichier suivante : **&lt;Produit\>-&lt;version du produit\>-&lt;ID d’article de la base de connaissances\>-&lt;plateforme\>-&lt;langue\>.exe**.

     Pour plus d’informations, consultez [Utiliser le programme d’installation de correctif logiciel pour installer les mises à jour de System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md).



<!--HONumber=Jan17_HO2-->


