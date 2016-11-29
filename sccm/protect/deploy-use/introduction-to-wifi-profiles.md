---
title: "Présentation des profils Wi-Fi | System Center Configuration Manager"
description: "Découvrez comment utiliser des profils Wi-Fi dans System Center Configuration Manager pour déployer des paramètres de réseau sans fil pour les utilisateurs de votre organisation."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 86725460-c2f3-49ed-90aa-6b2724d34d69
caps.latest.revision: 8
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 30fefb291a6fccb630d5e3272ce7266339c9139c


---
# <a name="introduction-to-wi-fi-profiles-in-system-center-configuration-manager"></a>Présentation des profils Wi-Fi dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez des profils Wi-Fi dans System Center Configuration Manager pour déployer des paramètres de réseau sans fil pour les utilisateurs de votre organisation. En déployant ces paramètres, vous réduisez l'effort que doit fournir l'utilisateur final pour se connecter au réseau sans fil.  

 Par exemple, vous avez installé un nouveau réseau Wi-Fi nommé **Contoso Wi-Fi**. Vous souhaitez maintenant configurer tous les appareils qui exécutent le système d'exploitation iOS avec les paramètres requis pour la connexion à ce réseau. Vous pouvez créer un profil Wi-Fi contenant les paramètres nécessaires pour se connecter au réseau sans fil **Contoso Wi-Fi** . Vous pouvez ensuite déployer ce profil à tous les utilisateurs disposant d'appareils qui exécutent iOS dans votre hiérarchie. Les utilisateurs des appareils iOS voient le réseau de l'entreprise dans la liste des réseaux sans fil et peuvent immédiatement se connecter à ce réseau.  

 Vous pouvez configurer les types d'appareil suivants avec des profils Wi-Fi :  

-   Appareils qui exécutent Windows 8.1 32 bits  

-   Appareils qui exécutent Windows 8.1 64 bits  

-   Appareils qui exécutent Windows RT 8.1  

-   Appareils qui exécutent Windows Phone 8.1  

-   Appareils qui exécutent Windows 10 Desktop ou Mobile  

-   Appareils IPhone qui exécutent iOS 5, iOS 6, iOS 7 et iOS 8  

-   Appareils IPad qui exécutent iOS 5, iOS 6, iOS 7 et iOS 8  

-   Appareils Android qui exécutent la version 4  

> [!IMPORTANT]  
>  Pour déployer des profils sur des appareils Android, iOS, Windows Phone et sur des appareils Windows 8.1 ou version ultérieure inscrits, ces appareils doivent être inscrits dans Microsoft Intune. Pour plus d'informations sur la façon d'inscrire vos appareils, consultez [Gérer les appareils mobiles avec Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).  

 Lorsque vous créez un profil Wi-Fi, vous pouvez inclure un large éventail de paramètres de sécurité. Ceux-ci incluent des certificats pour l’authentification de client et la validation de serveur qui ont été mis en service à l’aide des profils de certificat Configuration Manager. Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  



<!--HONumber=Nov16_HO1-->


