---
title: "Inscrire des appareils iOS avec un programme d’inscription des appareils - Configuration Manager | Microsoft Docs"
description: "Activez l’inscription d’appareils iOS via le programme DEP pour les déploiements hybrides dans Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78d44adc-9b1c-4bc6-b72d-e93873916ea6
caps.latest.revision: 9
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 4eee9731a4a27328c47c0d15931cab28cf520a18
ms.openlocfilehash: 555da7187b505a926731350d16787bc02d28dad3
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017

---
# <a name="ios-device-enrollment-program-dep-enrollment-for-hybrid-deployments-with-configuration-manager"></a>Inscription d’appareils iOS via le programme DEP pour les déploiements hybrides avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les entreprises peuvent acheter des appareils iOS via le programme d’inscription des appareils (DEP, Device Enrollment Program) d’Apple, puis les gérer à l’aide de Microsoft Intune. Pour gérer des appareils iOS d’entreprise avec le programme d’inscription d’appareils d’Apple, les sociétés doivent suivre la procédure requise auprès d’Apple pour participer au programme et acquérir des appareils par son biais. Les détails de cette procédure sont disponibles à l’adresse suivante :  [https://deploy.apple.com](https://deploy.apple.com). Les avantages du programme incluent la configuration automatique des appareils sans connexion USB de chaque appareil à un ordinateur.  

 Avant d’inscrire des appareils iOS d’entreprise à l’aide du programme DEP, vous devez obtenir un jeton approprié auprès d’Apple. Ce jeton permet à Intune de synchroniser les informations sur les appareils participant à ce programme et appartenant à votre entreprise. Il permet également à Intune de charger des profils d’inscription sur Apple et d’attribuer des appareils à ces profils.  

## <a name="apple-dep-enrollment-for-ios-devices"></a>Inscription au programme d’inscription d’appareils d’Apple pour les appareils iOS  
 Les procédures suivantes décrivent comment déclarer les appareils iOS achetés via le programme DEP d’Apple en tant qu’appareils appartenant à l’entreprise gérés par Intune. Lorsque l’utilisateur allume l’appareil pour la première fois, le profil de gestion DEP est reçu sur l’appareil, l’Assistant Installation s’exécute et la gestion de l’appareil est mise en place.  

###  <a name="enable-dep-enrollment-in-configuration-manager-with-intune"></a>Activer l’inscription DEP (Device Enrollment Program) dans Configuration Manager avec Intune  

1.  **Commencer à gérer des appareils iOS avec Configuration Manager**   
    Avant de pouvoir inscrire des appareils IOS via le programme DEP, vous devez effectuer la procédure de [configuration de la gestion des appareils mobiles hybrides](../../mdm/deploy-use/setup-hybrid-mdm.md), notamment la [procédure de prise en charge de l’inscription iOS](../deploy-use/enroll-hybrid-ios-mac.md).

2.  **Créer une demande de jeton DEP**   
    Dans la console Configuration Manager, dans l’espace de travail **Administration**, développez **Configuration de la hiérarchie**, développez **Services cloud**, puis cliquez sur **Abonnements Windows Intune**. Cliquez sur **Créer une demande de jeton DEP** sous l’onglet **Accueil** , sur **Parcourir** pour spécifier l’emplacement de téléchargement de la demande de jeton DEP, puis sur **Télécharger**. Enregistrez le fichier de demande de jeton DEP (.pem) localement. Le fichier .pem est utilisé pour demander un jeton approuvé (.p7m) au portail du programme d’inscription d’appareils d’Apple.  

