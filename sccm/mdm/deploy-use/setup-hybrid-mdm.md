---
title: Configurer la gestion des appareils mobiles hybride | Microsoft Docs
description: "Configurez une inscription d’appareils hybride avec Configuration Manager et Intune."
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
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 48b91e88f78752cf7c05162b701ea2ca2f401de3
ms.openlocfilehash: 85df3df19f01f8ed6f5240851c47afce01a92880

---

# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurer une gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*


Avant de pouvoir gérer des appareils iOS, Windows et Android avec Configuration Manager, vous devez les inscrire dans Intune. Effectuez les étapes suivantes pour configurer une inscription d’appareils hybride avec Configuration Manager via Intune. En effectuant les étapes suivantes, vous allez activer l’inscription BYOD (« Apportez votre propre appareil ») pour vos utilisateurs. Ces étapes sont également des prérequis pour [l’inscription d’appareils appartenant à l’entreprise](enroll-company-owned-devices.md).

 |Étapes|Détails|  
 |-----------|-------------|  
 |**Étape 1 :** [Créer un regroupement MDM](#step-1-create-an-mdm-collection)|Créez un regroupement d’utilisateurs Configuration Manager comprenant les utilisateurs dont les appareils peuvent être inscrits|  
 |**Étape 2 :** [Respecter les critères pour les noms de domaine](#step-2-domain-name-requirements)|Vérifiez que le service de nom de domaine (DNS) de votre organisation et la gestion des utilisateurs Active Directory répondent aux critères MDM|
 |**Étape 3 :** [Configurer l’abonnement Intune](#step-3-configure-intune-subscription)|Le service Intune vous permet de gérer des appareils via Internet.|  
 |**Étape 4 :** [Ajouter les conditions générales](#step-4-add-terms-and-conditions)| Créez des conditions générales que les utilisateurs doivent accepter pour pouvoir utiliser l’application Portail d’entreprise|
 |**Étape 5 :** [Créer un point de connexion de service](#step-5-create-service-connection-point)|Le point de connexion de service envoie des informations sur les paramètres et le déploiement des logiciels à Configuration Manager. De plus, il récupère les messages d’état et d’inventaire à partir des appareils mobiles. |  
 |**Étape 6 :** [Activer l’inscription de la plateforme](#step-6-enable-platform-enrollment)|L’inscription MDM des appareils [iOS](#ios-and-mac-enrollment-setup) et [Windows](#windows-enrollment-setup) nécessite des étapes supplémentaires pour établir la communication entre le service et les appareils. Android ne nécessite aucune configuration supplémentaire.|  
 |**Étape 7 :** [Configurer une gestion supplémentaire](#step-7-set-up-additional-management)|(Facultatif) Configurer les éléments de configuration et l’accès conditionnel des appareils inscrits|
 |**Étape 8 :** [Vérifier la configuration MDM](#step-8-verify-mdm-configuration)|Affichez les fichiers journaux pour vérifier que le point de connexion de service a été créé et que les comptes d’utilisateur se synchronisent.|
 |**Étape 9 :** [Inscrire des appareils](#step-9-enroll-devices)|Indiquez aux utilisateurs comment inscrire leurs appareils, ou commencez à inscrire les appareils appartenant à l’entreprise pour répondre aux besoins de votre organisation|

Vous recherchez Intune sans Configuration Manager ?
> [!div class="button"]
[Afficher les documents relatifs à Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)

## <a name="step-1-create-an-mdm-collection"></a>Étape 1 : Créer un regroupement MDM
Vous avez besoin d’un regroupement d’utilisateurs Configuration Manager pour spécifier les utilisateurs qui peuvent inscrire des appareils à gérer. Seuls les regroupements d’utilisateurs peuvent être ciblés, car les licences Intune sont attribuées aux utilisateurs. À des fins de test, vous pouvez configurer une **règle directe** et ajouter des utilisateurs spécifiques qui peuvent inscrire des appareils. Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Regroupements d’utilisateurs**, cliquez sur l’onglet **Accueil** > **Créer** un groupe, puis cliquez sur **Créer un regroupement d’utilisateurs**. Pour une distribution plus large, utilisez **Règle de requête** et définissez des utilisateurs. Pour plus d’informations sur les regroupements, consultez [Guide pratique pour créer des regroupements](https://technet.microsoft.com/library/mt629371.aspx).

![Créer un regroupement d’utilisateurs pour MDM](../media/mdm-create-user-collection.png)

## <a name="step-2-domain-name-requirements"></a>Étape 2 : Respecter les critères pour les noms de domaine

Si nécessaire, procédez comme suit pour satisfaire toutes les dépendances externes à Configuration Manager :

1. Chaque utilisateur doit disposer d’une licence Intune pour l’inscription des appareils. Pour permettre l’association de licences Intune aux utilisateurs, chaque utilisateur doit disposer d’un nom d’utilisateur principal (UPN) qui peut être résolu publiquement (par exemple johndoe@contoso.com) ou un ID de connexion de substitution configuré dans Azure Active Directory. La configuration d’un ID de connexion de substitution permet aux utilisateurs de se connecter avec une adresse e-mail, même si leur UPN est au format NetBIOS (par exemple, CONTOSO\johndoe).

  - Si votre entreprise utilise des UPN qui peuvent être résolues publiquement (par exemple johndoe@contoso.com),, aucune configuration supplémentaire n’est nécessaire.
  - Si votre entreprise utilise un UPN qui ne peut pas être résolu (par exemple CONTOSO\johndoe), vous devez [configurer un ID de substitution dans Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2.  Déployez et configurez les services ADFS (Active Directory Federation Services). (Facultatif)

     Quand vous configurez l’authentification unique, vos utilisateurs peuvent se connecter à l’aide de leurs informations d’identification d’entreprise pour accéder aux services d’Intune.

     Pour plus d'informations, consultez les rubriques suivantes :
    -   [Préparer l’authentification unique](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [Planifier et déployer AD FS 2.0 en vue d’une utilisation avec l’authentification unique](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  Déploiement et configuration de la synchronisation d'annuaires

     La synchronisation de répertoires vous permet de remplir Intune avec des comptes d’utilisateur synchronisés. Les comptes d’utilisateur et les groupes de sécurité synchronisés sont ajoutés à Intune. L’échec d’activation de la synchronisation d’annuaires est une cause courante de l’incapacité des appareils à s’inscrire lors de la configuration du MDM Configuration Manager avec Microsoft Intune.

     Pour plus d’informations, consultez [Intégration d’annuaire](http://go.microsoft.com/fwlink/?LinkID=271120) dans la bibliothèque de documentation d’Active Directory.

4.  Facultatif et non recommandé : si vous n’utilisez pas les services ADFS (Active Directory Federation Services), réinitialisez les mots de passe Microsoft Online des utilisateurs.

     Si vous n'utilisez pas AD FS, vous devez définir un mot de passe Microsoft Online pour chaque utilisateur.

## <a name="step-3-configure-intune-subscription"></a>Étape 3 : Configurer l’abonnement Intune
 L’abonnement Intune vous permet de gérer des appareils via Internet. Vous pouvez notamment spécifier le regroupement d’utilisateurs pouvant inscrire des appareils, et définir les informations présentées aux utilisateurs. L’abonnement Intune effectue les opérations suivantes :

-   Récupération du certificat dont a besoin le point de connexion de service pour se connecter au service Intune
-   Définition du regroupement d’utilisateurs permettant aux utilisateurs d’inscrire des appareils mobiles
-   Définition et configuration des plateformes mobiles que vous souhaitez prendre en charge

> [!IMPORTANT]
>  La création d’un abonnement pour Microsoft Intune dans Configuration Manager place le point de connexion de service de votre site en « mode en ligne ». Consultez [À propos du point de connexion de service dans System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

### <a name="to-create-the-microsoft-intune-subscription"></a>Pour créer l'abonnement Microsoft Intune

1.  Si vous n’avez pas encore de compte Microsoft Intune, créez-en un sur [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216).  Une fois que vous avez créé votre compte Intune, vous n’avez pas besoin d’y ajouter des utilisateurs ou d’effectuer des configurations de paramètres supplémentaires.

2.  Dans la console Configuration Manager, cliquez sur **Administration**.

3.  Dans l'espace de travail **Administration** , développez **Services cloud**, puis cliquez sur **Abonnements Microsoft Intune**. Sous l'onglet **Accueil** , cliquez sur **Ajouter un abonnement Microsoft Intune**.

![Créer un abonnement Intune](../media/mdm-set-intune.png)

4.  Dans la page **Introduction** de l'Assistant Créer un abonnement Microsoft Intune, lisez le texte et cliquez sur **Suivant**.

5.  Dans la page **Abonnement** , cliquez sur **Se connecter** , puis connectez-vous en utilisant votre compte professionnel ou scolaire. Dans la boîte de dialogue **Définir l’autorité de gestion des appareils mobiles**, cochez la case permettant de gérer uniquement les appareils mobiles à l’aide de Configuration Manager via la console Configuration Manager. Pour poursuivre la procédure d'abonnement, vous devez sélectionner cette option.

    > [!IMPORTANT]
    >  Une fois que vous avez sélectionné Configuration Manager comme autorité de gestion, vous ne pouvez plus définir Microsoft Intune comme autorité de gestion.

6.  Pour prendre connaissance de la déclaration de confidentialité, cliquez sur les liens correspondants. Cliquez ensuite sur **Suivant**.

7.  Sur la page **Général** , spécifiez les options suivantes et cliquez sur **Suivant**.

  -   **Regroupement**: spécifiez un regroupement d'utilisateurs contenant les utilisateurs qui sont appelés à inscrire leurs appareils mobiles.

      > [!NOTE]
      >  Si un utilisateur est supprimé d’un regroupement, l’appareil de l’utilisateur continue d’être géré pendant 24 heures au maximum, le temps que l’enregistrement soit supprimé de la base de données utilisateur.

  -   **Nom de la société**: spécifiez le nom de votre entreprise.

  -   **URL vers la documentation de confidentialité**: si vous publiez des informations de confidentialité sur votre société par le biais d’un lien accessible sur Internet, fournissez un lien auquel les utilisateurs puissent accéder à partir du portail d’entreprise, par exemple http://www.contoso.com/CP_privacy.html. Les informations de confidentialité permettent de donner des précisions sur les informations que les utilisateurs partagent avec votre entreprise.

  -   **Modèle de couleurs pour le portail de la société**: modifiez éventuellement la couleur bleue par défaut des portails d'entreprise.

  -   **Code de site Configuration Manager**: spécifiez le code de site d'un site principal pour gérer les appareils mobiles.

    > [!NOTE]
    >  La modification du code de site affecte uniquement les nouvelles inscriptions et n'affecte pas les appareils inscrits existants.

8.  Dans la page **Coordonnées de contact de l’entreprise**, spécifiez les informations de contact de l’entreprise visibles par les utilisateurs, sous **Contacter le service informatique**, dans l’application Portail d’entreprise. Fournissez les informations de contact de votre entreprise, puis cliquez sur **Suivant**.

9. Dans la page **Logo de l’entreprise**, choisissez d’afficher éventuellement un logo dans le Portail d’entreprise, puis cliquez sur **Suivant**.

10. Effectuez toutes les étapes de l'Assistant.

## <a name="step-4-add-terms-and-conditions"></a>Étape 4 : Ajouter les conditions générales
 Une fois que vous avez configuré la gestion Intune pour les appareils mobiles, vous pouvez créer des **Conditions générales**. Utilisez les conditions générales pour expliquer aux utilisateurs ce qui se produit quand ils inscrivent leurs appareils. Les utilisateurs doivent accepter les conditions générales pour pouvoir inscrire un appareil. Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Paramètres de compatibilité** > **Conditions générales**, puis cliquez sur **Créer les conditions générales**. Voir [Conditions générales dans System Center Configuration Manager](terms-and-conditions.md).

##  <a name="step-5-create-service-connection-point"></a>Étape 5 : Créer un point de connexion de service
Après avoir créé votre abonnement, vous pouvez installer le rôle de système de site de point de connexion de service, qui vous permet de vous connecter au service Intune. Ce rôle de système de site envoie les paramètres et les applications au service Intune.

 Le point de connexion de service envoie des informations sur les paramètres et le déploiement des logiciels à Configuration Manager. De plus, il récupère les messages d’état et d’inventaire à partir des appareils mobiles. Le service Configuration Manager joue le rôle d’une passerelle qui communique avec les appareils mobiles et stocke les paramètres.

> [!NOTE]
>  Le rôle de système de site de point de connexion de service ne peut être installé que sur le site d’administration centrale ou un site principal autonome. Le point de connexion de service doit avoir accès à Internet.


### <a name="configure-the-service-connection-point-role"></a>Configurer le rôle de point de connexion de service

1.  Dans la console Configuration Manager, cliquez sur **Administration**.

2.  Dans l’espace de travail **Administration**, développez **Sites**, puis cliquez sur **Serveurs et rôles de système de site**.

3.  Ajoutez le rôle **Point de connexion de service** à un serveur de système de site nouveau ou existant en suivant l’étape correspondante :

    -   Nouveau serveur de système de site : sous l’onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un serveur de système de site** pour démarrer l’Assistant Création d’un serveur de système de site.

    -   Serveur de système de site existant : cliquez sur le serveur sur lequel vous souhaitez installer le rôle de point de connexion de service. Ensuite, sous l'onglet **Accueil** , dans le groupe **Serveur** , cliquez sur **Ajouter des rôles de système de site** pour démarrer l'Assistant Ajout des rôles de système de site.

4.  Dans la page **Sélection du rôle système** , sélectionnez **Point de connexion de service**, puis cliquez sur **Suivant**.

![Créer un point de connexion de service](../media/mdm-service-connection-point.png)

5.  Effectuez toutes les étapes de l'Assistant.

### <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>Comment le point de connexion de service s’authentifie-t-il auprès du service Microsoft Intune ?
 Le point de connexion de service étend les fonctionnalités de Configuration Manager en se connectant au service cloud Intune qui gère les appareils mobiles via Internet. Le point de connexion de service s’authentifie auprès du service Intune comme suit :

1.  Quand vous créez un abonnement Intune dans la console Configuration Manager, l’administrateur Configuration Manager est authentifié en se connectant à Azure Active Directory, qui effectue une redirection vers le serveur ADFS approprié pour demander le nom d’utilisateur et le mot de passe. Intune délivre ensuite un certificat au locataire.

2.  Le certificat de l’étape 1 est installé sur le rôle de site de point de connexion de service et il est utilisé pour authentifier et autoriser toutes les communications ultérieures avec le service Microsoft Intune.

## <a name="step-6-enable-platform-enrollment"></a>Étape 6 : Activer l’inscription de la plateforme
  Les différentes plateformes d’appareils nécessitent une configuration supplémentaire pour permettre l’inscription des appareils :
  - [Configuration de l’inscription pour iOS et Mac](#ios-and-mac-enrollment-setup) : obtenez un certificat Push MDM Apple
  - [Configuration de l’inscription pour Windows](#windows-enrollment-setup) : configurez le DNS et activez l’inscription pour les ordinateurs Windows, ainsi que pour les appareils Windows 10 Mobile et Windows Phone
  - Android : les appareils Android ne nécessitent aucune étape supplémentaire pour permettre l’inscription

Une fois que vous activez la gestion des appareils mobiles, vous pouvez spécifier le nombre d’appareils que chaque utilisateur peut inscrire, jusqu’à 15 chacun.

### <a name="ios-and-mac-enrollment-setup"></a>Configuration de l’inscription pour iOS et Mac
  Les étapes suivantes permettent de gérer les appareils Apple via le chargement d’un certificat Push MDM Apple vers le service Intune.

  1.  **Téléchargez une demande de signature de certificat** : un fichier de demande de signature de certificat (.csr) est nécessaire pour demander un certificat APNs auprès d’Apple.  

      1.  Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud**> **Abonnements Microsoft Intune**.  

      2.  Sous l’onglet **Accueil** , cliquez sur **Créer une demande de certificat APNs**. La boîte de dialogue **Effectuer une demande de signature de certificat APNs** s'ouvre.  

      3.  Cliquez sur**Parcourir** pour accéder à l'emplacement auquel vous souhaitez enregistrer le fichier du nouveau certificat de demande de signature (.csr). Enregistrez localement le fichier de demande de signature de certificat (.csr).  

      4.  Cliquez sur **Télécharger**. Le nouveau fichier .csr Microsoft Intune se télécharge et il est enregistré par Configuration Manager. Le fichier .csr est utilisé pour demander un certificat de relation d'approbation à partir du portail Apple Push Certificates.  

  2.  **Demandez un certificat APNs auprès d’Apple** : le certificat APNs (Apple Push Notification service) est utilisé pour établir une relation d’approbation entre le service de gestion, Intune et les appareils mobiles iOS inscrits.  

      1.  Dans un navigateur, accédez au [portail Apple Push Certificates](http://go.microsoft.com/fwlink/?LinkId=269844) et connectez-vous avec votre ID Apple d’entreprise. Cet ID Apple doit être utilisé ultérieurement pour renouveler votre certificat APNs.  

      2.  Terminez l’Assistant en utilisant le fichier (.csr) de demande de signature de certificat. Téléchargez le certificat APNs et enregistrez le fichier .pem localement. Ce fichier de certificat APNs (.pem) est utilisé pour établir une relation d’approbation entre le serveur Apple Push Notification et l’autorité de gestion des appareils mobiles Intune.  

  3.  **Activez l’inscription et téléchargez le certificat APNs** : pour activer l’inscription iOS, téléchargez le certificat APNs.  

      1.  Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud** > **Abonnement Microsoft Intune**.  

      2.  Sous l’onglet **Accueil** , dans le groupe **Abonnement** , cliquez sur **Configurer des plateformes** > **iOS**.  

          > [!NOTE]  
          >  Ne téléchargez pas le certificat APNs tant que vous n’avez pas activé l’inscription iOS dans la console Configuration Manager.  

      3.  Dans la boîte de dialogue **Propriétés des abonnements Microsoft Intune** , sélectionnez l’onglet **iOS** et cochez la case **Activer l’inscription iOS** .  

      4.  Cliquez sur **Parcourir**et accédez au fichier (.cer) du certificat APNs téléchargé à partir d’Apple. Configuration Manager affiche les informations du certificat APNs. Cliquez sur **OK** pour enregistrer le certificat APNs sur Intune.    


Informations supplémentaires sur la [configuration de l’inscription pour iOS et Mac](enroll-hybrid-ios-mac.md).

### <a name="windows-enrollment-setup"></a>Configuration de l’inscription pour Windows  
Vous pouvez utiliser Configuration Manager avec Intune pour gérer des postes de travail, des ordinateurs portables et d’autres appareils exécutant Windows en tant qu’appareils mobiles. Vous pouvez également configurer les appareils Windows 10 pour qu’ils s’[inscrivent automatiquement quand ils rejoignent Azure Active Directory](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/enroll-hybrid-windows#azure-active-directory-enrollment) en ajoutant un compte société ou un compte scolaire sur l’appareil.

Un alias DNS (type d’enregistrement CNAME) permet aux utilisateurs d’inscrire leurs périphériques avec plus de facilité grâce au renseignement automatique du nom du serveur pendant l’inscription d’appareils. Vous pouvez ensuite activer l’inscription des PC et appareils mobiles Windows.  

1. Dans la console Configuration Manager, dans l’espace de travail **Administration**, accédez à **Services cloud** > **Abonnements Microsoft Intune**, puis procédez comme suit :  
  - **PC Windows :** sous l’onglet **Accueil**, cliquez sur **Configurer des plateformes**, puis cliquez sur **Windows**. Sous l’onglet **Général** , sélectionnez **Activer l’inscription Windows**.  
  - **Windows 10 Mobile et Windows Phone :** sous l’onglet **Accueil**, cliquez sur **Configurer des plateformes**, puis cliquez sur **Windows Phone**.  Sous l’onglet **Général** , choisissez  **Windows Phone 8.1 et Windows 10 Mobile**.

2.  Vous pouvez également configurer Configuration Manager pour simplifier l’inscription à l’aide de l’application Portail d’entreprise.
(Facultatif) Créez un alias DNS (type d’enregistrement CNAME) dans les enregistrements DNS de votre entreprise, qui redirige les requêtes envoyées à une URL du domaine de votre entreprise aux serveurs de service cloud Microsoft.  Par exemple, si le domaine de votre entreprise est contoso.com, vous devez créer un enregistrement CNAME dans DNS, qui redirige EnterpriseEnrollment.contoso.com vers EnterpriseEnrollment-s.manage.microsoft.com.  

|Type|Nom de l'hôte|Pointe vers|  
|----------|---------------|---------------|  
|CNAME|enterpriseenrollment.domaine_entreprise.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.domaine_entreprise.com|EnterpriseRegistration.windows.net|  

Pour plus d’informations, consultez les détails relatifs à l’[inscription pour Windows](enroll-hybrid-windows.md).

### <a name="android-enrollment-setup"></a>Configuration de l’inscription pour Android
Vous pouvez utiliser Configuration Manager avec Intune pour gérer les téléphones et tablettes Android.
1.  Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud** > **Abonnement Microsoft Intune**.  

2.  Sous l’onglet **Accueil** , dans le groupe **Abonnement** , cliquez sur **Configurer des plateformes** > **Android**.  

3.  Dans la boîte de dialogue **Propriétés d’abonnement Microsoft Intune** , sélectionnez l’onglet **Android** et cochez la case **Activer l’inscription Android** .

Pour plus d’informations, consultez [Android](enroll-hybrid-android.md).

## <a name="step-7-set-up-additional-management"></a>Étape 7 : Configurer une gestion supplémentaire
(Facultatif) Vous pouvez configurer une gestion supplémentaire avant l’inscription des appareils. Ces solutions de gestion peuvent être créées et déployées après l’inscription des appareils, même si de nombreuses organisations préfèrent les déployer au fur et à mesure que les appareils sont intégrés à la gestion.

Les **éléments de configuration** vous permettent de gérer des paramètres tels que l’exigence d’un code confidentiel (PIN) ou d’un chiffrement sur les appareils inscrits, en fonction de leur plateforme :
- [Appareils Windows 10 et Windows 8.1](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)
- [Appareils Windows Phone](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client)
- [Appareils iOS et Mac](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)
- [Appareils Android et Samsung KNOX Standard](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)

**Les applications ** peuvent être déployées sur des appareils gérés :
- [Applications iOS](/sccm/apps/get-started/creating-ios-applications)
- [Applications Mac](/sccm/apps/get-started/creating-mac-computer-applications)
- [Applications Windows (PC)](/sccm/apps/get-started/creating-windows-applications)
- [Applications Windows Phone](/sccm/apps/get-started/creating-windows-phone-applications)
- [Applications Android](/sccm/apps/get-started/creating-android-applications)

L’**accès conditionnel** vous permet de gérer l’accès aux ressources de l’entreprise, notamment :  
- [Accès à l’e-mail](/sccm/protect/deploy-use/manage-email-access)
- [Accès à SharePoint](/sccm/protect/deploy-use/manage-sharepoint-online-access)
- [Accès à Skype Entreprise](/sccm/protect/deploy-use/manage-skype-for-business-online-access)
- [Dynamics CRM Online](/sccm/protect/deploy-use/manage-dynamics-crm-online-access)

## <a name="step-8-verify-mdm-configuration"></a>Étape 8 : Vérifier la configuration MDM

 Vous pouvez vérifier certains composants de gestion des périphériques en consultant les fichiers journaux suivants :

-   Consultez le fichier Cloudusersync.log pour vérifier que les comptes d'utilisateur sont bien synchronisés.

-   Consultez le fichier Sitecomp.log pour vérifier que le point de connexion de service a bien été créé.

## <a name="step-9-enroll-devices"></a>Étape 9 : Inscrire des appareils
La configuration hybride a été effectuée. Les appareils peuvent être inscrits dans Configuration Manager de plusieurs manières :
- Appareils appartenant à l’utilisateur (BYOD) : [informez les utilisateurs sur le mode d’inscription de leurs appareils](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) - L’aide relative à l’inscription est la même pour les appareils gérés par Intune et ceux gérés de manière hybride
- Appareils appartenant à l’entreprise : dans les informations décrivant l’[inscription des appareils appartenant à l’entreprise](enroll-company-owned-devices.md), vous trouverez de l’aide sur les différents moyens d’inscrire des appareils appartenant à l’entreprise en fonction des plateformes.

## <a name="managing-intune-subscriptions-associated-with-configuration-manager"></a>Gestion des abonnements Intune associés à Configuration Manager

Si vous ajoutez un abonnement Microsoft Intune (abonnement d’essai ou payant) à Configuration Manager, et si vous devez ensuite passer à un autre abonnement Intune, vous devez supprimer l’**abonnement Microsoft Intune** et le **point de connexion de service** dans la console Configuration Manager avant de pouvoir ajouter un nouvel abonnement.

### <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Comment supprimer un abonnement Intune de Configuration Manager

> [!IMPORTANT]
>  Tout le contenu, dont les inscriptions des utilisateurs, les stratégies et les déploiements d’applications configurés pour les appareils gérés par l’abonnement Intune, est supprimé quand vous supprimez l’abonnement.

1.  Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Abonnements Microsoft Intune**.

2.  Cliquez avec le bouton droit sur l’**abonnement Microsoft Intune** répertorié, puis cliquez sur **Supprimer**.

3.   Dans l’Assistant, cliquez sur **Remove Microsoft Intune Subscription from Configuration Manager** (Supprimer l’abonnement Microsoft Intune de Configuration Manager), sur **Suivant**, puis à nouveau sur **Suivant** pour supprimer l’abonnement.


### <a name="how-to-remove-the-service-connection-point-role"></a>Comment supprimer le rôle de point de connexion de service

1.  Accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Serveurs et rôles de système de site**.

2.  Sélectionnez le serveur hébergeant le rôle **Point de connexion de service**.

3.  Dans la liste **Rôles système de site**, sélectionnez **Point de connexion de service**, puis cliquez sur **Supprimer le rôle** dans le ruban. Confirmez que vous souhaitez supprimer le rôle. Le point de connexion de service est supprimé.

Vous pouvez à présent créer un nouveau point de connexion de service, ajouter un nouvel abonnement Intune à Configuration Manager et définir Configuration Manager comme autorité de gestion des appareils mobiles.

### <a name="how-to-change-mdm-authority-to-intune"></a>Comment définir l’autorité MDM sur Intune

Depuis la version 1610, vous pouvez définir l’autorité MDM sur Intune à la place de Configuration Manager. Des informations sur cette fonctionnalité seront bientôt disponibles.



<!--HONumber=Dec16_HO3-->


