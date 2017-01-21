---
title: "Déployer des clients Mac | Microsoft Docs"
description: "Découvrez comment déployer des clients sur des ordinateurs Mac dans System Center Configuration Manager."
ms.custom: na
ms.date: 11/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 66071227fd10a43f7cd4e64508494d485392ffcd
ms.openlocfilehash: 6cbddd623767522a0026e0736b1f647fddbecfb6


---
# <a name="how-to-deploy-clients-to-macs-in-system-center-configuration-manager"></a>Comment déployer des clients sur des Mac dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique décrit comment installer le client Configuration Manager sur des ordinateurs Mac.

## <a name="prerequisites-and-preparatory-steps"></a>Prérequis et étapes préparatoires

### <a name="mac-prerequisites"></a>Prérequis Mac

Avant d’installer le client, vérifiez que les ordinateurs Mac disposent des prérequis, comme décrit dans [Systèmes d’exploitation pris en charge pour Mac](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

### <a name="certificate-requirements"></a>Conditions de certificat
L’installation et la gestion de clients pour les ordinateurs Mac nécessitent des certificats d’infrastructure à clé publique (PKI). Les certificats PKI permettent de sécuriser les communications entre les ordinateurs Mac et le site Configuration Manager grâce à une authentification mutuelle et des transferts de données chiffrés. Configuration Manager peut demander et installer un certificat client utilisateur à l’aide des services de certificat Microsoft avec une autorité de certification d’entreprise (CA) et les rôles de système de site du point d’inscription et du point proxy d’inscription de Configuration Manager. Vous pouvez également demander et installer un certificat d’ordinateur indépendamment de Configuration Manager si le certificat répond aux critères de Configuration Manager.   
  
Les clients Mac de Configuration Manager procèdent toujours à une vérification de la révocation des certificats ; à la différence des clients Configuration Manager qui s’exécutent sous Windows, vous ne pouvez pas désactiver cette fonction de vérification de la liste de révocation de certificats (CRL).  
  
Si les clients Mac ne peuvent pas vérifier l’état de révocation du certificat d’un serveur du fait de leur incapacité à localiser la liste CRL, ils ne pourront pas se connecter aux systèmes de site Configuration Manager, tels que les points de gestion et de distribution. Vérifiez la conception de votre liste CRL pour être certain que les clients Mac (plus particulièrement ceux appartenant à une forêt différente de celle de l'autorité de certification émettrice) seront en mesure de localiser et de se connecter à un point de distribution de la liste CRL (CDP) pour la connexion des serveurs de système de site.  

Avant d’installer le client Configuration Manager sur un ordinateur Mac, choisissez le mode d’installation du certificat client :  

-   Utilisez l’inscription Configuration Manager à l’aide de l’outil CMEnroll et suivez les étapes décrites dans la section suivante de cette rubrique. Le processus d'inscription ne prenant pas en charge le renouvellement automatique de certificats, vous devez réinscrire les ordinateurs Mac avant l'expiration du certificat installé.  

-   Utilisez une demande de certificat et une méthode d’installation indépendante de Configuration Manager. Pour cette méthode d'installation, consultez la section [Use a certificate request and installation method that is independent from Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager) dans cette rubrique.  

Pour plus d’informations sur le certificat client Mac requis et sur les autres certificats PKI nécessaires à la prise en charge des ordinateurs Mac, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

Les clients Mac sont attribués automatiquement au site Configuration Manager qui les gère. Les clients Mac s'installent en tant que clients Internet uniquement, même si la communication est limitée à l'intranet. Cette configuration de client signifie qu'ils communiquent avec les rôles de système de site (points de gestion et points de distribution) sur le site qui leur est attribué si vous configurez ces rôles pour autoriser les connexions client depuis Internet. Les ordinateurs Mac ne communiquent pas avec les rôles de système de site extérieurs au site qui leur est attribué.  

> [!IMPORTANT]  
>  Le client Mac de Configuration Manager ne peut pas être utilisé afin de se connecter à un point de gestion configuré pour utiliser un [réplica de base de données](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  


### <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Déployer un certificat de serveur web sur des serveurs de système de site  
Si ces systèmes de site n’en ont pas, déployez un certificat de serveur web sur les ordinateurs qui ont ces rôles de système de site :  

-   Point de gestion  

-   Point de distribution  

-   Point d'inscription  

-   Point proxy d'inscription  

Le certificat de serveur Web doit contenir le nom de domaine Internet complet qui est spécifié dans les propriétés de système de site. Le serveur n’est pas obligé d’être accessible sur Internet pour prendre en charge les ordinateurs Mac. Si vous n'exigez pas de gestion des clients basée sur Internet, vous pouvez spécifier la valeur du nom de domaine complet intranet pour le nom de domaine complet Internet.  

Spécifiez la valeur du nom de domaine complet Internet du système de site dans le certificat de serveur web pour le point de gestion, le point de distribution et le point proxy d’inscription. 

Pour voir un exemple de déploiement qui crée et installe ce certificat de serveur web, consultez [Déploiement du certificat de serveur web pour les systèmes de site qui exécutent IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

 

### <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Déployer un certificat d’authentification client sur les serveurs de système de site  
 Si ces systèmes de site n’en ont pas, déployez un certificat d’authentification client sur les ordinateurs qui détiennent les rôles de système de site suivants :  

-   Point de gestion  

-   Point de distribution  

 Pour obtenir un exemple de déploiement qui crée et installe le certificat client pour les points de gestion, consultez [Déploiement du certificat client pour les ordinateurs Windows](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

 Pour obtenir un exemple de déploiement qui crée et installe le certificat client pour les points de distribution, consultez [Déploiement du certificat client pour les points de distribution](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### <a name="prepare-the-client-certificate-template-for-macs"></a>Préparer le modèle de certificat client pour les ordinateurs Mac  

> [!NOTE]  
>  Pour exécuter l’outil d’inscription Configuration Manager, vous devez disposer d’un compte d’utilisateur Active Directory.  

 Le modèle de certificat doit disposer d'autorisations de **lecture** et d' **inscription** pour le compte d'utilisateur appelé à inscrire le certificat sur l'ordinateur Mac.  

 Consultez [Déploiement du certificat client pour les ordinateurs Mac](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  

### <a name="configure-the-management-point-and-distribution-point"></a>Configurer le point de gestion et le point de distribution  
 Configurez des points de gestion pour les options suivantes :  

-   HTTPS  

-   Autorisez les connexions client à partir d’Internet. Cette valeur de configuration est nécessaire pour gérer les ordinateurs Mac. Toutefois, cela ne signifie pas que les serveurs de système de site doivent être accessibles sur Internet.  

-   Autoriser les appareils mobiles et les ordinateurs Mac à utiliser ce point de gestion  

 Même si les points de distribution ne sont pas indispensables à l’installation du client, vous devez en configurer pour permettre au client de se connecter à partir d’Internet si vous voulez déployer des logiciels sur ces ordinateurs après avoir installé le client.  

 
##### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Pour configurer les points de gestion et les points de distribution pour prendre en charge les ordinateurs Mac  

Avant d'entamer cette procédure, assurez-vous que le serveur de système de site exécutant le point de gestion et le point de distribution est configuré avec un nom de domaine Internet complet. Si ces serveurs de système de site ne prennent pas en charge la gestion des clients sur Internet, vous pouvez spécifier le nom de domaine complet intranet comme valeur du nom de domaine complet Internet. 

Les rôles de système de site doivent se trouver dans un site principal.  


1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration du site** > **Serveurs et rôles de système de site**, puis choisissez le serveur qui avec les rôles de système de site appropriés.  

3.  Dans le volet des détails, cliquez avec le bouton droit sur **Point de gestion**, choisissez **Propriétés du rôle** et, dans la boîte de dialogue **Propriétés du point de gestion**, configurez les options suivantes:  

    1.  Choisissez **HTTPS**.  

    2.  Choisissez **Autoriser les connexions client Internet uniquement** ou **Autoriser les connexions client Intranet et Internet**. Ces options nécessitent un nom de domaine complet Internet ou intranet.  

    3.  Choisissez **Autoriser les appareils mobiles et les ordinateurs Mac à utiliser ce point de gestion**.  

4.  Dans le volet des détails, cliquez avec le bouton droit sur **Point de distribution**, choisissez **Propriétés du rôle** et, dans la boîte de dialogue **Propriétés du point de distribution**, configurez les options suivantes:  

    -   Choisissez **HTTPS**.  

    -   Choisissez **Autoriser les connexions client Internet uniquement** ou **Autoriser les connexions client Intranet et Internet**. Ces options nécessitent un nom de domaine complet Internet ou intranet.  

    -   Choisissez **Importer un certificat**, accédez au fichier du certificat de point de distribution client exporté, puis spécifiez le mot de passe.  

5.  Répétez les étapes 2 à 4 pour tous les points de gestion et les points de distribution des sites principaux que vous prévoyez d’utiliser avec des ordinateurs Mac.  

### <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurer le point proxy d’inscription et le point d’inscription  
 Vous devez installer ces deux rôles de système de site sur le même site, mais il n'est pas nécessaire de les installer sur le même serveur de système de site ni sur la même forêt Active Directory.  

 Pour plus d’informations sur la sélection élective des rôles de système de site et sur les éléments à prendre en considération, consultez [Rôles de système de site](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) dans [Planifier des serveurs de système de site et des rôles système de site pour System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Ces procédures permettent de configurer les rôles de système de site pour prendre en charge les ordinateurs Mac. Utilisez l'une des procédures suivantes, selon que vous souhaitez installer un nouveau serveur de système de site pour prendre en charge les ordinateurs Mac ou utiliser un serveur de système de site existant :  

-   [Nouveau serveur de système de site](#new-site-system-server)  

-   [Serveur de système de site existant](#existing-site-system-server)  

####  <a name="new-site-system-server"></a>Nouveau serveur de système de site  

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Configuration du site** > **Serveurs et rôles de système de site**  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un serveur de système de site**.  

4.  Dans la page **Général**, spécifiez les paramètres généraux du système de site.  Vérifiez que vous spécifiez une valeur pour le nom de domaine complet Internet. Si le serveur ne n’est pas accessible à partir d’Internet, utilisez le nom de domaine complet intranet.  

5.  Dans la page **Sélection du rôle système**, sélectionnez **Point proxy d’inscription** et **Point d’inscription** dans la liste des rôles disponibles.  

6.  Dans la page **Point proxy d’inscription**, vérifiez les paramètres et apportez les modifications nécessaires.  

7.  Dans la page **Paramètres du point d’inscription**, vérifiez les paramètres et apportez les modifications nécessaires. Ensuite, terminez l’Assistant.  

#### <a name="existing-site-system-server"></a>Serveur de système de site existant  

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Configuration du site** > **Serveurs et rôles de système de site**, puis choisissez le serveur à utiliser pour prendre en charge les ordinateurs Mac.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Ajouter des rôles de système de site**.  

4.  Sur la page **Général** , spécifiez les paramètres généraux du système de site, puis cliquez sur **Suivant**. Vérifiez que vous spécifiez une valeur pour le nom de domaine complet Internet. Si le serveur ne n’est pas accessible à partir d’Internet, utilisez le nom de domaine complet intranet.   

5.  Dans la page **Sélection du rôle système**, choisissez **Point proxy d’inscription** et **Point d’inscription** dans la liste des rôles disponibles.  

6.  Dans la page **Point proxy d’inscription**, vérifiez les paramètres et apportez les modifications nécessaires.  

7.  Dans la page **Paramètres du point d’inscription**, vérifiez les paramètres et apportez les modifications nécessaires. Ensuite, terminez l’Assistant.  

### <a name="optional-install-the-reporting-services-point"></a>Facultatif : Installer le point Reporting Services  
 Installez le point Reporting Services si vous voulez exécuter des rapports pour les ordinateurs Mac.  

 Pour plus d’informations sur l’installation et la configuration du point Reporting Services, consultez [Configuration des rapports dans System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).  


##  <a name="install-and-configure-the-client-for-macs"></a>Installer et configurer le client pour les ordinateurs Mac  


### <a name="configure-client-settings-for-enrollment"></a>Configurer les paramètres client pour l’inscription  
 Vous devez utiliser les paramètres client par défaut pour configurer l'inscription pour les ordinateurs Mac ; vous ne pouvez pas utiliser de paramètres client personnalisés.  

 Pour plus d'informations sur les paramètres client, voir [À propos des paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

 Cela est nécessaire pour permettre à Configuration Manager de demander et d’installer le certificat sur l’ordinateur Mac.  

#### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Pour configurer les paramètres client par défaut pour permettre à Configuration Manager d’inscrire des certificats pour les ordinateurs Mac  

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Paramètres client** > **Paramètres client par défaut**.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Sélectionnez la section **Inscription**, puis configurez ces paramètres :  

    1.  **Autoriser les utilisateurs à inscrire des appareils mobiles et des ordinateurs Mac : Oui**  

    2.  **Profil d’inscription :** choisissez **Définir un profil**.  

6.  Dans la boîte de dialogue **Profil d’inscription d’appareil mobile**, choisissez **Créer**.  

7.  Dans la boîte de dialogue **Créer un profil d'inscription** , entrez un nom pour ce profil d'inscription, puis configurez le **Code du site de gestion**. Sélectionnez le site principal Configuration Manager contenant les points de gestion qui géreront les ordinateurs Mac.  

    > [!NOTE]  
    >  Si vous ne pouvez pas sélectionner le site, vérifiez qu'au moins un point de gestion dans le site est configuré pour la prise en charge des appareils mobiles.  

8.  Choisissez **Ajouter**.  

9. Dans la boîte de dialogue **Ajouter une autorité de certification pour les appareils mobiles**, sélectionnez le serveur de l’autorité de certification émettrice des certificats pour les ordinateurs Mac.  

10. Dans la boîte de dialogue **Créer un profil d’inscription**, sélectionnez le modèle de certificat d’ordinateur Mac que vous avez créé à l’étape 3.  

11. Cliquez sur **OK** pour fermer la boîte de dialogue **Profil d’inscription**, puis la boîte de dialogue **Paramètres client par défaut**.  

    > [!TIP]  
    >  Si vous voulez modifier l'intervalle de la stratégie client, utilisez le paramètre client **Intervalle d'interrogation de stratégie client** dans le groupe de paramètres client **Stratégie client** .  

 Tous les utilisateurs sont configurés avec ces paramètres la prochaine fois qu’ils téléchargent la stratégie du client. Pour lancer la récupération de stratégie pour un seul client, consultez [Lancer une récupération de stratégie pour un client Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Outre les paramètres client d’inscription, assurez-vous d’avoir configuré les paramètres d’appareil client Configuration Manager suivants :  

-   **Inventaire matériel** : Activez et configurez ce paramètre si vous voulez collecter l’inventaire matériel des ordinateurs clients Mac et Windows. Pour plus d’informations, consultez [Comment étendre l’inventaire matériel dans System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

-   **Paramètres de compatibilité** : Activez et configurez ce paramètre si vous voulez évaluer et corriger les paramètres sur les ordinateurs clients Mac et Windows. Pour plus d’informations, consultez [Planifier et configurer les paramètres de compatibilité](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

> [!NOTE]  
>  Pour plus d’informations sur les paramètres client Configuration Manager, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

### <a name="download-the-client-source-files-for-macs"></a>Télécharger les fichiers sources du client pour les ordinateurs Mac  
 Vous devez télécharger et installer les programmes suivants pour pouvoir installer et gérer le client Configuration Manager sur les ordinateurs Mac :  

-   **Ccmsetup** : Cette application permet d’installer le client Configuration Manager sur les ordinateurs Mac.  

-   **CMDiagnostics** : Cet outil permet de collecter les informations de diagnostic relatives au client Configuration Manager sur les ordinateurs Mac.  

-   **CMUninstall** : Cet outil permet de désinstaller le client Configuration Manager sur les ordinateurs Mac.  

-   **CMAppUtil** : cet outil permet de convertir les packages d’applications Apple dans un format qui peut être déployé sous forme d’application Configuration Manager.  

-   **CMEnroll** : cet outil permet de demander et d’installer le certificat client d’un ordinateur Mac en vue d’installer le client Configuration Manager.  

> [!IMPORTANT]  
>  Quand vous installez un nouveau client pour les ordinateurs Mac, vous devez peut-être également installer des mises à jour Configuration Manager pour refléter les nouvelles informations client dans la console Configuration Manager.  

##### <a name="to-download-and-install-the-mac-os-x-client-files"></a>Pour télécharger et installer les fichiers du client Mac OS X  

1.  Téléchargez le package de fichiers du client Mac OS X, **ConfigmgrMacClient.msi**, et enregistrez-le sur un ordinateur exécutant Windows.  

     Ce fichier n’est pas fourni dans le support d’installation de Configuration Manager. Vous pouvez télécharger ce fichier à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  Sur l'ordinateur Windows, exécutez le fichier **ConfigmgrMacClient.msi** que vous venez de télécharger pour extraire le package du client Mac (Macclient.dmg) dans un dossier du disque local (par défaut, **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copiez le fichier Macclient.dmg dans un dossier de l'ordinateur Mac.  

4.  Sur l’ordinateur Mac, exécutez le fichier Macclient.dmg pour extraire les fichiers dans un dossier du disque local.  

5.  Dans ce dossier, assurez-vous que les fichiers Ccmsetup et CMClient.pkg ont été extraits, qu'un dossier nommé Outils a été créé et qu'il contient les outils CMDiagnostics, CMUninstall, CMAppUtil et CMEnroll.  

### <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Installer le client, puis inscrire le certificat client sur l’ordinateur Mac  
 Cette procédure installe le client et utilise l’outil CMEnroll pour demander et installer le certificat client pour un ordinateur Mac afin que vous puissiez gérer cet ordinateur à l’aide de Configuration Manager.  

 Vous pouvez inscrire le client à l’aide de l’Assistant Inscription d’ordinateur Mac sans avoir à utiliser l’outil CMEnroll, comme décrit dans [Inscrire le client à l’aide de l’Assistant Inscription d’ordinateur Mac](#enroll-the-client-by-using-the-mac-computer-enrollment-wizard)  

#### <a name="to-install-the-client-and-enroll-the-certificate-by-using-the-cmenroll-tool"></a>Pour installer le client et inscrire le certificat à l'aide de l'outil CMEnroll  

1.  Sur l’ordinateur Mac, accédez au dossier dans lequel vous avez extrait le contenu du fichier macclient.dmg.  

2.  Entrez la ligne de commande suivante : **sudo ./ccmsetup**  

3.  Patientez jusqu'à ce que le message **Installation terminée** s'affiche à l'écran. Même si le programme d’installation affiche un message vous demandant de redémarrer maintenant, ne suivez pas cette instruction et passez à l’étape suivante.  

4.  Dans le dossier Outils sur l’ordinateur Mac, tapez la commande suivante : **sudo ./CMEnroll -s &lt;nom_serveur_proxy_inscription> -ignorecertchainvalidation -u &lt;nom_utilisateur>**  

    Une fois le client installé, l’Assistant Inscription d’ordinateur Mac s’ouvre pour vous aider à inscrire l’ordinateur Mac. Pour inscrire le client par cette méthode, consultez [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) dans cette rubrique.  

5. Tapez le mot de passe du compte d’utilisateur Active Directory.  Quand vous entrez cette commande, vous êtes invité à entrer deux mots de passe : la première invite concerne le compte de superutilisateur qui exécute la commande. La seconde invite est pour le compte d'utilisateur Active Directory. Les invites semblent identiques, assurez-vous que vous les spécifiez dans le bon ordre.  

    Le nom d'utilisateur peut se présenter sous l'une des formes suivantes :  

    -   « domaine\nom ». Par exemple: « contoso\mnorth »  

    -   'user@domain'. Exemple : 'mnorth@contoso.com'  

     Le nom d'utilisateur et le mot de passe correspondant doivent correspondre à un compte d'utilisateur Active Directory disposant des autorisations de lecture et d'inscription dans le modèle de certificat client Mac.  

     Exemple : si le serveur de point proxy d’inscription se nomme **server02.contoso.com** et que des autorisations ont été accordées au nom d’utilisateur **contoso\mnorth** pour le modèle de certificat client Mac, tapez la ligne suivante : **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u ’contoso\mnorth’**  

    > [!NOTE]  
    >  Si le nom d’utilisateur contient l’un des caractères **&lt;>"+=,**, l’inscription échoue. Pour résoudre ce problème, obtenez un certificat hors bande avec un nom d'utilisateur qui ne contient pas ces caractères.  
    >  
    >  Pour une expérience utilisateur plus transparente, vous pouvez mettre les étapes d'installation et les commandes sous forme de script afin que les utilisateurs n'aient qu'à fournir leurs nom d'utilisateur et mot de passe.  

5.  Patientez jusqu'à l'affichage d'un message indiquant que l' **inscription s'est déroulée correctement** .  

6.  Pour limiter le certificat inscrit à Configuration Manager, sur l’ordinateur Mac, ouvrez une fenêtre de terminal et apportez les modifications suivantes :  

    a.  Entrez la commande **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Dans la boîte de dialogue **Trousseau d’accès**, dans la zone **Trousseau**, choisissez **Système**, puis dans la zone **Catégorie**, choisissez **Clés**.  

    c.  Développez les clés pour afficher les certificats clients. Lorsque vous avez identifié le certificat avec une clé privée que vous venez d'installer, double-cliquez sur la clé.  

    d.  Sous l’onglet **Contrôle d’accès**, choisissez **Confirmer avant d’autoriser l’accès**.  

    e.  Accédez à **/Library/Application Support/Microsoft/CCM**, sélectionnez **CCMClient**, puis choisissez **Ajouter**.  

    f.  Choisissez **Enregistrer les modifications** et fermez la boîte de dialogue **Trousseau d’accès**.  

7.  Redémarrez l'ordinateur Mac.  

 Vérifiez que l'installation du client a abouti en ouvrant l'élément **Configuration Manager** dans les **Préférences Système** de l'ordinateur Mac. Vous pouvez également mettre à jour et afficher le regroupement **Tous les systèmes** pour vérifier que l'ordinateur Mac figure désormais dans ce regroupement en tant que client géré.  

> [!TIP]  
>  Pour vous aider à résoudre les problèmes liés au client Mac, vous pouvez utiliser le programme CMDiagnostics inclus avec le package client Mac OS X afin de recueillir les informations suivantes :  
>   
>  -   Liste des processus en cours.  
> -   Version du système d'exploitation Mac OS X.  
> -   Rapports des défaillances du système Mac OS X liées au client Configuration Manager, y compris les fichiers **CCM\*.crash** et **System Preference.crash**.  
> -   Le fichier de nomenclature et le fichier de liste des propriétés (.plist) créés par l’installation du client Configuration Manager.  
> -   Le contenu du dossier /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  Les informations recueillies par le programme CmDiagnostics sont ajoutées à un fichier zip enregistré sur le bureau de l’ordinateur et nommé cmdiag-*<nom_hôte\>***-***<date_et_heure\>*.zip.  

####  <a name="enroll-the-client-by-using-the-mac-computer-enrollment-wizard"></a>Inscrire le client à l’aide de l’Assistant Inscription d’ordinateur Mac  

1.  Quand vous avez terminé l’installation du client, l’Assistant Inscription d’ordinateur s’ouvre. Si l'Assistant ne s'ouvre pas ou si vous fermez l'Assistant par inadvertance, cliquez sur **Inscription** sur la page des préférences **Configuration Manager** pour ouvrir l'Assistant.  

2.  Dans la deuxième page de l’Assistant, spécifiez les informations suivantes :  

    -   **Nom d'utilisateur** : le nom d'utilisateur peut se présenter sous l'une des formes suivantes :  

        -   « domaine\nom ». Par exemple: « contoso\mnorth »  

        -   'user@domain'. Exemple : 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  Lorsque vous utilisez une adresse électronique pour renseigner le champ **Nom d’utilisateur**, Configuration Manager utilise automatiquement le nom de domaine de l’adresse électronique et le nom par défaut du serveur de point proxy d’inscription pour renseigner le champ **Nom du serveur**. Si ce nom de domaine et ce nom de serveur ne correspondent pas au nom du serveur de point proxy d'inscription, vous devez informer vos utilisateurs du nom correct à utiliser pour qu'ils puissent l'entrer lors de l'inscription de leurs ordinateurs Mac.  

         Le nom d'utilisateur et le mot de passe correspondant doivent correspondre à un compte d'utilisateur Active Directory disposant des autorisations de lecture et d'inscription dans le modèle de certificat client Mac.  

    -   **Mot de passe** : entrez un mot de passe correspondant au nom d’utilisateur spécifié.  

    -   **Nom du serveur** : entrez le nom du serveur de point proxy d’inscription.  

3.  Cliquez sur **Suivant** pour continuer, puis terminez l'Assistant.  

## <a name="maintenance-tasks-for-mac-clients"></a>Tâches de maintenance pour les clients Mac

###  <a name="uninstalling-the-mac-client"></a>Désinstallation du client Mac  

1.  Sur un ordinateur Mac, ouvrez une fenêtre de terminal et accédez au dossier dans lequel vous avez extrait le contenu du fichier macclient.dmg que vous avez téléchargé.  

2.  Accédez au dossier Outils, puis entrez la ligne de commande suivante :  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  La propriété **c** demande au programme de désinstallation du client de supprimer aussi les fichiers journaux d’incident et ceux du client. Cette étape est facultative, mais constitue une pratique recommandée pour éviter toute confusion si vous réinstallez le client ultérieurement.  

3.  Si nécessaire, supprimez manuellement le certificat d’authentification de client que Configuration Manager utilisait, ou révoquez-le. CMUnistall ne supprime et ne révoque pas ce certificat.  

###  <a name="renewing-the-mac-client-certificate"></a>Renouvellement du certificat client Mac  
 Pour renouveler le certificat client Mac, utilisez une des méthodes suivantes :  

-   [Assistant Renouvellement de certificat](#renew-certificate-wizard)  

-   [Renouveler le certificat manuellement](#renew-certificate-manually)  

####  <a name="renew-certificate-wizard"></a>Assistant Renouvellement de certificat  

1.  Configurez les valeurs suivantes comme *chaînes* dans le fichier ccmclient.plist qui contrôle l’ouverture de l’Assistant Renouvellement de certificat :  

    -   **RenewalPeriod1** : spécifie, en secondes, la première période de renouvellement pendant laquelle les utilisateurs peuvent renouveler le certificat. La valeur par défaut correspond à 3 888 000 secondes (45 jours). Ne configurez pas de valeur inférieure à 300, sinon la période est rétablie à la valeur par défaut. 


    -   **RenewalPeriod2** : spécifie, en secondes, la deuxième période de renouvellement pendant laquelle les utilisateurs peuvent renouveler le certificat. La valeur par défaut correspond à 259 200 secondes (3 jours). Si cette valeur est configurée sur une valeur supérieure ou égale à 300 secondes et inférieure ou égale à **RenewalPeriod1**, la valeur configurée est utilisée. Si **RenewalPeriod1** est supérieure à 3 jours, une valeur de 3 jours sera utilisée pour **RenewalPeriod2**.  Si **RenewalPeriod1** est inférieure à 3 jours, **RenewalPeriod2** est définie sur la même valeur que **RenewalPeriod1**.  

    -   **RenewalReminderInterval1** : spécifie, en secondes, la fréquence à laquelle l’Assistant Renouveler le certificat sera affiché pour les utilisateurs lors de la première période de renouvellement. La valeur par défaut correspond à 86 400 secondes (1 jour). Si **RenewalReminderInterval1** est supérieur à 300 secondes et inférieur à la valeur configurée pour **RenewalPeriod1**, la valeur configurée sera utilisée. Dans le cas contraire, la valeur par défaut de 1 jour sera utilisée.  

    -   **RenewalReminderInterval2** : spécifie, en secondes, la fréquence à laquelle l’Assistant Renouveler le certificat sera affiché pour les utilisateurs lors de la deuxième période de renouvellement. La valeur par défaut correspond à 28 800 secondes (8 heures). Si **RenewalReminderInterval2** est supérieure à 300 secondes, inférieure ou égale à **RenewalReminderInterval1** et inférieure ou égale à **RenewalPeriod2**, la valeur configurée sera utilisée. Sinon, une valeur de 8 heures sera utilisée.  

     **Exemple** : si les valeurs sont laissées sur leurs valeurs par défaut, 45 jours avant l’expiration du certificat, l’Assistant s’ouvre toutes les 24 heures.  Dans les 3 jours de la date d'expiration du certificat, l'Assistant s'ouvre toutes les 8 heures.  

     **Exemple** : utilisez la ligne de commande suivante, ou un script, pour définir la première période de renouvellement sur 20 jours.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  Lorsque l'Assistant Renouveler le certificat s'ouvre, les champs **Nom d'utilisateur** et **Nom du serveur** sont en général déjà remplis et l'utilisateur ne doit entrer qu'un mot de passe pour renouveler le certificat.  

    > [!NOTE]  
    >  Si l'Assistant ne s'ouvre pas ou si vous fermez l'Assistant par inadvertance, cliquez sur **Renouveler** sur la page des préférences **Configuration Manager** pour ouvrir l'Assistant.  

####  <a name="renewing-the-mac-client-certificate-manually"></a>Renouvellement manuel du certificat client Mac  
 La période de validité classique pour le certificat client Mac est de 1 an. Configuration Manager ne renouvelle pas automatiquement le certificat utilisateur demandé à l’inscription ; vous devez donc procéder comme suit pour renouveler manuellement le certificat.  

> [!IMPORTANT]  
>  Si le certificat a expiré, vous devez désinstaller, réinstaller et réinscrire le client Mac.  

 Cette procédure supprime l'ID SMS, qui est requis pour demander un nouveau certificat pour le même ordinateur Mac. Lorsque vous supprimez et remplacez l’ID SMS client, tout historique client stocké, tel que l’inventaire, est supprimé après la suppression du client de la console Configuration Manager.  

1.  Créez et remplissez un regroupement d’appareils pour les ordinateurs Mac qui doivent renouveler les certificats utilisateur.  

    > [!WARNING]  
    >  Configuration Manager ne surveille pas la période de validité du certificat qu’il inscrit pour les ordinateurs Mac. Vous devez surveiller cette validité indépendamment de Configuration Manager pour identifier les ordinateurs Mac à ajouter à ce regroupement.  

2.  Dans l'espace de travail **Ressources et compatibilité** , démarrez l' **Assistant Création d'élément de configuration**.  

3.  Sur la page **Général** de l'Assistant, spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Type :Mac OS X**  

4.  Sur la page **Plateformes prises en charge** de l'Assistant, assurez-vous que toutes les versions de Mac OS X sont sélectionnées.  

5.  Dans la page **Paramètres** de l’Assistant, choisissez **Nouveau**, puis dans la boîte de dialogue **Créer un paramètre**, spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Type de paramètre :Script**  

    -   **Type de données :Chaîne**  

6.  Dans la boîte de dialogue **Créer un paramètre**, sous **Script de découverte**, choisissez **Ajouter un script** pour spécifier un script de découverte des ordinateurs Mac configurés avec un SMSID configuré.  

7.  Dans la boîte de dialogue **Modifier un script de découverte** , entrez le script Shell suivant :  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Choisissez **OK** pour fermer la boîte de dialogue **Modifier un script de découverte**.  

9. Dans la boîte de dialogue **Créer un paramètre**, sous **Script de correction (facultatif)**, choisissez **Ajouter un script** pour spécifier un script de suppression du SMSID détecté sur les ordinateurs Mac.  

10. Dans la boîte de dialogue **Créer un script de correction** , entrez le script Shell suivant :  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Choisissez **OK** pour fermer la boîte de dialogue **Créer un script de correction**.  

12. Sur la page **Règles de compatibilité** de l'Assistant, cliquez sur **Nouveau**, puis dans la boîte de dialogue **Créer une règle** , spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Paramètre sélectionné :** Choisissez **Parcourir**, puis sélectionnez le script de découverte que vous avez spécifié précédemment.  

    -   Dans **les valeurs suivantes** , entrez **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Activez l'option **Exécuter le script de correction spécifié lorsque ce paramètre n'est pas compatible**.  

13. Effectuez toutes les étapes de l'Assistant Création d'élément de configuration.  

14. Créez une ligne de base de configuration contenant l’élément de configuration que vous venez de créer et déployez-la sur le regroupement d’appareils créé à l’étape 1.  

     Pour plus d’informations sur la création et le déploiement de lignes de base de configuration, consultez [Comment créer des bases de référence de configuration dans System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) et [Comment déployer des lignes de base de configuration dans System Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. Sur les ordinateurs Mac sur lesquels l'ID SMS a été supprimé, exécutez la commande suivante pour installer un nouveau certificat :  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Lorsque vous y êtes invité, fournissez le mot de passe du compte de superutilisateur qui exécute la commande, puis le mot de passe du compte d'utilisateur Active Directory.  

16. Pour limiter le certificat inscrit à Configuration Manager, sur l’ordinateur Mac, ouvrez une fenêtre de terminal et apportez les modifications suivantes :  

    a.  Entrez la commande **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Dans la boîte de dialogue **Trousseau d’accès**, dans la zone **Trousseau**, choisissez **Système**, puis dans la zone **Catégorie**, choisissez **Clés**.  

    c.  Développez les clés pour afficher les certificats clients. Lorsque vous avez identifié le certificat avec une clé privée que vous venez d'installer, double-cliquez sur la clé.  

    d.  Sous l’onglet **Contrôle d’accès**, choisissez **Confirmer avant d’autoriser l’accès**.  

    e.  Accédez à **/Library/Application Support/Microsoft/CCM**, sélectionnez **CCMClient**, puis choisissez **Ajouter**.  

    f.  Choisissez **Enregistrer les modifications** et fermez la boîte de dialogue **Trousseau d’accès**.  

17. Redémarrez l'ordinateur Mac.  

##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Utiliser une demande de certificat et une méthode d'installation indépendantes de Configuration Manager  
 Si vous n’utilisez pas l’inscription Configuration Manager, mais que vous demandez et installez le certificat client indépendamment de Configuration Manager, les étapes de configuration sont légèrement différentes

Tout d’abord, procédez *uniquement* comme suit :

a. [Déployer un certificat de serveur web sur les serveurs de système de site](#deploy-a-web-server-certificate-to-site-system-servers)

b. [Déployer un certificat d’authentification client sur les serveurs de système de site](#deploy-a-client-authentication-certificate-to-site-system-servers)

c. [Configurer le point de gestion et le point de distribution](#configure-the-management-point-and-distribution-point)

d. [Facultatif : Installer le point Reporting Services](#optional:-install-the-reporting-services-point)

e. [Télécharger les fichiers sources du client pour les ordinateurs Mac](#download-the-client-source-files-forMacs).  
  

#### <a name="to-install-the-client-certificate-independently-from-configuration-manager-and-install-the-client"></a>Pour installer le certificat client indépendamment de Configuration Manager et installer le client  

1.  Pour installer le certificat client indépendamment de Configuration Manager, utilisez les instructions qui accompagnent la méthode de déploiement de certificat choisie pour demander et installer le certificat client sur l’ordinateur Mac.  

2.  Accédez au dossier dans lequel vous avez extrait le contenu du fichier macclient.dmg, téléchargé depuis le Centre de téléchargement Microsoft.  

3.  Entrez la ligne de commande suivante : **sudo ./ccmsetup -MP <nom_de_domaine_complet_Internet_du_point_de_gestion\> -SubjectName <valeur_objet_certificat\>**.  La valeur de l'objet Certificat est sensible à la casse, vous devez l'entrer exactement telle qu'elle apparaît dans les détails du certificat.  

     Exemple : si le nom de domaine complet Internet dans les propriétés du système de site est **server03.contoso.com** et que le certificat client Mac porte le nom de domaine complet **mac12.contoso.com** comme nom commun dans l’objet certificat, tapez : **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  Patientez jusqu'à l'affichage du message d' **installation terminée** , puis redémarrez l'ordinateur Mac.  

5.  Pour vérifier que Configuration Manager peut accéder à ce certificat, sur l’ordinateur Mac, ouvrez une fenêtre de terminal et apportez les modifications suivantes :  

    a.  Entrez la commande **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Dans la boîte de dialogue **Trousseau d’accès**, dans la zone **Trousseau**, choisissez **Système**, puis dans la zone **Catégorie**, choisissez **Clés**.  

    c.  Développez les clés pour afficher les certificats clients. Lorsque vous avez identifié le certificat avec une clé privée que vous venez d'installer, double-cliquez sur la clé.  

    d.  Sous l’onglet **Contrôle d’accès**, choisissez **Confirmer avant d’autoriser l’accès**.  

    e.  Accédez à **/Library/Application Support/Microsoft/CCM**, sélectionnez **CCMClient**, puis choisissez **Ajouter**.  

    f.  Choisissez **Enregistrer les modifications** et fermez la boîte de dialogue **Trousseau d’accès**.  

6.  Si vous disposez de plusieurs certificats qui contiennent la même valeur d’objet, vous devez spécifier le numéro de série du certificat pour identifier le certificat que vous voulez utiliser pour le client Configuration Manager. Pour ce faire, utilisez la commande suivante : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<numéro_série\>"**.  

     Exemple : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Vérifiez que l’installation du client a abouti en ouvrant l’élément **Configuration Manager** dans les **Préférences système** de l’ordinateur Mac. Vous pouvez également mettre à jour et afficher le regroupement **Tous les systèmes** pour vérifier que l’ordinateur Mac figure désormais dans ce regroupement comme client géré.  

### <a name="renewing-the-mac-client-certificate"></a>Renouvellement du certificat client Mac  
 Utilisez la procédure suivante avant de renouveler le certificat d'ordinateur sur les ordinateurs Mac.  

 Cette procédure supprime l'ID SMS qui est requis par le client pour utiliser un certificat nouveau ou renouvelé sur l'ordinateur Mac.  

> [!IMPORTANT]  
>  Lorsque vous supprimez et remplacez l’ID SMS client, tout historique client stocké, tel que l’inventaire, est supprimé après la suppression du client de la console Configuration Manager.  

#### <a name="to-renew-the-mac-client-certificate"></a>Pour renouveler le certificat client Mac  

1.  Créez et remplissez un regroupement d’appareils pour les ordinateurs Mac qui doivent renouveler les certificats d’ordinateur.  

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

8.  Choisissez **OK** pour fermer la boîte de dialogue **Modifier un script de découverte**.  

9. Dans la boîte de dialogue **Créer un paramètre**, sous **Script de correction (facultatif)**, choisissez **Ajouter un script** pour spécifier un script de suppression du SMSID détecté sur les ordinateurs Mac.  

10. Dans la boîte de dialogue **Créer un script de correction** , entrez le script Shell suivant :  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Choisissez **OK** pour fermer la boîte de dialogue **Créer un script de correction**.  

12. Dans la page **Règles de compatibilité** de l’Assistant, choisissez **Nouveau**, puis dans la boîte de dialogue **Créer une règle**, spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Paramètre sélectionné :** Choisissez **Parcourir**, puis sélectionnez le script de découverte que vous avez spécifié précédemment.  

    -   Dans **les valeurs suivantes** , entrez **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Activez l'option **Exécuter le script de correction spécifié lorsque ce paramètre n'est pas compatible**.  

13. Effectuez toutes les étapes de l'Assistant Création d'élément de configuration.  

14. Créez une ligne de base de configuration contenant l'élément de configuration que vous venez de créer et déployez-la sur le regroupement de périphériques créé à l'étape 1.  

     Pour plus d’informations sur la création et le déploiement de bases de référence de configuration, consultez [Comment créer des bases de référence de configuration dans System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Après avoir installé un nouveau certificat sur les ordinateurs Mac sur lesquels l'ID SMS a été supprimé, exécutez la commande suivante pour configurer le client de sorte à utiliser le nouveau certificat :  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. Si vous disposez de plusieurs certificats qui contiennent la même valeur d’objet, vous devez spécifier le numéro de série du certificat pour identifier le certificat que vous voulez utiliser pour le client Configuration Manager. Pour ce faire, utilisez la commande suivante : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<numéro_série\>"**.  

     Exemple : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Redémarrez l’ordinateur Mac.  



<!--HONumber=Dec16_HO3-->


