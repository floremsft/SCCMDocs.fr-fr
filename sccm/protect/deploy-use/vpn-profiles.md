---
title: Profils VPN dans System Center Configuration Manager | Microsoft Docs
description: "Découvrez comment utiliser des profils VPN dans System Center Configuration Manager pour déployer des paramètres VPN pour les utilisateurs de votre organisation."
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: 6
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: c11440556abc11d2c19ee0ff3c2bc9e518951e49
ms.lasthandoff: 03/04/2017


---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Profils VPN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Utilisez des profils VPN dans System Center Configuration Manager (aussi appelé ConfigMgr ou SCCM) pour déployer des paramètres VPN sur les utilisateurs de votre organisation. En déployant ces paramètres, vous réduisez l'effort que doit fournir l'utilisateur final pour se connecter aux ressources du réseau d'entreprise.  

 Par exemple, vous souhaitez provisionner tous les appareils qui exécutent le système d’exploitation Windows RT avec les paramètres requis pour se connecter à un partage de fichiers sur le réseau d’entreprise. Vous pouvez créer un profil VPN contenant les paramètres nécessaires pour la connexion au réseau d’entreprise, puis déployer ce profil auprès de tous les utilisateurs qui disposent d’appareils exécutant Windows RT dans votre hiérarchie. Les utilisateurs d’appareils exécutant Windows RT voient s’afficher la connexion VPN dans la liste des réseaux disponibles et peuvent facilement se connecter à ce réseau.  

 Quand vous créez un profil VPN, vous pouvez inclure de nombreux paramètres de sécurité, notamment des certificats pour la validation du serveur et l’authentification du client, configurés à l’aide de profils de certificat System Center Configuration Manager. Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  

 Les sections ci-dessous indiquent quels appareils vous pouvez configurer avec des profils VPN si vous utilisez Configuration Manager.

 Consultez la page [Utilisation de profils VPN sur des appareils mobiles dans System Center Configuration Manager](/sccm/mdm/deploy-use/create-vpn-profiles) pour passer en revue les appareils que vous pouvez configurer en utilisant Configuration Manager avec Microsoft Intune.  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Profils VPN si Configuration Manager est utilisé  
 Le tableau suivant décrit les profils VPN que vous pouvez configurer pour diverses plateformes d’appareil.  

|Type de connexion|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|Non|Non|Non|Non|  
|**Pulse Secure**|Oui|Non|Oui|Oui|  
|**Client F5 Edge**|Oui|Non|Oui|Oui|  
|**Dell SonicWALL Mobile Connect**|Oui|Non|Oui|Oui|  
|**Check Point Mobile VPN**|Oui|Non|Oui|Oui|  
|**Microsoft SSL (SSTP)**|Oui|Oui|Oui|Non|  
|**Microsoft Automatic**|Oui|Oui|Oui|Non|  
|**IKEv2**|Oui|Oui|Oui|Non|  
|**PPTP**|Oui|Oui|Oui|Non|  
|**L2TP**|Oui|Oui|Oui|Non|  

### <a name="next-steps"></a>Étapes suivantes  
 Utilisez les rubriques suivantes pour planifier, configurer, utiliser et gérer des profils VPN dans Configuration Manager.  

-   [Configuration requise pour les profils VPN dans System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Sécurité et confidentialité pour les profils VPN dans System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)

