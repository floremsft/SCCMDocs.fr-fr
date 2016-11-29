---
title: "Déployer des clients Mac | System Center Configuration Manager"
description: "Découvrez comment déployer des clients sur des ordinateurs Mac dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: eae9e76085a95cb09fe01a32fd4b57294bc1cc20


---
# <a name="how-to-deploy-clients-to-macs-in-system-center-configuration-manager"></a>How to deploy clients to Macs in System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

L’installation et la gestion de clients pour les ordinateurs Mac dans System Center Configuration Manager nécessitent des certificats d’infrastructure à clé publique (PKI). Configuration Manager peut demander et installer un certificat client utilisateur à l’aide des services de certificat Microsoft avec une autorité de certification d’entreprise (CA) et les rôles de système de site du point d’inscription et du point proxy d’inscription de Configuration Manager. Vous pouvez également demander et installer un certificat d’ordinateur indépendamment de Configuration Manager si le certificat répond aux critères de Configuration Manager. Les certificats PKI permettent de sécuriser les communications entre les ordinateurs Mac et le site Configuration Manager grâce à une authentification mutuelle et des transferts de données chiffrés.  

> [!IMPORTANT]  
>  Les clients Mac de Configuration Manager procèdent toujours à une vérification de la révocation des certificats ; à la différence des clients Configuration Manager qui s’exécutent sous Windows, vous ne pouvez pas désactiver cette fonction de vérification de la liste de révocation de certificats (CRL).  
>   
>  Si les clients Mac ne peuvent pas vérifier l’état de révocation du certificat d’un serveur du fait de leur incapacité à localiser la liste CRL, ils ne pourront pas se connecter aux systèmes de site Configuration Manager, tels que les points de gestion et de distribution. Vérifiez la conception de votre liste CRL pour être certain que les clients Mac (plus particulièrement ceux appartenant à une forêt différente de celle de l'autorité de certification émettrice) seront en mesure de localiser et de se connecter à un point de distribution de la liste CRL (CDP) pour la connexion des serveurs de système de site.  

 Avant d’installer le client Configuration Manager sur un ordinateur Mac, choisissez le mode d’installation du certificat client :  

-   Utilisez l’inscription Configuration Manager à l’aide de l’outil CMEnroll et suivez les étapes décrites dans la section suivante de cette rubrique. Le processus d'inscription ne prenant pas en charge le renouvellement automatique de certificats, vous devez réinscrire les ordinateurs Mac avant l'expiration du certificat installé.  

-   Utilisez une demande de certificat et une méthode d’installation indépendante de Configuration Manager. Pour cette méthode d'installation, consultez la section [Use a certificate request and installation method that is independent from Configuration Manager](#BKMK_ManualCertifcateInstallation) dans cette rubrique.  

> [!NOTE]  
>  Pour plus d’informations sur le certificat client Mac requis et sur les autres certificats PKI nécessaires à la prise en charge des ordinateurs Mac, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

 Les clients Mac sont attribués automatiquement au site Configuration Manager qui les gère. Les clients Mac s'installent en tant que clients Internet uniquement, même si la communication est limitée à l'intranet. Cette configuration de client signifie qu'ils communiquent avec les rôles de système de site (points de gestion et points de distribution) sur le site qui leur est attribué si vous configurez ces rôles pour autoriser les connexions client depuis Internet. Les ordinateurs Mac ne communiquent pas avec les rôles de système de site extérieurs au site qui leur est attribué.  

> [!IMPORTANT]  
>  Le client Mac de Configuration Manager ne peut pas être utilisé pour se connecter à un point de gestion configuré pour utiliser un réplica de base de données. Pour plus d’informations sur les réplicas de base de données, consultez [Réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 Utilisez les sections suivantes pour installer, configurer et gérer des ordinateurs Mac pour Configuration Manager :  

-   [Procédure d’installation et de configuration du client pour les ordinateurs Mac](#InstallSteps)  

-   [Uninstalling the Mac client](#uninstallMacClient)  

-   [Renewing the Mac client certificate](#BKMK_Renew)  

-   [Use a certificate request and installation method that is independent from Configuration Manager](#BKMK_ManualCertifcateInstallation)  

##  <a name="a-nameinstallstepsa-steps-to-install-and-configure-the-client-for-macs"></a><a name="InstallSteps"></a> Procédure d’installation et de configuration du client pour les ordinateurs Mac  

> [!IMPORTANT]  
>  Avant d’effectuer ces étapes, assurez-vous que votre ordinateur Mac dispose de la configuration requise. Pour plus d’informations, consultez [Systèmes d’exploitation pris en charge pour les ordinateurs Mac](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

### <a name="step-1-deploy-a-web-server-certificate-to-site-system-servers"></a>Étape 1 : Déployer un certificat de serveur web sur les serveurs de système de site  
 Ces systèmes de site peuvent déjà détenir ce certificat pour d’autres clients Configuration Manager. À défaut, déployez un certificat de serveur Web sur les ordinateurs qui détiennent les rôles de système de site suivants :  

-   Point de gestion  

-   Point de distribution  

-   Point d'inscription  

-   Point proxy d'inscription  

> [!IMPORTANT]  
>  Le certificat de serveur Web doit contenir le nom de domaine Internet complet qui est spécifié dans les propriétés de système de site.  
>   
>  Cela ne signifie pas que le serveur doit être accessible sur Internet pour prendre en charge les ordinateurs Mac. Si vous n'exigez pas de gestion des clients basée sur Internet, vous pouvez spécifier la valeur du nom de domaine complet intranet pour le nom de domaine complet Internet.  

 Pour voir un exemple de déploiement qui crée et installe ce certificat de serveur web, consultez [Déploiement du certificat de serveur web pour les systèmes de site qui exécutent IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

> [!IMPORTANT]  
>  Assurez-vous de spécifier la valeur du nom de domaine complet Internet du système de site dans le certificat de serveur web pour le point de gestion, le point de distribution et le point proxy d’inscription.  

### <a name="step-2-deploy-a-client-authentication-certificate-to-site-system-servers"></a>Étape 2 : Déployer un certificat d’authentification client sur les serveurs de système de site  
 Ces systèmes de site peuvent déjà détenir ce certificat pour les fonctionnalités Configuration Manager. À défaut, déployez un certificat d'authentification client sur les ordinateurs qui détiennent les rôles de système de site suivants :  

-   Point de gestion  

-   Point de distribution  

 Pour obtenir un exemple de déploiement qui crée et installe le certificat client pour les points de gestion, consultez [Déploiement du certificat client pour les ordinateurs Windows](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

 Pour obtenir un exemple de déploiement qui crée et installe le certificat client pour les points de distribution, consultez [Déploiement du certificat client pour les points de distribution](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### <a name="step-3-prepare-the-client-certificate-template-for-macs"></a>Étape 3 : Préparer le modèle de certificat client pour les ordinateurs Mac  

> [!NOTE]  
>  Pour exécuter l’outil d’inscription Configuration Manager, vous devez disposer d’un compte d’utilisateur Active Directory.  

 Le modèle de certificat doit disposer d'autorisations de **lecture** et d' **inscription** pour le compte d'utilisateur appelé à inscrire le certificat sur l'ordinateur Mac.  

 Consultez [Déploiement du certificat client pour les ordinateurs Mac](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  

### <a name="step-4-configure-the-management-point-and-distribution-point"></a>Étape 4 : Configurer le point de gestion et le point de distribution  
 Configurez des points de gestion pour les options suivantes :  

-   HTTPS  

-   Autoriser les connexions client à partir d'Internet  

    > [!NOTE]  
    >  Cette valeur de configuration est nécessaire pour gérer les ordinateurs Mac. Toutefois, cela ne signifie pas que les serveurs de système de site doivent être accessibles sur Internet.  

-   Autoriser les appareils mobiles et les ordinateurs Mac à utiliser ce point de gestion  

 Même si les points de distribution ne sont pas indispensables à l’installation du client sur les ordinateurs Mac, vous devez en configurer pour permettre au client de se connecter depuis Internet si vous prévoyez de déployer des logiciels sur ces ordinateurs Mac après avoir installé le client Configuration Manager.  

 Cette procédure permet de configurer les points de gestion et les points de distribution existants pour prendre en charge les ordinateurs Mac. Avant d'entamer cette procédure, assurez-vous que le serveur de système de site exécutant le point de gestion et le point de distribution est configuré avec un nom de domaine Internet complet. Si ces serveurs de système de site ne prennent pas en charge la gestion des clients basée sur Internet, vous pouvez spécifier le nom de domaine complet intranet pour la valeur de nom de domaine complet Internet. De plus, vérifiez que ces rôles de système de site se trouvent dans un site principal.  

##### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Pour configurer les points de gestion et les points de distribution pour prendre en charge les ordinateurs Mac  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, sélectionnez **Serveurs et rôles de système de site**, puis sélectionnez le serveur contenant les rôles de système de site à configurer.  

3.  Dans le volet des détails, cliquez avec le bouton droit sur **Point de gestion**, cliquez sur **Propriétés du rôle**, et dans la boîte de dialogue **Propriétés du point de gestion** , configurez les options suivantes, puis cliquez sur **OK**:  

    1.  Sélectionnez **HTTPS**.  

    2.  Sélectionnez **Autoriser les connexions client Internet uniquement** ou **Autoriser les connexions client Intranet et Internet**. Ces options nécessitent qu'un nom de domaine complet Internet soit spécifié dans les propriétés de système de site, même si le serveur de système de site n'est pas accessible sur Internet.  

    3.  Sélectionnez **Autoriser les appareils mobiles et les ordinateurs Mac à utiliser ce point de gestion**.  

4.  Dans le volet des détails, cliquez avec le bouton droit sur **Point de distribution**, cliquez sur **Propriétés du rôle**, et dans la boîte de dialogue **Propriétés du point de distribution** , configurez les options suivantes, puis cliquez sur **OK**:  

    -   Sélectionnez **HTTPS**.  

    -   Sélectionnez **Autoriser les connexions client Internet uniquement** ou **Autoriser les connexions client Intranet et Internet**. Ces options nécessitent qu'un nom de domaine complet Internet soit spécifié dans les propriétés de système de site, même si le serveur de système de site n'est pas accessible sur Internet.  

    -   Cliquez sur **Importer un certificat**, accédez au fichier du certificat de point de distribution client exporté, puis spécifiez le mot de passe.  

5.  Répétez les étapes 2 à 4 de cette procédure pour tous les points de gestion et les points de distribution des sites principaux que vous prévoyez d'utiliser avec des ordinateurs Mac.  

### <a name="step-5-configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Étape 5 : Configurer le point proxy d’inscription et le point d’inscription  
 Vous devez installer ces deux rôles de système de site sur le même site, mais il n'est pas nécessaire de les installer sur le même serveur de système de site ni sur la même forêt Active Directory.  

 Pour plus d’informations sur la sélection élective des rôles de système de site et sur les éléments à prendre en considération, consultez [Rôles de système de site](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) dans [Planifier des serveurs de système de site et des rôles système de site pour System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Ces procédures permettent de configurer les rôles de système de site pour prendre en charge les ordinateurs Mac. Utilisez l'une des procédures suivantes, selon que vous souhaitez installer un nouveau serveur de système de site pour prendre en charge les ordinateurs Mac ou utiliser un serveur de système de site existant :  

-   [Pour installer et configurer les systèmes de site d’inscription : nouveau serveur de système de site](#BKMK_HowtoInstallEnrollmentSiteSystems_new)  

-   [Pour installer et configurer les systèmes de site d’inscription : serveur de système de site existant](#BKMK_HowtoInstallEnrollmentSiteSystems_existing)  

####  <a name="a-namebkmkhowtoinstallenrollmentsitesystemsnewa-to-install-and-configure-the-enrollment-site-systems-new-site-system-server"></a><a name="BKMK_HowtoInstallEnrollmentSiteSystems_new"></a> Pour installer et configurer les systèmes de site d’inscription : nouveau serveur de système de site  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Serveurs et rôles de système de site**.  

3.  Sur l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un serveur de système de site**.  

4.  Sur la page **Général** , spécifiez les paramètres généraux du système de site, puis cliquez sur **Suivant**.  

    > [!IMPORTANT]  
    >  Assurez-vous que vous spécifiez une valeur pour le nom de domaine complet Internet, même si le serveur de système de site n'est pas accessible sur Internet. Si vous n'avez pas de nom de domaine complet Internet car le serveur de système de site ne sera pas accessible sur Internet, vous pouvez spécifier la valeur de nom de domaine complet intranet comme nom de domaine complet Internet. Les ordinateurs Mac se connectent toujours au nom de domaine Internet complet, même lorsqu'ils se trouvent sur l'intranet.  

5.  Sur la page **Sélection du rôle système** , sélectionnez **Point proxy d'inscription** et **Point d'inscription** dans la liste des rôles disponibles, puis cliquez sur **Suivant**.  

6.  Sur la page **Point proxy d'inscription** , vérifiez les paramètres et apportez les modifications requises, puis cliquez sur **Suivant**.  

7.  Sur la page **Paramètres du point d'inscription** , vérifiez les paramètres et apportez les modifications requises, puis cliquez sur **Suivant**.  

8.  Effectuez toutes les étapes de l'Assistant.  

####  <a name="a-namebkmkhowtoinstallenrollmentsitesystemsexistinga-to-install-and-configure-the-enrollment-site-systems-existing-site-system-server"></a><a name="BKMK_HowtoInstallEnrollmentSiteSystems_existing"></a> Pour installer et configurer les systèmes de site d’inscription : serveur de système de site existant  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, sélectionnez **Serveurs et rôles de système de site**, puis sélectionnez le serveur à utiliser pour prendre en charge les ordinateurs Mac.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Ajouter des rôles de système de site**.  

4.  Sur la page **Général** , spécifiez les paramètres généraux du système de site, puis cliquez sur **Suivant**.  

    > [!IMPORTANT]  
    >  Assurez-vous que vous spécifiez une valeur pour le nom de domaine complet Internet, même si le serveur de système de site n'est pas accessible sur Internet. Si vous n'avez pas de nom de domaine complet Internet car le serveur de système de site ne sera pas accessible sur Internet, vous pouvez spécifier la valeur de nom de domaine complet intranet comme nom de domaine complet Internet. Les ordinateurs Mac se connectent toujours au nom de domaine Internet complet, même lorsqu'ils se trouvent sur l'intranet.  

5.  Sur la page **Sélection du rôle système** , sélectionnez **Point proxy d'inscription** et **Point d'inscription** dans la liste des rôles disponibles, puis cliquez sur **Suivant**.  

6.  Sur la page **Point proxy d'inscription** , vérifiez les paramètres et apportez les modifications requises, puis cliquez sur **Suivant**.  

7.  Sur la page **Paramètres du point d'inscription** , vérifiez les paramètres et apportez les modifications requises, puis cliquez sur **Suivant**.  

8.  Effectuez toutes les étapes de l'Assistant.  

### <a name="step-6-optional-install-the-reporting-services-point"></a>Étape 6 : Facultatif : Installer le point de Reporting Services  
 Installez le point de Reporting Services si vous souhaitez exécuter des rapports pour les ordinateurs Mac.  

 Pour plus d’informations sur l’installation et la configuration du point Reporting Services, consultez [Configuration des rapports dans System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).  

### <a name="step-7-configure-client-settings-for-enrollment"></a>Étape 7 : Configurer les paramètres client pour l’inscription  
 Vous devez utiliser les paramètres client par défaut pour configurer l'inscription pour les ordinateurs Mac ; vous ne pouvez pas utiliser de paramètres client personnalisés.  

 Pour plus d'informations sur les paramètres client, voir [À propos des paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

 Cette étape est nécessaire pour permettre à Configuration Manager de demander et installer le certificat sur l’ordinateur Mac.  

##### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Pour configurer les paramètres client par défaut pour permettre à Configuration Manager d’inscrire des certificats pour les ordinateurs Mac  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**.  

3.  Cliquez sur **Paramètres client par défaut**.  

    > [!IMPORTANT]  
    >  Vous ne pouvez pas utiliser un paramètre client personnalisé pour la configuration de l'inscription ; vous devez utiliser les paramètres client par défaut.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Sélectionnez la section **Inscription** , puis configurez les paramètres utilisateur suivants :  

    1.  **Autoriser les utilisateurs à inscrire des appareils mobiles et des ordinateurs Mac : Oui**  

    2.  **Profil d’inscription** : cliquez sur **Définir un profil**.  

6.  Dans la boîte de dialogue **Profil d'inscription d'appareil mobile** , cliquez sur **Créer**.  

7.  Dans la boîte de dialogue **Créer un profil d'inscription** , entrez un nom pour ce profil d'inscription, puis configurez le **Code du site de gestion**. Sélectionnez le site principal Configuration Manager contenant les points de gestion qui géreront les ordinateurs Mac.  

    > [!NOTE]  
    >  Si vous ne pouvez pas sélectionner le site, vérifiez qu'au moins un point de gestion dans le site est configuré pour la prise en charge des appareils mobiles.  

8.  Cliquez sur **Ajouter**.  

9. Dans la boîte de dialogue **Ajouter une autorité de certification pour les appareils mobiles** , sélectionnez le serveur de l'autorité de certification émettrice des certificats pour les ordinateurs Mac, puis cliquez sur **OK**.  

10. Dans la boîte de dialogue **Créer un profil d'inscription** , sélectionnez le modèle de certificat d'ordinateur Mac que vous avez créé à l'étape 3, puis cliquez sur **OK**.  

11. Cliquez sur **OK** pour fermer la boîte de dialogue **Profil d'inscription** , puis cliquez sur **OK** pour fermer la boîte de dialogue **Paramètres client par défaut** .  

    > [!TIP]  
    >  Si vous voulez modifier l'intervalle de la stratégie client, utilisez le paramètre client **Intervalle d'interrogation de stratégie client** dans le groupe de paramètres client **Stratégie client** .  

 Tous les utilisateurs seront configurés avec ces paramètres lors de leur prochain téléchargement de la stratégie client. Pour lancer la récupération de stratégie pour un seul client, consultez [Lancer une récupération de stratégie pour un client Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Outre les paramètres client d’inscription, assurez-vous d’avoir configuré les paramètres d’appareil client Configuration Manager suivants :  

-   **Inventaire matériel**: activez et configurez ce paramètre client si vous souhaitez collecter l’inventaire matériel des ordinateurs clients Mac et Windows. Pour plus d’informations, consultez [Comment étendre l’inventaire matériel dans System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

-   **Paramètres de compatibilité**: activez et configurez ce paramètre client si vous souhaitez évaluer et corriger les paramètres sur les ordinateurs clients Mac et Windows. Pour plus d’informations, consultez [Planifier et configurer les paramètres de compatibilité](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

> [!NOTE]  
>  Pour plus d’informations sur les paramètres client Configuration Manager, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

### <a name="step-8-download-the-client-source-files-for-macs"></a>Étape 8 : Télécharger les fichiers sources du client pour les ordinateurs Mac  
 Vous devez télécharger et installer les programmes suivants pour pouvoir installer et gérer le client Configuration Manager sur les ordinateurs Mac :  

-   **Ccmsetup** : cette application permet d’installer le client Configuration Manager sur les ordinateurs Mac de votre organisation.  

-   **CMDiagnostics** : cet outil permet de collecter les informations de diagnostic relatives au client Configuration Manager sur les ordinateurs Mac de votre organisation.  

-   **CMUninstall** : cet outil permet de désinstaller le client Configuration Manager sur les ordinateurs Mac de votre organisation.  

-   **CMAppUtil** : cet outil permet de convertir les packages d’applications Apple dans un format qui peut être déployé sous forme d’application Configuration Manager.  

-   **CMEnroll** : cet outil permet de demander et d’installer le certificat client d’un ordinateur Mac en vue d’installer le client Configuration Manager.  

> [!IMPORTANT]  
>  Quand vous installez un nouveau client pour les ordinateurs Mac, vous devez peut-être également installer des mises à jour Configuration Manager pour refléter les nouvelles informations client dans la console Configuration Manager.  

##### <a name="to-download-and-install-the-mac-os-x-client-files"></a>Pour télécharger et installer les fichiers du client Mac OS X  

1.  Téléchargez le package de fichiers du client Mac OS X, **ConfigmgrMacClient.msi**, et enregistrez-le sur un ordinateur exécutant Windows.  

     Ce fichier n’est pas fourni dans le support d’installation de Configuration Manager. Vous pouvez télécharger ce fichier à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  Sur l'ordinateur Windows, exécutez le fichier **ConfigmgrMacClient.msi** que vous venez de télécharger pour extraire le package du client Mac (Macclient.dmg) dans un dossier du disque local (par défaut, **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copiez le fichier Macclient.dmg dans un dossier de l'ordinateur Mac.  

4.  Sur l'ordinateur Mac, exécutez le fichier Macclient.dmg que vous venez de télécharger pour extraire les fichiers dans un dossier du disque local.  

5.  Dans ce dossier, assurez-vous que les fichiers Ccmsetup et CMClient.pkg ont été extraits, qu'un dossier nommé Outils a été créé et qu'il contient les outils CMDiagnostics, CMUninstall, CMAppUtil et CMEnroll.  

### <a name="step-9-install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Étape 9 : Installer le client, puis inscrire le certificat client sur l’ordinateur Mac  
 Cette procédure installe le client et utilise l’outil CMEnroll pour demander et installer le certificat client pour un ordinateur Mac afin que vous puissiez gérer cet ordinateur à l’aide de Configuration Manager.  

 Vous pouvez inscrire le client à l'aide de l'Assistant Inscription d'ordinateur Mac sans avoir à utiliser l'outil CMEnroll. Pour plus d'informations, reportez-vous à la procédure ci-dessous.  

##### <a name="to-install-the-client-and-enroll-the-certificate-by-using-the-cmenroll-tool"></a>Pour installer le client et inscrire le certificat à l'aide de l'outil CMEnroll  

1.  Sur l'ordinateur Mac, accédez au dossier dans lequel vous avez extrait le contenu du fichier Macclient.dmg téléchargé à partir du Centre de téléchargement Microsoft.  

2.  Entrez la ligne de commande suivante : **sudo ./ccmsetup**  

3.  Patientez jusqu'à ce que le message **Installation terminée** s'affiche à l'écran. Même si le programme d'installation affiche un message vous demandant de redémarrer maintenant, ne suivez pas cette instruction et passez à l'étape suivante.  

4.  Dans le dossier Outils sur l’ordinateur Mac, tapez la commande suivante : **sudo ./CMEnroll -s &lt;nom_serveur_proxy_inscription> -ignorecertchainvalidation -u &lt;nom_utilisateur>**  

    > [!NOTE]  
    >  Une fois le client installé, l’Assistant Inscription d’ordinateur Mac s’ouvre pour vous aider à inscrire l’ordinateur Mac. Pour inscrire le client par cette méthode, consultez [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) dans cette rubrique.  

     Vous êtes ensuite invité à taper le mot de passe du compte d'utilisateur Active Directory.  

    > [!IMPORTANT]  
    >  Lorsque vous entrez cette commande, vous êtes invité à entrer deux mots de passe : la première invite est pour le compte de superutilisateur qui exécute la commande. La seconde invite est pour le compte d'utilisateur Active Directory. Les invites semblent identiques, assurez-vous que vous les spécifiez dans le bon ordre.  

     Le nom d'utilisateur peut se présenter sous l'une des formes suivantes :  

    -   « domaine\nom ». Par exemple: « contoso\mnorth »  

    -   'user@domain'. Exemple : 'mnorth@contoso.com'  

     Le nom d'utilisateur et le mot de passe correspondant doivent correspondre à un compte d'utilisateur Active Directory disposant des autorisations de lecture et d'inscription dans le modèle de certificat client Mac.  

     Exemple : si le serveur de point proxy d’inscription se nomme **server02.contoso.com** et que des autorisations ont été accordées au nom d’utilisateur **contoso\mnorth** pour le modèle de certificat client Mac, tapez la ligne suivante : **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u ’contoso\mnorth’**  

    > [!IMPORTANT]  
    >  Si le nom d’utilisateur contient l’un des caractères **&lt;>"+=,**, l’inscription échoue.  
    >   
    >  Pour résoudre ce problème, obtenez un certificat hors bande avec un nom d'utilisateur qui ne contient pas ces caractères.  

    > [!NOTE]  
    >  Pour une expérience utilisateur plus transparente, vous pouvez mettre les étapes d'installation et les commandes sous forme de script afin que les utilisateurs n'aient qu'à fournir leurs nom d'utilisateur et mot de passe.  

5.  Patientez jusqu'à l'affichage d'un message indiquant que l' **inscription s'est déroulée correctement** .  

6.  Pour limiter le certificat inscrit à Configuration Manager, sur l’ordinateur Mac, ouvrez une fenêtre de terminal et apportez les modifications suivantes :  

    1.  Entrez la commande **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    2.  Dans la boîte de dialogue **Trousseau d'accès** , dans la zone **Trousseau** , cliquez sur **Système**, puis dans la zone **Catégorie** , cliquez sur **Clés**.  

    3.  Développez les clés pour afficher les certificats clients. Lorsque vous avez identifié le certificat avec une clé privée que vous venez d'installer, double-cliquez sur la clé.  

    4.  Dans l'onglet **Contrôle d'accès** , sélectionnez **Confirmer avant d'autoriser l'accès**.  

    5.  Accédez à **/Library/Application Support/Microsoft/CCM**, sélectionnez **CCMClient**, puis cliquez sur **Ajouter**.  

    6.  Cliquez sur **Enregistrer les modifications** , puis fermez la boîte de dialogue **Trousseau d'accès** .  

7.  Redémarrez l'ordinateur Mac.  

 Vérifiez que l'installation du client a abouti en ouvrant l'élément **Configuration Manager** dans les **Préférences Système** de l'ordinateur Mac. Vous pouvez également mettre à jour et afficher le regroupement **Tous les systèmes** pour vérifier que l'ordinateur Mac figure désormais dans ce regroupement en tant que client géré.  

> [!TIP]  
>  Pour vous aider à résoudre les problèmes liés au client Mac, vous pouvez utiliser le programme CMDiagnostics inclus avec le package client Mac OS X afin de recueillir les informations suivantes :  
>   
>  -   Liste des processus en cours.  
> -   Version du système d'exploitation Mac OS X.  
> -   Rapports des défaillances du système Mac OS X liées au client Configuration Manager, y compris les fichiers **CCM\*.crash** et **System Preference.crash**.  
> -   Le fichier de nomenclature et le fichier de liste des propriétés (.plist) créés par l’installation du client Configuration Manager.  
> -   Le contenu du dossier /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  Les informations recueillies par le programme CmDiagnostics sont ajoutées à un fichier zip enregistré sur le bureau de l’ordinateur et nommé cmdiag-*<nom_hôte\>***-***<date_et_heure\>*.zip.  

####  <a name="a-namebkmkenrollr2a-to-enroll-the-client-by-using-the-mac-computer-enrollment-wizard"></a><a name="BKMK_EnrollR2"></a> Pour inscrire le client à l’aide de l’Assistant Inscription d’ordinateur Mac  

1.  Lorsque vous avez terminé l'installation du client, l'Assistant Inscription d'ordinateur s'ouvre. Cliquez sur **Suivant** pour passer la page d'accueil.  

    > [!NOTE]  
    >  Si l'Assistant ne s'ouvre pas ou si vous fermez l'Assistant par inadvertance, cliquez sur **Inscription** sur la page des préférences **Configuration Manager** pour ouvrir l'Assistant.  

2.  Sur la page suivante de l'Assistant, spécifiez les informations suivantes :  

    -   **Nom d'utilisateur** : le nom d'utilisateur peut se présenter sous l'une des formes suivantes :  

        -   « domaine\nom ». Par exemple: « contoso\mnorth »  

        -   'user@domain'. Exemple : 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  Lorsque vous utilisez une adresse électronique pour renseigner le champ **Nom d’utilisateur**, Configuration Manager utilise automatiquement le nom de domaine de l’adresse électronique et le nom par défaut du serveur de point proxy d’inscription pour renseigner le champ **Nom du serveur**. Si ce nom de domaine et ce nom de serveur ne correspondent pas au nom du serveur de point proxy d'inscription, vous devez informer vos utilisateurs du nom correct à utiliser pour qu'ils puissent l'entrer lors de l'inscription de leurs ordinateurs Mac.  

         Le nom d'utilisateur et le mot de passe correspondant doivent correspondre à un compte d'utilisateur Active Directory disposant des autorisations de lecture et d'inscription dans le modèle de certificat client Mac.  

    -   **Mot de passe** : entrez un mot de passe correspondant au nom d’utilisateur spécifié.  

    -   **Nom du serveur** : entrez le nom du serveur de point proxy d’inscription.  

3.  Cliquez sur **Suivant** pour continuer, puis terminez l'Assistant.  

##  <a name="a-nameuninstallmacclienta-uninstalling-the-mac-client"></a><a name="uninstallMacClient"></a> Désinstallation du client Mac  
 Si vous souhaitez désinstaller le client Mac, utilisez le script CMUninstall fourni avec les fichiers du client Mac que vous avez téléchargés à partir du site Web. Pour désinstaller le client Configuration Manager des ordinateurs Mac, aidez-vous des informations figurant dans la procédure suivante.  

#### <a name="to-uninstall-the-mac-client"></a>Pour désinstaller le client Mac  

1.  Sur un ordinateur Mac, ouvrez une fenêtre de terminal et accédez au dossier dans lequel vous avez extrait le contenu du fichier macclient.dmg, téléchargé depuis le Centre de téléchargement Microsoft.  

2.  Accédez au dossier Outils, puis entrez la ligne de commande suivante :  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  La propriété **c** demande au programme de désinstallation du client de supprimer aussi les fichiers journaux d’incident et ceux du client. Cette étape est facultative, mais constitue une pratique recommandée pour éviter toute confusion si vous réinstallez le client ultérieurement.  

3.  Si nécessaire, supprimez manuellement le certificat d’authentification de client que Configuration Manager utilisait, ou révoquez-le. CMUnistall ne supprime et ne révoque pas ce certificat.  

##  <a name="a-namebkmkrenewa-renewing-the-mac-client-certificate"></a><a name="BKMK_Renew"></a> Renouvellement du certificat client Mac  
 Pour renouveler le certificat client Mac, utilisez une des méthodes suivantes :  

-   [Renewing the Mac client certificate by using the Renew Certificate Wizard](#BKMK_UI)  

-   [Renewing the Mac client certificate manually](#BKMK_Man)  

###  <a name="a-namebkmkuia-renewing-the-mac-client-certificate-by-using-the-renew-certificate-wizard"></a><a name="BKMK_UI"></a> Renouvellement du certificat client Mac à l’aide de l’Assistant Renouveler le certificat  
 Utilisez la procédure suivante pour configurer et utiliser l’Assistant Renouveler le certificat dans Configuration Manager.  

##### <a name="to-renew-the-mac-client-certificate-by-using-the-renew-certificate-wizard"></a>Pour renouveler le certificat client Mac à l'aide de l'Assistant Renouveler le certificat  

1.  Configurez les valeurs suivantes dans le fichier ccmclient.plist ; elles contrôlent le moment où l'Assistant Renouveler le certificat s'ouvre :  

    > [!IMPORTANT]  
    >  Vous devez configurer ces valeurs sous forme de chaînes. Si vous configurez les valeurs en tant que nombres entiers (à l’aide de la propriété **-int** ), elles ne seront pas lues.  

    -   **RenewalPeriod1** : spécifie, en secondes, la première période de renouvellement pendant laquelle les utilisateurs peuvent renouveler le certificat. La valeur par défaut correspond à 3 888 000 secondes (45 jours).  

        > [!NOTE]  
        >  Si **RenewalPeriod1** est configurée sur une valeur supérieure ou égale à 300 secondes, la valeur configurée sera utilisée.  Si la valeur configurée est supérieure à 0 et inférieur à 300 secondes, la valeur par défaut de 45 jours sera utilisée.  

    -   **RenewalPeriod2** : spécifie, en secondes, la deuxième période de renouvellement pendant laquelle les utilisateurs peuvent renouveler le certificat. La valeur par défaut correspond à 259 200 secondes (3 jours).  

        > [!NOTE]  
        >  Si **RenewalPeriod2** est configuré sur une valeur supérieure ou égale à 300 secondes et inférieure ou égale à **RenewalPeriod1**, la valeur configurée sera utilisée. Si **RenewalPeriod1** est supérieure à 3 jours, une valeur de 3 jours sera utilisée pour **RenewalPeriod2**.  Si **RenewalPeriod1** est inférieure à 3 jours, **RenewalPeriod2** est définie sur la même valeur que **RenewalPeriod1**.  

    -   **RenewalReminderInterval1** : spécifie, en secondes, la fréquence à laquelle l’Assistant Renouveler le certificat sera affiché pour les utilisateurs lors de la première période de renouvellement. La valeur par défaut correspond à 86 400 secondes (1 jour).  

        > [!NOTE]  
        >  Si **RenewalReminderInterval1** est supérieur à 300 secondes et inférieur à la valeur configurée pour **RenewalPeriod1**, la valeur configurée sera utilisée. Dans le cas contraire, la valeur par défaut de 1 jour sera utilisée.  

    -   **RenewalReminderInterval2** : spécifie, en secondes, la fréquence à laquelle l’Assistant Renouveler le certificat sera affiché pour les utilisateurs lors de la deuxième période de renouvellement. La valeur par défaut correspond à 28 800 secondes (8 heures).  

        > [!NOTE]  
        >  Si **RenewalReminderInterval2** est supérieure à 300 secondes, inférieure ou égale à **RenewalReminderInterval1** et inférieure ou égale à **RenewalPeriod2**, la valeur configurée sera utilisée. Sinon, une valeur de 8 heures sera utilisée.  

     **Exemple** : si les valeurs sont laissées sur leurs valeurs par défaut, 45 jours avant l’expiration du certificat, l’Assistant s’ouvre toutes les 24 heures.  Dans les 3 jours de la date d'expiration du certificat, l'Assistant s'ouvre toutes les 8 heures.  

     **Exemple** : utilisez la ligne de commande suivante, ou un script, pour définir la première période de renouvellement sur 20 jours.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  Lorsque l'Assistant Renouveler le certificat s'ouvre, les champs **Nom d'utilisateur** et **Nom du serveur** sont en général déjà remplis et l'utilisateur ne doit entrer qu'un mot de passe pour renouveler le certificat.  

    > [!NOTE]  
    >  Si l'Assistant ne s'ouvre pas ou si vous fermez l'Assistant par inadvertance, cliquez sur **Renouveler** sur la page des préférences **Configuration Manager** pour ouvrir l'Assistant.  

###  <a name="a-namebkmkmana-renewing-the-mac-client-certificate-manually"></a><a name="BKMK_Man"></a> Renouvellement manuel du certificat client Mac  
 La période de validité classique pour le certificat client Mac est de 1 an. Configuration Manager ne renouvelle pas automatiquement le certificat utilisateur demandé à l’inscription ; vous devez donc procéder comme suit pour renouveler manuellement le certificat.  

> [!IMPORTANT]  
>  Si le certificat a expiré, vous devez désinstaller, réinstaller et réinscrire le client Mac.  

 Cette procédure supprime l'ID SMS, qui est requis pour demander un nouveau certificat pour le même ordinateur Mac. Une fois le nouveau certificat demandé, il est utilisé automatiquement par Configuration Manager.  

> [!IMPORTANT]  
>  Lorsque vous supprimez et remplacez l’ID SMS client, tout historique client stocké, tel que l’inventaire, est supprimé après la suppression du client de la console Configuration Manager.  

##### <a name="to-renew-the-mac-client-certificate-manually"></a>Pour renouveler manuellement le certificat client Mac  

1.  Créez un regroupement de périphériques pour les ordinateurs Mac qui doivent renouveler les certificats utilisateur, puis ajoutez les ordinateurs Mac au regroupement.  

    > [!WARNING]  
    >  Configuration Manager ne surveille pas la période de validité du certificat qu’il inscrit pour les ordinateurs Mac. Vous devez surveiller cette validité indépendamment de Configuration Manager pour identifier les ordinateurs Mac à ajouter à ce regroupement.  

2.  Dans l'espace de travail **Ressources et compatibilité** , démarrez l' **Assistant Création d'élément de configuration**.  

3.  Sur la page **Général** de l'Assistant, spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Type :Mac OS X**  

4.  Sur la page **Plateformes prises en charge** de l'Assistant, assurez-vous que toutes les versions de Mac OS X sont sélectionnées.  

5.  Sur la page **Paramètres** de l'Assistant, cliquez sur **Nouveau** , puis dans la boîte de dialogue **Créer un paramètre** , spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Type de paramètre :Script**  

    -   **Type de données :Chaîne**  

6.  Dans la boîte de dialogue **Créer un paramètre** , sous **Script de découverte**, cliquez sur **Ajouter un script** pour définir un script de découverte des ordinateurs Mac configurés avec un ID SMS.  

7.  Dans la boîte de dialogue **Modifier un script de découverte** , entrez le script Shell suivant :  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Cliquez sur **OK** pour fermer la boîte de dialogue **Modifier un script de découverte** .  

9. Dans la boîte de dialogue **Créer un paramètre** , sous **Script de correction (facultatif)**, cliquez sur **Ajouter un script** pour définir un script de suppression de l'ID SMS détecté sur les ordinateurs Mac.  

10. Dans la boîte de dialogue **Créer un script de correction** , entrez le script Shell suivant :  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Cliquez sur **OK** pour fermer la boîte de dialogue **Créer un script de correction** .  

12. Sur la page **Règles de compatibilité** de l'Assistant, cliquez sur **Nouveau**, puis dans la boîte de dialogue **Créer une règle** , spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Paramètre sélectionné** : cliquez sur **Parcourir** , puis sélectionnez le script de découverte que vous avez spécifié précédemment.  

    -   Dans **les valeurs suivantes** , entrez **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Activez l'option **Exécuter le script de correction spécifié lorsque ce paramètre n'est pas compatible**.  

13. Effectuez toutes les étapes de l'Assistant Création d'élément de configuration.  

14. Créez une ligne de base de configuration contenant l'élément de configuration que vous venez de créer et déployez-la sur le regroupement de périphériques créé à l'étape 1.  

     Pour plus d’informations sur la création et le déploiement de lignes de base de configuration, consultez [Comment créer des bases de référence de configuration dans System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) et [Comment déployer des lignes de base de configuration dans System Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. Sur les ordinateurs Mac sur lesquels l'ID SMS a été supprimé, exécutez la commande suivante pour installer un nouveau certificat :  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Lorsque vous y êtes invité, fournissez le mot de passe du compte de superutilisateur qui exécute la commande, puis le mot de passe du compte d'utilisateur Active Directory.  

16. Pour limiter le certificat inscrit à Configuration Manager, sur l’ordinateur Mac, ouvrez une fenêtre de terminal et apportez les modifications suivantes :  

    1.  Entrez la commande **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    2.  Dans la boîte de dialogue **Trousseau d'accès** , dans la zone **Trousseau** , cliquez sur **Système**, puis dans la zone **Catégorie** , cliquez sur **Clés**.  

    3.  Développez les clés pour afficher les certificats clients. Lorsque vous avez identifié le certificat avec une clé privée que vous venez d'installer, double-cliquez sur la clé.  

    4.  Dans l'onglet **Contrôle d'accès** , sélectionnez **Confirmer avant d'autoriser l'accès**.  

    5.  Accédez à **/Library/Application Support/Microsoft/CCM**, sélectionnez **CCMClient**, puis cliquez sur **Ajouter**.  

    6.  Cliquez sur **Enregistrer les modifications** , puis fermez la boîte de dialogue **Trousseau d'accès** .  

17. Redémarrez l'ordinateur Mac.  

##  <a name="a-namebkmkmanualcertifcateinstallationa-use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a><a name="BKMK_ManualCertifcateInstallation"></a> Utiliser une demande de certificat et une méthode d’installation indépendantes de Configuration Manager  
 Si vous n’utilisez pas l’inscription Configuration Manager, mais que vous demandez et installez le certificat client indépendamment de Configuration Manager, les étapes de configuration sont légèrement différentes :  

1.  Effectuez les étapes 1, 2, 4, 6 (facultative) et 8.  

2.  N'effectuez pas les étapes 3, 5, 7 et 9.  

3.  Installez le client à l'aide des instructions suivantes.  

#### <a name="to-install-the-client-certificate-independently-from-configuration-manager-and-install-the-client"></a>Pour installer le certificat client indépendamment de Configuration Manager et installer le client  

1.  Pour installer le certificat client indépendamment de Configuration Manager, utilisez les instructions qui accompagnent la méthode de déploiement de certificat choisie pour demander et installer le certificat client sur l’ordinateur Mac.  

2.  Accédez au dossier dans lequel vous avez extrait le contenu du fichier macclient.dmg, téléchargé depuis le Centre de téléchargement Microsoft.  

3.  Entrez la ligne de commande suivante : **sudo ./ccmsetup -MP <nom_de_domaine_complet_Internet_du_point_de_gestion\> -SubjectName <valeur_objet_certificat\>**  

    > [!IMPORTANT]  
    >  La valeur de l'objet Certificat est sensible à la casse, vous devez l'entrer exactement telle qu'elle apparaît dans les détails du certificat.  

     Exemple : si le nom de domaine complet Internet dans les propriétés du système de site est **server03.contoso.com** et que le certificat client Mac porte le nom de domaine complet **mac12.contoso.com** comme nom commun dans l’objet certificat, tapez : **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  Patientez jusqu'à l'affichage du message d' **installation terminée** , puis redémarrez l'ordinateur Mac.  

5.  Pour vous assurer que Configuration Manager peut accéder à ce certificat, sur l’ordinateur Mac, ouvrez une fenêtre de terminal et apportez les modifications suivantes :  

    1.  Entrez la commande **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    2.  Dans la boîte de dialogue **Trousseau d'accès** , dans la zone **Trousseau** , cliquez sur **Système**, puis dans la zone **Catégorie** , cliquez sur **Clés**.  

    3.  Développez les clés pour afficher les certificats clients. Lorsque vous avez identifié le certificat avec une clé privée que vous venez d'installer, double-cliquez sur la clé.  

    4.  Dans l'onglet **Contrôle d'accès** , sélectionnez **Confirmer avant d'autoriser l'accès**.  

    5.  Accédez à **/Library/Application Support/Microsoft/CCM**, sélectionnez **CCMClient**, puis cliquez sur **Ajouter**.  

    6.  Cliquez sur **Enregistrer les modifications** , puis fermez la boîte de dialogue **Trousseau d'accès** .  

6.  Si vous disposez de plusieurs certificats qui contiennent la même valeur d’objet, vous devez spécifier le numéro de série du certificat pour identifier le certificat que vous voulez utiliser pour le client Configuration Manager. Pour ce faire, utilisez la commande suivante : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<numéro_série\>"**.  

     Exemple : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Vérifiez que l'installation du client a abouti en ouvrant l'élément **Configuration Manager** dans les **Préférences Système** de l'ordinateur Mac. Vous pouvez également mettre à jour et afficher le regroupement **Tous les systèmes** pour vérifier que l'ordinateur Mac figure désormais dans ce regroupement en tant que client géré.  

### <a name="renewing-the-mac-client-certificate"></a>Renouvellement du certificat client Mac  
 Utilisez la procédure suivante avant de renouveler le certificat d'ordinateur sur les ordinateurs Mac.  

 Cette procédure supprime l'ID SMS qui est requis par le client pour utiliser un certificat nouveau ou renouvelé sur l'ordinateur Mac.  

> [!IMPORTANT]  
>  Lorsque vous supprimez et remplacez l’ID SMS client, tout historique client stocké, tel que l’inventaire, est supprimé après la suppression du client de la console Configuration Manager.  

##### <a name="to-renew-the-mac-client-certificate"></a>Pour renouveler le certificat client Mac  

1.  Créez un regroupement de périphériques pour les ordinateurs Mac qui doivent renouveler les certificats d'ordinateur, puis ajoutez les ordinateurs Mac au regroupement.  

2.  Dans l'espace de travail **Ressources et compatibilité** , démarrez l' **Assistant Création d'élément de configuration**.  

3.  Sur la page **Général** de l'Assistant, spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Type :Mac OS X**  

4.  Sur la page **Plateformes prises en charge** de l'Assistant, assurez-vous que toutes les versions de Mac OS X sont sélectionnées.  

5.  Sur la page **Paramètres** de l'Assistant, cliquez sur **Nouveau** , puis dans la boîte de dialogue **Créer un paramètre** , spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Type de paramètre :Script**  

    -   **Type de données :Chaîne**  

6.  Dans la boîte de dialogue **Créer un paramètre** , sous **Script de découverte**, cliquez sur **Ajouter un script** pour définir un script de découverte des ordinateurs Mac configurés avec un ID SMS.  

7.  Dans la boîte de dialogue **Modifier un script de découverte** , entrez le script Shell suivant :  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Cliquez sur **OK** pour fermer la boîte de dialogue **Modifier un script de découverte** .  

9. Dans la boîte de dialogue **Créer un paramètre** , sous **Script de correction (facultatif)**, cliquez sur **Ajouter un script** pour définir un script de suppression de l'ID SMS détecté sur les ordinateurs Mac.  

10. Dans la boîte de dialogue **Créer un script de correction** , entrez le script Shell suivant :  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Cliquez sur **OK** pour fermer la boîte de dialogue **Créer un script de correction** .  

12. Sur la page **Règles de compatibilité** de l'Assistant, cliquez sur **Nouveau**, puis dans la boîte de dialogue **Créer une règle** , spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Paramètre sélectionné** : cliquez sur **Parcourir** , puis sélectionnez le script de découverte que vous avez spécifié précédemment.  

    -   Dans **les valeurs suivantes** , entrez **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Activez l'option **Exécuter le script de correction spécifié lorsque ce paramètre n'est pas compatible**.  

13. Effectuez toutes les étapes de l'Assistant Création d'élément de configuration.  

14. Créez une ligne de base de configuration contenant l'élément de configuration que vous venez de créer et déployez-la sur le regroupement de périphériques créé à l'étape 1.  

     Pour plus d’informations sur la création et le déploiement de bases de référence de configuration, consultez [Comment créer des bases de référence de configuration dans System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Après avoir installé un nouveau certificat sur les ordinateurs Mac sur lesquels l'ID SMS a été supprimé, exécutez la commande suivante pour configurer le client de sorte à utiliser le nouveau certificat :  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. Si vous disposez de plusieurs certificats qui contiennent la même valeur d’objet, vous devez spécifier le numéro de série du certificat pour identifier le certificat que vous voulez utiliser pour le client Configuration Manager. Pour ce faire, utilisez la commande suivante : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<numéro_série\>"**.  

     Exemple : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Redémarrez l'ordinateur Mac.  



<!--HONumber=Nov16_HO1-->


