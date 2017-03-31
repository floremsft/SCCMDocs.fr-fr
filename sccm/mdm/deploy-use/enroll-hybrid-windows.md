---
title: Configurer la gestion des appareils mobiles hybride Windows avec System Center Configuration Manager et Microsoft Intune | Microsoft Docs
description: Configurez la gestion des appareils Windows avec System Center Configuration Manager et Microsoft Intune.
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 4189fe34efc2ae134150a89791dc10bbab1b9d02
ms.lasthandoff: 03/17/2017


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurer la gestion hybride des appareils mobiles Windows avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique explique aux administrateurs informatiques comment utiliser Configuration Manager et Microsoft Intune pour permettre à leurs utilisateurs d’inscrire des appareils mobiles et des PC Windows à la gestion. Deux méthodes d’inscription sont disponibles :
-  Inscription automatique à Azure Active Directory (AD) quand les utilisateurs connectent leur compte à un appareil
- Inscription quand les utilisateurs installent l’application Portail d’entreprise et s’y connectent

## <a name="choose-how-to-enroll-windows-devices"></a>Choisir comment inscrire les appareils Windows

Deux facteurs déterminent le mode d’inscription des appareils Windows :
- **Utilisez-vous Azure Active Directory Premium ?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) est inclus avec Enterprise Mobility + Security et d’autres plans de licence.
- **Quelles versions des clients Windows allez-vous inscrire ?** <br>Les appareils Windows 10 peuvent s’inscrire automatiquement quand vous ajoutez un compte professionnel ou scolaire. L’inscription des versions antérieures doit s’effectuer à l’aide de l’application Portail d’entreprise.

