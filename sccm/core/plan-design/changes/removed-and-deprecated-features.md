---
title: "Fonctionnalités dépréciées | Documents Microsoft"
description: "Découvrez les fonctionnalités, produits et systèmes d’exploitation que System Center Configuration Manager ne prend plus en charge."
ms.custom: na
ms.date: 12/05/2016
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
ms.sourcegitcommit: ffebee1e85008611a9841dc849bea735d15a88c6
ms.openlocfilehash: 888b6de9fd2b70e8b4f58e32cca7cf5e615d1dca


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Fonctionnalités supprimées et déconseillées dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique décrit les fonctionnalités, produits et systèmes d’exploitation dont la prise en charge est supprimée dans System Center Configuration Manager ou qui seront supprimés dans une prochaine mise à jour (dépréciés). Elle a pour but de vous avertir suffisamment tôt des changements à venir qui pourraient affecter votre utilisation de Configuration Manager.  

 Ces informations peuvent faire l'objet de modifications dans les futures versions et ne pas inclure chaque fonctionnalité, produit ou système d'exploitation déconseillé.  

## <a name="how-to-use-this-information"></a>Utilisation de ces informations  
Quand une fonctionnalité ou un système d’exploitation est répertorié pour la première fois comme étant déprécié, il est prévu de supprimer la prise en charge de son utilisation avec Configuration Manager dans une version future de celui-ci. Ces informations sont fournies pour vous aider à vous aider à planifier des alternatives à l’utilisation de cette fonctionnalité ou de ce système d’exploitation.  Lors de la publication de la première version de Configuration Manager où cette prise en charge est supprimée, les détails de cette rubrique sont mis à jour pour indiquer cette version spécifique.  

Quand la prise en charge est supprimée pour une fonctionnalité ou un système d’exploitation, la fonctionnalité ou le système d’exploitation reste pris en charge quand vous utilisez une version antérieure de Configuration Manager aussi longtemps que celui-ci reste pris en charge. Cependant, quand vous utilisez une version de Configuration Manager publiée après la date ou la version indiquée, cette version de Configuration Manager ne fournit pas de prise en charge.

**Par exemple :** Si la suppression de la prise en charge d’une fonctionnalité a été planifiée pour la première mise à jour publiée après septembre 2016, cela signifie que la prise en charge de cette fonctionnalité n’est plus incluse dans la mise à jour 1610, publiée en octobre 2016.
-  Avec la mise à jour 1610, la fonctionnalité ne serait ainsi plus prise en charge.
-  Ce contenu serait mis à jour pour indiquer que la prise en charge a été supprimée avec la version 1610.
Cependant, si vous continuez à utiliser une version antérieure qui prend en charge la fonctionnalité, comme la version 1602 ou 1606, vous pouvez continuer à utiliser cette fonctionnalité, jusqu’à ce que la version que vous utilisez supprime la prise en charge.

