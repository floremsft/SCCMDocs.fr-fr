---
title: "Utilisation de profils VPN dans System Center Configuration Manager | Microsoft Docs"
description: "Utilisez des profils VPN sur des appareils mobiles dans System Center Configuration Manager."
ms.custom: na
ms.date: 07/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: 18
caps.handback.revision: 0
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: e4a53caab7d76b604a3fee7dcfc4dc48f22b0fb0
ms.contentlocale: fr-fr
ms.lasthandoff: 07/29/2017

---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Utilisation de profils VPN sur des appareils mobiles dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Découvrez comment utiliser des profils VPN dans System Center Configuration Manager pour déployer des paramètres VPN pour les utilisateurs de votre organisation. Lorsque vous déployez ces paramètres, vous réduisez l'effort que doit fournir l'utilisateur final pour se connecter aux ressources du réseau d'entreprise.  

 Par exemple, vous souhaitez configurer tous les appareils qui exécutent le système d'exploitation iOS en utilisant les paramètres requis pour se connecter à un partage de fichiers sur le réseau d'entreprise. Vous pouvez créer un profil VPN contenant les paramètres nécessaires pour la connexion au réseau d'entreprise, puis déployer ce profil auprès de tous les utilisateurs qui disposent d'appareils exécutant iOS dans votre hiérarchie. Les utilisateurs d'appareils iOS voient la connexion VPN dans la liste des réseaux disponibles et peuvent se connecter à ce réseau avec un minimum d'effort.  

 Lorsque vous créez un profil VPN, vous pouvez inclure un large éventail de paramètres de sécurité. Par exemple, vous pouvez spécifier les certificats pour l’authentification de client et la validation de serveur qui ont été configurés à l’aide des profils de certificat System Center Configuration Manager. Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md).  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Profils VPN si Configuration Manager est utilisé en association avec Intune

 Pour déployer des profils sur des appareils iOS, Android, Windows Phone et Windows 8.1, ces appareils doivent être inscrits dans Microsoft Intune. Les appareils sur d’autres plateformes peuvent également être inscrits auprès Intune. Pour plus d’informations sur la procédure d’inscription, consultez [Gérer les appareils mobiles avec Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). Ce tableau affiche le type de connexion pris en charge pour chaque plateforme d’appareil :  

 |Type de connexion|iOS et macOS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop et Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|Oui|Oui|Non|Non|Non|Non|Oui (OMA-URI)|
 |Cisco (IPSec)|iOS uniquement|Non|Non|Non|Non|Non|Non|  
 |Pulse Secure|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
 |Client F5 Edge|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
 |Dell SonicWALL Mobile Connect|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
 |Check Point Mobile VPN|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
 |Microsoft SSL (SSTP)|Non|Non|Oui|Oui|Oui|Non|Non|  
 |Microsoft Automatic|Non|Non|Oui|Oui|Oui|Non|Oui (OMA-URI)|  
 |IKEv2|Oui (Stratégie personnalisée)|Non|Oui|Oui|Oui|Oui|Oui (OMA-URI)|  
 |PPTP|Oui|Non|Oui|Oui|Oui|Non|Oui (OMA-URI)|  
 |L2TP|Oui|Non|Oui|Oui|Oui|Non|Oui (OMA-URI)|  

## <a name="create-vpn-profiles"></a>Création de profils VPN
La section [Guide pratique pour créer des profils VPN dans System Center Configuration Manager](../../protect/deploy-use/create-vpn-profiles.md) fournit des informations générales sur la création de profils VPN.

###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Fonctionnalités VPN Windows 10 disponibles quand vous utilisez Configuration Manager avec Intune  


> [!NOTE]  
> Le nom d’un profil VPN qui utilise des fonctionnalités VPN Windows 10 ne peut pas être au format Unicode ni contenir des caractères spéciaux.


