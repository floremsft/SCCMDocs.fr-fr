---
title: "Créer des profils Wi-Fi | System Center Configuration Manager"
description: "Découvrez comment utiliser des profils Wi-Fi dans System Center Configuration Manager pour déployer des paramètres de réseau sans fil pour les utilisateurs de votre organisation."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
caps.latest.revision: 13
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 295ccc2ce7c1dae55c45113cc8ff826e30f7079a


---
# <a name="how-to-create-wi-fi-profiles-in-system-center-configuration-manager"></a>Comment créer des profils Wi-Fi dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Utilisez des profils Wi-Fi dans System Center Configuration Manager pour déployer des paramètres de réseau sans fil pour les utilisateurs de votre organisation. En déployant ces paramètres, il est plus facile pour les utilisateurs de se connecter au Wi-Fi.  

 Par exemple, vous avez installé un nouveau réseau Wi-Fi nommé **Contoso Wi-Fi**. Vous souhaitez maintenant configurer tous les appareils qui exécutent le système d'exploitation iOS avec les paramètres requis pour la connexion à ce réseau. Vous pouvez créer un profil Wi-Fi contenant les paramètres nécessaires pour se connecter au réseau sans fil **Contoso Wi-Fi** . Vous pouvez ensuite déployer ce profil à tous les utilisateurs disposant d'appareils qui exécutent iOS dans votre hiérarchie. Les utilisateurs des appareils iOS voient le réseau de l'entreprise dans la liste des réseaux sans fil et peuvent immédiatement se connecter à ce réseau.  

 Vous pouvez configurer les types d'appareil suivants avec des profils Wi-Fi :  

-   Appareils qui exécutent Windows 8.1 32 bits  

-   Appareils qui exécutent Windows 8.1 64 bits  

-   Appareils qui exécutent Windows RT 8.1  

-   Appareils qui exécutent Windows Phone 8.1  

-   Appareils qui exécutent Windows 10 Desktop ou Mobile  

-   Appareils IPhone qui exécutent iOS 5, iOS 6, iOS 7 et iOS 8  

-   Appareils IPad qui exécutent iOS 5, iOS 6, iOS 7 et iOS 8  

-   Appareils Android qui exécutent la version 4  

> [!IMPORTANT]  
>  Pour déployer des profils sur des appareils Android, iOS, Windows Phone et sur des appareils Windows 8.1 ou version ultérieure inscrits, ces appareils doivent être inscrits dans Microsoft Intune. Pour plus d’informations sur la façon d’inscrire vos appareils, consultez [Inscrire des appareils pour la gestion dans Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).  

 Lorsque vous créez un profil Wi-Fi, vous pouvez inclure un large éventail de paramètres de sécurité. Ceux-ci incluent des certificats pour l’authentification de client et la validation de serveur qui ont été mis en service à l’aide des profils de certificat Configuration Manager. Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  

## <a name="steps-to-create-a-wi-fi-profile"></a>Étapes de création d'un profil Wi-Fi  
 Les étapes suivantes permettent de créer un profil Wi-Fi à l'aide de l' **Assistant Création d'un profil Wi-Fi**.  

