---
title: "Accès conditionnel | Microsoft Docs"
description: "Découvrez comment utiliser l’accès conditionnel dans System Center Configuration Manager pour sécuriser la messagerie et d’autres services."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: 26
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: ea9184cd4fdc87513ed489f0f568efa6d64c1caa
ms.lasthandoff: 03/06/2017


---

# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>Gérer l’accès aux services dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>Accès conditionnel dans System Center Configuration Manager
Utilisez l’**accès conditionnel** pour sécuriser la messagerie électronique et d’autres services sur des appareils inscrits auprès de Microsoft Intune, en fonction de conditions que vous spécifiez.  

 Pour plus d’informations sur l’**accès conditionnel sur des PC gérés avec System Center Configuration Manager** et dont la conformité est évaluée, consultez [Gérer l’accès aux services O365 pour les PC gérés par System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


 La procédure classique pour configurer l'accès conditionnel est la suivante :  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Utilisez l'accès conditionnel pour gérer l'accès aux services suivants :  

-   Microsoft Exchange sur site  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated  

-   SharePoint Online  

-   Skype Entreprise Online

-   Dynamics CRM Online

 Pour implémenter un accès conditionnel, vous configurez deux types de stratégies dans Configuration Manager :  

-   Les **stratégies de conformité** sont des stratégies facultatives que vous pouvez déployer dans des regroupements d’utilisateurs et qui évaluent des paramètres comme :  

    -   Code secret  

    -   Chiffrement  

    -   Si l'appareil est jailbreaké ou rooté  

    -   Indique si les e-mails sur l’appareil sont gérés par une stratégie Configuration Manager ou Intune  

     **Si aucune stratégie de conformité n’est déployée sur un appareil, les stratégies d’accès conditionnel applicables vont traiter l’appareil comme étant conforme**.  

-   Les **stratégies d’accès conditionnel** sont configurées pour un service particulier. Elles définissent des règles qui déterminent notamment quels groupes d’utilisateurs de sécurité Azure Active Directory ou quels regroupements d’utilisateurs Configuration Manager sont ciblés ou exempts.  

     Vous configurez la stratégie d’accès conditionnel Exchange sur site à partir de la console Configuration Manager. Cependant, quand vous configurez une stratégie Exchange Online ou SharePoint Online, la console d’administration Intune, où vous configurez la stratégie, s’ouvre.  

     Contrairement aux autres stratégies Intune ou Configuration Manager, vous ne déployez pas les stratégies d’accès conditionnel. Au lieu de cela, vous les configurez une seule fois et elles s'appliquent à tous les utilisateurs gérés.  

 Quand un appareil ne remplit pas les conditions que vous configurez, l'utilisateur est guidé tout au long du processus d'inscription de cet appareil et du processus de résolution du problème qui empêche l'appareil d'être conforme.  

**Avant** de commencer à utiliser l’accès conditionnel, vérifiez que la **configuration requise** appropriée est satisfaite :  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Configuration requise pour Exchange Online (en utilisant l’environnement mutualisé partagé)
L'accès conditionnel à Exchange Online prend en charge les appareils qui exécutent :
-   Windows 8.1 et versions ultérieures (quand ils sont inscrits auprès d’Intune)
-   Windows 7.0 ou Windows 8.1 (quand ils sont joints au domaine)
-   Windows Phone 8.1 et versions ultérieures
-   iOS 7.1 et versions ultérieures
-   Android 4.0 et ultérieur, Samsung Knox Standard 4.0 et ultérieur

 **De plus** :
-   Les appareils doivent être joints à un espace de travail, qui inscrit l'appareil auprès du service Azure Active Directory Device Registration Service (AAD DRS).<br />     
- Les PC joints au domaine doivent être inscrits automatiquement auprès d'Azure Active Directory via la stratégie de groupe ou MSI.

  La section **Accès conditionnel pour les PC** dans cette rubrique décrit la configuration requise pour l'activation de l'accès conditionnel pour un PC.<br />     
  Le service AAD DRS sera activé automatiquement pour les clients Intune et Office 365. Les clients qui ont déjà déployé le service d'inscription d'appareils AD FS ne verront pas les appareils inscrits dans leur annuaire Active Directory local.
-   Vous devez utiliser un abonnement Office 365 qui inclut Exchange Online (comme E3) et les utilisateurs doivent disposer d'une licence pour Exchange Online.
-   Le **connecteur Exchange Server** est facultatif. Il connecte Configuration Manager à Microsoft Exchange Online et vous aide à surveiller les informations des appareils par le biais de la console Configuration Manager (consultez [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
Il n'est pas nécessaire d'utiliser le connecteur pour utiliser des stratégies de conformité ou d'accès conditionnel, mais il est obligatoire pour exécuter les rapports qui aident à évaluer l'impact de l'accès conditionnel.

## <a name="requirements-for-exchange-online-dedicated"></a>Configuration requise pour Exchange Online Dedicated
L'accès conditionnel à Exchange Online Dedicated prend en charge les appareils qui exécutent :
-   Windows 8 et versions ultérieures (quand ils sont inscrits auprès d’Intune)
-   Windows 7.0 ou Windows 8.1 (quand ils sont joints au domaine)

  Accès conditionnel aux PC joints au domaine uniquement pour les locataires dans le nouvel environnement dédié Exchange Online.
-   Windows Phone 8 et versions ultérieures
-   Tout appareil iOS utilisant un client de messagerie Exchange ActiveSync (EAS)
-   Android 4 et ultérieur.
-   Pour les locataires dans l’**environnement Exchange Online Dedicated hérité** :    

  Vous devez utiliser le **connecteur Exchange Server** qui connecte Configuration Manager à Microsoft Exchange sur site. Ceci vous permet de gérer les appareils mobiles et active l’accès conditionnel (consultez [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
-   Pour les locataires dans le **nouvel environnement Exchange Online Dedicated** :     
  Le **connecteur Exchange Server** est facultatif. Il connecte Configuration Manager à Microsoft Exchange Online et vous aide à gérer les informations sur les appareils (consultez [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)). Il n'est pas nécessaire d'utiliser le connecteur pour utiliser des stratégies de conformité ou d'accès conditionnel, mais il est obligatoire pour exécuter les rapports qui aident à évaluer l'impact de l'accès conditionnel.  

## <a name="requirements-for-exchange-on-premises"></a>Configuration requise pour Exchange sur site
L'accès conditionnel à Exchange sur site prend en charge les :
-   Windows 8 et versions ultérieures (quand ils sont inscrits auprès d’Intune)
-   Windows Phone 8 et versions ultérieures
-   Application de messagerie native sur iOS
-   Application de messagerie native sur Android 4 ou version ultérieure
-   L’application Microsoft Outlook n’est pas prise en charge (Android et iOS).

**De plus** :

-  La version d’Exchange doit être Exchange 2010 ou une version ultérieure. Le groupe de serveurs d’accès au client (CAS) du serveur Exchange est pris en charge.

> [!TIP]
> Si votre environnement Exchange est dans une configuration de serveur CAS, vous devez configurer le connecteur Exchange sur site pour pointer vers l’un des serveurs CAS.
- Vous devez utiliser le **connecteur Exchange Server** qui connecte Configuration Manager à Microsoft Exchange sur site. Ceci vous permet de gérer les appareils mobiles et active l’accès conditionnel (consultez [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
  - Assurez-vous d’utiliser la dernière version du **connecteur Exchange local**. Le connecteur Exchange local doit être configuré via la console Configuration Manager. Pour obtenir une procédure pas à pas, consultez [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Le connecteur doit être configuré seulement sur le site principal de System Center Configuration Manager.</li><li>Ce connecteur prend en charge l’environnement CAS Exchange. <br />        Quand vous configurez le connecteur, vous devez faire en sorte qu’il communique avec l’un des serveurs CAS Exchange.

- Exchange ActiveSync peut être configuré avec l'authentification basée sur certificat ou l'entrée d'informations d'identification utilisateur.


## <a name="requirements-for-skype-for-business-online"></a>Configuration requise pour Skype Entreprise Online
L'accès conditionnel à SharePoint Online prend en charge les appareils qui exécutent :
 -   iOS 7.1 et versions ultérieures
 -   Android 4.0 et versions ultérieures
 -   Samsung Knox Standard 4.0 ou ultérieur

**De plus,** vous devez activer l’authentification moderne pour Skype Entreprise Online. Remplissez ce [formulaire de connexion](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) pour vous inscrire au programme d’authentification moderne.

Tous vos utilisateurs finaux doit utiliser Skype Entreprise Online. Si vous avez un déploiement avec Skype Entreprise Online et Skype Entreprise en local, la stratégie d’accès conditionnel n’est pas appliquée aux utilisateurs finaux qui se trouvent dans le déploiement local.

## <a name="requirements-for-sharepoint-online"></a>Configuration requise pour SharePoint Online
L'accès conditionnel à SharePoint Online prend en charge les appareils qui exécutent :
 -   Windows 8.1 et versions ultérieures (quand ils sont inscrits auprès d’Intune)
 -   Windows 7.0 ou Windows 8.1 (quand ils sont joints au domaine)
 -   Windows Phone 8.1 et versions ultérieures
 -   iOS 7.1 et versions ultérieures
 -   Android 4.0 et ultérieur, Samsung Knox Standard 4.0 et ultérieur

 **De plus** :
 -   Les appareils doivent être joints à un espace de travail, qui inscrit l'appareil auprès du service Azure Active Directory Device Registration Service (AAD DRS).

 Les PC joints au domaine doivent être inscrits automatiquement auprès d'Azure Active Directory via la stratégie de groupe ou MSI. La section **Accès conditionnel pour les PC** dans cette rubrique décrit la configuration requise pour l'activation de l'accès conditionnel pour un PC.

 Le service AAD DRS sera activé automatiquement pour les clients Intune et Office 365. Les clients qui ont déjà déployé le service d'inscription d'appareils AD FS ne verront pas les appareils inscrits dans leur annuaire Active Directory local.
 -   Un abonnement SharePoint Online est requis et les utilisateurs doivent disposer d'une licence pour SharePoint Online.

 ### <a name="conditional-access-for-pcs"></a>Accès conditionnel pour les PC

 Vous pouvez configurer l'accès conditionnel pour les PC qui exécutent des applications de bureau Office pour accéder à **Exchange Online** et **SharePoint Online** pour les PC qui répondent aux exigences suivantes :
 -   Le PC doit exécuter Windows 7.0 ou Windows 8.1.
 -   Le PC doit être joint au domaine ou être conforme.

 Pour être conforme, le PC doit être inscrit dans Intune et se conformer aux stratégies.

 Pour les PC joints à un domaine, vous devez le configurer pour qu’il [s’inscrive automatiquement](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) auprès d’Azure Active Directory.
 -   [L'authentification moderne Office 365 doit être activée](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)et toutes les mises à jour Office les plus récentes doivent être installées.<br />     L'authentification moderne permet aux clients Windows Office 2013 d'utiliser la connexion basée sur la bibliothèque ADAL (Active Directory Authentication Library) et permet de bénéficier d'une sécurité accrue telle que l' **authentification multifacteur**et l' **authentification basée sur certificat**.
 -   Configurez des règles de revendications AD FS pour bloquer les protocoles autres que l'authentification moderne.  

## <a name="next-steps"></a>Étapes suivantes  
 Lisez les rubriques suivantes pour savoir comment configurer des stratégies de conformité et des stratégies d'accès conditionnel pour votre scénario :  

-   [Gérer des stratégies de conformité d’appareils dans System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

-   [Gérer l’accès à la messagerie dans System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

-   [Gérer l’accès à SharePoint Online dans System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Gérer l’accès à Skype Entreprise Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>Voir aussi  

 [Bien démarrer avec les paramètres de compatibilité dans System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)

