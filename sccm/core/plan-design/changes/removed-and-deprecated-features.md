---
title: "Fonctionnalités dépréciées | Microsoft Docs"
description: "Découvrez les fonctionnalités, produits et systèmes d’exploitation que System Center Configuration Manager ne prend plus en charge."
ms.custom: na
ms.date: 06/27/2017
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
ms.translationtype: HT
ms.sourcegitcommit: ef42d1483053e9a6c502f4ebcae5a231aa6ba727
ms.openlocfilehash: 98fa323cb94013d875e2cea41b80fff8cc75b6b2
ms.contentlocale: fr-fr
ms.lasthandoff: 07/26/2017

---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Fonctionnalités supprimées et déconseillées dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique décrit les fonctionnalités, produits et systèmes d’exploitation dont la prise en charge est supprimée pour System Center Configuration Manager, ou qui seront supprimés dans une prochaine mise à jour (dépréciés). Elle annonce les changements à venir qui pourraient affecter votre utilisation de Configuration Manager.  

Ces informations peuvent faire l’objet de modifications dans les futures versions et ne pas inclure chaque fonctionnalité, produit ou système d’exploitation déprécié.  

## <a name="how-to-use-this-information"></a>Utilisation de ces informations  
Quand une fonctionnalité ou un système d’exploitation sont répertoriés pour la première fois comme étant dépréciés, leur prise en charge dans Configuration Manager est prévue d’être supprimée dans une version future. Ces informations sont fournies pour vous permettre de planifier des alternatives à l’utilisation de cette fonctionnalité ou de ce système d’exploitation. Cette rubrique est mise à jour quand est publiée la première version de Configuration Manager où la prise en charge est supprimée.  

Quand la prise en charge d’une fonctionnalité ou d’un système d’exploitation est supprimée, la fonctionnalité ou le système d’exploitation continuent d’être pris en charge dans les versions antérieures de Configuration Manager aussi longtemps que celles-ci restent prise en charge. Cependant, quand vous utilisez une version de Configuration Manager publiée après la date ou la version indiquée, cette version de Configuration Manager ne fournit pas de prise en charge.

Par exemple, si la suppression de la prise en charge d’une fonctionnalité a été planifiée dans la première mise à jour publiée après septembre 2016, la prise en charge de cette fonctionnalité n’est plus incluse dans la mise à jour 1610, publiée en octobre 2016.
-  Avec la mise à jour 1610, la fonctionnalité ne serait ainsi plus prise en charge.
-  Cette rubrique serait mise à jour pour indiquer que la prise en charge a été supprimée avec la version 1610.
Cependant, si vous continuez à utiliser une version antérieure qui prend en charge la fonctionnalité, comme la version 1602 ou 1606, vous pouvez continuer à utiliser cette fonctionnalité, jusqu’à ce que la version que vous utilisez supprime la prise en charge.

