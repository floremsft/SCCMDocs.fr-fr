---
title: Configurer la gestion des appareils mobiles hybride Android avec System Center Configuration Manager et Microsoft Intune | Microsoft Docs
description: "Préparez la gestion des appareils mobiles Android avec Configuration Manager et Intune."
ms.custom: na
ms.date: 03/27/2017
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
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 199096db7a23fb14db98b95e75246ed254848ab7
ms.openlocfilehash: f6b949247435a2fede680cd8e146e5d7cf3989d9
ms.lasthandoff: 03/27/2017


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurer la gestion hybride des appareils mobiles Android avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique aide l’administrateur informatique à activer l’inscription hybride des appareils Android et Android for Work. Les appareils peuvent être gérés avec Configuration Manager en utilisant un abonnement Microsoft Intune configuré. Les utilisateurs peuvent télécharger l'application de portail d'entreprise Android depuis Google Play qui leur permet d'inscrire des appareils Android (y compris Samsung KNOX Standard) et Android for Work. En tant qu’administrateur de Configuration Manager, vous pouvez gérer les paramètres de conformité, réinitialiser ou supprimer des appareils Android, déployer des applications et collecter l’inventaire matériel et logiciel. Si l’application de portail d’entreprise Android n’est pas installée sur les appareils Android, vous ne disposez pas de toutes les fonctions de gestion, telles que les paramètres de conformité et d’inventaire, mais vous pouvez encore déployer des applications sur des appareils Android.  

## <a name="enable-android-enrollment"></a>Activer l’inscription Android  
Les étapes suivantes permettent à Configuration Manager de gérer des appareils Android sans profil professionnel (par exemple, l’inscription « Android classique »).

1.  **Prérequis** : avant de configurer l’inscription d’une plateforme, observez les prérequis et les procédures indiqués dans [Configurer la gestion hybride des appareils mobiles](setup-hybrid-mdm.md).  
2.  Dans la console Configuration Manager, dans l’espace de travail **Administration**, sélectionnez **Vue d’ensemble** > **Services cloud** > **Abonnements Microsoft Intune** puis choisissez votre abonnement Intune.  
3.  Sous l’onglet **Accueil** , dans le groupe **Abonnement** , sélectionnez **Configurer des plateformes** > **Android**.  

4.  Dans la boîte de dialogue **Propriétés d’abonnement Microsoft Intune** , sélectionnez l’onglet **Android** et cochez la case **Activer l’inscription Android** .  

 Une fois la configuration effectuée, vous devez faire savoir aux utilisateurs comment inscrire leurs périphériques. Consultez [Ce qu’il faut dire aux utilisateurs sur l’inscription de leurs appareils](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Ces informations s’appliquent aux appareils mobiles gérés par Microsoft Intune et Configuration Manager.

## <a name="enable-android-for-work-enrollment"></a>Activer l’inscription Android for Work
Les étapes suivantes permettent à Configuration Manager de gérer des appareils Android sans profil professionnel (par exemple, l’inscription « Android classique »).

 1. Créez un compte Google sur https://accounts.google.com/SignUp à utiliser comme compte d’administrateur Android for Work ou connectez-vous à l’aide du compte qui sera associé à toutes les tâches de gestion Android for Work pour ce client Intune. Ce compte Google peut être partagé par les administrateurs qui gèrent des appareils Android. Il s’agit du compte Google utilisé par votre organisation pour gérer et publier des applications dans la console Play for Work. Vous utiliserez ce compte pour approuver les applications dans le magasin Play for Work. Veillez donc à prendre note du nom du compte et du mot de passe.
 2. Activez l’inscription Android en liant le compte Google au client Intune géré dans Configuration Manager :
   1. Dans la console Configuration Manager, dans l’espace de travail **Administration**, sélectionnez **Vue d’ensemble** > **Services cloud** > **Abonnements Microsoft Intune** puis choisissez votre abonnement Intune.
   2. Sous l’onglet **Accueil** , dans le groupe **Abonnement** , sélectionnez **Configurer des plateformes** > **Android for Work**.
   3. Dans la boîte de dialogue, sélectionnez **Configurer Android for Work dans la console Intune**. La console Intune s’ouvre dans votre navigateur web.
   4. Utilisez vos informations d’identification d’administrateur Intune pour vous connecter au portail Intune.
   5. Sélectionnez **Configurer** pour ouvrir le site web Android for Work de Google Play.
   6. Dans la page de connexion de Google, entrez les informations d’identification du compte Google de l’étape 1, puis fournissez les informations relatives à votre société.
 3. Quand vous revenez au portail Intune, Android for Work est activé et vous avez trois options d’inscription pour les appareils Android for Work :
   - **Gérer tous les appareils comme Android** - (Désactivé) Tous les appareils Android, notamment ceux qui prennent en charge Android for Work, sont inscrits comme appareils Android conventionnels.
   - **Gérer les appareils pris en charge comme Android for Work** - (Activé) Tous les appareils qui prennent en charge Android for Work sont inscrits comme appareils Android for Work. Tout appareil Android qui ne prend pas en charge Android for Work est inscrit comme appareil Android conventionnel.
   - **Gérer les appareils pris en charge pour les utilisateurs uniquement dans ces groupes comme Android for Work** - (Activé uniquement pour certains groupes) Vous permet de cibler la gestion Android for Work à un ensemble limité d’utilisateurs. Seuls les membres des groupes sélectionnés qui inscrivent un appareil qui prend en charge Android for Work sont inscrits comme appareils Android for Work. Tous les autres sont inscrits comme appareils Android.

> [!NOTE]
> Un problème connu empêche le bon fonctionnement de l’option **Gérer les appareils pris en charge pour les utilisateurs uniquement dans ces groupes comme Android for Work**. Les appareils des utilisateurs dans les groupes Azure AD spécifiés sont inscrits en tant qu’appareils Android et non en tant qu’appareils Android for Work. Pour activer Android for Work, vous devez utiliser **Gérer les appareils pris en charge comme Android for Work**.


Une fois la configuration effectuée, vous devez faire savoir aux utilisateurs comment inscrire leurs appareils. Consultez [Ce qu’il faut dire aux utilisateurs sur l’inscription de leurs appareils](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Ces informations s’appliquent aux appareils mobiles gérés par Microsoft Intune et Configuration Manager.

Vous verrez le nom du compte et le nom de l’organisation dans le portail Intune une fois la liaison établie. À ce stade, vous pouvez fermer les deux navigateurs.

### <a name="enroll-an-android-for-work-device"></a>Inscrire un appareil Android for Work
 L’inscription des appareils Android for Work pour vos utilisateurs finaux est similaire à celles des appareils Android. Les utilisateurs peuvent télécharger et installer l’application Portail d’entreprise pour Android sur leurs appareils mobiles. L’application les invite à créer un profil professionnel dans le cadre du processus d’inscription.  Une fois le profil professionnel créé, les utilisateurs doivent basculer vers la version gérée du portail d’entreprise. Le portail d’entreprise géré est marqué d’un petit porte-documents orange dans le coin inférieur droit.

### <a name="manage-android-for-work-devices"></a>Gérer des appareils Android for Work
Une fois que vous avez activé l’inscription Android for Work, vous pouvez effectuer les tâches de gestion suivantes pour les appareils Android for Work :
- [Approuver les applications](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Créer des éléments de configuration](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gérer les paramètres de conformité](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gérer les profils de messagerie](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Réinitialiser de façon sélective le profil professionnel](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< Étape précédente](create-service-connection-point.md) [Étape suivante >](set-up-additional-management.md)

