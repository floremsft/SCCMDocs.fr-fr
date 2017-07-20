---
title: "Serveurs de système de site pris en charge | Microsoft Docs"
description: "Déterminez les versions de Windows que vous pouvez utiliser pour héberger un site ou un rôle de système de site System Center Configuration Manager."
ms.custom: na
ms.date: 06/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 0ec241d07f51b80b84d65676ef1207b31a9a9983
ms.openlocfilehash: be635e4df79b57b6f650287fa3774d2c10613cee
ms.contentlocale: fr-fr
ms.lasthandoff: 06/28/2017


---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Systèmes d’exploitation pris en charge pour les serveurs de système de site System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Cet article explique en détail les versions de Windows que vous pouvez utiliser pour héberger un site ou un rôle de système de site System Center Configuration Manager.


Utilisez les informations de cette rubrique ainsi que celles contenues dans les articles suivants :
-   [Matériel recommandé pour Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Prérequis des sites et systèmes de site pour Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Taille et échelle de Configuration Manager en chiffres](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016 : Standard et Datacenter
À compter de la version 1606, avec le correctif cumulatif KB3186654 (ou la version de base de référence 1606 publiée en octobre 2016), ce système d’exploitation est pris en charge pour les éléments suivants :

**Serveurs de site :**  

-   Site d'administration centrale  

-   Site principal  

-   Site secondaire  

**Serveurs de système de site :**  

-   Point de service Web du catalogue des applications  

-   Point du site web du catalogue des applications  

-   Point de synchronisation Asset Intelligence  

-   Point d'enregistrement de certificat  

-   Point de distribution  

     Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Point Endpoint Protection  

-   Point d'inscription  

-   Point proxy d'inscription  

-   Point d’état de secours  

-   Point de gestion

-   Point de Reporting Services  

-   Point de connexion de service  

-   Serveur de bases de données du site  

     Les serveurs de bases de données du site ne sont pas pris en charge sur un contrôleur de domaine en lecture seule (RODC). Pour plus d'informations, voir [Vous pouvez rencontrer des problèmes lors de l'installation de SQL Server sur un contrôleur de domaine](http://go.microsoft.com/fwlink/p/?LinkId=264856) dans la Base de connaissances Microsoft. En outre, les serveurs de site secondaire ne sont pris en charge sur aucun contrôleur de domaine.  

-   SMS_Provider  

-   Point de mise à jour logicielle  

-   Point de migration d'état

## <a name="windows-server-2012-r2-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64) : Standard et Datacenter  
**Serveurs de site :**  

-   Site d'administration centrale  

-   Site principal  

-   Site secondaire  

**Serveurs de système de site :**  

-   Point de service Web du catalogue des applications  

-   Point du site web du catalogue des applications  

-   Point de synchronisation Asset Intelligence  

-   Point d'enregistrement de certificat  

-   Point de distribution  

     Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Point Endpoint Protection  

-   Point d'inscription  

-   Point proxy d'inscription  

-   Point d’état de secours  

-   Point de gestion

-   Point de Reporting Services  

-   Point de connexion de service  

-   Serveur de bases de données du site  

     Les serveurs de bases de données du site ne sont pas pris en charge sur un contrôleur de domaine en lecture seule (RODC). Pour plus d'informations, voir [Vous pouvez rencontrer des problèmes lors de l'installation de SQL Server sur un contrôleur de domaine](http://go.microsoft.com/fwlink/p/?LinkId=264856) dans la Base de connaissances Microsoft. En outre, les serveurs de site secondaire ne sont pris en charge sur aucun contrôleur de domaine.  

-   SMS_Provider  

-   Point de mise à jour logicielle  

-   Point de migration d'état  

## <a name="windows-server-2012-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64) : Standard et Datacenter  
**Serveurs de site :**  

-   Site d'administration centrale  

-   Site principal  

-   Site secondaire  

**Serveurs de système de site :**  

-   Point de service Web du catalogue des applications  

-   Point du site web du catalogue des applications  

-   Point de synchronisation Asset Intelligence  

-   Point d'enregistrement de certificat  

-   Point de distribution  

     Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Point Endpoint Protection  

-   Point d'inscription  

-   Point proxy d'inscription  

-   Point d’état de secours  

-   Point de gestion

-   Point de Reporting Services  

-   Point de connexion de service  

-   Serveur de bases de données du site  

     Les serveurs de bases de données du site ne sont pas pris en charge sur un contrôleur de domaine en lecture seule (RODC). Pour plus d'informations, voir [Vous pouvez rencontrer des problèmes lors de l'installation de SQL Server sur un contrôleur de domaine](http://go.microsoft.com/fwlink/p/?LinkId=264856) dans la Base de connaissances Microsoft. En outre, les serveurs de site secondaire ne sont pris en charge sur aucun contrôleur de domaine.  

-   SMS_Provider  

-   Point de mise à jour logicielle  

-   Point de migration d'état  

## <a name="windows-server-2008-r2-with-sp1-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 R2 avec SP1 (x64) : Standard, Enterprise et Datacenter  
 Windows Server 2008 R2 bénéficie désormais du support étendu au lieu du support standard, comme indiqué dans la [Politique de support Microsoft](https://support.microsoft.com/lifecycle). Pour plus d’informations sur le support à venir de ces systèmes d’exploitation utilisés comme serveurs de système de site avec Configuration Manager, consultez [Fonctionnalités supprimées et déconseillées dans System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 Depuis Configuration Manager version 1702, ce système d’exploitation n’est pas pris en charge pour les serveurs de site ou la plupart des rôles de système de site, mais il continue d’être pris en charge pour le rôle de système de site de point de distribution (dont les points de distribution d’extraction, ainsi que pour PXE et la multidiffusion).

 Les versions antérieures à 1702 continuent de prendre en charge son utilisation pour les éléments suivants.


**Serveurs de site :**  

-   Site d'administration centrale  

-   Site principal  

-   Site secondaire  

**Serveurs de système de site :**  

-   Point de service Web du catalogue des applications  

-   Point du site web du catalogue des applications  

-   Point de synchronisation Asset Intelligence  

-   Point d'enregistrement de certificat  

-   Point de distribution  

     Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Point Endpoint Protection  

-   Point d'inscription  

-   Point proxy d'inscription  

-   Point d’état de secours  

-   Point de gestion

-   Point de Reporting Services  

-   Point de connexion de service  

-   Serveur de bases de données du site  

     Les serveurs de bases de données du site ne sont pas pris en charge sur un contrôleur de domaine en lecture seule (RODC). Pour plus d'informations, voir [Vous pouvez rencontrer des problèmes lors de l'installation de SQL Server sur un contrôleur de domaine](http://go.microsoft.com/fwlink/p/?LinkId=264856) dans la Base de connaissances Microsoft. En outre, les serveurs de site secondaire ne sont pris en charge sur aucun contrôleur de domaine.  

-   SMS_Provider  

-   Point de mise à jour logicielle  

-   Point de migration d'état  

## <a name="windows-server-2008-with-sp2-x86-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 avec SP2 (x86, x64) : Standard, Enterprise et Datacenter  
 Windows Server 2008 bénéficie désormais du support étendu au lieu du support standard, comme indiqué dans la [Politique de support Microsoft](https://support.microsoft.com/lifecycle). Pour plus d’informations sur le support à venir de ces systèmes d’exploitation utilisés comme serveurs de système de site avec Configuration Manager, consultez [Fonctionnalités supprimées et déconseillées dans System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

Ce système d’exploitation n’est pas pris en charge pour les serveurs de site ou les rôles de système de site, à l’exception du point de distribution et du point de distribution d’extraction. Vous pouvez continuer à utiliser ce système d’exploitation comme point de distribution jusqu’à l’annonce de la dépréciation de ce support ou jusqu’à l’expiration du support étendu de ce système d’exploitation. Pour plus d’informations, consultez [Échec de l’installation de System Center Configuration Manager CB et LTSB sur Windows Server 2008](https://support.microsoft.com/help/4015095).

**Serveurs de système de site :**  
-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution sur ce système d’exploitation sont pris en charge pour PXE, mais ne prennent pas en charge le démarrage réseau des ordinateurs clients en mode EFI. Les ordinateurs clients avec un démarrage BIOS ou EFI en mode hérité sont pris en charge.  

    -   Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64) : Professionnel et Entreprise  
**Serveurs de système de site :**  

-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne sont pas pris en charge pour PXE.  

    -   Les points de distribution sur cette version du système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86, x64) : Professionnel et Entreprise  
**Serveurs de système de site :**  

-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne sont pas pris en charge pour PXE.  

    -   Les points de distribution sur cette version du système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-8-x86-x64-professional-and-enterprise"></a>Windows 8 (x86, x64) : Professionnel et Entreprise
**Serveurs de système de site :**  

-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne sont pas pris en charge pour PXE.  

    -   Les points de distribution sur cette version du système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 avec SP1 (x86, x64) : Professionnel, Entreprise et Édition Intégrale  
**Serveurs de système de site :**  

-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne sont pas pris en charge pour PXE.  

    -   Les points de distribution sur cette version du système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


## <a name="the-server-core-installation-of-windows-server-2016"></a>Installation minimale de Windows Server 2016
À compter de la version 1606, avec le correctif cumulatif KB3186654 (ou la version de base de référence 1606 publiée en octobre 2016), ce système d’exploitation est pris en charge comme point de distribution avec les restrictions suivantes :  
  -   Seule la version 64 bits est prise en charge.
  -   Les points de distribution sur ce système d’exploitation ne prennent pas en charge PXE ou la multidiffusion.  


## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>Installation minimale de Windows Server 2012 R2  
 Outre les systèmes d’exploitation antérieurs indiqués, l’installation minimale de Windows Server 2012 R2 est prise en charge pour une utilisation comme point de distribution avec les limitations suivantes :  

-   Seule la version 64 bits est prise en charge.

-   Les points de distribution sur ce système d’exploitation ne prennent pas en charge PXE ou la multidiffusion.  

## <a name="the-server-core-installation-of-windows-server-2012"></a>Installation minimale de Windows Server 2012  
 Outre les systèmes d’exploitation antérieurs indiqués, l’installation minimale de Windows Server 2012 est également prise en charge pour une utilisation comme point de distribution avec les limitations suivantes :  

-   Seule la version 64 bits est prise en charge.  

-   Les points de distribution sur ce système d’exploitation ne prennent pas en charge PXE ou la multidiffusion.