-   [Étape 1 : Démarrer l’Assistant Création d’un profil Wi-Fi](#BKMK_Step1)  

-   [Étape 2 : Fournir des informations générales sur le profil Wi-Fi](#BKMK_Step2)  

-   [Étape 3 : Fournir des informations sur le réseau sans fil](#BKMK_Step3)  

-   [Étape 4 : Configurer la sécurité pour le profil Wi-Fi](#BKMK_Step4)  

-   [Étape 5 : Configurer des paramètres avancés pour le profil Wi-Fi](#BKMK_Step5)  

-   [Étape 6 : Configurer les paramètres du proxy pour ce profil Wi-Fi](#BKMK_Step6)  

-   [Étape 7 : Configurer les plateformes prises en charge pour le profil Wi-Fi](#BKMK_Step7)  

-   [Étape 8 : Terminer l'Assistant](#BKMK_Step8)  

##  <a name="a-namebkmkstep1a-step-1-start-the-create-wi-fi-profile-wizard"></a><a name="BKMK_Step1"></a> Étape 1 : Démarrer l’Assistant Création d’un profil Wi-Fi  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , développez **Paramètres de compatibilité**, puis **Accès aux ressources de l'entreprise**, et cliquez sur **Profils Wi-Fi**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un profil Wi-Fi**.  

##  <a name="a-namebkmkstep2a-step-2-provide-general-information-about-the-wi-fi-profile"></a><a name="BKMK_Step2"></a> Étape 2 : Fournir des informations générales sur le profil Wi-Fi  

1.  Dans la page **Général** de l’Assistant Création d’un profil Wi-Fi, entrez un nom unique et une description pour le profil Wi-Fi. Vous pouvez utiliser jusqu'à 256 caractères.  

2.  Si vous souhaitez utiliser les paramètres d’un autre profil Wi-Fi, sélectionnez **Importer un élément de profil Wi-Fi existant à partir d’un fichier**.  

    > [!IMPORTANT]  
    >  Assurez-vous que le profil Wi-Fi que vous importez contient du code XML valide pour un profil Wi-Fi. Configuration Manager ne valide pas le profil lorsque vous importez le fichier.  

3.  Dans  
                            **Gravité de non-compatibilité pour les rapports** : spécifiez le niveau de gravité signalé en cas de non-compatibilité du profil Wi-Fi sur des appareils clients (par exemple, en cas d’échec de l’installation du profil). Les niveaux de gravité disponibles sont les suivants :  

    -   **Aucun** : les ordinateurs qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec pour les rapports Configuration Manager.  

    -   **Informations** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations** pour les rapports Configuration Manager.  

    -   **Avertissement** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement** pour les rapports Configuration Manager.  

    -   **Critique** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager.  

    -   **Critique avec événement** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager. Ce niveau de gravité est également enregistré comme un événement Windows dans le journal des événements des applications.  

##  <a name="a-namebkmkstep3a-step-3-provide-information-about-the-wireless-network"></a><a name="BKMK_Step3"></a> Étape 3 : Fournir des informations sur le réseau sans fil  

1.  Dans la page **Profil Wi-Fi** de l’Assistant Création d’un profil Wi-Fi, spécifiez le nom descriptif de la connexion Internet sans fil (32 caractères maximum). Il s'agit du nom qui sera affiché sur les appareils comme nom de réseau.  

    > [!IMPORTANT]  
    >  Configuration Manager ne prend pas en charge l’utilisation des caractères apostrophe (**â€˜**) ni virgule (**,**) dans le nom du réseau.  

2.  Dans **SSID**, spécifiez le nom (SSID) du réseau sans fil auquel vous souhaitez que les appareils puissent se connecter. Vous pouvez utiliser jusqu'à 32 caractères. Le nom SSID est sensible à la casse, veillez donc à l'entrer exactement comme il est configuré.  

3.  Si vous souhaitez autoriser les appareils à se reconnecter automatiquement au réseau sans fil quand il est à portée, sélectionnez **Me connecter automatiquement lorsque ce réseau est à portée**.  

4.  Si vous souhaitez autoriser les appareils à continuer à rechercher d’autres réseaux sans fil quand ils sont connectés à ce réseau, sélectionnez  
                            **Rechercher d’autres réseaux sans fil tout en étant connecté à ce réseau**.  

5.  Si vous souhaitez autoriser les appareils à se connecter au réseau quand il n’est pas visible dans la liste des réseaux (car il est masqué et ne diffuse pas son nom), sélectionnez **Se connecter quand le réseau ne diffuse pas son nom (SSID)**.  

##  <a name="a-namebkmkstep4a-step-4-configure-security-for-the-wi-fi-profile"></a><a name="BKMK_Step4"></a> Étape 4 : Configurer la sécurité pour le profil Wi-Fi  

> [!IMPORTANT]  
>  Si vous créez un profil Wi-Fi pour la gestion des appareils mobiles locale, la branche CB (Current Branch) de Configuration Manager prend uniquement en charge les configurations de sécurité Wi-Fi suivantes :  
>   
>  Types de sécurité : **WPA2-Entreprise** ou **WPA2-Personnel**  
> Types de chiffrement : **AES** ou **TKIP**  
> Types EAP : **Carte à puce ou autre certificat** ou **PEAP**  

1.  Dans la page **Configuration de la sécurité** de l’Assistant Création d’un profil Wi-Fi, sélectionnez le protocole de sécurité utilisé par le réseau sans fil ou sélectionnez **Aucune authentification (Open)** si le réseau n’est pas sécurisé.  

     Pour les appareils Android uniquement : les types de sécurité **WPA â€“ Personal**, **WPA2 â€“ Personal** et **WEP** ne sont pas pris en charge.  

2.  sélectionnez la méthode de chiffrement utilisée par le réseau sans fil.  

3.  sélectionnez le type EAP qui est utilisé pour l'authentification auprès du réseau sans fil.  

     Pour les appareils Windows Phone uniquement : les types EAP **LEAP** et **EAP-FAST** ne sont pas pris en charge.  

4.  Cliquez sur **Configurer** pour spécifier les propriétés du type EAP sélectionné. Cette option peut ne pas être disponible pour certains types de protocoles EAP sélectionnés.  

    > [!IMPORTANT]  
    >  Lorsque vous cliquez sur **Configurer**, une boîte de dialogue Windows s'ouvre. Pour cette raison, vous devez vous assurer que le système d’exploitation de l’ordinateur qui exécute la console Configuration Manager prend en charge la configuration du type de protocole EAP sélectionné.  
    >   
    >  Pour les appareils iOS, si vous avez choisi une méthode autre qu'EAP pour l'authentification, quelle que soit la méthode choisie, MS-CHAP v2 est utilisé pour la connexion.  

5.  Si vous souhaitez stocker les informations d’identification des utilisateurs pour qu’ils ne soient pas obligés de les entrer à chaque ouverture de session, sélectionnez **Conserver les informations d’identification de l’utilisateur à chaque ouverture de session**.  

### <a name="for-ios-devices-only"></a>Pour les appareils iOS uniquement :  
 configurez les informations pour tous les certificats qui sont requis pour la connexion Wi-Fi. Vous devez configurer le certificat client et le nom du certificat de serveur approuvé ou le certificat racine comme suit :  

-   **Noms de certificat de serveur approuvé** : si le serveur auquel se connecte l’appareil utilise un certificat d’authentification de serveur pour identifier le serveur et sécuriser le canal de communication, entrez le ou les noms sous le nom d’objet de ce certificat ou l’autre nom d’objet de ce certificat. Le ou les noms sont généralement le nom de domaine complet du serveur. Par exemple, si le certificat de serveur est identifié par le nom commun srv1.contoso.com dans l'objet du certificat, entrez **srv1.contoso.com**. Si le certificat de serveur est identifié par plusieurs noms spécifiés dans l'autre nom d'objet, entrez chaque nom, séparé par un point-virgule.  

    > [!TIP]  
    >  Si le certificat client sélectionné pour le protocole EAP ou pour l'authentification client d'un appareil iOS est utilisé à des fins d'authentification sur un serveur RADIUS, tel qu'un serveur exécutant NPS, l'autre nom de l'objet doit être défini sur le nom d'utilisateur principal.  

-   **Sélectionner des certificats racines pour la validation du serveur**: si le serveur auquel se connecte l’appareil utilise un certificat d’authentification de serveur non approuvé par l’appareil, sélectionnez le profil de certificat qui contient le certificat racine pour le certificat de serveur pour créer une chaîne de certificats de confiance sur l’appareil.  

-   **Sélectionner un certificat client pour l'authentification du client**: si le serveur ou l'appareil réseau requiert un certificat client pour authentifier l'appareil de connexion, sélectionnez le profil de certificat qui contient le certificat d'authentification du client.  

> [!NOTE]  
>  Pour pouvoir sélectionner le certificat racine et le certificat client, vous devez tout d'abord les configurer et les déployer comme un profil de certificat. Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  

##  <a name="a-namebkmkstep5a-step-5-configure-advanced-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step5"></a> Étape 5 : Configurer des paramètres avancés pour le profil Wi-Fi  
 Sur la page **Paramètres avancés** de l'Assistant Création d'un profil Wi-Fi, spécifiez des paramètres avancés pour le profil Wi-Fi, tels que le mode d'authentification, les options d'authentification unique et la conformité aux normes FIPS (Federal Information Processing Standards). Pour plus d’informations sur ces options, voir la documentation de Windows.  

> [!NOTE]  
>  Les paramètres avancés peuvent varier ou ne pas être disponibles selon les options sélectionnées sur la page **Configuration de la sécurité** de l'Assistant.  

##  <a name="a-namebkmkstep6a-step-6-configure-proxy-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step6"></a> Étape 6 : Configurer les paramètres du proxy pour ce profil Wi-Fi  

1.  Sur la page **Paramètres proxy** de l'Assistant Création d'un profil Wi-Fi, activez la case à cocher **Configurer les paramètres du proxy pour ce profil Wi-Fi** si votre connexion Wi-Fi utilise un serveur proxy.  

2.  Spécifiez des détails sur votre serveur proxy et ses paramètres. Pour plus d'informations, consultez la documentation de Windows Server.  

##  <a name="a-namebkmkstep7a-step-7-configure-supported-platforms-for-the-wi-fi-profile"></a><a name="BKMK_Step7"></a> Étape 7 : Configurer les plateformes prises en charge pour le profil Wi-Fi  
 Sur la page **Plateformes prises en charge** de l'Assistant Création d'un profil Wi-Fi, sélectionnez les systèmes d'exploitation dans lesquels vous voulez installer le profil Wi-Fi. Sinon, cliquez sur **Sélectionner tout** pour installer le profil Wi-Fi sur tous les systèmes d'exploitation disponibles.  

##  <a name="a-namebkmkstep8a-step-8-complete-the-wizard"></a><a name="BKMK_Step8"></a> Étape 8 : Terminer l'Assistant  
 Dans la page **Résumé** de l'Assistant, passez en revue les actions qui seront exécutées, puis terminez l'Assistant. Le nouveau profil Wi-Fi figure dans le nœud **Profils Wi-Fi** dans l'espace de travail **Ressources et Conformité** .  

 Pour plus d’informations sur le déploiement du profil Wi-Fi, consultez [Comment déployer des profils Wi-Fi dans System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  



<!--HONumber=Nov16_HO1-->