|Option|Plus d'informations|Type de connexion|  
    |------------|----------------------|---------------------|  
    |**Ignorer VPN en cas de connexion à un réseau Wi-Fi d'entreprise**|La connexion VPN n’est pas utilisée quand l’appareil est connecté au réseau Wi-Fi d’entreprise. Entrez le nom du réseau approuvé, utilisé pour déterminer si l’appareil est connecté au réseau d’entreprise.|Tout|  
    |**Règles de trafic réseau**|Définissez les protocoles, les ports locaux et distants et les plages d’adresses à activer pour la connexion VPN.<br /><br /> **Remarque :** si vous ne créez pas de règle de trafic réseau, l’ensemble des protocoles, ports et plages d’adresses sont activés. Dès lors que vous créez une règle, seuls les protocoles, les ports et les plages d’adresses que vous spécifiez dans cette règle ou dans des règles supplémentaires sont utilisés par la connexion VPN.|Tout|  
    |**Itinéraires**|Itinéraires qui utilisent la connexion VPN. Notez que la création de plus de 60 itinéraires peut entraîner l’échec de la stratégie. |Tout|  
    |**Serveurs DNS**|Serveurs DNS utilisés par la connexion VPN une fois la connexion établie.|Tout|  
    |**Applications qui se connectent automatiquement au VPN**|Vous pouvez ajouter des applications, ou importer des listes d’applications, qui utilisent automatiquement la connexion VPN. Le type d’application détermine l’identificateur de l’application. Pour une application de bureau, fournissez le chemin de fichier de l’application. Pour une application universelle, indiquez le nom de la famille de packages (PFN). Pour savoir comment rechercher le nom PFN pour une application, consultez [Rechercher le nom de la famille de packages pour le VPN par application](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |Tout|

> [!IMPORTANT]
> Nous vous recommandons de sécuriser toutes les listes d’applications associées que vous compilez à utiliser dans la configuration du VPN par application. Si un utilisateur non autorisé modifie votre liste et que vous l’importez dans la liste d’applications du VPN par application, vous allez potentiellement autoriser l’accès au VPN à des applications qui ne doivent pas avoir accès. Une façon de sécuriser les listes d’applications consiste à utiliser une liste de contrôle d’accès (ACL).


1.  Dans la page **Méthode d’authentification** de l’Assistant, spécifiez les informations suivantes :  

    -   **Méthode d’authentification :** sélectionnez la méthode d’authentification qui sera utilisée par la connexion VPN. Les méthodes disponibles peuvent varier selon le type de connexion, comme indiqué dans le tableau suivant.  

        |Méthode d'authentification|Types de&nbsp;connexion&nbsp;pris en charge|  
        |---------------------------|--------------------------------|  
        |**Certificats**<br /><br /> **Remarques** :<ul><li>Si le certificat client est utilisé pour l'authentification sur un serveur RADIUS, tel qu'un serveur NPS, l'autre nom de l'objet dans le certificat doit être défini sur le nom d'utilisateur principal.</li><li>Pour les déploiements Android, sélectionnez l’identificateur EKU et la valeur de hachage de l’empreinte numérique de l’émetteur du certificat.  Sinon, les utilisateurs doivent sélectionner manuellement le certificat approprié.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Pulse Secure</li><li>Client F5 Edge</li><li>Dell SonicWALL Mobile Connect</li><li> Check Point Mobile VPN</li></ul>|  
        |**Nom d'utilisateur et mot de passe**|<ul><li>Pulse Secure</li><li>Client F5 Edge</li><li>Dell SonicWALL Mobile Connect</li><li> Check Point Mobile VPN</li></ul>|  
        |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
        |**Microsoft PEAP (Protected EAP)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Mot de passe sécurisé Microsoft (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Carte à puce ou autre certificat**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**RSA SecurID** (iOS uniquement)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Utiliser des certificats d’ordinateur**|<ul><li>IKEv2</li></ul>|  

         Selon les options sélectionnées, vous devrez peut-être spécifier d'autres informations, par exemple :  

        -   **Conserver les informations d’identification de l’utilisateur à chaque ouverture de session** : les informations d’identification sont mémorisées pour que les utilisateurs n’aient pas à les entrer chaque fois qu’une connexion est établie.  

        -   **Sélectionner un certificat client pour l’authentification du client** : sélectionnez le [certificat SCEP](create-pfx-certificate-profiles.md) client précédemment créé et qui sera utilisé pour authentifier la connexion VPN.   

            > [!NOTE]  
            >  Pour les appareils iOS, le profil SCEP que vous sélectionnez sera incorporé au profil VPN. Pour les autres plateformes, une règle de mise en application est ajoutée pour s'assurer que le profil VPN n'est pas installé si le certificat n'est pas présent ou non conforme.  
            >   
            >  Si le certificat SCEP que vous spécifiez n'est pas conforme ou n'a pas été déployé, le profil VPN n'est pas installé sur l'appareil.
            >  
            >  Les appareils qui exécutent iOS prennent uniquement en charge RSA SecurID et MSCHAP v2 comme méthode d’authentification quand le type de connexion est PPTP. Pour éviter toute erreur, déployez un profil VPN PPTP distinct sur les appareils qui exécutent iOS.  

        - **Accès conditionnel**
            - Choisissez **Activer l’accès conditionnel pour cette connexion VPN** pour vérifier que les appareils qui se connectent au VPN ont été testés en vue de la conformité de l’accès conditionnel avant la connexion. Les stratégies de conformité sont décrites dans [Stratégies de conformité des appareils dans System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md).
            - Choisissez **Activer l’authentification unique avec certificat de remplacement** pour choisir un certificat autre que le certificat d’authentification VPN pour la conformité des appareils. Si vous choisissez cette option, indiquez les valeurs de **Utilisation améliorée de la clé** (liste séparée par des virgules) et **Hachage de l’émetteur** pour le certificat approprié que le client VPN doit localiser.

         - Pour **Protection des informations Windows**, indiquez l’identité d’entreprise gérée par l’entreprise, qui est généralement le domaine principal de votre organisation, par exemple, *contoso.com*. Vous pouvez spécifier plusieurs domaines appartenant à votre organisation en les séparant avec le caractère « | ». Par exemple, *contoso.com|newcontoso.com*.   
            Pour plus d’informations sur la protection des informations Windows, consultez [Créer une stratégie Protection des informations Windows (WIP) à l’aide de Microsoft Intune](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Configurer l’accès conditionnel pour VPN](media/vpn-conditional-access.png)

         En cas de prise en charge par la version de Windows qui exécute Configuration Manager _et_ la méthode d’autorisation sélectionnée, vous pouvez choisir l’option **Configurer** pour ouvrir la boîte de dialogue des propriétés Windows et configurer les propriétés de la méthode d’authentification.  Si l’option **Configurer** est désactivée, utilisez d’autres moyens pour configurer les propriétés de la méthode d’authentification.

2.  Sur la page **Paramètres du proxy** de l'**Assistant Création d'un profil VPN**, cochez la case **Configurer les paramètres du proxy pour ce profil VPN** si votre connexion VPN utilise un serveur proxy. Indiquez ensuite les informations sur le serveur proxy. Pour plus d’informations, consultez la documentation de Windows Server.  

    > [!NOTE]  
    >  Sur les ordinateurs Windows 8.1, le profil VPN n’affiche pas les informations de proxy tant que vous n’êtes pas connecté au VPN avec cet ordinateur.  


3. Configurer les paramètres DNS supplémentaires (si nécessaire).  
 Dans la page **Configurer une connexion VPN automatique**, vous pouvez configurer les paramètres suivants :  

    -   **Activer VPN à la demande** : utilisez cette option si vous souhaitez configurer d’autres paramètres DNS pour les appareils Windows Phone 8.1. Ce paramètre s’applique uniquement aux appareils Windows Phone 8.1 et ne doit être activé que sur les profils VPN destinés à être déployés sur des appareils Windows Phone 8.1.

    -   **Liste de suffixes DNS** (appareils Windows Phone 8.1 uniquement) : configurez les domaines qui établiront une connexion VPN. Pour chaque domaine que vous spécifiez, ajoutez le suffixe DNS, l'adresse du serveur DNS et l'une des actions à la demande suivantes :  

        -   **Ne jamais établir** : ne jamais ouvrir de connexion VPN.  

        -   **Établir si nécessaire** : ouvrir une connexion VPN uniquement si l’appareil doit se connecter aux ressources.  

        -   **Toujours établir** : toujours ouvrir la connexion VPN.  

    -   **Fusionner** : copie tous les suffixes DNS que vous avez configurés dans la **Liste de réseaux approuvés**.  

    -   **Liste de réseaux approuvés** (appareils Windows Phone 8.1 uniquement) : spécifiez un suffixe DNS sur chaque ligne. Si l'appareil se trouve sur un réseau approuvé, la connexion VPN n'est pas ouverte.  

    -   **Liste de recherche de suffixes** (appareils Windows Phone 8.1 uniquement) : spécifiez un suffixe DNS sur chaque ligne. Chaque suffixe DNS sera recherché lors de la connexion à un site web à l’aide d’un nom court.  

     Par exemple, vous spécifiez les suffixes DNS **domain1.contoso.com** et **domain2.contoso.com**, puis vous accédez à l'URL **http://mywebsite**. Les adresses suivantes seront recherchées :  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  Pour les appareils Windows Phone 8.1 uniquement  
    >   
    >  Si l'option *Envoyer tout le trafic réseau via la connexion VPN* est sélectionnée *et* que la connexion VPN utilise le tunneling complet, la connexion VPN s'ouvre automatiquement avec le premier profil d’appareil. Pour ouvrir une connexion avec un autre profil, définissez le profil par défaut de votre choix.  
    >   
    >  Si l'option *Envoyer tout le trafic réseau via la connexion VPN* n'est *pas* sélectionnée *et* que la connexion VPN utilise le tunneling fractionné, les connexions VPN peuvent être ouvertes automatiquement pour les itinéraires configurés ou les suffixes DNS spécifiques à la connexion.  


4. Sur la page **Plates-formes prises en charge** de l'**Assistant Création d'un profil VPN**, sélectionnez les systèmes d'exploitation sur lesquels le profil VPN sera installé ou choisissez **Sélectionner tout** pour installer le profil VPN sur tous les systèmes d'exploitation disponibles.  

5. Fermez l'Assistant. Le nœud **Profils VPN** dans l'espace de travail **Ressources et Conformité** affiche le nouveau profil VPN.  


**Déploiement :** consultez [Déployer des profils Wi-Fi, VPN, de messagerie et de certificat](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) pour en savoir plus sur le déploiement des profils VPN.

### <a name="next-steps"></a>Étapes suivantes  
 Utilisez les rubriques suivantes pour planifier, configurer, utiliser et gérer des profils VPN dans Configuration Manager.  

-   [Configuration requise pour les profils VPN dans System Center Configuration Manager](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Sécurité et confidentialité pour les profils VPN dans System Center Configuration Manager](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)

