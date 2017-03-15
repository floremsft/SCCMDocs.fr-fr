---
title: "Créer des profils de certificat PFX | Microsoft Docs"
description: "Découvrez comment utiliser des fichiers PFX dans System Center Configuration Manager pour générer des certificats spécifiques à l’utilisateur qui prennent en charge l’échange de données chiffrées."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: eddecee8886296fb6132d7477afebbfc7fd280d1
ms.lasthandoff: 03/06/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Comment créer des profils de certificat PFX dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les profils de certificat fonctionnent avec les services de certificats Active Directory et le rôle Service d’inscription d’appareil réseau pour configurer des certificats d’authentification pour les appareils gérés afin que les utilisateurs puissent accéder en toute transparence aux ressources d’entreprise. Par exemple, vous pouvez créer et déployer des profils de certificat pour fournir les certificats nécessaires aux utilisateurs pour établir des connexions VPN et sans fil.

La section [Présentation des profils de certificat dans System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md) fournit des informations générales sur la création et la configuration des profils de certificat. Elle met en évidence des informations spécifiques sur les profils de certificat associés à la gestion des appareils mobiles.

- Les profils de certificat permettent l’inscription et le renouvellement de certificats auprès d’une autorité de certification d’entreprise pour les appareils exécutant iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop et Mobile, et Android. Ces certificats peuvent ensuite être utilisés pour les connexions VPN et Wi-Fi.

-  Pour pouvoir déployer des profils de certificat utilisant SCEP, vous devez installer un module de stratégie pour NDES sur un serveur exécutant Windows Server 2012 R2 avec le rôle de services de certificats Active Directory et un service NDES accessible aux appareils qui nécessitent les certificats. Pour les appareils inscrits par Microsoft Intune, le service NDES doit être accessible sur Internet, par exemple dans un sous-réseau filtré (également appelé DMZ).

-  Configuration Manager prend en charge le déploiement de certificats sur différents magasins de certificats, en fonction de la configuration requise, du type d’appareil et du système d’exploitation. Les appareils et les systèmes d'exploitation suivants sont pris en charge :
 -   Windows RT 8.1  
 -   Windows 8.1  
 -   Windows Phone 8.1  
 -   Windows 10 Desktop et Mobile  
 -   iOS  
 -   Android  
 > [!IMPORTANT]  
 >  Pour déployer des profils sur des appareils Android, iOS, Windows Phone et sur des appareils Windows 8.1 ou version ultérieure inscrits, ces appareils doivent être [inscrits dans Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).   

