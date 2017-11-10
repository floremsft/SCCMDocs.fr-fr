---
title: "Gérer l’accès aux services O365 pour les PC gérés"
titleSuffix: Configuration Manager
description: "Découvrez comment configurer l’accès conditionnel pour les PC gérés par System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
caps.latest.revision: "15"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: a49e53ca81d8bd01747c41ab9c25de7fd6396f32
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Gérer l’accès aux services O365 pour les PC gérés par System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

À compter de la version 1602 de Configuration Manager, vous pouvez configurer l’accès conditionnel pour les PC gérés par System Center Configuration Manager.  

> [!IMPORTANT]  
> Il s’agit d’une fonctionnalité en préversion disponible dans les mises à jour 1602, 1606 et 1610. Des fonctionnalités en préversion sont incluses dans le produit à des fins de test anticipé en environnement de production, mais ne doivent pas être considérées comme prêtes pour une utilisation en production. Pour plus d’informations, consultez [Utiliser des fonctionnalités de préversions de mises à jour](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).
> - Après avoir installé la mise à jour 1602, le type de fonctionnalité s’affiche comme commercialisé même s’il s’agit d’une préversion.
> - Si vous mettez ensuite à jour la version 1602 vers la version 1606, le type de fonctionnalité s’affiche comme commercialisé même s’il reste en préversion.
> - Si vous mettez à jour la version 1511 directement vers la version 1606, le type de fonctionnalité s’affiche en tant que préversion.

Si vous recherchez des informations sur la façon de configurer l’accès conditionnel pour des appareils inscrits et gérés par Intune, ou des PC joints au domaine et non évalués sur le plan de la compatibilité, consultez [Gérer l’accès aux services dans System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md).

## <a name="supported-services"></a>Services pris en charge  

-   Exchange Online
-   SharePoint Online

## <a name="supported-pcs"></a>PC pris en charge  

-   Windows 7
-   Windows 8.1
-   Windows 10

## <a name="supported-windows-servers"></a>Serveurs Windows pris en charge

-   2008 R2
-   2012
-   2012 R2
-   2016

    > [!IMPORTANT]
    > Pour les serveurs Windows auxquels plusieurs utilisateurs peuvent être connectés simultanément, les mêmes stratégies d’accès conditionnel doivent être déployées pour tous les utilisateurs connectés.

## <a name="configure-conditional-access"></a>Configurer un accès conditionnel  
 Pour configurer un accès conditionnel, vous devez créer une stratégie de conformité, puis configurer une stratégie d’accès conditionnel. Lorsque vous configurez des stratégies d’accès conditionnel pour des PC, vous pouvez exiger que ceux-ci soient conformes à la stratégie de conformité pour pouvoir accéder aux services Exchange Online et SharePoint Online.  

### <a name="prerequisites"></a>Conditions préalables  

-   Synchronisation d’ADFS et abonnement O365. L’abonnement O365 est nécessaire pour configurer Exchange Online et SharePoint Online.  

-   Abonnement Microsoft Intune L’abonnement Microsoft Intune doit être configuré dans la console Configuration Manager. L’abonnement Intune sert à transférer l’état de conformité des appareils à Azure Active Directory et à accorder les licences d’utilisateur.  

 Les PC doivent répondre aux exigences suivantes :  

