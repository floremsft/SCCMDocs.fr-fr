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
ms.sourcegitcommit: 593fbd0587d54490246f48ae54f666bac6b7830d
ms.openlocfilehash: 0ff83aed4d5e19806a8c69f4b45e39a6156dee7e


---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Profils VPN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Utilisez des profils VPN dans System Center Configuration Manager (aussi appelé ConfigMgr ou SCCM) pour déployer des paramètres VPN sur les utilisateurs de votre organisation. En déployant ces paramètres, vous réduisez l'effort que doit fournir l'utilisateur final pour se connecter aux ressources du réseau d'entreprise.  

 Par exemple, vous souhaitez provisionner tous les appareils qui exécutent le système d'exploitation iOS avec les paramètres requis pour se connecter à un partage de fichiers sur le réseau d'entreprise. Vous pouvez créer un profil VPN contenant les paramètres nécessaires pour la connexion au réseau d'entreprise, puis déployer ce profil auprès de tous les utilisateurs qui disposent d'appareils exécutant iOS dans votre hiérarchie. Les utilisateurs d'appareils iOS voient la connexion VPN dans la liste des réseaux disponibles et peuvent se connecter à ce réseau avec un minimum d'effort.  

 Quand vous créez un profil VPN, vous pouvez inclure de nombreux paramètres de sécurité, notamment des certificats pour la validation du serveur et l’authentification du client, configurés à l’aide de profils de certificat System Center Configuration Manager. Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  

 Les sections ci-dessous indiquent quels appareils vous pouvez configurer avec des profils VPN si vous utilisez Configuration Manager ou Configuration Manager avec Microsoft Intune.  

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

## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Profils VPN si Configuration Manager est utilisé en association avec Intune  
 Pour déployer des profils sur des appareils iOS, Android, Windows Phone et Windows 8.1, ces appareils doivent être inscrits dans Microsoft Intune. Les appareils sur d’autres plateformes peuvent également être inscrits auprès Intune. Pour plus d’informations sur la procédure d’inscription, consultez [Gérer les appareils mobiles avec Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). Ce tableau présente le type de connexion pris en charge pour chaque plateforme d’appareil :  

|Type de connexion|iOS et Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop et Mobile|  
|---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
|Cisco AnyConnect|Oui|Oui|Non|Non|Non|Non|Oui (OMA-URI)|  
|Pulse Secure|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
|Client F5 Edge|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
|Dell SonicWALL Mobile Connect|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
|Check Point Mobile VPN|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
|Microsoft SSL (SSTP)|Non|Non|Oui|Oui|Oui|Non|Non|  
|Microsoft Automatic|Non|Non|Oui|Oui|Oui|Non|Oui (OMA-URI)|  
|IKEv2|Oui (Stratégie personnalisée)|Non|Oui|Oui|Oui|Oui|Oui (OMA-URI)|  
|PPTP|Oui|Non|Oui|Oui|Oui|Non|Oui (OMA-URI)|  
|L2TP|Oui|Non|Oui|Oui|Oui|Non|Oui (OMA-URI)|  

### <a name="next-steps"></a>Étapes suivantes  
 Utilisez les rubriques suivantes pour planifier, configurer, utiliser et gérer des profils VPN dans Configuration Manager.  

-   [Configuration requise pour les profils VPN dans System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Sécurité et confidentialité pour les profils VPN dans System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)



<!--HONumber=Dec16_HO3-->


