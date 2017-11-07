---
title: "Gérer l'accès à SharePoint Online"
titleSuffix: Configuration Manager
description: "Apprenez à utiliser la stratégie d’accès conditionnel System Center Configuration Manager SharePoint Online pour gérer l’accès à OneDrive."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
caps.latest.revision: "11"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 2c1d7cd3462a54a064ec47d0b375ee4cdb25a4b4
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Gérer l’accès à SharePoint Online dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Utilisez la stratégie d’accès conditionnel System Center Configuration Manager **SharePoint Online** pour gérer l’accès aux fichiers OneDrive Entreprise situés sur SharePoint Online, en fonction des conditions que vous spécifiez.
Vous pouvez contrôler l'accès à SharePoint Online à partir des applications suivantes pour les plateformes répertoriées :  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android et iOS)  

-   Microsoft Word (Android et iOS)  

-   Microsoft Excel (Android et iOS)  

-   Microsoft PowerPoint (Android et iOS)  

-   Microsoft OneNote (Android et iOS)

Les applications de bureau Office peuvent accéder à SharePoint Online sur les PC exécutant :  

-   Office 2013 et ultérieur pour ordinateur avec [l’authentification moderne](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) activée.  

-   Windows 7.0 ou Windows 8.1  

> [!NOTE]  
>  Les PC doivent être joints au domaine ou conformes aux stratégies définies dans Intune.  



 Quand un utilisateur ciblé tente de se connecter à un fichier à l'aide d'une application prise en charge telle que OneDrive sur son appareil, l'évaluation suivante se produit :  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Pour vous connecter aux fichiers requis, l'appareil exécutant OneDrive doit :  

-   Être inscrit auprès de Microsoft Intune ou d’un PC joint à un domaine.  

-   Inscrire l’appareil dans Azure Active Directory (cela se produit automatiquement quand l’appareil est inscrit auprès d’Intune).  

     Pour un PC joint à un domaine, vous devez le configurer de manière à ce qu'il [s'inscrive automatiquement](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) dans Azure Active Directory.  

-   Être conforme aux stratégies de conformité Configuration Manager éventuellement déployées.  

 L'état de l'appareil est stocké dans Azure Active Directory, qui autorise ou bloque l'accès aux fichiers en fonction des conditions spécifiées.  

 Si une condition n'est pas remplie, l'utilisateur reçoit l'un des messages suivants quand il tente de se connecter :  

-   Si l’appareil n’est pas inscrit auprès d’Intune ou dans Azure Active Directory, l’utilisateur reçoit un message contenant des instructions pour installer l’application Portail d’entreprise et inscrire l’appareil.  

-   Si l’appareil n’est pas conforme, l’utilisateur reçoit un message le dirigeant vers le portail web Intune, où il peut trouver des informations sur le problème et des solutions pour y remédier.  

- Pour les appareils mobiles :

  Vous pouvez restreindre l’accès à SharePoint Online par le biais d’un navigateur à partir des appareils **iOS** et **Android**.  L’accès sera autorisé uniquement à partir des navigateurs pris en charge sur les appareils compatibles :
* Safari (iOS)
* Chrome (Android)
* Managed Browser (iOS et Android)

  Les navigateurs non pris en charge seront bloqués.
-   Sur un PC :  


    -   Si la stratégie est définie de manière à exiger la jonction à un domaine et que le PC n'est pas joint à un domaine, un message invitant l'utilisateur à contacter l'administrateur informatique s'affiche.  

    -   Si la stratégie définie exige la jonction à un domaine ou la conformité, le PC ne répond pas aux conditions et un message contenant des instructions sur la façon d'installer l'application Portail d'entreprise et d'inscrire l'appareil s'affiche.  

 Vous pouvez bloquer l'accès à SharePoint Online dans les applications suivantes :  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android et iOS)  

-   Microsoft Word (Android et iOS)  

-   Microsoft Excel (Android et iOS)  

-   Microsoft PowerPoint (Android et iOS)  

-   Microsoft OneNote (Android et iOS)  

