---
title: Pare-feu et domaines | System Center Configuration Manager
description: "Configurez les pare-feu, les ports et les domaines pour préparer votre infrastructure pour les communications System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cd2da8ea3bf0e1351f791d88af3dcbf95f8d6be8


---
# <a name="configure-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>Configurer les pare-feu, les ports et les domaines pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour préparer votre réseau à prendre en charge System Center Configuration Manager, prévoyez de configurer l’infrastructure, notamment les pare-feu, pour autoriser les communications Configuration Manager.  

|Considération|Détails|  
|-------------------|-------------|  
|**Ports et protocoles** utilisés par les différentes fonctionnalités de Configuration Manager. Certains ports sont nécessaires, tandis que d’autres **Domaines et services** peuvent être personnalisés.|La plupart des communications Configuration Manager utilisent des ports courants, tels que le port 80 pour le protocole HTTP et le port 443 pour le protocole HTTPS. Toutefois, [certains rôles de système de site prennent en charge l’utilisation de sites web personnalisés](/sccm/core/plan-design/network/websites-for-site-system-servers) et de ports personnalisés.<br /><br /> **Avant de déployer Configuration Manager**, identifiez les ports que vous souhaitez utiliser et configurez les pare-feu de manière appropriée.<br /><br /> **Ultérieurement, si vous avez besoin de modifier un port** après avoir installé Configuration Manager, n’oubliez pas de mettre à jour les pare-feu sur les appareils et sur le réseau, et également de modifier la configuration du port dans Configuration Manager.<br /><br /> Pour plus d’informations, consultez : </br>- [Guide pratique pour configurer les ports de communication des clients](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [Ports utilisés dans Configuration Manager](../../../core/plan-design/hierarchy/ports.md) </br>- [Conditions requises pour l’accès Internet pour le point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|**Domaines et services** auxquels les serveurs et clients de site pourraient devoir accéder.|Certaines fonctionnalités de Configuration Manager peuvent nécessiter que les clients et les serveurs de site accèdent à des services et domaines spécifiques sur Internet, comme Windowsudpate.microsoft.com ou le service Microsoft Intune.<br /><br /> Si vous voulez utiliser Microsoft Intune pour gérer des appareils mobiles, vous devez également configurer l’accès aux [ports et domaines requis par Intune](https://docs.microsoft.com/en-us/intune/get-started/network-infrastructure-requirements-for-microsoft-intune).|  
|**Serveurs proxy** pour les serveurs de système de site et les communications client. Vous pouvez spécifier des serveurs proxy distincts pour les différents clients et serveurs du système de site.|Étant donné que ces configurations sont effectuées lors de l’installation d’un rôle de système de site ou d’un client, il vous suffit de connaître les configurations de serveur proxy pour référence ultérieure lorsque vous configurerez des rôles de système de site et des clients.<br /><br /> Si vous ne savez pas si votre déploiement nécessite l’utilisation de serveurs proxy, consultez [Prise en charge des serveurs proxy dans System Center Configuration Manager](../../../core/plan-design/network/proxy-server-support.md) pour en savoir plus sur les rôles de système de site et les actions de client susceptibles d’utiliser un serveur proxy.|  



<!--HONumber=Nov16_HO1-->


