---
title: "Prérequis pour le contrôle à distance"
titleSuffix: Configuration Manager
description: "Prenez connaissance des prérequis pour le contrôle à distance dans System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: e7287ae7df68ebbcb8f251b8d001233a647596ee
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="prerequisites-for-remote-control-in-system-center-configuration-manager"></a>Configuration requise pour le contrôle à distance dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le contrôle à distance dans System Center Configuration Manager comporte des dépendances externes et des dépendances au sein du produit.  

## <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  

|Dépendance|Plus d'informations|  
|----------------|----------------------|  
|Pilote de carte vidéo d'ordinateur|Assurez-vous que la toute dernière version du pilote vidéo est installée sur les ordinateurs clients pour garantir des performances optimales du contrôle à distance.|  

 Les appareils exécutant Windows Embedded, Windows Embedded for Point of Service (POS) et Windows Fundamentals for Legacy PCs ne prennent pas en charge l’observateur de contrôle à distance, mais ils prennent en charge le client du contrôle à distance.  

 Le contrôle à distance de Configuration Manager ne permet pas d’administrer à distance les ordinateurs clients qui exécutent Systems Management Server 2003 ou Configuration Manager 2007.  

> [!NOTE]  
>  Aucun service Windows n’est nécessaire comme dépendance externe pour le contrôle à distance.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Systèmes d’exploitation pris en charge pour l’observateur de contrôle à distance  
La visionneuse de contrôle à distance est gérée sur tous les systèmes d’exploitation pris en charge pour la console Configuration Manager. Pour plus d’informations, consultez l’article [Configurations prises en charge pour les consoles System Center Configuration Manager](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager  

|Dépendance|Plus d'informations|  
|----------------|----------------------|  
|Le contrôle à distance doit être activé pour les clients|Par défaut, le contrôle à distance n’est pas activé quand vous installez Configuration Manager. Pour plus d’informations sur l’activation et la configuration du contrôle à distance, consultez [Configuration du contrôle à distance dans System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Point de Reporting Services|Le rôle de système de site du point de Reporting Services doit être installé avant que vous puissiez exécuter des rapports pour le contrôle à distance. Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Autorisations de sécurité pour gérer le contrôle à distance|Pour accéder aux ressources du regroupement et lancer une session de contrôle à distance à partir de la console Configuration Manager : autorisations **Lecture**, **Lire la ressource** et **Contrôle à distance** pour l’objet **Regroupement**.<br /><br /> Le rôle de sécurité **Opérateur d’outils à distance** inclut ces autorisations qui sont nécessaires pour gérer le contrôle à distance dans Configuration Manager.<br /><br /> Pour plus d’informations, consultez [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Par ailleurs, il faut donner aux utilisateurs concernés l’autorisation d’utiliser le contrôle à distance en les ajoutant à la liste **Observateurs autorisés du contrôle à distance et de l’assistance à distance** dans les paramètres client **Outils de contrôle à distance**.