## <a name="configure-conditional-access-for-sharepoint-online"></a>Configurer l’accès conditionnel pour SharePoint Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Étape 1 : configurer les groupes de sécurité Active Directory  
 Avant de commencer, configurez les groupes de sécurité Azure Active Directory pour la stratégie d'accès conditionnel. Vous pouvez configurer ces groupes dans le **Centre d'administration Office 365**ou dans le **Portail de compte Intune**. Ces groupes contiennent les utilisateurs qui seront ciblés par la stratégie ou exemptés de celle-ci. Quand un utilisateur est ciblé par une stratégie, chaque appareil qu'il utilise doit être conforme à cette stratégie pour qu'il puisse accéder aux ressources.  

 Vous pouvez spécifier deux types de groupes dans une stratégie SharePoint Online :  

-   **Groupes ciblés** : groupes d’utilisateurs auxquels s’applique la stratégie.  

-   **Groupes exemptés** : groupes d’utilisateurs exempts de la stratégie (facultatif).  

 Si un utilisateur se trouve dans les deux groupes, il est exempt de la stratégie.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Étape 2 : configurer et déployer une stratégie de conformité  
 Assurez-vous de créer une stratégie de conformité et de la déployer sur tous les appareils qui seront ciblés par la stratégie d'accès conditionnel SharePoint Online.  

