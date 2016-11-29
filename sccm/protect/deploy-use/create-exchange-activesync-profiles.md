---
title: "Créer des profils de messagerie Exchange ActiveSync | System Center Configuration Manager"
description: "Découvrez comment créer et configurer des profils de messagerie dans System Center Configuration Manager qui fonctionnent avec Microsoft Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 15f0fd50-e196-44e5-b435-234d7ff6a5cd
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 613ed15742322e2eb90eec3c9f493e3b1755d93a


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Profils de messagerie Exchange ActiveSync dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les profils de messagerie fonctionnent avec Microsoft Intune pour vous permettre de configurer des appareils avec des profils de messagerie et des restrictions en utilisant Exchange ActiveSync. Cela permet à vos utilisateurs d'accéder à la messagerie d'entreprise sur leurs appareils avec une installation minimale requise de leur part.  

 Vous pouvez configurer les types d'appareils suivants avec des profils de messagerie :  

-   Appareils exécutant Windows Phone 8  

-   Appareils exécutant Windows Phone 8.1  

-   Appareils exécutant Windows 10 Mobile  

-   Appareils iPhone exécutant iOS 5, iOS 6, iOS 7 et iOS 8  

-   Appareils iPad exécutant iOS 5, iOS 6, iOS 7 et iOS 8  

> [!IMPORTANT]  
>  Pour déployer des profils sur des appareils iOS, Android Samsung KNOX, Windows Phone, Windows 8.1 ou Windows 10, ces appareils doivent être inscrits auprès de Microsoft Intune. Pour plus d'informations sur la façon d'inscrire vos appareils, consultez [Gérer les appareils mobiles avec Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 En plus de configurer un compte de messagerie sur l'appareil, vous pouvez également configurer des paramètres de synchronisation pour les contacts, les calendriers et les tâches.  

 Quand vous créez un profil de messagerie, vous pouvez inclure de nombreux paramètres de sécurité, notamment des certificats pour l’identité, le chiffrement et la signature configurés à l’aide de profils de certificat System Center Configuration Manager. Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).    


## <a name="create-a-new-exchange-activesync-email-profile"></a>Créer un profil de messagerie Exchange ActiveSync  

Démarrer l’Assistant Création d’un profil de messagerie Exchange ActiveSync  

1.  Dans la console System Center Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , développez **Paramètres de compatibilité**, puis **Accès aux ressources de l'entreprise**et cliquez sur **Profils de messagerie**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un profil Exchange ActiveSync**. 

4.  Suivez les instructions de l’Assistant   

### <a name="to-configure-exchange-activesync-settings-for-the-exchange-activesync-email-profile"></a>Pour configurer les paramètres Exchange ActiveSync du profil de messagerie Exchange ActiveSync  

1.  Dans la page **Exchange ActiveSync** de l'Assistant Création d'un profil de messagerie Exchange ActiveSync, indiquez les informations suivantes :  

    -   **Hôte Exchange ActiveSync :** Spécifiez le nom d’hôte de l’instance Exchange Server d’entreprise qui héberge les services Exchange ActiveSync.  

    -   **Nom du compte :** Spécifiez le nom d’affichage du compte de messagerie tel qu’il sera affiché aux utilisateurs sur leurs appareils.  

    -   **Nom d’utilisateur du compte :** Choisissez comment le nom d’utilisateur du compte de messagerie est configuré sur les appareils clients. Vous pouvez sélectionner l'une des options suivantes dans la liste déroulante :  

        -   **Nom principal de l'utilisateur** : utiliser le nom principal complet de l'utilisateur pour se connecter à Exchange.  

        -   Utiliser**sAMAccountName**   

        -   **Adresse SMTP principale** : utiliser l'adresse SMTP principale des utilisateurs pour se connecter à Exchange.  

    -   **Adresse de messagerie :** Sélectionnez la façon dont l’adresse de messagerie de l’utilisateur est générée sur chaque ordinateur client. Vous pouvez sélectionner l'une des options suivantes dans la liste déroulante :  

        -   **Adresse SMTP principale** : utiliser l'adresse SMTP principale des utilisateurs pour se connecter à Exchange.  

        -   **Nom principal de l'utilisateur** : utiliser le nom principal complet de l'utilisateur comme adresse de messagerie.  

    -   **Domaine du compte :** Choisissez l’une des options suivantes :  

        -   **Obtenir à partir d'Active Directory**  

        -   **Personnalisé**  

         Ce champ s'applique uniquement si **sAMAccountName** est sélectionné dans la liste déroulante **Nom d'utilisateur du compte** .  

    -   **Méthode d’authentification :** Choisissez une des méthodes d’authentification suivantes pour authentifier la connexion à Exchange ActiveSync :  

        -   **Certificats** : un certificat d'identité est utilisé pour authentifier la connexion Exchange ActiveSync.  

        -   **Nom d'utilisateur et mot de passe** : l'utilisateur de l'appareil doit fournir un mot de passe pour se connecter à Exchange ActiveSync (le nom d'utilisateur est configuré dans le cadre du profil de messagerie).  

    -   **Certificat d’identité :** Cliquez sur **Sélectionner** , puis sélectionnez un certificat à utiliser pour l’identité.  

        > [!NOTE]  
        >  Avant de pouvoir sélectionner le certificat d'identité, vous devez d'abord le configurer en tant que profil de certificat SCEP (Simple Certificate Enrollment Protocol). Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Cette option est disponible uniquement si vous avez sélectionné **Certificats** sous **Méthode d'authentification**.  

    -   **Utiliser S/MIME** : envoyer le courrier électronique sortant à l'aide du chiffrement S/MIME. Cette option s'applique aux appareils iOS uniquement.  

    -   **Certificats de chiffrement :** Cliquez sur **Sélectionner** , puis sélectionnez un certificat à utiliser pour le chiffrement. Cette option s'applique aux appareils iOS uniquement.  

        > [!NOTE]  
        >  Avant de pouvoir sélectionner le certificat de chiffrement, vous devez d'abord le configurer en tant que profil de certificat SCEP (Simple Certificate Enrollment Protocol). Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Cette option est disponible uniquement si vous avez sélectionné **Utiliser S/MIME**.  

    -   **Certificats de signature :** Cliquez sur **Sélectionner** , puis sélectionnez un certificat à utiliser pour la signature. Cette option s'applique aux appareils iOS uniquement.  

        > [!NOTE]  
        >  Avant de pouvoir sélectionner le certificat de signature, vous devez d'abord le configurer en tant que profil de certificat SCEP (Simple Certificate Enrollment Protocol). Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Cette option est disponible uniquement si vous avez sélectionné **Utiliser S/MIME**.  

