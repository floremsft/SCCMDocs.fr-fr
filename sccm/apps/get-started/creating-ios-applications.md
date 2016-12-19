---
title: "Créer des applications iOS | Documents Microsoft"
description: "Examinez les éléments à prendre en compte quand vous créez et déployez des applications pour des appareils iOS."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5420109-6538-4430-9ca6-db352ee84c2e
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: e9e34359f4412ba07b9fb49f871a1eb2d36cecf8
ms.openlocfilehash: eb2d1245932d71bd10fd63d95a155eae7d128836


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Créer des applications iOS avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Gardez à l’esprit les considérations suivantes quand vous créez et déployez des applications pour appareils iOS.  

## <a name="general-considerations"></a>Éléments généraux à prendre en compte  
 Configuration Manager prend en charge le déploiement des types d’applications suivants :  

|Type d'appareil|Fichiers pris en charge|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> Dans System Center Configuration Manager, vous n’avez pas besoin de spécifier de fichier de liste de propriétés (.plist) lors de l’importation d’une application iOS.|  

 Les actions de déploiement suivantes sont prises en charge :  

|Type d'appareil|Actions prises en charge|  
|-----------------|-----------------------|  
|iOS|**Disponible**, **Obligatoire**. L’utilisateur doit donner son consentement pour l’installation et la désinstallation.

> [!IMPORTANT]  
>  Actuellement, les utilisateurs finaux ne peuvent pas installer des applications d’entreprise à partir de l’application Portail d’entreprise Microsoft Intune pour iOS. Cela est dû au fait qu’il existe des restrictions concernant les applications publiées dans l’App Store iOS (consultez Directives de révision App Store, à la section 2). Les utilisateurs peuvent installer des applications d’entreprise (y compris les applications App Store gérées et des packages d’applications métiers) via le portail web Intune sur leur appareil (portal.manage.microsoft.com). Pour plus d’informations sur les fonctionnalités de gestion des appareils mobiles activées par l’application Portail d’entreprise Intune, consultez [Fonctionnalités de gestion des appareils inscrits de Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx).  



<!--HONumber=Dec16_HO3-->


