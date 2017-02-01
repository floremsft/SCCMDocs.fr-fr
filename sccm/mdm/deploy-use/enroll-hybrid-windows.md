---
title: Configurer la gestion des appareils mobiles hybride Windows avec System Center Configuration Manager et Microsoft Intune | Microsoft Docs
description: Configurez la gestion des appareils Windows avec System Center Configuration Manager et Microsoft Intune.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: d242c9ae0ca6e3a3f3bee3a93176b9ab802319ae
ms.openlocfilehash: a75cba2a6bb280c29f300c8ef2d3fbfbc7a558d2


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurer la gestion hybride des appareils mobiles Windows avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser Configuration Manager avec Intune pour gérer des ordinateurs de bureau, des ordinateurs portables et d’autres appareils exécutant Windows en tant qu’appareils mobiles. Vous pouvez configurer Azure Active Directory pour autoriser l’inscription automatique des PC Windows. Vous pouvez également configurer Configuration Manager pour simplifier l’inscription à l’aide de l’application Portail d’entreprise.


Les options d’inscription Windows incluent ce qui suit :

- [Inscription automatique auprès d’Azure AD](#azure-active-directory-enrollment)
- [PC Windows](#set-up-windows-device-enrollment)
- [Appareils Windows 10 Mobile et Windows Phone](#enable-windows-phone-devices)

## <a name="azure-active-directory-enrollment"></a>Inscription Azure Active Directory

L’inscription automatique permet aux utilisateurs d’inscrire des PC Windows 10 appartenant à l’entreprise ou personnels et des appareils Windows 10 Mobile dans Intune en ajoutant un compte professionnel ou scolaire et en acceptant leur gestion. En arrière-plan, l’appareil de l’utilisateur s’inscrit et rejoint Azure Active Directory. Une fois inscrit, l’appareil peut être géré avec Intune.

**Conditions préalables**
- Abonnement Premium à Azure Active Directory ([abonnement d’évaluation](http://go.microsoft.com/fwlink/?LinkID=816845))
- Abonnement Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Configurer l’inscription automatique de la gestion des appareils mobiles

1. Dans le [portail de gestion Azure](https://manage.windowsazure.com) (https://manage.windowsazure.com), accédez au nœud **Active Directory** et sélectionnez votre annuaire.

2. Cliquez sur l’onglet **Applications** pour voir apparaître **Microsoft Intune** dans la liste des applications.

    ![Applications Azure AD avec Microsoft Intune](../media/aad-intune-app.png)

3. Cliquez sur la flèche **Microsoft Intune** pour voir apparaître une page qui vous permet de configurer Microsoft Intune.

4. Cliquez sur **Configurer** pour démarrer la configuration de l’inscription automatique de la gestion des appareils mobiles avec Microsoft Intune.

5. Spécifiez les URL pour Intune :

  - **URL d’inscription de MDM** : utilisez `https://enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc` pour l’URL d’inscription de MDM.
  - **URL des conditions d’utilisation de MDM** : utilisez la valeur par défaut. Cette URL présente les conditions d’utilisation applicables aux utilisateurs qui inscrivent des appareils.
  - **URL de conformité de MDM** : utilisez la valeur par défaut. Si un appareil se révèle non conforme, un message **Accès refusé** s’affiche avec cette URL. L’URL pointe vers une page qui permet aux utilisateurs de comprendre pourquoi leur appareil n’est pas conforme à la stratégie et comment ils peuvent le remettre en conformité.

6.  Spécifiez les appareils des utilisateurs qui doivent être gérés par Microsoft Intune. Les appareils Windows 10 de ces utilisateurs sont automatiquement inscrits à la gestion avec Microsoft Intune.

  - **Tous**
  - **Groupes**
  - **Aucun**

7. Choisissez **Enregistrer**.

## <a name="configure-windows-pc-enrollment"></a>Configurer l’inscription des PC Windows
 Pour activer la gestion des appareils mobiles Windows, vous devez activer la gestion du système d’exploitation.  Vous pouvez également ajouter un CNAME DNS pour simplifier l’inscription pour les utilisateurs.

### <a name="create-dns-alias-for-device-enrollment"></a>Créer un alias DNS pour l’inscription d’appareils  
 Un alias DNS (type d’enregistrement CNAME) permet aux utilisateurs d’inscrire leurs appareils avec plus de facilité grâce au renseignement automatique du nom du serveur pendant l’inscription d’appareils. Pour créer un alias DNS (type d’enregistrement CNAME), vous devez configurer un enregistrement CNAME dans les enregistrements DNS de votre entreprise, qui redirige les demandes envoyées à une URL dans le domaine de votre entreprise aux serveurs de service cloud Microsoft.  Par exemple, si le domaine de votre entreprise est contoso.com, vous devez créer un enregistrement CNAME dans DNS, qui redirige EnterpriseEnrollment.contoso.com vers EnterpriseEnrollment-s.manage.microsoft.com.  

 La création d’entrées CNAME dans DNS est facultative, mais les enregistrements CNAME facilitent l’inscription pour les utilisateurs. Si aucun enregistrement CNAME d’inscription n’est trouvé, les utilisateurs sont invités à taper le nom du serveur de gestion des appareils mobiles ([https://enrollment.manage.microsoft.com](https://enrollment.manage.microsoft.com)).

|Type|Nom de l'hôte|Pointe vers|  
|----------|---------------|---------------|  
|CNAME|enterpriseenrollment.domaine_entreprise.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.domaine_entreprise.com|EnterpriseRegistration.windows.net|  
### <a name="to-enable-enrollment-for-windows-devices"></a>Pour activer l’inscription des appareils Windows  

1.  **Prérequis** : avant de configurer l’inscription d’une plateforme, observez les prérequis et les procédures indiqués dans [Configurer la gestion hybride des appareils mobiles](setup-hybrid-mdm.md).  

2.  Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud** > **Abonnements Microsoft Intune**.  

    > [!WARNING]  
    >  Si d’autres boîtes de dialogue Configuration Manager sont ouvertes, fermez-les avant de poursuivre cette procédure.  

3.  Sous l'onglet **Accueil** , cliquez sur **Configurer des plateformes**, puis sur **Windows**.  

4.  Sous l’onglet **Général** , sélectionnez **Activer l’inscription Windows**.  

 Une fois la configuration effectuée, vous devez faire savoir aux utilisateurs comment inscrire leurs appareils. Consultez [Ce qu’il faut dire aux utilisateurs sur l’inscription de leurs appareils](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Ces informations s’appliquent aux appareils mobiles gérés par Microsoft Intune et Configuration Manager.

## <a name="enable-windows-phone-devices"></a>Activer les appareils Windows Phone  
  Si vos utilisateurs inscriront uniquement des appareils Windows Phone 8.1 et versions ultérieures, et que vous ne déploierez pas d’applications métier sur les appareils Windows Phone, aucun certificat Symantec n’est nécessaire. Après avoir activé l’inscription Windows Phone, vous devez demander aux utilisateurs d’installer l’application Portail d’entreprise à partir du Windows Phone Store pour inscrire leurs appareils.  

  Effectuez les étapes suivantes pour les appareils Windows Phone que vous allez gérer.  

### <a name="to-enable-enrollment-for-windows-phone-81-and-later-devices"></a>Pour activer l’inscription pour les appareils Windows Phone 8.1 et versions ultérieures  

 1.  **Prérequis** : avant de configurer l’inscription d’une plateforme, observez les prérequis et les procédures indiqués dans [Configurer la gestion hybride des appareils mobiles](setup-hybrid-mdm.md).  

 2.  Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud** > **Abonnements Microsoft Intune**.  

     > [!WARNING]  
     >  Si d’autres boîtes de dialogue Configuration Manager sont ouvertes, fermez-les avant de poursuivre cette procédure.  

 3.  Sous l'onglet **Accueil** , cliquez sur **Configurer des plateformes**, puis sur **Windows Phone**.  

 4.  Sous l’onglet **Général** , choisissez  **Windows Phone 8.1 et Windows 10 Mobile**. Vous pouvez charger les données du fichier .xml AET ou un fichier .pfx pour prendre en charge le déploiement de l’application Portail d’entreprise, ou de demander aux utilisateurs de télécharger l’application Portail d’entreprise à partir du Windows Phone Store.  

      Cliquez sur **OK**.  

  Une fois la configuration effectuée, vous devez faire savoir aux utilisateurs comment inscrire leurs appareils. Consultez [Ce qu’il faut dire aux utilisateurs sur l’inscription de leurs appareils](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Ces informations s’appliquent aux appareils mobiles gérés par Microsoft Intune et Configuration Manager.  



<!--HONumber=Jan17_HO4-->


