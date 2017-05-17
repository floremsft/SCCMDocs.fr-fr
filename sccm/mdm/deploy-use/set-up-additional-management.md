---
title: "Configurer des solutions de gestion supplémentaires via System Center Configuration Manager | Microsoft Docs"
description: "Configurez des solutions de gestion supplémentaires via System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 947d2a85f2ac68c7ccaf9a1237fd60e89e7d1d10
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017

---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>Configurer des solutions de gestion supplémentaires grâce à System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

(Facultatif) Vous pouvez configurer une gestion supplémentaire avant l’inscription des appareils. Ces solutions de gestion peuvent être créées et déployées après l’inscription des appareils, même si de nombreuses organisations préfèrent les déployer au fur et à mesure que les appareils sont intégrés à la gestion.

Les **éléments de configuration** vous permettent de gérer des paramètres tels que l’exigence d’un code confidentiel (PIN) ou d’un chiffrement sur les appareils inscrits, en fonction de leur plateforme :
- [Appareils Windows 10 et Windows 8.1](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Appareils Windows Phone](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [Appareils iOS et Mac](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Appareils Android et Samsung KNOX Standard](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

**Les applications ** peuvent être déployées sur des appareils gérés :
- [Applications iOS](creating-ios-applications.md)
- [Applications Mac](../../apps/get-started/creating-mac-computer-applications.md)
- [Applications Windows (PC)](../../apps/get-started/creating-windows-applications.md)
- [Applications Windows Phone](creating-windows-phone-applications.md)
- [Applications Android](creating-android-applications.md)

L’**accès conditionnel** vous permet de gérer l’accès aux ressources de l’entreprise, notamment :  
- [Accès à l’e-mail](manage-email-access.md)
- [Accès à SharePoint](manage-sharepoint-online-access.md)
- [Accès à Skype Entreprise](manage-skype-for-business-online-access.md)
- [Dynamics CRM Online](manage-dynamics-crm-online-access.md)

**L’authentification multifacteur (MFA)** vous permet de demander l’utilisation de plusieurs méthodes de vérification, ce qui permet d’appliquer une deuxième couche critique de sécurité aux transactions et connexions utilisateur.
Auparavant, vous deviez accéder à la console Intune ou à la console Configuration Manager pour définir l’authentification multifacteur pour les inscriptions Intune. Désormais, vous pouvez vous connecter au [portail Microsoft Azure](https://manage.windowsazure.com) en utilisant vos informations d’identification Intune et configurer les paramètres de l’authentification multifacteur via Azure AD. Pour en savoir plus, voir [Authentification multifacteur pour les inscriptions d’appareils Intune](https://aka.ms/mfa_ad).

> [!div class="button"]
[< Étape précédente](enable-platform-enrollment.md) [Étape suivante >](verify-mdm-configuration.md)