###   <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>configurer les paramètres de synchronisation du profil de messagerie Exchange ActiveSync.  

1.  Dans la page **Configurer les paramètres de synchronisation** de l'Assistant Création d'un profil de messagerie Exchange ActiveSync, indiquez les informations suivantes :  

    -   **Planification :** Sélectionnez la planification selon laquelle les appareils vont synchroniser les données d’Exchange Server. Cette option s'applique uniquement aux appareils Windows Phone. Choisissez parmi :  

        -   **Non configuré** : aucun calendrier de synchronisation n'est appliqué. Cela permet aux utilisateurs de configurer leur propre calendrier de synchronisation.  

        -   **À mesure que les messages arrivent** : les données telles que les messages électroniques et les éléments de calendrier sont automatiquement synchronisées à la réception.  

        -   **15 minutes** : les données telles que les messages électroniques et les éléments de calendrier sont automatiquement synchronisées toutes les 15 minutes.  

        -   **30 minutes** : les données comme les messages électroniques et les éléments de calendrier sont automatiquement synchronisées toutes les 30 minutes.  

        -   **60 minutes** : les données comme les messages électroniques et les éléments de calendrier sont automatiquement synchronisées toutes les 60 minutes.  

        -   **Manuel** : la synchronisation doit être lancée manuellement par l'utilisateur de l'appareil.  

    -   **Nombre de jours de courrier électronique à synchroniser :** Dans la liste déroulante, sélectionnez le nombre de jours de courrier électronique à synchroniser. Choisissez l'une des valeurs suivantes :  

        -   **Non configuré** : le paramètre n'est pas appliqué. Cela permet aux utilisateurs de configurer la quantité de courrier électronique téléchargé sur leur appareil.  

        -   **Illimité** : synchroniser tous le courrier électronique disponible.  

        -   **1 jour**  

        -   **3 jours**  

        -   **1 semaine**  

        -   **2 semaines**  

        -   **1 mois**  

    -   **Autoriser le déplacement des messages vers d'autres comptes de messagerie** : sélectionnez cette option pour permettre aux utilisateurs de déplacer les messages électroniques entre les différents comptes configurés sur l'appareil. Cette option s'applique aux appareils iOS uniquement.  

    -   **Autoriser l'envoi de courrier depuis des applications tierces** : sélectionnez cette option pour autoriser les utilisateurs à envoyer du courrier électronique à partir de certaines applications de messagerie tierces non définies par défaut. Cette option s'applique aux appareils iOS uniquement.  

    -   **Synchroniser les adresses de messagerie récemment utilisées** : sélectionnez cette option pour synchroniser la liste des adresses de messagerie qui ont été récemment utilisées sur l'appareil. Cette option s'applique aux appareils iOS uniquement.  

    -   **Utiliser SSL** : sélectionnez cette option pour utiliser une communication SSL (Secure Sockets Layer) pour l'envoi et la réception des messages électroniques, et pour communiquer avec le serveur Exchange.  

    -   **Type de contenu à synchroniser :** Sélectionnez les types de contenu à synchroniser avec les appareils. Cette option s'applique uniquement aux appareils Windows Phone. Choisissez parmi :  

        -   **Courrier électronique**  

        -   **Contacts**  

        -   **Calendrier**  

        -   **Tâches**  

###  <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>spécifier les plateformes prises en charge pour le profil de messagerie Exchange ActiveSync.  
 
1.  Dans la page **Plateformes prises en charge** de l'Assistant Création d'un profil de messagerie Exchange ActiveSync, sélectionnez les systèmes d'exploitation sur lesquels le profil de messagerie sera installé ou cliquez sur **Sélectionner tout** pour installer le profil de messagerie sur tous les systèmes d'exploitation disponibles.  

2.  Effectuez toutes les étapes de l'Assistant.

Pour plus d’informations sur le déploiement des profils de messagerie Exchange ActiveSync, consultez [Guide pratique pour déployer des profils dans System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  



<!--HONumber=Nov16_HO1-->


