---
title: "Déployer l’application Lookout for Work | Microsoft Docs"
description: "Configurez et déployez les applications Lookout for Work."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 1d9cac06b266fb9ff991e3714240c2ea1bbb3f17
ms.contentlocale: fr-fr
ms.lasthandoff: 03/06/2017


---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configurer et déployer les applications Lookout for Work

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article explique comment configurer et déployer l’application Lookout for Work pour les appareils Android et iOS.

## <a name="android-google-play-store-app"></a>Android (application Google Play Store)
1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.

2.  Dans la page **Général** de l’Assistant Déploiement logiciel, spécifiez les informations suivantes :
  * Type : sélectionnez **Package d’application pour Android sur Google Play**.
  * Emplacement : copiez le lien de l’application Lookout for Work à partir du Google Play Store et collez-le ici
  * Serveur de publication : Lookout Mobile Security
  * Nom : Lookout for Work
  * Description : Lookout offre la meilleure protection contre les menaces mobiles pour assurer la sécurité de votre appareil. Quand l’application Lookout est installée sur l’appareil, elle protège votre appareil contre les menaces et elle vous avertit (ainsi que l’administrateur de votre entreprise) des menaces détectées.
  * Catégorie administrative : gestion de l’ordinateur

  En cas de réussite de l’opération, l’application Lookout for Work s’affiche désormais dans la liste des applications.

3.  Sous l’onglet **Accueil**, dans le groupe **Déploiement**, choisissez **Déployer** pour déployer l’application Lookout for Work sur les utilisateurs.
>[!IMPORTANT]
>Vous devez sélectionner les mêmes utilisateurs que ceux qui ont été ajoutés à l’option Gestion des inscriptions dans la console Lookout MTP.

  Choisissez l’option **Installation requise** pour exiger que l’application Lookout soit installée sur l’appareil de l’utilisateur.

## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (version Enterprise signée de l’application Lookout)

* **Étape 1 :** Vérifiez que la **gestion iOS** est configurée sur votre appareil. Pour obtenir des instructions sur la configuration de votre appareil relative à la gestion iOS, consultez [Configurer la gestion des appareils iOS et Mac]().

* **Étape 2 :** **Resignez** l’application iOS Lookout for Work. Lookout distribue son application iOS Lookout for Work en dehors de l’App Store iOS. **Avant de distribuer l’application**, vous devez resigner l’application avec votre certificat de développeur d’entreprise iOS. Pour obtenir des instructions détaillées pour resigner des applications iOS Lookout for Work, consultez [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/en-us/articles/114094038714) sur le site Lookout.


* **Étape 3 :** Activez l’authentification Azure Active Directory pour les utilisateurs iOS de la manière suivante :
  1.  Connectez-vous au [portail de gestion Azure Active Directory](https://manage.windowsazure.com) et accédez à la page d’application.
  2.  Ajoutez l’**application iOS Lookout for Work** comme **application cliente native**.
  ![capture d’écran de la boîte de dialogue Ajouter des applications présentant l’option d’application cliente native](media/aad-add-app.png)

  3. Remplacez **com.lookout.enterprise.nom_de_votre_entreprise** par l’ID d’ensemble client que vous avez sélectionné quand vous avez signé le package IPA.
  4.  Ajoutez l’URI de redirection supplémentaire **&lt;companyportal://code/>** suivi d’une version codée URL de votre URI de redirection d’origine.
  5.  Ajoutez **Autorisations déléguées** à votre application.

  Pour plus d’informations, consultez [Configurer une application cliente native](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).


* **Étape 4 :** Chargez le fichier .ipa resigné comme décrit dans la rubrique [Créer des applications iOS avec System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/get-started/creating-ios-applications). Définissez la version de système d’exploitation minimale sur iOS version 8.0 ou ultérieure.


* **Étape 5 :** Créez la stratégie de configuration d’application gérée comme décrit dans la rubrique [Configurer des applications iOS à l’aide de stratégies de configuration des applications dans System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).


* **Étape 6 :** **Pour déployer l’application sur les utilisateurs**, sélectionnez l’application Lookout for Work dans la page **Applications**, sous l’onglet **Accueil**, dans le groupe **Déploiement**, choisissez **Déployer**.

  Vous devez sélectionner les mêmes utilisateurs que ceux qui ont été ajoutés à l’option Gestion des inscriptions dans la console Lookout.  
Choisissez l’option **Installation requise** pour exiger que l’application Lookout soit installée sur l’appareil de l’utilisateur.

## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>Que se passe-t-il quand l’application déployée est ouverte sur l’appareil ?




Quand l’utilisateur ouvre l’application Lookout for Work sur l’appareil, il est invité à activer l’application et à choisir l’option Se connecter avec Azure Active Directory. Une procédure pas à pas pour l’utilisateur final est décrite dans les rubriques suivantes :

* [Vous êtes invité à installer Lookout for Work sur votre appareil Android](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [Vous devez résoudre une menace détectée par Lookout for Work sur votre appareil Android](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## <a name="next-steps"></a>Étapes suivantes
* [Activer une règle de protection des appareils contre les menaces dans la stratégie de conformité](enable-device-threat-protection-rule-compliance-policy.md)

