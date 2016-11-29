---
title: Configurer la gestion des appareils iOS et Mac hybride avec System Center Configuration Manager et Microsoft Intune
description: Configurez la gestion des appareils iOS avec System Center Configuration Manager et Microsoft Intune.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: 10
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3754f0e49d8393aed51bb6519af99b9eb728402f


---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurer la gestion des appareils iOS hybride avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec Configuration Manager et Intune, vous pouvez activer l’inscription d’appareils iOS et Mac OS X BYOD (« Apportez votre propre appareil ») pour octroyer l’accès à la messagerie et aux ressources de l’entreprise aux utilisateurs iPhone, iPad et Mac. Une fois que les utilisateurs installent l’application portail d’entreprise Intune, leurs appareils peuvent être ciblés avec la stratégie. Pour pouvoir gérer des appareils iOS et Mac, vous devez importer un certificat des services de notifications Push Apple (APN) provenant d’Apple. Ce certificat permet à Intune de gérer les appareils iOS et Mac et établit une connexion IP agréée et chiffrée avec les services de l’autorité de gestion des appareils mobiles.  

 Vous pouvez aussi inscrire des appareils iOS d’entreprise.  Consultez [Inscrire des appareils d’entreprise](enroll-company-owned-devices.md).  

## <a name="enable-ios-device-enrollment"></a>Activer l’inscription d’appareils iOS  
 Pour prendre en charge l’inscription d’appareils iOS, procédez comme suit :  

#### <a name="set-up-ios-device-enrollment-in-configuration-manager"></a>Configurer l’inscription d’appareils iOS dans Configuration Manager  

1.  **Conditions préalables** : pour configurer l’inscription pour n’importe quelle plateforme, conformez-vous aux conditions préalables et appliquez les procédures indiquées dans [Configurer la gestion hybride des appareils mobiles](setup-hybrid-mdm.md).    

2.  **Téléchargez une demande de signature de certificat** : un fichier de demande de signature de certificat (.csr) est nécessaire pour demander un certificat APNs auprès d’Apple.  

    1.  Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud**> **Abonnements Microsoft Intune**.  

    2.  Sous l’onglet **Accueil** , cliquez sur **Créer une demande de certificat APNs**. La boîte de dialogue **Effectuer une demande de signature de certificat APNs** s'ouvre.  

    3.  Cliquez sur**Parcourir** pour accéder à l'emplacement auquel vous souhaitez enregistrer le fichier du nouveau certificat de demande de signature (.csr). Enregistrez localement le fichier de demande de signature de certificat (.csr).  

    4.  Cliquez sur **Télécharger**. Le nouveau fichier .csr Microsoft Intune se télécharge et il est enregistré par Configuration Manager. Le fichier .csr est utilisé pour demander un certificat de relation d'approbation à partir du portail Apple Push Certificates.  

3.  **Demandez un certificat APNs auprès d’Apple** : le certificat APNs (Apple Push Notification service) est utilisé pour établir une relation d’approbation entre le service de gestion, Intune et les appareils mobiles iOS inscrits.  

    1.  Dans un navigateur, accédez au [portail Apple Push Certificates](http://go.microsoft.com/fwlink/?LinkId=269844) et connectez-vous avec votre ID Apple d’entreprise. Cet ID Apple doit être utilisé ultérieurement pour renouveler votre certificat APNs.  

    2.  Terminez l’Assistant en utilisant le fichier (.csr) de demande de signature de certificat. Téléchargez le certificat APNs et enregistrez le fichier .pem localement. Ce fichier de certificat APNs (.pem) est utilisé pour établir une relation d’approbation entre le serveur Apple Push Notification et l’autorité de gestion des appareils mobiles Intune.  

4.  **Activez l’inscription et téléchargez le certificat APNs** : pour activer l’inscription iOS, téléchargez le certificat APNs.  

    1.  Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud** > **Abonnement Microsoft Intune**.  

    2.  Sous l’onglet **Accueil** , dans le groupe **Abonnement** , cliquez sur **Configurer des plateformes** > **iOS**.  

        > [!NOTE]  
        >  Ne téléchargez pas le certificat APNs tant que vous n’avez pas activé l’inscription iOS dans la console Configuration Manager.  

    3.  Dans la boîte de dialogue **Propriétés des abonnements Microsoft Intune** , sélectionnez l’onglet **iOS** et cochez la case **Activer l’inscription iOS** .  

    4.  Cliquez sur **Parcourir**et accédez au fichier (.cer) du certificat APNs téléchargé à partir d’Apple. Configuration Manager affiche les informations du certificat APNs. Cliquez sur **OK** pour enregistrer le certificat APNs sur Intune.  

 Une fois la configuration effectuée, vous devez faire savoir aux utilisateurs comment inscrire leurs appareils. Consultez [Ce qu’il faut dire aux utilisateurs sur l’inscription de leurs appareils](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Ces informations s’appliquent aux appareils mobiles gérés par Microsoft Intune et Configuration Manager.



<!--HONumber=Nov16_HO1-->