||**Azure AD Premium**|**Autre AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Inscription automatique](#automatic-enrollment) |[Inscription par le biais de l’application Portail d’entreprise](#company-portal-enrollment)|
|**Versions précédentes de Windows**|[Inscription par le biais de l’application Portail d’entreprise](#company-portal-enrollment)|[Inscription par le biais de l’application Portail d’entreprise](#company-portal-enrollment)|

## <a name="automatic-enrollment"></a>Inscription automatique

L’inscription automatique permet aux utilisateurs d’inscrire des appareils Windows 10 appartenant à l’entreprise ou personnels en ajoutant un compte professionnel ou scolaire et en acceptant leur gestion. En arrière-plan, l’appareil de l’utilisateur s’inscrit auprès d’Azure Active Directory et s’y connecte. Une fois inscrit, l’appareil peut être géré avec Intune. Les appareils gérés peuvent continuer à utiliser le portail d’entreprise pour les tâches, mais ils n’ont pas besoin de l’installer pour s’inscrire.

**Conditions préalables**
- Abonnement Premium à Azure Active Directory ([abonnement d’évaluation](http://go.microsoft.com/fwlink/?LinkID=816845))
- Abonnement Microsoft Intune

### <a name="configure-automatic-enrollment"></a>Configurer l’inscription automatique

1. Connectez-vous au [portail Azure](https://manage.windowsazure.com), accédez au nœud **Active Directory** dans le volet gauche, puis sélectionnez votre annuaire.
2. Sélectionnez l’onglet **Configurer** et faites défiler son contenu jusqu’à la section **Appareils**.
3. Sélectionnez **Tous** pour **Les utilisateurs peuvent joindre des appareils à Azure AD**.
4. Sélectionnez le nombre maximal d’appareils que vous souhaitez autoriser par utilisateur.

Par défaut, l’authentification à deux facteurs n’est pas activée pour le service. Toutefois, l’authentification à deux facteurs est recommandée au moment de l’inscription d’un appareil. Avant d’exiger l’authentification à deux facteurs pour ce service, vous devez configurer un fournisseur d’authentification à deux facteurs dans Azure Active Directory et configurer vos comptes d’utilisateur pour l’authentification multifacteur. Consultez [Bien démarrer avec le serveur Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="company-portal-enrollment"></a>Inscription par le biais de l’application Portail d’entreprise
Pour inscrire des appareils Windows, vos utilisateurs finaux ou un [gestionnaire d’inscription d’appareil](enroll-devices-with-device-enrollment-manager.md) peuvent installer l’application Portail d’entreprise et se connecter avec leurs informations d’identification professionnelles. Si vous voulez simplifier l’inscription pour vos utilisateurs finaux, ajoutez un CNAME à votre inscription DNS.

### <a name="enable-windows-device-management"></a>Activer la gestion des appareils Windows
Pour activer la gestion des appareils Windows sur des PC ou des appareils mobiles, procédez comme suit :

1.  Avant de configurer l’inscription pour n’importe quelle plateforme, tenez compte des prérequis et des procédures figurant dans [Configurer la gestion hybride des appareils mobiles](setup-hybrid-mdm.md).  
2.  Dans la console Configuration Manager, dans l’espace de travail **Administration**, accédez à **Vue d’ensemble** > **Services Cloud** > **Abonnements Microsoft Intune**.  
3.  Dans le ruban, cliquez sur **Configurer des plateformes**, puis sélectionnez la plateforme Windows :
    - **Windows** pour les PC et ordinateurs portables Windows, puis procédez comme suit :
      1. Sous l’onglet **Général**, cochez la case **Activer l’inscription Windows**.
      2. Si vous utilisez un certificat pour signer le code et déployer l’application Portail d’entreprise, accédez à **Certificat de signature de code**. Les utilisateurs d’appareils peuvent également installer l’application Portail d’entreprise à partir du Windows Store, ou vous pouvez déployer l’application à partir du Windows Store pour Entreprises sans signature de code.
      3. Vous pouvez aussi configurer [Paramètres Windows Hello Entreprise](windows-hello-for-business-settings.md).
    - **Windows Phone** pour les téléphones et tablettes Windows, puis procédez comme suit :
      1. Sous l’onglet **Général**, cochez la case **Windows Phone 8.1 et Windows 10 Mobile**. Windows Phone 8.0 n’est plus pris en charge.
      2. Si votre organisation a besoin de charger indépendamment des applications d’entreprise, vous pouvez charger le jeton ou le fichier exigé. Pour plus d’informations sur le chargement indépendant d’applications, consultez [Créer des applications Windows](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Jeton d’inscription d’application**
        - **Fichier .pfx**
        - **Aucun** Si vous utilisez un certificat Symantec, vous pouvez spécifier **Afficher une alerte avant l’expiration du certificat Symantec**.
4. Cliquez sur **OK** pour fermer la boîte de dialogue.  Pour simplifier le processus d’inscription à l’aide du portail d’entreprise, créez un alias DNS pour l’inscription des appareils. Ensuite, expliquez aux utilisateurs comment inscrire leurs appareils.

### <a name="create-dns-alias-for-device-enrollment"></a>Créer un alias DNS pour l’inscription d’appareils  
Un alias DNS (type d’enregistrement CNAME) permet aux utilisateurs d’inscrire plus facilement leurs appareils. En effet, il leur suffit de se connecter au service sans même que l’adresse d’un serveur leur soit demandée. Pour créer un alias DNS (type d’enregistrement CNAME), vous devez configurer un enregistrement CNAME dans les enregistrements DNS de votre entreprise, qui redirige les demandes envoyées à une URL dans le domaine de votre entreprise aux serveurs du service cloud Microsoft.  Par exemple, si le domaine de votre entreprise est contoso.com, vous devez créer un enregistrement CNAME dans DNS, qui redirige EnterpriseEnrollment.contoso.com vers EnterpriseEnrollment-s.manage.microsoft.com.  

 La création d’entrées CNAME dans DNS est facultative, mais les enregistrements CNAME facilitent l’inscription pour les utilisateurs. Si aucun enregistrement CNAME d’inscription n’est trouvé, les utilisateurs sont invités à taper le nom du serveur de gestion des appareils mobiles (enrollment.manage.microsoft.com).

|Type|Nom de l'hôte|Pointe vers|TTL|  
|----------|---------------|---------------|---|
|CNAME|enterpriseenrollment.domaine_entreprise.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 heure|

Si vous avez plusieurs suffixes UPN, vous devez créer un enregistrement CNAME pour chaque nom de domaine et pointer chacun d’eux vers EnterpriseEnrollment-s.manage.microsoft.com. Par exemple, si les utilisateurs de Contoso utilisent name@contoso.com, mais aussi name@us.contoso.com et name@eu.constoso.com comme e-mail/UPN, l’administrateur DNS de Contoso doit créer les enregistrements CNAME suivants.

|Type|Nom de l'hôte|Pointe vers|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 heure|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 heure|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 heure|

## <a name="tell-users-how-to-enroll-devices"></a>Expliquer aux utilisateurs comment inscrire des appareils  

 Une fois la configuration effectuée, vous devez faire savoir aux utilisateurs comment inscrire leurs appareils. Pour obtenir de l’aide, consultez [Ce qu’il faut dire aux utilisateurs sur l’inscription de leurs appareils](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Indiquez aux utilisateurs de consulter [Inscrire un appareil Windows dans Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Ces informations s’appliquent aux appareils mobiles gérés par Microsoft Intune et Configuration Manager.

> [!div class="button"]
[< Étape précédente](create-service-connection-point.md) [Étape suivante >](set-up-additional-management.md)

