---
title: "Serveurs de système de site pris en charge | Microsoft Docs"
description: "Déterminez les versions de Windows que vous pouvez utiliser pour héberger un site ou un rôle de système de site System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
translationtype: Human Translation
ms.sourcegitcommit: d23b98b362fb016c53974f851c48fa7200d2b2e3
ms.openlocfilehash: b7c24dee94bca4ce69e0ba8f33129a0b21819d13


---
# <a name="supported-operating-systems-for-system-center-configuration-manager--site-system-servers"></a>Systèmes d’exploitation pris en charge pour les serveurs de système de site System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Cet article explique en détail les versions de Windows que vous pouvez utiliser pour héberger un site ou un rôle de système de site System Center Configuration Manager.


Utilisez les informations de cette rubrique ainsi que celles contenues dans les articles suivants :
-   [Matériel recommandé pour Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Prérequis des sites et systèmes de site pour Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Taille et échelle de Configuration Manager en chiffres](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-----standard-datacenter"></a>Windows Server 2016 – Standard, Datacenter
Windows Server 2016 est pris en charge à compter de Configuration Manager version 1606 assortie du correctif cumulatif KB3186654 (ou version de référence 1606 publiée en octobre 2016).

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

     Les points de distribution prennent en charge diverses configurations ayant chacune des conditions requises différentes. Dans certains cas, ils prennent également en charge l’installation non seulement sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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

-   Point de migration d’état

## <a name="windows-server-2012-r2-x64---standard-datacenter"></a>Windows Server 2012 R2 (x64) – Standard, Datacenter  
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

     Les points de distribution prennent en charge diverses configurations ayant chacune des conditions requises différentes. Dans certains cas, ils prennent également en charge l’installation non seulement sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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

-   Point de migration d’état  

## <a name="windows-server-2012-x64---standard-datacenter"></a>Windows Server 2012 (x64) – Standard, Datacenter  
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

     Les points de distribution prennent en charge diverses configurations ayant chacune des conditions requises différentes. Dans certains cas, ils prennent également en charge l’installation non seulement sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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

-   Point de migration d’état  

## <a name="windows-server-2008-r2-with-sp1-x64-----standard-enterprise-datacenter"></a>Windows Server 2008 R2 SP1 (x64) – Standard, Entreprise, Datacenter  
 Windows Server 2008 R2 bénéficie désormais du support étendu au lieu du support standard, comme indiqué dans la [politique de support Microsoft](https://support.microsoft.com/lifecycle). Pour plus d’informations sur la prise en charge à venir de ces systèmes d’exploitation en tant que serveurs de système de site avec Configuration Manager, consultez [Fonctionnalités supprimées et déconseillées dans System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

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

     Les points de distribution prennent en charge diverses configurations ayant chacune des conditions requises différentes. Dans certains cas, ils prennent également en charge l’installation non seulement sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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

-   Point de migration d’état  

## <a name="windows-server-2008-with-sp2-x86-x64---standard-enterprise-datacenter"></a>Windows Server 2008 avec SP2 (x86, x64) – Standard, Entreprise, Datacenter  
 Windows Server 2008 bénéficie désormais du support étendu au lieu du support standard, comme indiqué dans la [politique de support Microsoft](https://support.microsoft.com/lifecycle). Pour plus d’informations sur la prise en charge à venir de ces systèmes d’exploitation en tant que serveurs de système de site avec Configuration Manager, consultez [Fonctionnalités supprimées et déconseillées dans System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

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

    -   Les points de distribution sur ce système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution sur ce système d’exploitation sont pris en charge pour PXE, mais ne prennent pas en charge le démarrage réseau des ordinateurs clients en mode EFI. Les ordinateurs clients avec un démarrage BIOS ou EFI en mode hérité sont pris en charge.  

    -   Les points de distribution prennent en charge diverses configurations ayant chacune des conditions requises différentes. Dans certains cas, ils prennent également en charge l’installation non seulement sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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

-   Point de migration d’état  

## <a name="windows-10-x86-x64---pro-enterprise"></a>Windows 10 (x86, x64) – Professionnel, Entreprise  
**Serveurs de système de site :**  

-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne sont pas pris en charge pour PXE.  

    -   Les points de distribution sur cette version du système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution prennent en charge diverses configurations ayant chacune des conditions requises différentes. Dans certains cas, ils prennent également en charge l’installation non seulement sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-81-x86-x64---professional-enterprise"></a>Windows 8.1 (x86, x64) – Professionnel, Entreprise  
**Serveurs de système de site :**  

-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne sont pas pris en charge pour PXE.  

    -   Les points de distribution sur cette version du système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution prennent en charge diverses configurations ayant chacune des conditions requises différentes. Dans certains cas, ils prennent également en charge l’installation non seulement sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-8-x86-x64---professional-enterprise-distribution-point"></a>Windows 8 (x86, x64) – Point de distribution Professionnel, Entreprise  
**Serveurs de système de site :**  

-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne sont pas pris en charge pour PXE.  

    -   Les points de distribution sur cette version du système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution prennent en charge diverses configurations ayant chacune des conditions requises différentes. Dans certains cas, ils prennent également en charge l’installation non seulement sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-7-with-sp1-x86-x64---professional-enterprise-ultimate"></a>Windows 7 avec SP1 (x 86, x 64) – Professionnel, Entreprise, Édition Intégrale  
**Serveurs de système de site :**  

-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne sont pas pris en charge pour PXE.  

    -   Les points de distribution sur cette version du système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution prennent en charge diverses configurations ayant chacune des conditions requises différentes. Dans certains cas, ils prennent également en charge l’installation non seulement sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="the-server-core-installation-of-windows-server-2012"></a>Installation minimale de Windows Server 2012  
 Outre les systèmes d’exploitation antérieurs, l’installation minimale de Windows Server 2012 est prise en charge pour une utilisation en tant que point de distribution avec les limitations suivantes :  

-   Seul x64 est pris en charge.  

-   Les points de distribution sur ce système d’exploitation ne prennent pas en charge PXE ou la multidiffusion.  

## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>Installation minimale de Windows Server 2012 R2  
 Outre les systèmes d’exploitation antérieurs, l’installation minimale de Windows Server 2012 R2 est prise en charge pour une utilisation en tant que point de distribution avec les limitations suivantes :  

-   Seul x64 est pris en charge.  

-   Les points de distribution sur ce système d’exploitation ne prennent pas en charge PXE ou la multidiffusion.  



<!--HONumber=Dec16_HO3-->


