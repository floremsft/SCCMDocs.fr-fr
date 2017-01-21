---
title: Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune
description: "Découvrez la gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 22e673122f0f664d1240c11451b7e6db78481b26
ms.openlocfilehash: 83832465e93997a2893e024c565ee00f471036d1

---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*


Vous pouvez gérer des appareils iOS, Windows et Android avec Configuration Manager et Microsoft Intune. Toutes les tâches de gestion sont administrées à partir de la console Configuration Manager, où vous effectuez toutes vos autres tâches de gestion de manière intégrée et transparente avec le service en ligne de Microsoft Intune via Internet.  Vous pouvez utiliser Configuration Manager pour permettre aux utilisateurs d’accéder aux ressources d’entreprise sur leurs appareils de manière sécurisée et gérée. Avec la gestion des appareils, vous protégez les données d’entreprise tout en permettant aux utilisateurs d’inscrire leurs appareils personnels ou d’entreprise pour accéder aux données d’entreprise. Fonctionnalités de gestion des appareils :

-   Mise hors service et réinitialisation des appareils
-   Configuration des paramètres de compatibilité tels que les mots de passe, la sécurité, l'itinérance, le chiffrement et la communication sans fil
-   Déploiement d’applications métier sur les appareils
-   Déploiement d'applications sur des appareils qui se connectent au Windows Store, au Windows Phone Store, à l'App Store ou à Google Play
-   Collecte de l'inventaire matériel
-   Collecte de l'inventaire logiciel à l'aide de rapports intégrés

Pour en savoir plus sur les nouvelles fonctionnalités disponibles pour la gestion des appareils mobiles (MDM) hybride, consultez [Nouvelles fonctionnalités pour la gestion des appareils mobiles (MDM) hybride](../understand/whats-new-in-hybrid-mobile-device-management.md).

