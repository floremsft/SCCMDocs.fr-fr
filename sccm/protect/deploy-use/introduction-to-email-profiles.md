---
title: "Présentation des profils de messagerie | Microsoft Docs"
description: "Découvrez comment utiliser des profils de messagerie pour permettre à vos utilisateurs d’accéder à la messagerie d’entreprise sur leurs appareils avec une installation minimale."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c4e2dc48-91c2-438f-9e1a-947b1125b0e2
caps.latest.revision: 3
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: b936a0914f8811f755cbb6983fefc063fbc4f97c


---
# <a name="introduction-to-email-profiles-in-system-center-configuration-manager"></a>Présentation des profils de messagerie dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les profils de messagerie fonctionnent avec Microsoft Intune pour vous permettre de configurer des appareils avec des profils de messagerie et des restrictions en utilisant Exchange ActiveSync. Cela permet à vos utilisateurs d'accéder à la messagerie d'entreprise sur leurs appareils avec une installation minimale requise de leur part.  

 Vous pouvez configurer les types d'appareils suivants avec des profils de messagerie :  

-   Appareils exécutant Windows Phone 8  

-   Appareils exécutant Windows Phone 8.1  

-   Appareils exécutant Windows 10 Mobile  

-   Appareils iPhone exécutant iOS 5, iOS 6, iOS 7 et iOS 8  

-   Appareils IPad qui exécutent iOS 5, iOS 6, iOS 7 et iOS 8  

> [!IMPORTANT]  
>  Pour déployer des profils sur des appareils iOS, Android Samsung KNOX Standard, Windows Phone, Windows 8.1 ou Windows 10, ces appareils doivent être inscrits dans Intune. Pour plus d'informations sur la façon d'inscrire vos appareils, consultez [Gérer les appareils mobiles avec Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 En plus de configurer un compte de messagerie sur l'appareil, vous pouvez également configurer des paramètres de synchronisation pour les contacts, les calendriers et les tâches.  

 Quand vous créez un profil de messagerie, vous pouvez inclure de nombreux paramètres de sécurité, notamment des certificats pour l’identité, le chiffrement et la signature configurés à l’aide de profils de certificat System Center Configuration Manager. Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  



<!--HONumber=Dec16_HO3-->


