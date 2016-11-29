---
title: Configurer la gestion hybride des appareils mobiles Android avec System Center Configuration Manager et Microsoft Intune
description: "Préparez la gestion des appareils mobiles Android avec Configuration Manager et Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fa189e812a2e3104cb337ccf40c693621745ee53


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurer la gestion hybride des appareils mobiles Android avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour System Center Configuration Manager, les utilisateurs peuvent télécharger l’application de portail d’entreprise Android depuis Google Play qui leur permet d’inscrire des appareils Android (y compris Samsung KNOX). Avec l’application de portail d’entreprise Android, vous pouvez gérer les paramètres de conformité, réinitialiser ou supprimer des appareils Android, déployer des applications et collecter l’inventaire matériel et logiciel. Si l’application de portail d’entreprise Android n’est pas installée sur les appareils Android, vous ne disposez pas de toutes les fonctions de gestion, telles que les paramètres de conformité et d’inventaire, mais vous pouvez encore déployer des applications sur des appareils Android.  

## <a name="prepare-to-manage-android-mobile-devices-with-configuration-manager-and-intune"></a>Préparer la gestion des appareils mobiles Android avec Configuration Manager et Intune  
 Les étapes suivantes permettent à Configuration Manager de gérer des appareils Android.  

#### <a name="to-enable-android-enrollment"></a>Pour activer l’inscription Android  

1.  **Prérequis** : avant de configurer l’inscription d’une plateforme, observez les prérequis et les procédures indiqués dans [Configurer la gestion hybride des appareils mobiles](setup-hybrid-mdm.md).  

2.  Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud** > **Abonnement Microsoft Intune**.  

3.  Sous l’onglet **Accueil** , dans le groupe **Abonnement** , cliquez sur **Configurer des plateformes** > **Android**.  

4.  Dans la boîte de dialogue **Propriétés d’abonnement Microsoft Intune** , sélectionnez l’onglet **Android** et cochez la case **Activer l’inscription Android** .  

 Une fois la configuration effectuée, vous devez faire savoir aux utilisateurs comment inscrire leurs périphériques. Consultez [Ce qu’il faut dire aux utilisateurs sur l’inscription de leurs appareils](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Ces informations s’appliquent aux appareils mobiles gérés par Microsoft Intune et Configuration Manager.



<!--HONumber=Nov16_HO1-->