Ce document part du principe que vous utilisez déjà Configuration Manager pour gérer les ordinateurs et que vous souhaitez étendre la console Configuration Manager avec Intune pour gérer des appareils mobiles. Pour comprendre les différences entre Intune et la gestion des appareils mobiles (MDM) hybride, consultez [Choisir entre la solution autonome Microsoft Intune et la gestion des appareils mobiles hybride avec System Center Configuration Manager](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

Après avoir étendu Configuration Manager avec Intune, vous pouvez inscrire et gérer des appareils d’entreprise ou autoriser les utilisateurs à inscrire leurs appareils personnels. Vous pouvez également gérer des appareils d’entreprise avec Intune à partir de Configuration Manager.

## <a name="hybrid-mdm-enrollment"></a>Inscription pour la gestion des appareils mobiles (MDM) hybride
Les appareils peuvent être gérés à l’aide de la gestion hybride s’ils ont été préalablement inscrits auprès du service. Le processus d’inscription des appareils dépend du type et de la propriété de l’appareil, ainsi que du niveau de gestion souhaité. L’inscription « Apportez votre propre appareil » (BYOD) permet aux utilisateurs d’inscrire leurs téléphones, tablettes ou PC personnels. L’inscription d’appareils d’entreprise (COD) permet de gérer les appareils en utilisant des fonctionnalités comme la réinitialisation à distance, le partage d’appareils ou l’affinité entre utilisateur et appareil.

 Si vous utilisez [Exchange ActiveSync](#mobile-device-management-with-exchange-activesync-and-configuration-manager) (localement ou hébergé dans le cloud), vous pouvez choisir la gestion Intune simple sans inscription. Vous pouvez également gérer des PC Windows à l’aide du [logiciel client Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).

## <a name="overview-of-device-enrollment-methods"></a>Présentation des méthodes d’inscription des appareils

 Le tableau suivant présente les différentes méthodes d’inscription et les fonctionnalités qu’elles prennent en charge. Ces fonctionnalités sont les suivantes :
 - **Réinitialisation** : réinitialise l’appareil aux paramètres d’usine, en supprimant toutes les données. [Mettre des appareils hors service](../deploy-use/wipe-lock-reset-devices.md)
 - **Affinité** : associe les appareils à des utilisateurs. Fonctionnalité nécessaire pour la gestion des applications mobiles (MAM) et l’accès conditionnel aux données d’entreprise. [Affinité utilisateur](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
 - **Verrouillage** : empêche les utilisateurs de retirer leur appareil de la gestion. Les appareils iOS nécessitent le mode de verrouillage Supervisé. [Verrouillage à distance](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

 **Méthodes d’inscription des appareils iOS**

| **Méthode** |  **Réinitialisation** |  **Affinité**    |   **Verrouillage** | **Détails** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Non|    Oui |   Non | [Plus d’informations](../deploy-use/setup-hybrid-mdm.md#step-6-enable-platform-enrollment)|
|**[Gestionnaire d’inscription d’appareil](#dem)**|   Non |Non |Non  | [Plus d’informations](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   Oui |   Facultatif |  Facultatif|[Plus d’informations](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| Oui |   Facultatif |  Non| [Plus d’informations](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Méthodes d’inscription des appareils Windows et Android**

| **Méthode** |  **Réinitialisation** |  **Affinité**    |   **Verrouillage** | **Détails**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Non|    Oui |   Non | [Plus d’informations](../deploy-use/setup-hybrid-mdm.md#set-up-device-management)|
|**[Gestionnaire d’inscription d’appareil](#dem)**|   Non |Non |Non  |[Plus d’informations](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Pour répondre à une série de questions qui vous aideront à déterminer la méthode appropriée, consultez [Choisir comment inscrire des appareils](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
Avec la méthode d’inscription BYOD (« Apportez votre propre appareil »), les utilisateurs d’appareils personnels installent l’application Portail d’entreprise et inscrivent leurs propres appareils. Ils peuvent ensuite se connecter au réseau d’entreprise et rejoindre le domaine ou Azure Active Directory. Dans beaucoup de scénarios de gestion d’appareils d’entreprise (COD), l’inscription BYOD est nécessaire pour la plupart des plateformes d’appareils. Consultez [Configurer la gestion des appareils mobiles (MDM) hybride](../deploy-use/setup-hybrid-mdm.md). ([Retour au tableau](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>Appareils d’entreprise
Les appareils d’entreprise (COD) peuvent être gérés à l’aide de la console Configuration Manager. Il est possible d’inscrire des appareils iOS directement par le biais des outils fournis par Apple. Tous les types d’appareils peuvent être inscrits par un administrateur ou un responsable à l’aide du gestionnaire d’inscription d’appareil. Les appareils dotés d’un numéro IMEI peuvent également être identifiés et référencés comme appartenant à l’entreprise pour mettre en œuvre des scénarios COD.

[Inscrire des appareils d’entreprise](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>Gestionnaire d’inscription d’appareil
Le gestionnaire d’inscription d’appareil est un compte d’utilisateur spécial qui permet d’inscrire et de gérer plusieurs appareils d’entreprise. Les responsables peuvent installer l’application Portail d’entreprise et inscrire de nombreux appareils sans utilisateur. En savoir plus sur le [gestionnaire d’inscription d’appareil](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Retour au tableau](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
Le programme d’inscription d’appareil (ou DEP) d’Apple vous permet de créer et déployer une stratégie « à distance » sur des appareils iOS achetés et gérés avec DEP. L’appareil est inscrit quand l’utilisateur le démarre pour la première fois et exécute l’Assistant d’installation iOS. Cette méthode prend en charge le mode **iOS supervisé**, qui fournit les fonctionnalités suivantes :
   -    Inscription verrouillée
   -    Accès conditionnel
   -    Détection de jailbreak
   -    Gestion des applications mobiles

En savoir plus sur la méthode [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Retour au tableau](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB-SA
Cette méthode permet d’inscrire des appareils connectés par USB en utilisant l’Assistant Configuration. L’administrateur crée une stratégie et l’exporte vers Apple Configurator. Les appareils d’entreprise connectés par USB sont préparés à l’aide d’une stratégie. L’administrateur doit inscrire manuellement chaque appareil. Après avoir reçu leur appareil, les utilisateurs exécutent l’Assistant Configuration pour inscrire l’appareil. Cette méthode prend en charge le mode **iOS supervisé**, qui fournit les fonctionnalités suivantes :
   -    Accès conditionnel
   -    Détection de jailbreak
   -    Gestion des applications mobiles

En savoir plus sur l’[inscription via l’Assistant Configuration avec Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Retour au tableau](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Gestion des appareils mobiles avec Exchange ActiveSync et Configuration Manager
Les appareils mobiles qui ne sont pas inscrits mais qui se connectent à Exchange ActiveSync (EAS) peuvent être gérés par Intune à l’aide de la stratégie de gestion des appareils mobiles EAS. Intune utilise un connecteur Exchange pour communiquer avec EAS, localement ou hébergé dans le cloud.

[Gestion des appareils mobiles à l’aide d’Exchange ActiveSync et d’Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)


##  <a name="supported-device-platforms"></a>Plateformes d’appareils prises en charge

La gestion des appareils mobiles (MDM) hybride avec Configuration Manager permet de gérer les plateformes d’appareils suivantes :

[!INCLUDE[../includes/mdm-supported-devices](../includes/mdm-supported-devices.md)]

## <a name="next-steps"></a>Étapes suivantes
 - [Configuration requise pour l’inscription d’appareils](../deploy-use/setup-hybrid-mdm.md)
 - [Gérer des appareils d’entreprise](../deploy-use/enroll-company-owned-devices.md)



<!--HONumber=Nov16_HO1-->


