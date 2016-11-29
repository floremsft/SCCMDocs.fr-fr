---
title: "Créer des applications iOS | System Center Configuration Manager"
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4c3845635846cae183e81d0ddb9c8222dabd8929


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Créer des applications iOS avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

En plus des autres exigences et procédures System Center Configuration Manager à observer pour créer une application, vous devez aussi prendre en compte les éléments suivants au moment de créer et de déployer des applications pour des appareils iOS.  

## <a name="general-considerations"></a>Éléments généraux à prendre en compte  
 Configuration Manager prend en charge le déploiement des types d’applications suivants :  

|Type d'appareil|Fichiers pris en charge|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> Dans System Center Configuration Manager, vous n’avez pas besoin de spécifier de fichier de liste de propriétés (.plist) lors de l’importation d’une application iOS.|  

 Les actions de déploiement suivantes sont prises en charge :  

|Type d'appareil|Actions prises en charge|  
|-----------------|-----------------------|  
|iOS|Disponible, Obligatoire (l’utilisateur doit toutefois donner son consentement pour l’installation), Désinstaller|  

> [!IMPORTANT]  
>  Actuellement, les utilisateurs finaux ne peuvent pas installer des applications d’entreprise à partir de l’application Portail d’entreprise Microsoft Intune pour iOS. Cette limitation est due à des restrictions portant sur les applications publiées dans l’App Store iOS (consultez les consignes éditoriales sur l’App Store, à la section 2). Les utilisateurs peuvent installer des applications d’entreprise (y compris les applications App Store gérées et des packages d’applications métiers) via le portail web Intune sur leur appareil (portal.manage.microsoft.com). Pour plus d’informations sur les fonctionnalités de gestion des appareils mobiles activées par l’application Portail d’entreprise Intune, consultez [Fonctionnalités de gestion des appareils inscrits dans Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx).  



<!--HONumber=Nov16_HO1-->