Pour plus d'informations, voir :
 - Le site web [Politique de support Microsoft](https://support.microsoft.com/lifecycle).
 - [Prise en charge des versions Current Branch de System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).




## <a name="deprecated-operating-systems"></a>Systèmes d’exploitation dépréciés
### <a name="server-operating-systems"></a>Systèmes d’exploitation serveur  

|**Systèmes d’exploitation**|**Première annonce de dépréciation**|**Support supprimé** |  
|-|-|-|  
|Windows Server 2008|10 juillet 2015|Version 1511 </br></br>Le support prend fin quand un système de site est supprimé (voir la remarque 1).|  
|Windows Server 2008 R2|10 juillet 2015| Version 1702  (voir la note 2)|  

-   Remarque 1 : Ce système d’exploitation n’est pas pris en charge pour les serveurs de site ou les rôles de système de site, à l’exception du point de distribution et du point de distribution d’extraction. Vous pouvez continuer à utiliser ce système d’exploitation comme point de distribution jusqu’à l’annonce de la dépréciation de ce support ou jusqu’à l’expiration du support étendu de ce système d’exploitation. Pour plus d’informations, consultez [Échec de l’installation de System Center Configuration Manager CB et LTSB sur Windows Server 2008](https://support.microsoft.com/help/4015095).

-   Remarque 2 : depuis la version 1702, ce système d’exploitation n'est pas pris en charge pour les serveurs de site ou la plupart des rôles de système de site, mais les versions antérieures à 1702 continuent de prendre en charge son utilisation. Ce système d’exploitation continue d’être pris en charge pour le rôle de système de site de point de distribution (dont les points de distribution d’extraction, ainsi que pour PXE et la multidiffusion) jusqu’à l’annonce de la dépréciation de ce support ou jusqu’à l’expiration du support étendu de ce système d’exploitation. Depuis la version 1602, vous pouvez mettre à niveau sur place le système d’exploitation d’un serveur de site à partir de Windows Server 2008 R2 vers Windows Server 2012 R2.  

     Pour plus d’informations sur la mise à niveau sur place d’un système d’exploitation de serveurs de site, consultez la section qui traite de la [mise à niveau sur place du système d’exploitation des serveurs de site qui exécutent Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) dans [Nouveautés de System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



### <a name="client-operating-systems"></a>Systèmes d'exploitation client  

 Sauf indication contraire, chaque système d’exploitation pris en charge en tant que client Configuration Manager est pris en charge jusqu’à sa date de fin de support étendu. Pour plus d’informations sur les dates de fin du support étendu, consultez la [Politique de support Microsoft](https://support.microsoft.com/lifecycle). Si la prise en charge de Configuration Manager pour un système d’exploitation se termine avant la date de fin du support étendu, une date de dépréciation et une date de suppression du support de ce système d’exploitation seront mentionnées ici.  

|**Systèmes d’exploitation**|**Première annonce de dépréciation**|**Support supprimé**|  
|-|-|-|  
|Windows XP|10 juillet 2015|Version 1511|  
|Windows XP Embedded|10 juillet 2015|Version 1702|  
|Windows Server 2003|10 juillet 2015|Version 1511|  
|Windows Server 2003 R2|10 juillet 2015|Version 1511|  
|Windows Vista|10 juillet 2015|Version 1511|  
|Mac OS X 10.6 - 10.8|10 juillet 2015|Version 1511|  
|Windows Mobile 6.0 - 6.5|10 juillet 2015|Version 1511|  
|Nokia Symbian Belle|10 juillet 2015|Version 1511|  
|Windows CE 5.0 - 6.0|10 juillet 2015|Version 1511|  


## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Support déprécié pour les versions de SQL Server en tant que base de données de site  

|**Versions de SQL Server**|**Première annonce de dépréciation**|**Support supprimé**|   
|-|-|-|  
|SQL Server 2008|10 juillet 2015|Version 1511|  
|SQL Server 2008 R2|10 juillet 2015|Version 1702|  

Si vous devez mettre à niveau votre version de SQL Server, nous vous recommandons les méthodes suivantes, de la plus simple à la plus complexe.
1. [Mise à niveau de SQL Server sur place](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recommandé).
2. Installez une nouvelle version de SQL Server sur un nouvel ordinateur, puis [utilisez l’option de déplacement de la base de données](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) du programme d’installation de Configuration Manager pour pointer votre serveur de site vers la nouvelle version de SQL Server.
3. Utilisez la [sauvegarde et la récupération](/sccm/protect/understand/backup-and-recovery).


## <a name="deprecated-features"></a>Fonctionnalités dépréciées  

|**Fonctionnalité**|**Première annonce de dépréciation**|**Support supprimé**|  
|-|-|-|  
|Protection d’accès réseau (NAP) : telle que dans System Center 2012 Configuration Manager|10 juillet 2015|Version 1511|  
|Gestion hors bande : telle que dans System Center 2012 Configuration Manager|16 octobre 2015|Version 1511|
|Séquences de tâches : <br /> - OSDPreserveDriveLetter  <br /><br /> Lors d’un déploiement de système d’exploitation, par défaut, le programme d’installation Windows détermine désormais la meilleure lettre de lecteur à utiliser (généralement C:). Si vous souhaitez spécifier un autre lecteur à utiliser, vous pouvez modifier l’emplacement dans l’étape de séquence de tâches Appliquer le système d’exploitation. Accédez au paramètre **Sélectionnez l’emplacement où vous souhaitez appliquer ce système d’exploitation**, sélectionnez **Lettre de lecteur logique spécifique**, puis choisissez le lecteur que vous souhaitez utiliser. |20 juin 2016 |Version 1606 |
|Séquences de tâches : <br /> - Convertir en disque dynamique <br /> - Installer les outils de déploiement |18 novembre 2016|La prise en charge de ces séquences de tâches prend fin avec la première mise à jour publiée après le 1er juin 2017.|
|Le Centre logiciel a été modernisé. Les applications qui seraient apparues uniquement dans le catalogue des applications dépendant de Silverlight (applications accessibles à l’utilisateur) apparaissent désormais dans le Centre logiciel, sous l’onglet **Applications**. Il est toujours possible d’accéder au catalogue des applications via le lien situé sous l’onglet **État de l’installation** du Centre logiciel.<br><br>Dans les prochains mois, la version précédente du Centre logiciel ne sera plus disponible.<br><br>Vous pouvez configurer les clients pour qu’ils utilisent le nouveau Centre logiciel en activant le paramètre client **Agent ordinateur** > **Utiliser le nouveau Centre logiciel**.<br><br>Pour plus d’informations sur le Centre logiciel, consultez [Planifier et configurer la gestion des applications dans System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 décembre 2016|La prise en charge de la version précédente du centre logiciel se termine avec la première mise à jour publiée après le 1 janvier 2018.|
|Gestion de disques durs virtuels avec Configuration Manager. </br></br>Cela inclut la suppression des options permettant de créer un nouveau disque dur virtuel ou de gérer un disque dur virtuel à l’aide d’une séquence de tâches, ainsi que la suppression du nœud Disques durs virtuels dans la console Configuration Manager. </br></br>Une fois cette prise en charge supprimée, les disques durs virtuels existants ne seront pas supprimés, mais ils ne seront plus accessibles à partir de la console Configuration Manager.  |6 janvier 2017 |La prise en charge des disques durs virtuels prend fin avec la première mise à jour publiée après le 1er juin 2017.|
|Outil d'évaluation de mise à niveau System Center Configuration Manager. </br></br>L’outil d’évaluation de mise à niveau dépend à la fois de System Center Configuration Manager et des outils d'analyse de compatibilité des applications (ACT) 6.x. La dernière version d’ACT a été intégrée à Windows 10 v1511 ADK. Comme il n’y aura plus aucune mise à jour d’ACT, la prise en charge de l’outil d’évaluation de mise à niveau cessera. </br></br>L’outil d’évaluation de mise à niveau est remplacé par la fonctionnalité [Disponibilité pour la mise à niveau](/sccm/core/clients/manage/upgrade/upgrade-analytics). Une note de dépréciation a été ajoutée à la [page de téléchargement UAT](https://www.microsoft.com/download/details.aspx?id=37145) le 12/09/2016. |12/09/2016  | 11 juillet 2017 |  


<br></br>
Informations supplémentaires sur les fonctionnalités supprimées avec la version 1511 de System Center Configuration Manager :

###  <a name="bkmk_amt"></a> Gestion hors bande  
 Avec Configuration Manager, la prise en charge native des ordinateurs AMT à partir de la console Configuration Manager est supprimée.  

-   Les ordinateurs AMT restent entièrement gérés quand vous utilisez le [module complémentaire Intel SCS pour Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). Ce module complémentaire vous permet d’accéder aux dernières fonctionnalités permettant de gérer AMT tout en supprimant les limitations introduites jusqu’à ce que Configuration Manager puisse intégrer ces changements.  

-   La gestion hors bande dans System Center 2012 Configuration Manager n’est pas affectée par cette modification.  

###  <a name="bkmk_nap"></a> Protection d’accès au réseau  
 System Center Configuration Manager ne prend pas en charge la protection d’accès réseau. La fonctionnalité est dépréciée dans Windows Server 2012 R2 et a été supprimée dans Windows 10.  

 Pour les solutions de protection d'accès réseau, consultez la section *Fonctionnalités déconseillées* dans [Vue d'ensemble des services de stratégie et d'accès réseau](https://technet.microsoft.com/library/hh831683.aspx).

