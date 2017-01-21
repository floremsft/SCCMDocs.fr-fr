---
title: Configurer des sites | Microsoft Docs
description: "Consultez cette liste de vérification pour vous assurer que vous prenez en compte les configurations les plus courantes qui affectent les sites et les hiérarchies."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: 15
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: a6936dac2159118b192a930eecb4595b0f4d4a59


---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>Configurer les sites et hiérarchies pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir installé votre premier site System Center Configuration Manager ou ajouté des sites supplémentaires à votre hiérarchie, utilisez la liste de vérification suivante relative aux configurations les plus courantes qui affectent les sites et les hiérarchies.  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>Liste de vérification des configurations courantes pour les nouveaux sites et les sites supplémentaires  
 Dans la plupart des déploiements, vous n’avez pas besoin de configurer les options suivantes dans un ordre spécifique.  

-   Certaines options sont liées, telles que les limites, les groupes de limites et la découverte de forêts Active Directory.  

-   Plusieurs configurations ont des valeurs par défaut que vous pouvez utiliser sans modification de configuration, au moins temporairement.  

-   D’autres configurations, telles que celles des groupes de limites et des groupes de points de distribution, doivent être configurées avant de pouvoir être utilisées.  

|Action|Détails|  
|------------|-------------|  
|Configurer l’administration basée sur des rôles|L’administration basée sur des rôles détermine la séparation des attributions d’administration pour contrôler la façon dont les utilisateurs administratifs peuvent afficher et gérer les différents objets et données dans votre environnement Configuration Manager.<br /><br /> Les configurations de l’administration basée sur des rôles sont partagées avec tous les sites dans une hiérarchie.   <br />Voir [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Publier les données de site dans les services de domaine Active Directory (AD DS)|Lorsque vous publiez des données de site dans les services AD DS, vous facilitez la recherche de services et l’utilisation efficace des ressources de site pour les clients.<br /><br /> Vous devez d’abord [Étendre le schéma Active Directory pour System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md), puis chaque site doit être configuré pour la [Publication de données de site pour System Center Configuration Manager](../../../../core/servers/deploy/configure/publish-site-data.md) individuellement.|  
|Configurer un point de connexion de service|Sur le site de niveau supérieur de votre hiérarchie, vous devez prévoir d’installer et de configurer le point de connexion de service. Pour plus d’informations, consultez [À propos du point de connexion de service dans System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Ajouter des rôles de système de site|Installez un ou plusieurs rôles de système de site supplémentaires sur des sites individuels.  Consultez [Ajouter des rôles de système de site pour System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md).|  
|Configurer les limites et groupes de limites de site|Spécifiez les limites qui définissent les emplacements réseau sur votre intranet pouvant contenir les appareils que vous souhaitez gérer, puis configurez les groupes de limites pour permettre aux clients situés à ces emplacements réseau de trouver les ressources des services Configuration Manager. Voir [Définir des limites de site et les groupes de limites pour System Center Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).|  
|Configurer les groupes de points de distribution|Configurez des groupes logiques de points de distribution pour faciliter la gestion des déploiements. Voir [Gérer les groupes de points de distribution](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) dans [Installer et configurer des points de distribution pour System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).|  
|Exécuter la découverte|Exécutez la découverte pour trouver les ressources sur votre réseau, notamment l’infrastructure réseau, les appareils et les utilisateurs.<br /><br /> Consultez [Exécuter la découverte pour System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md).|  
|Ajouter de la redondance et de la capacité pour les administrateurs qui gèrent votre infrastructure|Vous pouvez installer des fournisseurs SMS et des consoles Configuration Manager supplémentaires pour étendre les fonctionnalités mises à la disposition des administrateurs qui gèrent votre infrastructure :<br /><br /> **Installez des fournisseurs SMS supplémentaires** pour fournir une redondance aux points de contact qui gèrent votre site et votre hiérarchie. Consultez [Gérer le fournisseur SMS](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) dans [Modifier votre infrastructure System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).<br /><br /> **Installez des consoles Configuration Manager supplémentaires** pour fournir un accès à plusieurs utilisateurs administratifs supplémentaires simultanément. Voir [Installer des consoles Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md).|  
|Configurer des composants de site|Vous pouvez configurer des composants de site sur chaque site pour modifier le comportement des rôles de système du site et les rapports d’état du site. Consultez [Composants de site pour System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md).|  
|Créer des regroupements personnalisés|En utilisant les informations découvertes sur les appareils et les utilisateurs, créez des regroupements personnalisés d’objets pour simplifier les tâches de gestion à venir. Voir [Comment créer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|Configurer les paramètres de gestion des déploiements à haut risque|Configurez les paramètres d’un site pour avertir les utilisateurs administratifs quand ils créent un déploiement de séquence de tâches à haut risque.  Consultez [Paramètres de gestion de déploiements à haut risque pour System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md).|  
|Configurer des réplicas de base de données pour les points de gestion|Configurez un réplica de base de données pour réduire la charge processeur placée sur le serveur de base de données de site par les points de gestion qui traitent les demandes des clients. Consultez [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).|  
|Configurer un groupe de disponibilité SQL Server AlwaysOn pour héberger la base de données du site|À partir de la version 1602, vous pouvez configurer des groupes de disponibilité, telle une solution de haute disponibilité et de récupération d’urgence, pour héberger la base de données des sites principaux et du site d’administration centrale. Voir [SQL Server AlwaysOn pour une base de données de site à haut niveau de disponibilité pour System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).|  
|Modifier la réplication entre sites|Pour en savoir plus sur les sujets suivants, consultez [Transfert de données entre sites dans System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md) :<br /><br /> Configurer [File-based replication](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) entre sites secondaires<br /><br /> Configurer [Database replication links](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Configurer [Distributed views](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  



<!--HONumber=Dec16_HO3-->