-   [Conditions préalables](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) pour l’inscription automatique auprès d’Azure Active Directory.  

     Vous pouvez inscrire des PC auprès d’Azure AD via la stratégie de conformité.  

    -   Pour des PC Windows 8.1 et Windows 10, vous pouvez utiliser une stratégie de groupe Active Directory pour configurer vos appareils de façon à ce qu’ils s’inscrivent automatiquement auprès d’Azure AD.  

    -   o   Pour des PC Windows 7, vous devez déployer le package logiciel d’inscription de l’appareil sur le PC par le biais de System Center Configuration Manager. Pour plus de détails, consultez[Inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

-   Les PC doivent utiliser Office 2013 ou Office 2016 avec l’authentification moderne [activée](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a).  

 Les étapes décrites ci-dessous s’appliquent tant à Exchange Online qu’à SharePoint Online.  

### <a name="step-1-configure-compliance-policy"></a>Étape 1. Configurer une stratégie de conformité  
 Dans la console Configuration Manager, créez une stratégie de conformité avec les règles suivantes :  

-   Exiger l’inscription dans Azure Active Directory : cette règle vérifie si l’appareil de l’utilisateur a fait l’objet d’une jonction d’espace de travail à Azure AD. Si ce n’est pas le cas, l’appareil est automatiquement inscrit dans Azure AD. L’inscription automatique est prise en charge seulement sur Windows 8.1. Pour les PC Windows 7, déployez un fichier MSI pour effectuer l’inscription automatique. Pour plus d’informations, consultez [Inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

-   **Toutes les mises à jour requises installées avec une échéance supérieure à X jours :** cette règle vérifie si l’appareil de l’utilisateur a toutes les mises à jour obligatoires (spécifiées dans la règle Mises à jour automatiques requises) dans le délai et la période de grâce que vous avez spécifiés. Elle installe automatiquement toutes les mises à jour obligatoires en attente.  

-   **Exiger le chiffrement de lecteur BitLocker :** cette règle vérifie si le lecteur principal (par exemple C:\\) de l’appareil est chiffré avec BitLocker. Si le chiffrement BitLocker n’est pas activé sur le lecteur principal, l’accès de l’appareil aux services de messagerie et SharePoint est bloqué.  

-   **Exiger un logiciel anti-programme malveillant :** Cette règle vérifie si le logiciel anti-programme malveillant (System Center Endpoint Protection ou Windows Defender uniquement) est activé et en cours d’exécution. S’il n’est pas activé, l’accès aux services de messagerie et SharePoint est bloqué.  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Étape 2. Évaluer l’incidence de l’accès conditionnel  
 Exécutez le rapport de conformité de l’accès conditionnel. Il figure dans la section Analyse, sous Rapports > Gestion de la conformité et des paramètres. Cette opération affiche l’état de conformité de tous les appareils.  L’accès à Exchange Online et à SharePoint Online d’appareils signalés comme non conformes est bloqué.  

 ![Rapport CA &#95;conformité&#95;](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Configurer les groupes de sécurité Active Directory  
 Les stratégies d’accès conditionnel ciblent des groupes d’utilisateurs en fonction des types de stratégies. Ces groupes contiennent les utilisateurs qui seront ciblés par la stratégie ou exemptés de celle-ci. Quand un utilisateur est ciblé par une stratégie, chaque appareil qu’il utilise doit être conforme à celle-ci pour pouvoir accéder au service.  

 Groupes d’utilisateurs de sécurité Active Directory. Ces groupes d’utilisateurs doivent être synchronisés sur Azure Active Directory. Vous pouvez configurer ces groupes vie le Centre d’administration Office 365 ou le Portail du compte Microsoft Intune.  

 Vous pouvez spécifier deux types de groupes dans chaque stratégie. :  

-   **Groupes ciblés** : groupes d’utilisateurs auxquels la stratégie est appliquée. Le même groupe doit être utilisé pour satisfaire aux exigences de conformité et à la stratégie d’accès conditionnel.  

-   **Groupes exemptés :** groupes d’utilisateurs exempts de la stratégie (facultatif)  
    Si un utilisateur se trouve dans les deux, il est exempté de la stratégie.  

     Seuls les groupes ciblés par la stratégie d’accès conditionnel sont évalués.  

### <a name="step-3--create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Étape 3.  Créer une stratégie d’accès conditionnel pour Exchange Online et SharePoint Online  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Pour créer une stratégie pour Exchange Online, sélectionnez **Activer la stratégie d’accès conditionnel pour Exchange Online**.  

     Pour créer une stratégie pour SharePoint Online, sélectionnez **Activer la stratégie d’accès conditionnel pour SharePoint Online**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Liens**, cliquez sur **Configurer la stratégie d’accès conditionnel dans la console Intune**. Il se peut que vous deviez fournir le nom d’utilisateur et le mot de passe du compte utilisé pour connecter Configuration Manager à Intune.  

     La console d’administration Intune s’ouvre.  

4.  Pour Exchange Online, dans la console d’administration Microsoft Intune, cliquez sur **Stratégie > Accès conditionnel > Stratégie Exchange Online**.  

     Pour SharePoint Online, dans la console d’administration Microsoft Intune, cliquez sur **Stratégie > Accès conditionnel > Stratégie SharePoint Online**.  

5.  Définissez la configuration requise du PC Windows sur l’option**Les appareils doivent être conformes**.  

6.  Sous **Groupes ciblés**, cliquez sur **Modifier** pour sélectionner les groupes de sécurité Active Directory auxquels la stratégie sera appliquée.  

    > [!NOTE]  
    >  Le même groupe d’utilisateurs de sécurité doit être utilisé pour déployer la stratégie de conformité et le groupe ciblé pour la stratégie d’accès conditionnel.  

     Sous **Groupes exemptés**, vous pouvez éventuellement cliquez sur **Modifier** pour sélectionner les groupes de sécurité Azure Active Directory exempts de cette stratégie.  

7.  Cliquez sur **Enregistrer** pour créer et enregistrer la stratégie.  

 Les utilisateurs finaux bloqués en raison d’un défaut de conformité peuvent consulter les informations relatives à la conformité dans le Centre logiciel System Center Configuration Manager et lancer une nouvelle évaluation de la stratégie une fois les problèmes de conformité résolus.  

<!---
##  <a name="bkmk_KnownIssues"></a> Known issues  
 You may see the following issues when using this feature:  

-   In this 1602 update,  the 5 day compliance is not enforced. Even if compliance check on the end-user's device has happened more than 5 days ago, users still can access Office 365 and SharePoint online.  

-   When a device is not compliant with the compliance policy, the reason is not automatically displayed. The end- user must go to the new Software Center to find the reason for non-compliance. The reason is displayed in the Device compliance section of the Software Center.  

-   Windows 10 users may see multiple access failures when trying to reach O365 and/or SharePoint online resources. Note that conditional access is not fully supported for Windows 10.  
--->
## <a name="see-also"></a>Voir aussi

- [Protéger les données et l’infrastructure des sites avec System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)
- [Organigramme de résolution des problèmes d’accès conditionnel pour Configuration Manager](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0)
