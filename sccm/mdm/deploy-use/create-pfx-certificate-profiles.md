---
title: "Créer des profils de certificat PFX | Microsoft Docs"
description: "Découvrez comment utiliser des fichiers PFX dans System Center Configuration Manager pour générer des certificats spécifiques à l’utilisateur qui prennent en charge l’échange de données chiffrées."
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 26feb0b166beb7e48cb800a5077d00dbc3eec51a
ms.openlocfilehash: 27435316c6e47531ff989bc8956ca0c874131a0e
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Comment créer des profils de certificat PFX dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les profils de certificat fonctionnent avec les services de certificats Active Directory et le rôle Service d’inscription d’appareil réseau pour configurer des certificats d’authentification pour les appareils gérés afin que les utilisateurs puissent accéder en toute transparence aux ressources d’entreprise. Par exemple, vous pouvez créer et déployer des profils de certificat pour fournir les certificats nécessaires aux utilisateurs pour établir des connexions VPN et sans fil.

La section sur les [profils de certificat](../../protect/deploy-use/introduction-to-certificate-profiles.md) fournit des informations générales sur la création et la configuration des profils de certificat. Elle met en évidence des informations spécifiques sur les profils de certificat associés aux certificats PFX.

-  Configuration Manager prend en charge le déploiement de certificats sur différents magasins de certificats, en fonction de la configuration requise, du type d’appareil et du système d’exploitation. Les appareils suivants sont pris en charge lorsqu’ils sont inscrits dans Intune :

 -   iOS  

- Pour connaître les autres conditions préalables, voir [Configuration requise pour les profils de certificat dans System Center Configuration Manager](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Profils de certificat PFX
System Center Configuration Manager vous permet d’importer puis d’approvisionner des fichiers d’échange d’informations personnelles (.pfx) sur les appareils des utilisateurs. Vous pouvez utiliser des fichiers PFX pour générer des certificats spécifiques à l'utilisateur pour prendre en charge l'échange de données chiffrées.

> [!TIP]  
>  Une procédure pas à pas décrivant ce processus est disponible dans [Comment créer et déployer des profils de certificat PFX dans Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Créer et déployer un profil de certificat PFX (Personal Information Exchange)  

### <a name="get-started"></a>Bien démarrer

1.  Dans la console System Center Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , développez **Paramètres de compatibilité**, puis **Accès aux ressources de l'entreprise**, et cliquez sur **Profils de certificat**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un profil de certificat**.

4.  Dans la page **Général** de l'Assistant **Créer un profil de certificat** , spécifiez les informations suivantes :  

    -   **Nom**: entrez un nom unique pour le profil de certificat. Vous pouvez utiliser jusqu'à 256 caractères.  

    -   **Description** : entrez une description qui donne un aperçu du profil de certificat et d’autres informations utiles pour identifier facilement ce profil dans la console System Center Configuration Manager. Vous pouvez utiliser jusqu'à 256 caractères.  

    -   **Spécifiez le type de profil de certificat que vous voulez créer** - Pour les certificats PFX, choisissez :  

        -   **Échange d’informations personnelles - Paramètres PKCS #12 (PFX) - Importation** : sélectionnez cette option pour importer un certificat PFX.  
       

### <a name="import-a-pfx-certificate"></a>Importer un certificat PFX

Pour importer un certificat PFX, vous avez besoin du Kit de développement logiciel (SDK) de Configuration Manager. Les certificats que vous importez pour un utilisateur seront déployés sur tous les appareils inscrits par l’utilisateur.

1. Sur la page **Certificat PFX** de **l’Assistant Créer un profil de certificat**, spécifiez où le certificat sera stocké sur les appareils où vous le déployez :
    -     **Installer dans le module de plateforme sécurisée (TPM) s'il existe**  
    -   **Installer dans le module de plateforme sécurisée (TPM) sinon mettre en échec** 
    -   **Installer dans Windows Hello Entreprise, sinon mettre en échec** 
    -   **Installer dans le fournisseur de stockage de la clé du logiciel** 
2. Cliquez sur **Suivant**. 
3. Sur la page **Plateformes prises en charge** de l’Assistant, sélectionnez les plateformes des appareils où ce certificat sera installé, puis cliquez sur **Suivant**.
4. À l'aide du Kit de développement logiciel (SDK) pour Windows 8.1 disponible à partir du Centre de téléchargement ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525), déployez un script de création de fichier PFX. Le script de création de fichier PFX ajouté dans Configuration Manager 2012 SP2 ajoute une classe SMS_ClientPfxCertificate au kit SDK. Cette classe comprend les méthodes suivantes :  

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

   -   blob\ = objet blob PFX chiffré en base64  
   -   $Password = mot de passe pour le fichier PFX  
   -   $ProfileName = nom du profil PFX  
   -   ComputerName = nom de l'ordinateur hôte   



### <a name="finish-up"></a>Terminer

1.  Cliquez sur **Suivant**, passez en revue la page **Résumé** , puis fermez l'Assistant.  
2.  Le profil de certificat contenant le fichier PFX est désormais disponible à partir de l'espace de travail **Profils de certificat** . 
3.  Pour déployer le profil, dans l’espace de travail **Ressources et conformité**, accédez à **Paramètres de compatibilité** > **Accès aux ressources de l’entreprise** > **Profils de certificat**, cliquez avec le bouton droit sur le certificat requis, puis cliquez sur **Déployer**. 



## <a name="see-also"></a>Voir aussi
La section [Créer un profil de certificat](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) vous guide tout au long des étapes de l’Assistant Créer un profil de certificat.

Pour en savoir plus sur le déploiement des profils de certificat, voir [Déployer des profils dans System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).