> [!NOTE]  
>  Tandis que les stratégies de conformité sont déployées sur des groupes Intune ou des regroupements Configuration Manager, les stratégies d’accès conditionnel sont ciblées sur les groupes de sécurité Azure Active Directory.  

 Pour plus d’informations sur la configuration de la stratégie de conformité, consultez [Gérer des stratégies de conformité d’appareils dans System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Si vous n'avez pas déployé de stratégie de conformité et que vous activez la stratégie SharePoint Online, l'accès est accordé à tous les appareils ciblés.  

 Quand vous êtes prêt, passez à l' **Étape 3**.  

###  <a name="BKMK_OneDrive"></a> Étape 3 : configurer la stratégie SharePoint Online  


 Ensuite, configurez la stratégie de manière à restreindre l'accès à SharePoint Online aux appareils gérés et conformes. Cette stratégie sera stockée dans Azure Active Directory.

 >[!NOTE]
 >Vous pouvez aussi créer une stratégie d’accès conditionnel dans la console de gestion Azure AD. Celle-ci vous permet de créer les stratégies d’accès conditionnel aux appareils (appelées dans Azure AD « stratégies d’accès conditionnel en fonction de l’appareil ») en plus des autres stratégies d’accès conditionnel comme l’authentification multifacteur. Vous pouvez aussi définir des stratégies d’accès conditionnel pour des applications d’entreprise tierces comme Salesforce et Box prises en charge par Azure AD. Pour plus d’informations, consultez [Guide pratique pour définir la stratégie d’accès conditionnel en fonction de l’appareil Azure Active Directory pour contrôler l’accès aux applications connectées Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/).  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Sélectionnez **Activer la stratégie d'accès conditionnel pour SharePoint Online**.  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  Sous **Accès à l’application** pour Outlook et les applications qui utilisent une authentification moderne, vous pouvez choisir de restreindre l’accès aux seuls appareils conformes pour chaque plateforme.  

    > [!TIP]  
    >  L'**authentification moderne** permet aux clients Office de bénéficier de la connexion basée sur la bibliothèque ADAL (Active Directory Authentication Library).  
    >   
    >  -   L'authentification ADAL permet aux clients Office de procéder à une authentification basée sur un navigateur (également appelée authentification passive).  Pour s'authentifier, l'utilisateur est dirigé vers une page web de connexion.  
    > -   Cette nouvelle méthode de connexion autorise de nouveaux scénarios tels que l'accès conditionnel basé sur la **compatibilité des appareils** et sur l'exécution préalable de l' **authentification multifacteur** .  
    >   
    >  Cet [article](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) contient des informations plus détaillées sur le fonctionnement de l’authentification moderne.  

     Pour les PC Windows, ceux-ci doivent être joints à un domaine ou inscrits auprès d’Intune et être conformes. Vous pouvez définir les conditions suivantes :  

    -   **Les appareils doivent être joints à un domaine ou conformes.** Cela signifie que les PC doivent être joints à un domaine ou conformes aux stratégies définies dans Intune. Si un PC ne remplit pas l’une des conditions requises, l’utilisateur est invité à inscrire l’appareil auprès d’Intune.  

    -   **Les appareils doivent être joints à un domaine** . Cela signifie que les PC doivent être joints à un domaine pour accéder à Exchange Online. Si le PC n'est pas joint à un domaine, l'accès à la messagerie électronique est bloqué et l'utilisateur est invité à contacter l'administrateur informatique.  

    -   **Les appareils doivent être conformes** Cela signifie que les PC doivent être inscrits dans Intune et être conformes. Si le PC n'est pas inscrit, un message contenant des instructions sur la procédure d'inscription à suivre s'affiche.  

4.  Sous **Accès du navigateur à SharePoint et à OneDrive Entreprise**, vous pouvez choisir d’autoriser l’accès à Exchange Online uniquement par le biais des navigateurs pris en charge : Safari (iOS) et Chrome (Android). L’accès à partir d’autres navigateurs sera bloqué.  Les mêmes restrictions de plateforme que celles que vous avez sélectionnées pour l’accès aux applications pour OneDrive s’appliquent également ici.

    Sur les appareils **Android** , les utilisateurs doivent activer l’accès du navigateur.  Pour cela, l’utilisateur final doit activer l’option « Activer l’accès du navigateur » sur l’appareil inscrit :
    1.  Lancez **l’application Portail d’entreprise**.
    2.  Accédez à la page **Paramètres** via les trois points (...) ou le bouton de menu matériel.
    3.  Appuyez sur le bouton **Activer l’accès du navigateur** .
    4.  Dans le navigateur Chrome, déconnectez-vous d’Office 365 et redémarrez Chrome.

    Sur les plateformes **iOS et Android** , pour identifier l’appareil utilisé pour accéder au service, Azure Active Directory émet un certificat TLS (Transport Layer Security) pour l’appareil.  L’appareil affiche le certificat et invite l’utilisateur final à le sélectionner, comme indiqué dans les captures d’écran ci-dessous. L’utilisateur final doit sélectionner ce certificat pour pouvoir continuer à utiliser le navigateur.

     **iOS**

     ![capture d’écran de l’invite de certificat sur un ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Android**

      ![capture d’écran de l’invite de certificat sur un appareil Android](media/mdm-browser-ca-android-cert-prompt.png)

4.  Sous l'onglet **Accueil** , dans le groupe **Liens** , cliquez sur **Configurer la stratégie d'accès conditionnel dans la console Intune**. Il se peut que vous deviez fournir le nom d’utilisateur et le mot de passe du compte utilisé pour connecter Configuration Manager à Intune.  

     La console d’administration Intune s’ouvre.  

5.  Dans la console [console d'administration Microsoft Intune](https://manage.microsoft.com), cliquez sur **Stratégie** > **Accès conditionnel** > **SharePoint Online Stratégie**.  

6.  Sélectionnez **Bloquez l'accès des applications à SharePoint Online si l'appareil n'est pas conforme**.  

7.  Sous **Groupes ciblés**, cliquez sur **Modifier** pour sélectionner les groupes de sécurité Active Directory auxquels la stratégie sera appliquée.  

8.  Sous **Groupes exemptés**, vous pouvez éventuellement cliquer sur **Modifier** pour sélectionner les groupes de sécurité Azure Active Directory exempts de cette stratégie.  

9. Une fois terminé, cliquez sur **Enregistrer**.  

 La stratégie d'accès conditionnel prend effet immédiatement. Il est donc inutile de la déployer.  

 Consultez [Gérer l’accès à SharePoint Online avec Microsoft Intune](https://technet.microsoft.com/library/dn705844.aspx) pour savoir comment contrôler la stratégie à partir de la console Intune.  

### <a name="see-also"></a>Voir aussi  

 [Gérer l’accès aux services dans System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
