---
title: "Notions de base des sites et des hiérarchies | System Center Configuration Manager"
description: "Obtenez des informations de base sur les sites et les hiérarchies System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 07e10ead8d4b147a4a96b1e5189597e1ac4d4f52


---
# <a name="fundamentals-of-sites-and-hierarchies-for-system-center-configuration-manager"></a>Notions de base des sites et des hiérarchies pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Un déploiement System Center Configuration Manager doit être installé dans un domaine Active Directory et a pour base un ou plusieurs sites Configuration Manager formant une hiérarchie de sites. Qu’il s’agisse d’un site unique ou d’une hiérarchie à plusieurs sites, le type et l’emplacement des sites que vous installez permettent de faire monter en puissance (développer) votre déploiement si nécessaire et d’offrir des services clés aux appareils et utilisateurs gérés.

## <a name="hierarchies-of-sites"></a>Hiérarchies de sites
Quand vous installez System Center Configuration Manager pour la première fois, le premier site Configuration Manager que vous installez détermine l’étendue de votre hiérarchie, base à partir de laquelle vous allez gérer les appareils et les utilisateurs au sein de votre entreprise. Ce premier site doit être un site d’administration centrale ou un site principal autonome.  

 Un **site d’administration centrale** convient aux déploiements à grande échelle, et fournit un point d’administration centrale ainsi que la flexibilité nécessaire pour prendre en charge les appareils distribués dans l’ensemble de votre infrastructure réseau globale. Après avoir installé un site d’administration centrale, vous devez installer un ou plusieurs sites principaux en tant que sites enfants.  Cela résulte du fait qu’un site d’administration centrale ne prend pas directement en charge la gestion des périphériques, ce qui est la fonction d’un site principal. Un site d’administration centrale prend en charge plusieurs sites principaux enfants qui permettent de gérer directement des périphériques et de contrôler la bande passante réseau quand vos périphériques gérés se trouvent dans différents emplacements géographiques.  

 Un **site principal autonome** convient pour des déploiements plus petits et permet de gérer des appareils sans devoir installer des sites supplémentaires. Si un site principal autonome risque de limiter la taille de votre déploiement, il prend en charge un scénario d’extension ultérieure de votre hiérarchie par l’installation d’un nouveau site d’administration centrale. Dans le cadre de ce scénario d’extension du site, votre site principal autonome devient un site principal enfant, et vous pouvez installer des sites principaux enfants supplémentaires sous votre nouveau site d’administration centrale.  Cela vous permet ensuite d’étendre votre déploiement initial dans la perspective d’une croissance future de votre entreprise.  

> [!TIP]  
>  Un site principal autonome et un site principal enfant sont en fait du même type : il s’agit de sites principaux. La différence de nom est basée sur la relation de hiérarchie qui est créée quand vous utilisez également un site d’administration centrale.  Cette relation de hiérarchie peut également limiter l’installation de certains rôles système de site qui étendent les fonctionnalités de Configuration Manager. En effet, certains rôles de système de site ne peuvent être installés que sur le site de niveau supérieur de la hiérarchie, un site d’administration centrale ou un site principal autonome.  

 Après avoir installé votre premier site, vous pouvez installer des sites supplémentaires.  Si votre premier site est un site d’administration centrale, vous pouvez installer un ou plusieurs sites principaux enfants.  Après avoir installé un site principal (autonome ou principal de l’enfant), vous pouvez installer un ou plusieurs sites secondaires.  

 Un **site secondaire** peut uniquement être installé en tant que site enfant sous un site principal. Ce type de site étend la portée d’un site principal à la gestion de périphériques situés dans des emplacements où la connexion réseau au site principal est lente.   Même si un site secondaire étend le site principal, les clients sont toujours gérés par le site principal. Le site secondaire prend en charge les périphériques situés dans l’emplacement distant, en comprimant les informations que vous envoyez (déployez) aux clients et que ceux-ci renvoient au site, et en gérant leur transfert sur votre réseau.  

 Les schémas suivants offrent des exemples d'architecture de site.  

 ![Exemples de hiérarchie](media/Hierarchy_examples.png)  

 Pour plus d'informations, consultez les rubriques suivantes :  

-   [Présentation de System Center Configuration Manager](../../core/understand/introduction.md)  

-   [Concevoir une hiérarchie de sites pour System Center Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Installer des sites System Center Configuration Manager](/sccm/core/servers/deploy/install/installing-sites)  

## <a name="site-system-servers-and-site-system-roles"></a>Serveurs de système de site et rôles de système de site  
 Chaque site Configuration Manager installe des **rôles système de site** qui prennent en charge les opérations de gestion.  Quand vous installez un site, certains rôles sont installés par défaut, tels le rôle **serveur de site** (attribué à l’ordinateur sur lequel vous installez le site) et le rôle serveur de bases de données du site (attribué au serveur SQL Server hébergeant la base de données du site). Les autres rôles système de site sont facultatifs et utilisés uniquement lorsque vous souhaitez utiliser les fonctionnalités que ces rôles système de site activent.  Tout ordinateur hébergeant un rôle système de site est considéré comme un serveur de système de site.  

 Pour un déploiement plus petit de Configuration Manager, vous pouvez initialement exécuter tous vos rôles système de site directement sur l’ordinateur du serveur de site. Ensuite, à mesure que votre environnement géré et vos besoins augmentent, vous pouvez installer des serveurs de système de site supplémentaires pour héberger des rôles système de site supplémentaires afin d’améliorer l’efficacité du site en fournissant des services à davantage de périphériques.  

 Pour plus d’informations sur les différents rôles de système de site, consultez [Site system roles](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) (Rôles de système de site) dans [Planifier des serveurs de système de site et des rôles système de site pour System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Publication d’informations de site vers les services de domaine Active Directory  
 Pour simplifier la gestion de Configuration Manager, vous pouvez étendre le schéma Active Directory pour qu’il prenne en charge les informations utilisées par Configuration Manager, puis faire en sorte que les sites publient leurs informations clés sur les services de domaine Active Directory (AD DS). Cela permet aux ordinateurs que vous souhaitez gérer de récupérer en toute sécurité les informations relatives au site à partir de la source approuvée d’AD DS. Les informations que les clients peuvent récupérer identifient les sites disponibles, les serveurs de système de site et les services que ces serveurs fournissent.  

 **L’extension du schéma Active Directory** n’est effectuée qu’une seule fois par forêt, et peut être exécutée avant ou après l’installation de Configuration Manager.   Quand vous étendez le schéma, vous devez créer un conteneur Active Directory nommé **Gestion du système** dans chaque domaine contenant un site Configuration Manager qui publiera des données que des clients pourront trouver. Pour plus d’informations, consultez [Étendre le schéma Active Directory pour System Center Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

 La **publication des données du site** améliore la sécurité de votre hiérarchie Configuration Manager et réduit la surcharge administrative, mais n’est pas requise pour les fonctionnalités de base de Configuration Manager.  



<!--HONumber=Nov16_HO1-->