- Pour connaître les autres conditions préalables, voir [Configuration requise pour les profils de certificat dans System Center Configuration Manager](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Profils de certificat PFX
System Center Configuration Manager vous permet de configurer des fichiers d'échange d'informations personnelles (.pfx) sur les appareils des utilisateurs. Vous pouvez utiliser des fichiers PFX pour générer des certificats spécifiques à l'utilisateur pour prendre en charge l'échange de données chiffrées. Vous pouvez créer des certificats PFX dans Configuration Manager ou les importer. Avec System Center Configuration Manager, vous pouvez déployer des certificats PFX nouveaux ou importés sur des appareils iOS, Android et Windows 10. Vous pouvez ensuite déployer ces fichiers sur plusieurs appareils pour prendre en charge la communication PKI basée sur l'utilisateur.  

> [!TIP]  
>  Une procédure pas à pas décrivant ce processus est disponible dans [Comment créer et déployer des profils de certificat PFX dans Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

### <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Créer et déployer un profil de certificat PFX (Personal Information Exchange)  

1.  Dans la console System Center Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , développez **Paramètres de compatibilité**, puis **Accès aux ressources de l'entreprise**, et cliquez sur **Profils de certificat**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un profil de certificat**. L'Assistant **Créer un profil de certificat** s'ouvre.  

4.  Dans la page **Général** de l'Assistant **Créer un profil de certificat** , spécifiez les informations suivantes :  

    -   **Nom**: entrez un nom unique pour le profil de certificat. Vous pouvez utiliser jusqu'à 256 caractères.  

    -   **Description** : entrez une description qui donne un aperçu du profil de certificat et d’autres informations utiles pour identifier facilement ce profil dans la console System Center Configuration Manager. Vous pouvez utiliser jusqu'à 256 caractères.  

    -   **Spécifiez le type de profil de certificat que vous voulez créer**: choisissez un des types de profil de certificat suivants :  

        -   **Certificat d’Autorité de certification approuvé**: sélectionnez ce type de profil de certificat si vous souhaitez déployer un certificat d’autorité de certification racine ou intermédiaire approuvé pour former une chaîne d’approbation des certificats quand l’utilisateur ou l’appareil doit authentifier un autre appareil. Par exemple, l'appareil peut être un serveur RADIUS (Remote Authentication Dial-In User Service) ou un serveur VPN (réseau privé virtuel). Vous devez également configurer un profil de certificat d'Autorité de certification approuvé pour pouvoir créer un profil de certificat SCEP. Dans ce cas, le certificat d'Autorité de certification approuvé doit être le certificat racine approuvé pour l'Autorité de certification qui émet le certificat à l'utilisateur ou à l'appareil.  

        -   **Paramètres du protocole SCEP (Simple Certificate Enrollment Protocol)**: sélectionnez ce type de profil de certificat pour demander un certificat pour un appareil ou un utilisateur à l’aide du protocole SCEP et du service de rôle du service d’inscription d’appareils réseau.  

        -   **Échange d’informations personnelles -- Paramètres PKCS #12 (PFX) -- Importation** : sélectionnez cette option pour importer un certificat PFX.  

5.  Dans la fenêtre **Propriétés du certificat** de l'Assistant **Créer un profil de certificat** , spécifiez où le certificat PFX sera stocké sur les appareils ciblés.  

    -   **Installer dans le module de plateforme sécurisée (TPM) s'il existe**  

    -   **Installer dans le module de plateforme sécurisée (TPM) sinon mettre en échec**  

    -   **Installer dans le fournisseur de stockage de la clé du logiciel**  

     Cliquez sur **Suivant**.  

6.  Dans la fenêtre **Plateformes prises en charge** de l'Assistant **Créer un profil de certificat** , spécifiez les systèmes d'exploitation ou les plateformes qui peuvent recevoir le fichier PFX importé.  

    -   **Windows 10**  

    -   **iPhone**  

    -   **iPad**  

    -   **Android**  

7.  Cliquez sur **Suivant**, passez en revue la page **Résumé** , puis fermez l'Assistant.  

8.  Le profil de certificat contenant le fichier PFX est désormais disponible à partir de l'espace de travail **Profils de certificat** . Dans la console **Ressources et Conformité** , accédez à **Paramètres de compatibilité** > **Accès aux ressources de l'entreprise** > **Profils de certificat** et cliquez avec le bouton droit pour déployer le nouveau certificat dans Regroupements d'utilisateurs.  

9. À l'aide du Kit de développement logiciel (SDK) pour Windows 8.1 disponible à partir du Centre de téléchargement ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525), déployez un script de création de fichier PFX. Le script de création de fichier PFX ajouté dans Configuration Manager 2012 SP2 ajoute une classe SMS_ClientPfxCertificate au kit SDK. Cette classe comprend les méthodes suivantes :  

    -   ImportForUser  

    -   DeleteForUser  

     Exemple de script :  

    ```  
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  

    ```  

     Les variables de script suivantes doivent être modifiées pour votre script :  

    -   <blob\> = objet blob PFX chiffré en base64  

    -   $Password = mot de passe pour le fichier PFX  

    -   $ProfileName = nom du profil PFX  

    -   ComputerName = nom de l'ordinateur hôte  

### <a name="see-also"></a>Voir aussi
La section [Créer un profil de certificat](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) vous guide tout au long des étapes de l’Assistant Créer un profil de certificat.

Pour en savoir plus sur le déploiement des profils de certificat, voir [Déployer des profils dans System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