Pour plus d'informations, voir :
 - Site web [Politique de support Microsoft](https://support.microsoft.com/lifecycle)
 - [Prise en charge des versions Current Branch de Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)

**Fonctionnalités dépréciées :**  


|**Fonctionnalité**|**Première annonce de dépréciation**|**Support supprimé**|  
|-|-|-|  
|Protection d’accès réseau (NAP) : telle que dans System Center 2012 Configuration Manager|7/10/2015|Version 1511|  
|Gestion hors bande : telle que dans System Center 2012 Configuration Manager|10/16/2015|Version 1511|
|Séquences de tâches : <br /> - Convertir en disque dynamique <br /> - Installer les outils de déploiement |11/18/2016|La prise en charge de ces séquences de tâches prend fin avec la première mise à jour publiée après le 1er juin 2017|
|Le nouveau Centre logiciel été modernisé et les applications qui seraient apparues uniquement dans le catalogue des applications dépendant de Silverlight (applications accessibles à l’utilisateur) apparaissent maintenant dans le Centre logiciel sous l’onglet **Applications**. Il est toujours possible d’accéder au catalogue d’applications via le lien situé sous l’onglet **État de l’installation** du Centre logiciel.<br><br>Dans les prochains mois, nous allons supprimer la version précédente du Centre logiciel, qui ne sera alors plus disponible.<br><br>Vous pouvez faire en sorte que les clients utilisent le nouveau Centre logiciel en activant le paramètre client **Agent ordinateur** > **Utiliser le nouveau Centre logiciel**.<br><br>Pour plus d’informations sur le Centre logiciel, consultez [Planifier et configurer la gestion des applications dans System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|12/13/2016|Annoncé prochainement| 

 **Systèmes d’exploitation serveur dépréciés :**  

 |**Systèmes d’exploitation**|**Première annonce de dépréciation**|**Support supprimé** |  
|-|-|-|  
|Windows Server 2008|7/10/2015|La prise en charge prend fin avec la première mise à jour publiée après le 31/12/2016 *(voir remarque 1)*|  
|Windows Server 2008 R2|7/10/2015|La prise en charge prend fin avec la première mise à jour publiée après le 31/12/2016 *(voir remarque 2)*|  

-   *Remarque 1* : Après la fin de la prise en charge, ce système d’exploitation ne sera plus pris en charge pour les serveurs de site ou la plupart des rôles de système de site. Ce système d’exploitation continuera à être pris en charge pour le rôle système de site de point de distribution (dont le point de distribution d’extraction) jusqu’à ce que cette prise en charge soit annoncée comme déconseillée ou que la période étendue de prise en charge de ce système d’exploitation expire.  

-   *Remarque 2* : Après la fin de la prise en charge, ce système d’exploitation ne sera plus pris en charge pour les serveurs de site ou la plupart des rôles de système de site. Cependant, ce système d’exploitation continuera d’être pris en charge pour le point de migration d’état et le rôle de système de site de point de distribution (dont les points de distribution d’extraction et pour PXE et la multidiffusion) jusqu’à ce que cette prise en charge soit annoncée comme déconseillée ou que la période étendue de prise en charge de ce système d’exploitation expire.  Depuis la version 1602, vous pouvez mettre à niveau sur place le système d’exploitation d’un serveur de site à partir de Windows Server 2008 R2 vers Windows Server 2012 R2.  

     Pour plus d’informations sur la mise à niveau sur place d’un système d’exploitation de serveurs de site, consultez la section qui traite de la [mise à niveau sur place du système d’exploitation des serveurs de site qui exécutent Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) dans [Nouveautés de System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



 **Systèmes d’exploitation client dépréciés :**  

 Sauf indication contraire, chaque système d’exploitation pris en charge en tant que client Configuration Manager est pris en charge jusqu’à la date de fin de sa prise en charge étendue, comme expliqué dans [Politique de support Microsoft](https://support.microsoft.com/lifecycle).  Si la prise en charge de Configuration Manager pour un système d’exploitation se termine avant la date de fin de prise en charge étendue, une date de dépréciation et une date de suppression du support de ce système d’exploitation seront mentionnées ici.  

|**Systèmes d’exploitation**|**Première annonce de dépréciation**|**Support supprimé**|  
|-|-|-|  
|Windows XP|7/10/2015|Version 1511|  
|Windows XP Embedded|7/10/2015|Le support prend fin avec la première mise à jour publiée après le 31/12/2016|  
|Windows Server 2003|7/10/2015|Version 1511|  
|Windows Server 2003 R2|7/10/2015|Version 1511|  
|Windows Vista|7/10/2015|Version 1511|  
|Mac OS X 10.6 - 10.8|7/10/2015|Version 1511|  
|Windows Mobile 6.0 - 6.5|7/10/2015|Version 1511|  
|Nokia Symbian Belle|7/10/2015|Version 1511|  
|Windows CE 5.0 - 6.0|7/10/2015|Version 1511|  


 **Support déprécié des versions de SQL Server en tant que base de données du site :**  

|**Versions de SQL Server**|**Première annonce de dépréciation**|**Support supprimé**|   
|-|-|-|  
|SQL Server 2008|7/10/2015|Version 1511|  
|SQL Server 2008 R2|7/10/2015|Le support prend fin avec la première mise à jour publiée après le 31/12/2016|  

## <a name="features-removed-in-system-center-configuration-manager"></a>Fonctionnalités supprimées dans System Center Configuration Manager  
 À partir de la version initiale de System Center Configuration Manager, les fonctionnalités suivantes sont supprimées :

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a> Gestion hors bande  
 Avec Configuration Manager, la prise en charge native des ordinateurs AMT à partir de la console Configuration Manager est supprimée.  

-   Les ordinateurs AMT restent entièrement gérés quand vous utilisez le [module complémentaire Intel SCS pour Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html).  

-   Ce module complémentaire vous permet d’accéder aux dernières fonctionnalités pour gérer AMT tout en supprimant les limitations introduites jusqu’à ce que Configuration Manager puisse intégrer ces changements.  

-   La gestion hors bande dans System Center 2012 Configuration Manager n’est pas affectée par cette modification.  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a> Protection d’accès au réseau  
 System Center Configuration Manager ne prend pas en charge la protection d’accès réseau. La fonctionnalité était déconseillée dans Windows Server 2012 R2 et a été supprimée dans Windows 10.  

 Pour les solutions de protection d'accès réseau, consultez la section **Fonctionnalités déconseillées** dans [Vue d'ensemble des services de stratégie et d'accès réseau](https://technet.microsoft.com/library/hh831683.aspx).  



<!--HONumber=Dec16_HO3-->


