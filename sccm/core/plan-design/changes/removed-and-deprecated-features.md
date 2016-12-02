---
title: "Fonctionnalités dépréciées | System Center Configuration Manager"
description: "Découvrez les fonctionnalités, produits et systèmes d’exploitation que System Center Configuration Manager ne prend plus en charge."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f1e1070fd5b56b1abf22159e9f95b3b4bd8a8c6


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Fonctionnalités supprimées et déconseillées dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique décrit les fonctionnalités, produits et systèmes d’exploitation dont la prise en charge est supprimée dans System Center Configuration Manager ou qui seront supprimés dans une prochaine mise à jour (dépréciés). Elle a pour but de vous avertir suffisamment tôt des changements à venir qui pourraient affecter votre utilisation de Configuration Manager.  

 Ces informations peuvent faire l'objet de modifications dans les futures versions et ne pas inclure chaque fonctionnalité, produit ou système d'exploitation déconseillé.  

## <a name="deprecated-features-products-and-operating-systems"></a>Fonctionnalités, produits et systèmes d'exploitation déconseillés  
 Les produits et systèmes d'exploitation Microsoft répertoriés comme déconseillés bénéficient d'un support étendu ou ont atteint leur fin de vie. Les produits et systèmes d’exploitation Microsoft répertoriés comme étant dépréciés continuent d’être testés avec les versions actuelles de Configuration Manager au-delà du cycle de vie de leur support Microsoft.  Pour plus d'informations, consultez le site web [Politique de support Microsoft](https://support.microsoft.com/lifecycle) .  

 **Fonctionnalités dépréciées :**  


|**Fonctionnalité**|**Première annonce de dépréciation**|**Support supprimé**|  
|-|-|-|  
|Protection d’accès réseau (NAP) : telle que dans System Center 2012 Configuration Manager|7/10/2015|√|  
|Gestion hors bande : telle que dans System Center 2012 Configuration Manager|10/16/2015|√|  

 **Systèmes d’exploitation serveur dépréciés :**  

 |**Systèmes d’exploitation**|**Première annonce de dépréciation**|**Support supprimé**|  
|-|-|-|  
|Windows Server 2008|7/10/2015|La prise en charge prend fin avec la première mise à jour publiée après le 31/12/2016 (voir note 1)|  
|Windows Server 2008 R2|7/10/2015|La prise en charge prend fin avec la première mise à jour publiée après le 31/12/2016 (voir note 2)|  

-   Remarque 1 : après la fin de la prise en charge, ce système d’exploitation ne sera plus pris en charge pour les serveurs de site ou la plupart des rôles système de site. Ce système d’exploitation continuera à être pris en charge pour le rôle système de site de point de distribution (dont le point de distribution d’extraction) jusqu’à ce que cette prise en charge soit annoncée comme déconseillée ou que la période étendue de prise en charge de ce système d’exploitation expire.  

-   Remarque 2 : après la fin de la prise en charge, ce système d’exploitation ne sera plus pris en charge pour les serveurs de site ou la plupart des rôles système de site. Cependant, ce système d’exploitation continuera d’être pris en charge pour le point de migration d’état et le rôle de système de site de point de distribution (dont les points de distribution d’extraction et pour PXE et la multidiffusion) jusqu’à ce que cette prise en charge soit annoncée comme déconseillée ou que la période étendue de prise en charge de ce système d’exploitation expire.  Depuis la version 1602, vous pouvez mettre à niveau sur place le système d’exploitation d’un serveur de site à partir de Windows Server 2008 R2 vers Windows Server 2012 R2.  

     Pour plus d’informations sur la mise à niveau sur place d’un système d’exploitation de serveurs de site, consultez la section qui traite de la [mise à niveau sur place du système d’exploitation des serveurs de site qui exécutent Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) dans [Nouveautés de System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



 **Systèmes d’exploitation client dépréciés :**  

 Sauf indication contraire, chaque système d’exploitation pris en charge en tant que client Configuration Manager est pris en charge jusqu’à la date de fin de sa prise en charge étendue, comme expliqué dans [Politique de support Microsoft](https://support.microsoft.com/lifecycle).  Si la prise en charge de Configuration Manager pour un système d’exploitation se termine avant la date de fin de prise en charge étendue, une date de dépréciation et une date de suppression du support de ce système d’exploitation seront mentionnées ici.  

|**Systèmes d’exploitation**|**Première annonce de dépréciation**|**Support supprimé**|  
|-|-|-|  
|Windows XP|7/10/2015|√|  
|Windows XP Embedded|7/10/2015|Le support prend fin avec la première mise à jour publiée après le 31/12/2016|  
|Windows Server 2003|7/10/2015|√|  
|Windows Server 2003 R2|7/10/2015|√|  
|Windows Vista|7/10/2015|√|  
|Mac OS X 10.6 - 10.8|7/10/2015|√|  
|Windows Mobile 6.0 - 6.5|7/10/2015|√|  
|Nokia Symbian Belle|7/10/2015|√|  
|Windows CE 5.0 - 6.0|7/10/2015|√|  


 **Support déprécié des versions de SQL Server en tant que base de données du site :**  

|**Versions de SQL Server**|**Première annonce de dépréciation**|**Support supprimé**|   
|-|-|-|  
|SQL Server 2008|7/10/2015|√|  
|SQL Server 2008 R2|7/10/2015|Le support prend fin avec la première mise à jour publiée après le 31/12/2016|  

## <a name="features-removed-in-system-center-configuration-manager"></a>Fonctionnalités supprimées dans System Center Configuration Manager  
 À partir de la version initiale de System Center Configuration Manager, les fonctionnalités suivantes sont supprimées :

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a> Gestion hors bande  
 Avec Configuration Manager, la prise en charge native des ordinateurs AMT à partir de la console Configuration Manager est supprimée.  

-   Les ordinateurs AMT restent entièrement gérés quand vous utilisez le [module complémentaire Intel SCS pour Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html).  

-   Ce module complémentaire vous permet d’accéder aux dernières fonctionnalités pour gérer AMT tout en supprimant les limitations introduites jusqu’à ce que Configuration Manager puisse intégrer ces changements.  

-   La gestion hors bande dans System Center 2012 Configuration Manager n’est pas affectée par cette modification.  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a> Protection d’accès au réseau  
 System Center Configuration Manager ne prend pas en charge la protection d’accès réseau. La fonctionnalité était déconseillée dans Windows Server 2012 R2 et a été supprimée dans Windows 10.  

 Pour les solutions de protection d'accès réseau, consultez la section **Fonctionnalités déconseillées** dans [Vue d'ensemble des services de stratégie et d'accès réseau](https://technet.microsoft.com/library/hh831683.aspx).  



<!--HONumber=Nov16_HO1-->


