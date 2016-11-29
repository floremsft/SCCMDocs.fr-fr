---
title: "Comment créer des profils VPN dans System Center Configuration Manager"
description: "Découvrez comment créer des profils VPN dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: 15
caps.handback.revision: 0
ms.author: nbigman
ms.manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: e215b33ca24370ddd0e1b892d6ebe559023852a2
ms.openlocfilehash: ccea5cb46bf69dbb88f6fcb217a73c7939be0b02


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Comment créer des profils VPN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


> [!NOTE]  
>
> - Pour plus d’informations sur les types de connexion disponibles pour les différentes plateformes d’appareils, consultez [Profils VPN dans System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  
> - Pour les connexions VPN tierces, distribuez l’application VPN avant de déployer le profil VPN. Si vous ne déployez pas l’application, les utilisateurs sont invités à le faire quand ils tentent de se connecter au VPN. Pour découvrir comment déployer des applications, consultez [Déployer des applications avec System Center Configuration Manager](../../apps/deploy-use/deploy-applications).

### <a name="start-the-create-vpn-profile-wizard"></a>Démarrer l'Assistant Création d'un profil VPN  

1.  Dans la console System Center Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l’espace de travail **Ressources et Conformité** de la console System Center Configuration Manager, développez **Paramètres de compatibilité**, **Accès aux ressources de l’entreprise**, puis cliquez sur **Profils VPN**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un profil VPN**.  

### <a name="provide-general-information-about-the-vpn-profile"></a>Fournir des informations générales sur le profil VPN  

1.  Sur la page **Général** de l' **Assistant Création d'un profil VPN**, spécifiez les informations suivantes :  

    -   **Nom** : entrez un nom unique pour le profil VPN (jusqu'à 256 caractères).  

        > [!IMPORTANT]  
        >  N’utilisez pas les caractères \\/:*?<>&#124;, ou le caractère espace dans le nom du profil VPN, car ces caractères ne sont pas pris en charge par le profil VPN de Windows Server.  

    -   **Description** : entrez une description pour vous aider à trouver le profil dans la console System Center Configuration Manager (jusqu’à 256 caractères).  

    -   **Importer un élément de profil VPN existant à partir d’un fichier** : sélectionnez cette option pour afficher la page **Importer un profil VPN**. Dans cette page, vous pouvez importer des informations de profil VPN qui ont été précédemment exportées vers un fichier XML (systèmes d'exploitation Windows 8.1 et Windows RT uniquement).  

### <a name="provide-connection-information-for-the-vpn-profile"></a>Fournir des informations de connexion pour le profil VPN  

1.  Dans la page **Connexion** de l'Assistant, spécifiez les informations suivantes :  

    -   **Type de connexion :** dans la liste déroulante, sélectionnez le type de connexion pour la connexion VPN. Vous pouvez choisir parmi les types de connexions dans le tableau suivant qui présente les plateformes prises en charge.  

        > [!IMPORTANT]  
        >  Pour pouvoir utiliser les profils VPN déployés sur un appareil, vous devez installer les applications VPN tierces dont vous avez besoin. Vous pouvez vous aider des informations contenues dans la rubrique [Comment créer des applications avec System Center Configuration Manager](../../apps/deploy-use/create-applications.md) pour déployer l’application à l’aide de System Center Configuration Manager.  

    -   **Liste de serveurs :** cliquez sur **Ajouter** pour ajouter un nouveau serveur à utiliser pour la connexion VPN. Selon le type de connexion, vous pouvez ajouter un ou plusieurs serveurs VPN et également indiquer quel serveur sera le serveur par défaut.  

        > [!NOTE]  
        >  Les appareils qui exécutent iOS ne prennent pas en charge l'utilisation de plusieurs serveurs VPN. Si vous configurez plusieurs serveurs VPN et que vous déployez le profil VPN sur un appareil iOS, seul le serveur par défaut sera utilisé.  

     Des options supplémentaires dans le tableau suivant peuvent s'afficher, selon le type de connexion que vous avez sélectionné. Pour plus d'informations, consultez la documentation de votre serveur VPN.  

    |Option|Plus d'informations|Type de connexion|  
    |------------|----------------------|---------------------|  
    |**Domaine**|Spécifiez le nom du domaine d'authentification que vous souhaitez utiliser. Un domaine d'authentification est un regroupement de ressources d'authentification utilisé par le type de connexion Pulse Secure.|Pulse Secure|  
    |**Rôle**|Spécifiez le nom du rôle d'utilisateur qui a accès à cette connexion.|Pulse Secure|  
    |**Groupe de connexion ou domaine**|Spécifiez le nom du groupe de connexion ou domaine auquel vous souhaitez vous connecter.|Dell SonicWALL Mobile Connect|  
    |**Empreinte digitale**|Spécifiez une chaîne, par exemple « Code d'empreinte digitale Contoso », qui sera utilisée pour vérifier que le serveur VPN est digne de confiance.<br /><br /> Une empreinte digitale peut être :<br /><br /> - envoyée au client pour qu’il sache qu’il peut approuver n’importe quel serveur présentant cette même empreinte lors de la connexion ;<br /><br /> - si l’appareil n’a pas encore l’empreinte digitale, il invite l’utilisateur à approuver le serveur VPN auquel il se connecte en affichant l’empreinte digitale (l’utilisateur vérifie l’empreinte manuellement et clique sur Confiance pour se connecter).|Check Point Mobile VPN|  
    |**Envoyer tout le trafic réseau via la connexion VPN**|Si cette option n'est pas sélectionnée, vous pouvez spécifier des itinéraires supplémentaires pour la connexion (pour les types de connexion **Microsoft SSL (SSTP)**, **Microsoft Automatic**, **IKEv2**, **PPTP** et **L2TP** ). On appelle cela le tunneling VPN ou fractionné.<br /><br /> Seules les connexions au réseau d'entreprise sont envoyées via un tunnel VPN. La tunnelisation VPN n'est pas utilisée quand vous vous connectez à des ressources sur Internet.|Tout|  
    |**Suffixe DNS spécifique à la connexion**|Vous pouvez également spécifier le suffixe DNS spécifique à la connexion pour la connexion.|- <br />                            Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**Ignorer VPN en cas de connexion à un réseau Wi-Fi d'entreprise**|Indique que la connexion VPN n'est pas utilisée quand l'appareil est connecté au réseau Wi-Fi d'entreprise.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - Client F5 Edge<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
    |**Ignorer le VPN en cas de connexion à un réseau Wi-Fi domestique**|Indique que la connexion VPN n'est pas utilisée quand l'appareil est connecté à un réseau Wi-Fi domestique.|Tout|  
    |**Par VPN d'application (iOS 7 et versions ultérieures, Mac OS X 10.9 et versions ultérieures)**|Sélectionnez cette option si vous souhaitez associer cette connexion VPN à une application iOS pour que la connexion s'ouvre quand l'application est exécutée. Vous pouvez associer le profil VPN à une application lors de son déploiement.|- <br />                        Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - Client F5 Edge<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
    |**Code XML personnalisé (facultatif)**|Vous permet de spécifier des commandes XML personnalisées qui configurent la connexion VPN.<br /><br /> Exemples :<br /><br /> Pour **Pulse Secure**:<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> Pour **CheckPoint VPN Mobile**:<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> Pour **Dell SonicWALL Mobile Connect**:<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> Pour **Client F5 Edge**:<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> Pour plus d'informations sur la façon d'écrire des commandes XML personnalisées, reportez-vous à la documentation du VPN de chaque fabricant.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - Client F5 Edge<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  

####   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Fonctionnalités VPN Windows 10, disponibles quand vous utilisez Configuration Manager avec Intune  


> [!NOTE]  
> Le nom d’un profil VPN qui utilise des fonctionnalités VPN Windows 10 ne peut pas être au format Unicode ni contenir des caractères spéciaux.


|Option|Plus d'informations|Type de connexion|  
|------------|----------------------|---------------------|  
|**Ignorer VPN en cas de connexion à un réseau Wi-Fi d'entreprise**|Indique que la connexion VPN n'est pas utilisée quand l'appareil est connecté au réseau Wi-Fi d'entreprise. Entrez le nom du réseau approuvé, qui sera utilisé pour déterminer si l’appareil est connecté au réseau d’entreprise.|Tout|  
|**Règles de trafic réseau**|Définissez les protocoles, les ports locaux et distants et les plages d’adresses à activer pour la connexion VPN.<br /><br /> **Remarque :** si vous ne créez pas de règle de trafic réseau, l’ensemble des protocoles, ports et plages d’adresses sont activés. Dès lors que vous créez une règle, seuls les protocoles, les ports et les plages d’adresses que vous spécifiez dans cette règle ou dans des règles supplémentaires sont utilisés par la connexion VPN.|Tout|  
|**Itinéraires**|Itinéraires qui utilisent la connexion VPN. Notez que la création de plus de 60 itinéraires peut entraîner l’échec de la stratégie. |Tout|  
|**Serveurs DNS**|Serveurs DNS qui sont utilisés par la connexion VPN une fois la connexion établie.|Tout|  
|**Applications qui se connectent automatiquement au VPN**|Vous pouvez ajouter des applications, ou importer des listes d’applications, qui utilisent automatiquement la connexion VPN. Le type d’application détermine l’identificateur de l’application. Pour une application de bureau, fournissez le chemin de fichier de l’application. Pour une application universelle, indiquez le nom de la famille de packages (PFN). Pour savoir comment rechercher le nom PFN pour une application, consultez [Rechercher le nom de la famille de packages pour le VPN par application](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |Tout|

> [!IMPORTANT]
> Nous vous recommandons de sécuriser toutes les listes d’applications associées que vous compilez à utiliser dans la configuration du VPN par application. Si un utilisateur non autorisé modifie votre liste et que vous l’importez dans la liste d’applications du VPN par application, vous allez potentiellement autoriser l’accès au VPN à des applications qui ne doivent pas avoir accès. Une façon de sécuriser les listes d’applications consiste à utiliser une liste de contrôle d’accès (ACL).


### <a name="configure-the-authentication-method-for-the-vpn-profile"></a>Configurer la méthode d'authentification pour le profil VPN  

1.  Dans la page **Méthode d'authentification** , spécifiez les informations suivantes :  

    -   **Méthode d'authentification :** dans la liste déroulante, sélectionnez la méthode d'authentification qui sera utilisée par la connexion VPN. Les éléments dans la liste déroulante peuvent varier selon le type de connexion que vous avez précédemment sélectionné. Les méthodes d'authentification disponibles et les types de connexion pris en charge sont répertoriés dans le tableau suivant :  

        |Méthode d'authentification|Types de connexion pris en charge|  
        |---------------------------|--------------------------------|  
        |**Certificats**<br /><br /> **Remarque :** si le certificat client est utilisé pour l’authentification auprès d’un serveur RADIUS, tel un serveur NPS (Network Policy Server), l’autre nom de l’objet dans le certificat doit correspondre au nom d’utilisateur principal (UPN).|- <br />                            Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - Client F5 Edge<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Nom d'utilisateur et mot de passe**|- <br />                            Pulse Secure<br /><br /> - Client F5 Edge<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**Microsoft PEAP (Protected EAP)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Mot de passe sécurisé Microsoft (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Carte à puce ou autre certificat**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|-  Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** (iOS uniquement)|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Utiliser des certificats d’ordinateur**|IKEv2|  

         Selon les options que vous sélectionnez, vous devrez peut-être spécifier d'autres informations, par exemple :  

        -   **Conserver les informations d'identification de l'utilisateur à chaque connexion**: Sélectionnez cette option pour vous assurer que les informations d'identification sont mémorisées, pour que l'utilisateur n'ait pas à les entrer chaque fois qu'une connexion est établie.  

        -   **Sélectionnez un certificat client pour l'authentification du client** : sélectionnez le certificat SCEP client que vous avez créé précédemment et qui sera utilisé pour authentifier la connexion VPN. Pour plus d’informations sur l’utilisation de profils de certificat dans System Center Configuration Manager, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  

            > [!NOTE]  
            >  Pour les appareils iOS, le profil SCEP que vous sélectionnez sera incorporé au profil VPN. Pour les autres plateformes, une règle de mise en application est ajoutée pour s'assurer que le profil VPN n'est pas installé si le certificat n'est pas présent ou non conforme.  
            >   
            >  Si le certificat SCEP que vous spécifiez n’est pas conforme ou n’a pas été déployé, le profil VPN n’est pas installé sur l’appareil.
            >  
            >  Les appareils qui exécutent iOS prennent uniquement en charge RSA SecurID et MSCHAP v2 comme méthode d’authentification quand le type de connexion est PPTP. Pour éviter toute erreur, déployez un profil VPN PPTP distinct sur les appareils qui exécutent iOS.  

               - Paramètres **Accès conditionnel** et **Domaine principal de la Protection des données d’entreprise**, pris en charge uniquement quand vous utilisez Configuration Manager sans Intune, accessibles en sélectionnant **Advanced** (Avancé).
        
        ![Configurer l’accès conditionnel pour VPN](../media/vpn-conditional-access.png)

        -   Pour certaines méthodes d’authentification, vous pouvez cliquer sur **Configurer** pour ouvrir la boîte de dialogue Propriétés de Windows (si la version de Windows sur laquelle vous exécutez la console System Center Configuration Manager prend en charge cette méthode d’authentification), dans laquelle vous pouvez configurer les propriétés de la méthode d’authentification.  

### <a name="configure-proxy-settings-for-the-vpn-profile"></a>Configurer des paramètres proxy pour le profil VPN  

1.  Sur la page **Paramètres du proxy** de l' **Assistant Création d'un profil VPN**, activez la case à cocher **Configurer les paramètres du proxy pour ce profil VPN** si votre connexion VPN utilise un serveur proxy.  

2.  Spécifiez des détails sur votre serveur proxy et ses paramètres. Pour plus d’informations, consultez la documentation de Windows Server.  

> [!NOTE]  
>  Sur les ordinateurs Windows 8.1, le profil VPN n’affiche pas les informations de proxy tant que vous n’êtes pas connecté au VPN avec cet ordinateur.  


### <a name="configure-further-dns-settings-if-required"></a>Configurer les paramètres DNS supplémentaires (si nécessaire)  
 Dans la page **Configurer une connexion VPN automatique** de l'Assistant, vous pouvez configurer les paramètres suivants :  

-   **Activer VPN à la demande** : sélectionnez cette option si vous souhaitez configurer d’autres paramètres DNS dans cette page de l’Assistant pour les appareils Windows Phone 8.1.

> [!Note]  
> Ce paramètre s’applique uniquement aux appareils Windows Phone 8.1 et ne doit être activé que sur les profils VPN destinés à être déployés sur des appareils Windows Phone 8.1.


-   Liste de suffixes DNS (pour les appareils Windows Phone 8.1 uniquement) : configure les domaines qui établiront une connexion VPN. Pour chaque domaine que vous spécifiez, ajoutez le suffixe DNS, l'adresse du serveur DNS et l'une des actions à la demande suivantes :  

    -   **Ne jamais établir** : ne jamais ouvrir de connexion VPN  

    -   **Établir si nécessaire** : ouvrir une connexion VPN uniquement si l’appareil doit se connecter aux ressources  

    -   **Toujours établir** : toujours ouvrir la connexion VPN  

-   **Fusionner** : copie tous les suffixes DNS que vous avez configurés dans la **Liste de réseaux approuvés**.  

-   **Liste de réseaux approuvés** (pour les appareils Windows Phone 8.1 uniquement) : spécifiez un suffixe DNS sur chaque ligne. Si l'appareil se trouve sur un réseau approuvé, la connexion VPN n'est pas ouverte.  

-   **Liste de recherche de suffixes** (pour les appareils Windows Phone 8.1 uniquement) : spécifiez un suffixe DNS sur chaque ligne. Chaque suffixe DNS que vous spécifiez sera recherché lors de la connexion à un site web à l'aide d'un nom court.  

     Par exemple, vous spécifiez les suffixes DNS **domain1.contoso.com** et **domain2.contoso.com** , puis vous accédez à l'URL **http://mywebsite**. Les adresses suivantes seront recherchées :  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

> [!NOTE]  
>  Pour les appareils Windows Phone 8.1 uniquement  
>   
>  Si l'option **Envoyer tout le trafic réseau via la connexion VPN** est sélectionnée et que la connexion VPN utilise le tunneling complet, pour le premier profil configuré sur l'appareil la connexion VPN s'ouvre automatiquement. Si vous souhaitez qu'un autre profil ouvre automatiquement une connexion, vous devez le configurer comme profil par défaut sur l'appareil.  
>   
>  Si l'option **Envoyer tout le trafic réseau via la connexion VPN** n'est pas sélectionnée et que la connexion VPN utilise le tunneling fractionné, une connexion VPN peut être ouverte automatiquement si vous configurez des itinéraires ou un suffixe DNS spécifique à la connexion.  


### <a name="configure-supported-platforms-for-the-vpn-profile"></a>Configurer des plates-formes prises en charge pour le profil VPN  
 Les plates-formes prises en charge sont les systèmes d'exploitation sur lesquels le profil VPN sera installé.  

Sur la page **Plates-formes prises en charge** de l' **Assistant Création d'un profil VPN**, sélectionnez les systèmes d'exploitation sur lesquels le profil VPN sera installé ou cliquez sur **Sélectionner tout** pour installer le profil VPN sur tous les systèmes d'exploitation disponibles.  

### <a name="complete-the-wizard"></a>Terminer l'Assistant  
 Dans la page **Résumé** de l’Assistant, passez en revue les actions à exécuter, puis cliquez sur **Terminer**. Le nouveau profil VPN figure dans le nœud **Profils VPN** dans l'espace de travail **Ressources et Conformité** .  

### <a name="next-steps"></a>Étapes suivantes

- Pour les connexions VPN tierces, distribuez l’application VPN avant de déployer le profil VPN. Si vous ne déployez pas l’application, les utilisateurs sont invités à le faire quand ils tentent de se connecter au VPN. Pour découvrir comment déployer des applications, consultez [Déployer des applications avec System Center Configuration Manager](../../apps/deploy-use/deploy-applications).

- Déployez le profil VPN comme décrit dans [Guide pratique pour déployer des profils dans System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  



<!--HONumber=Nov16_HO1-->