3.  **Obtenir un jeton du programme d’inscription d’appareils**   
    Accédez au [portail du programme d’inscription d’appareils](https://deploy.apple.com) (https://deploy.apple.com) et connectez-vous avec votre ID Apple d’entreprise. Cet ID Apple doit être utilisé par la suite pour renouveler votre jeton DEP.  

    1.  Dans la console [portail du programme d’inscription d’appareils](https://deploy.apple.com), accédez à **Programme d’inscription d’appareils** > **Gérer les serveurs**, puis cliquez sur **Ajouter un serveur MDM**.  

    2.  Entrez le **Nom du serveur MDM**, puis cliquez sur **Suivant**. Le nom du serveur vous permet d'identifier le serveur MDM uniquement. Il ne s’agit pas du nom ou de l’URL du serveur Intune ou Configuration Manager.  

    3.  La boîte de dialogue **Ajouter <nom_serveur\>** s’ouvre. Cliquez sur **Choisir un fichier…** pour charger le fichier .pem que vous avez créé à l’étape précédente, puis cliquez sur **Suivant**.  

    4.  La boîte de dialogue **Ajouter <nom_serveur\>** affiche un lien **Votre jeton de serveur**. Téléchargez le fichier de jeton de serveur (.p7m) sur votre ordinateur, puis cliquez sur **Terminé**.  

     Ce fichier de certificat (.p7m) est utilisé pour établir une relation d’approbation entre le serveur Intune et le serveur du programme d’inscription d’appareils d’Apple.  

4.  **Ajouter le jeton DEP à Configuration Manager**   
    Dans la console Configuration Manage , dans l’espace de travail **Administration**, développez **Configuration de la hiérarchie**, puis cliquez sur **Abonnements Windows Intune**. Cliquez sur **Configurer des plateformes** sous l’onglet **Accueil** , puis cliquez sur **iOS**. Sélectionnez **Activer le programme d’inscription d’appareils**, accédez au fichier de certificat (.p7m), cliquez sur **Ouvrir**, sur **Télécharger**, puis sur **OK**.  

#### <a name="set-up-enrollment-for-apple-device-enrollment-program-dep-ios-devices"></a>Configurer l’inscription pour les appareils iOS via le Programme d’inscription d’appareils Apple  

1.  **Ajouter une stratégie d'inscription d'appareils d'entreprise**   
    Dans la console Configuration Manager, dans l’espace de travail **Ressources et Conformité**, développez **Vue d’ensemble**, **Tous les appareils d’entreprise** et **iOS**, puis cliquez sur **Profils d’inscription**. Cliquez sur **Créer un profil** sous l’onglet **Accueil** pour ouvrir l’Assistant Create Profile (Création d’un profil). Configurez les paramètres des pages suivantes :  

    1.  Dans la page **Général**, spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

        -   **Nom** : nom du profil d’inscription d’appareil. (Non visible pour les utilisateurs)  

        -   **Description** : description du profil d'inscription d'appareil. (Non visible pour les utilisateurs)  

        -   **Affinité utilisateur** : spécifie la façon dont les appareils sont inscrits. Voir [Affinité utilisateur pour les appareils gérés hybrides dans Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

            -   **Demander une affinité utilisateur**: l’appareil doit être affilié à un utilisateur durant la configuration initiale. Il peut ensuite être autorisé à accéder aux données de l’entreprise et à envoyer des messages électroniques au nom de cet utilisateur.  L’affinité utilisateur doit être configurée pour les appareils gérés par DEP qui appartiennent à des utilisateurs et doivent utiliser le portail d’entreprise (par exemple, pour installer des applications).  

            > [!NOTE]
            > Dans le cas de DEP avec affinité utilisateur, un point de terminaison ADFS WS-Trust 1.3 Username/Mixed doit être activé pour demander un jeton utilisateur.

            -   **Pas d’affinité utilisateur**: l’appareil n’est affilié à aucun utilisateur. Utilisez cette affiliation pour les appareils qui effectuent des tâches sans accéder aux données de l'utilisateur local. Les applications nécessitant une affiliation de l'utilisateur ne fonctionneront pas.  
             ![Capture d’écran montrant le nom de profil DEP, une description et une invite Affinité utilisateur](../media/dep-general.png)

    2.  Dans la page **Paramètres du Programme d’inscription des appareils**, spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

        -   **Service** : cette information s’affiche quand les utilisateurs appuient sur «À propos de la configuration » pendant l’activation.  

        -   **Numéro de téléphone du support** : s’affiche quand l’utilisateur clique sur le bouton **Besoin d’aide** pendant l’activation.
       ![Capture d’écran montrant l’affectation d’un profil DEP à des appareils iOS](../media/dep-settings.png)

        -   **Mode de préparation** : cet état est défini pendant l’activation et ne peut pas être modifié sans rétablir les paramètres d’usine de l’appareil :  

            -   **Non supervisé** : capacités de gestion limitées  

            -   **Supervisé** : active des options de gestion supplémentaires et désactive le verrou d’activation par défaut  

        -   **Verrouiller le profil d’inscription de l’appareil** : cet état est défini pendant l’activation et ne peut pas être modifié sans rétablir les paramètres d’usine.  

            -   **Désactiver** : permet de supprimer le profil de gestion à partir du menu **Paramètres**  

            -   **Activer** : (nécessite le **Mode de préparation** = **Supervisé**) désactive les paramètres iOS qui pourraient autoriser la suppression du profil de gestion  

    3.  Dans la page **Assistant Configuration** , configurez les paramètres qui personnalisent l’Assistant Configuration iOS qui démarre quand l’appareil est mis sous tension pour la première fois, puis cliquez sur **Suivant**. Ces paramètres incluent :  
        -   **Code secret** : demande un code secret pendant l’activation. Exige toujours un code secret, sauf si l’appareil doit être sécurisé ou si son accès doit être contrôlé d’une autre façon (c’est-à-dire, en mode plein écran qui limite l’appareil à une seule application).  
        -   **Services de localisation** : si cette option est activée, l’Assistant Installation vous invite à spécifier le service pendant l’activation  
        -   **Restaurer** : si cette option est activée, l’Assistant Installation invite à spécifier la sauvegarde iCloud pendant l’activation  
        -   **ID Apple** : un ID Apple est nécessaire pour télécharger des applications App Store iOS, y compris celles qui sont installées par Intune. Si cette option est activée, iOS demande un ID Apple aux utilisateurs quand Intune tente d’installer une application sans ID.  
        -   **Termes et Conditions** : si cette option est activée, l’Assistant Installation invite l’utilisateur à accepter les conditions générales d’Apple pendant l’activation  
        -   **Touch ID** : si cette option est activée, l’Assistant Installation vous invite à spécifier ce service pendant l’activation
        -   **Apple Pay** : si cette option est activée, l’Assistant Installation vous invite à spécifier ce service pendant l’activation
        -   **Zoom** : si cette option est activée, l’Assistant Installation vous invite à spécifier ce service pendant l’activation
        -   **Siri** : si cette option est activée, l’Assistant Installation vous invite à spécifier ce service pendant l’activation  
        -   **Envoyer les données de diagnostic à Apple** : si cette option est activée, l’Assistant Installation vous invite à spécifier ce service pendant l’activation  
        ![Capture d’écran montrant l’attribution d’un profil DEP à des appareils iOS](../media/dep-setup-assistant.png)

    4.  Sur la page **Gestion supplémentaire**, spécifiez si une connexion USB peut être utilisée pour les paramètres de la gestion supplémentaire. Quand vous sélectionnez **Demander un certificat**, vous devez importer un certificat de gestion Apple Configurator à utiliser pour ce profil.  Spécifiez **Interdire** pour empêcher la synchronisation des fichiers avec iTunes ou la gestion via Apple Configurator. Microsoft vous recommande de spécifier la valeur **Interdire**, exporter les configurations supplémentaires d’Apple Configurator, puis déployer en tant que profil de configuration iOS personnalisé via Intune, plutôt que d’utiliser ce paramètre pour permettre un déploiement manuel avec ou sans un certificat.  

        -   **Interdire** : empêche l’appareil de communiquer via USB (désactive l’appariement)  

        -   **Autoriser** : autorise un appareil à communiquer via une connexion USB pour n’importe quel PC ou Mac  

        -   **Demander un certificat** : permet un appariement avec un Mac avec un certificat importé dans le profil d’inscription  

2.  **Attribuer des appareils DEP pour la gestion**   
    Accédez au [portail du programme d’inscription d’appareils](https://deploy.apple.com) (https://deploy.apple.com) et connectez-vous avec votre ID Apple d’entreprise. Accédez à **Programme de déploiement** > **Programme d’inscription d’appareils** > **Gérer les appareils**. Spécifiez la façon dont vous allez **choisir des appareils**, fournissez les informations relatives aux appareils et spécifiez les détails par appareil : **Numéro de série**, **Numéro de commande**ou **Télécharger un fichier CSV**. Ensuite, sélectionnez **Attribuer au serveur** et sélectionnez le <*nom_serveur*> que vous avez spécifié à l'étape 3, puis cliquez sur **OK**.  

3.  **Synchroniser des appareils gérés par le programme DEP**   
    Dans la console **Ressources et Conformité**, accédez à **Tous les appareils d’entreprise** > **Appareils prédéclarés**. Sous l’onglet **Accueil** , cliquez sur **Synchronisation DEP**. Une demande de synchronisation est envoyée à Apple. Une fois la synchronisation terminée, les appareils gérés par le programme DEP s'affichent.

4.  **Attribuer un profil DEP**<br>Dans la console **Ressources et Conformité**, accédez à **Tous les appareils d’entreprise** > **iOS** > **Profils d’inscription**. Sélectionnez le profil d’inscription DEP, puis sous l’onglet **Accueil**, cliquez sur **Affecter aux appareils**. Sélectionnez les appareils qui utiliseront ce profil d’inscription, cliquez sur **Ajouter**, puis sur **OK**.   
     ![Capture d’écran montrant l’attribution d’un profil DEP à des appareils iOS](../media/dep-assign-profile.png)

5.  **Distribuer des appareils aux utilisateurs**   
    Vous pouvez maintenant distribuer vos appareils d'entreprise aux utilisateurs. La boîte de dialogue **État d’inscription** pour les appareils gérés indique **Non contacté** tant que l’appareil n’est pas sous tension et n’exécute pas l’Assistant Configuration pour inscrire l’appareil. Quand un appareil iOS est activé, il est inscrit pour être géré par Intune.

