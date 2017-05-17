---
title: "Prérequis pour le contrôle à distance | Microsoft Docs"
description: "Prenez connaissance des prérequis pour le contrôle à distance dans System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: eafa0d85935c2009cc63d17b06ed83a4666d7fac
ms.contentlocale: fr-fr
ms.lasthandoff: 12/16/2016


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
 Le tableau suivant fournit des informations sur les systèmes d'exploitation pris en charge pour l’observateur de contrôle à distance. Pour plus d’informations sur les systèmes d’exploitation client pris en charge, consultez [Configurations prises en charge pour System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

|Système d'exploitation|Prise en charge de l’observateur|Plus d'informations|  
|----------------------|--------------------|----------------------|  
|Windows XP (32 bits)|Oui|Pour exécuter l’observateur de contrôle à distance sur ce système d’exploitation, vous devez d’abord télécharger et installer la [mise à jour du client Remote Desktop Connection (connexion du bureau à distance) (RDC) 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) à partir du Centre de téléchargement Microsoft.|  
|Windows XP (64 bits)|Non|Aucune information supplémentaire.|  
|Windows Vista (32 bits)|Oui|Pour exécuter l’observateur de contrôle à distance sur ce système d’exploitation, vous devez d’abord télécharger et installer la [mise à jour du client RDC (Remote Desktop Connection) 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) à partir du Centre de téléchargement Microsoft.|  
|Windows Vista (64 bits)|Oui|Pour exécuter l’observateur de contrôle à distance sur ce système d’exploitation, vous devez d’abord télécharger et installer la [mise à jour du client RDC (Remote Desktop Connection) 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) à partir du Centre de téléchargement Microsoft.|  
|Windows 7 (32 bits)|Oui|Aucune information supplémentaire.|  
|Windows 7 (64 bits)|Oui|Aucune information supplémentaire.|  
|Windows Server 2003 (32 bits)|Non|Aucune information supplémentaire.|  
|Windows Server 2003 (64 bits)|Non|Aucune information supplémentaire.|  
|Windows Server 2008 (32 bits)|Non|Aucune information supplémentaire.|  
|Windows Server 2008 (64 bits)|Non|Aucune information supplémentaire.|  
|Windows Server 2008 R2 (64 bits)|Oui|Aucune information supplémentaire.|  

## <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager  

|Dépendance|Plus d'informations|  
|----------------|----------------------|  
|Le contrôle à distance doit être activé pour les clients|Par défaut, le contrôle à distance n’est pas activé quand vous installez Configuration Manager. Pour plus d’informations sur l’activation et la configuration du contrôle à distance, consultez [Configuration du contrôle à distance dans System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Point de Reporting Services|Le rôle de système de site du point de Reporting Services doit être installé avant que vous puissiez exécuter des rapports pour le contrôle à distance. Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Autorisations de sécurité pour gérer le contrôle à distance|Pour accéder aux ressources de regroupement et lancer une session de contrôle à distance à partir de la console Configuration Manager : autorisations **Contrôler AMT**, **Lecture**, **Lire la ressource** et **Contrôle à distance** pour l’objet **Regroupement**.<br /><br /> Le rôle de sécurité **Opérateur d’outils à distance** inclut ces autorisations qui sont nécessaires pour gérer le contrôle à distance dans Configuration Manager.<br /><br /> Pour plus d’informations, consultez [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Vous devez également ajouter les utilisateurs auxquels vous souhaitez accorder l’autorisation d’utiliser le contrôle à distance et l’assistance à distance dans la liste des vues autorisées de contrôle à distance et d’assistance à distance à l’aide de l’option **Observateurs autorisés des options de contrôle à distance et d’assistance à distance** dans les paramètres client **Outils de contrôle à distance** .|  

