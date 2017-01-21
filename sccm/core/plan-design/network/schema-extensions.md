---
title: "Extensions de schéma | Microsoft Docs"
description: "Étendre le schéma Active Directory pour prendre en charge System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: f230b6cbe97b72fee4f5d2e45260e6217ef2cec0


---
# <a name="schema-extensions-for-system-center-configuration-manager"></a>Extensions de schéma pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez étendre le schéma Active Directory pour prendre en charge Configuration Manager. Cette opération modifie un schéma Active Directory de forêts pour ajouter un nouveau conteneur et plusieurs attributs grâce auxquels les sites Configuration Manager peuvent publier dans Active Directory des informations clés accessibles aux clients de manière sécurisée.  Ces informations peuvent simplifier le déploiement et la configuration des clients et aider ces derniers à localiser les ressources du site, comme les serveurs sur lesquels le contenu a été déployé ou qui fournissent différents services aux clients.  

-   L’extension du schéma Active Directory n’est pas obligatoire, mais elle est recommandée.  

Avant d’ [étendre le schéma Active Directory](https://msdnstage.redmond.corp.microsoft.com/en-US/library/mt345589\(TechNet.10\).aspx), vous devez être familiarisé avec les services de domaine Active Directory et la [modification du schéma Active Directory](https://technet.microsoft.com/library/cc759402\(v=ws.10\).aspx).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Considérations relatives à l'extension du schéma Active Directory pour Configuration Manager  

-   Les extensions de schéma Active Directory pour System Center Configuration Manager sont identiques à celles utilisées par Configuration Manage 2007 et Configuration Manager 2012. Si vous avez déjà étendu le schéma pour l’une de ces versions, vous n’avez plus besoin de l’étendre.  

-   L’extension du schéma est une action irréversible, unique et à l’échelle de la forêt.  

-   L’extension du schéma ne peut être effectuée que par un utilisateur membre du groupe Administrateurs du schéma, ou disposant de suffisamment d’autorisations pour modifier le schéma.  

-   Bien que vous puissiez étendre le schéma avant ou après l’exécution du programme d’installation de Configuration Manager, nous vous recommandons d’effectuer l’opération avant de commencer à configurer vos sites et vos paramètres de hiérarchie.  Ce procédé simplifie la plupart des étapes de configuration ultérieures.  

-   Une fois que vous avez étendu le schéma, le catalogue global Active Directory est répliqué dans toute la forêt. Ainsi, choisissez une période calme, afin de ne pas affecter d’autres processus dépendant du réseau :  

    -   Dans les forêts Windows 2000, l’extension du schéma entraîne une synchronisation complète du catalogue global.  

    -   À partir des forêts Windows 2003, seuls les attributs ajoutés récemment sont répliqués.  

**Appareils et clients qui n’utilisent pas le schéma Active Directory :**  

-   Appareils mobiles gérés par le connecteur du serveur Exchange Server  

-   Client des ordinateurs Mac  

-   Client des serveurs Linux et UNIX  

-   Appareils mobiles inscrits par Configuration Manager  

-   Appareils mobiles inscrits par Microsoft Intune  

-   Clients d'appareil mobile hérités  

-   Clients Windows configurés pour être gérés uniquement via Internet  

-   Clients Windows détectés par Configuration Manager comme étant connectés à Internet  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Fonctionnalités qui bénéficient de l’extension du schéma  
**Installation de l’ordinateur client et attribution de site** : durant l’installation d’un nouveau client sur un ordinateur Windows, le client recherche des propriétés d’installation dans les services de domaine Active Directory.  

-   **Solutions de contournement :** si vous n’étendez pas le schéma, utilisez l’une des options suivantes pour fournir des détails de configuration dont les ordinateurs ont besoin pour l’installation :  

    -   **Utiliser l’installation poussée du client**. Avant d'utiliser la méthode d'installation du client, assurez-vous que toutes les conditions préalables sont remplies. Pour plus d’informations, voir « Dépendances liées aux méthodes d’installation » dans Configuration requise pour les clients d’ordinateurs.  

    -   **Installer les clients manuellement** et fournir les propriétés d'installation du client en utilisant les propriétés de ligne de commande d'installation CCMSetup. Ces méthodes doivent inclure :  

        -   Spécifiez un point de gestion ou un chemin source à partir duquel l’ordinateur peut télécharger les fichiers d’installation en utilisant la propriété CCMSetup **/mp:&lt;nom_ordinateur_nom_point_de_gestion\>** ou **/source:&lt;chemin_fichiers_sources_client\>** sur la ligne de commande CCMSetup lors de l’installation du client.  

        -   Spécifiez une liste de points de gestion initiale pour le client, afin qu'il puisse l'attribuer au site et ensuite télécharger les paramètres de stratégie client et du site. Pour ce faire, utilisez la propriété CCMSetup Client.msi de SMSMP.  

    -   **Publier le point de gestion dans DNS ou WINS** et configurer des clients pour utiliser cette méthode d’emplacement de service.  

**Configuration du port pour la communication client à serveur** : quand un client est installé, il est configuré avec les informations du port stockées dans Active Directory. Si vous modifiez ultérieurement le port de communication client à serveur pour un site, un client peut obtenir ce nouveau paramètre de port par les services de domaine Active Directory.  

-   **Solutions de contournement :** si vous n’étendez pas le schéma, utilisez l’une des options suivantes pour fournir de nouvelles configurations de port aux clients existants :  

    -   **Réinstaller les clients** à l’aide d’options qui configurent le nouveau port.  

    -   **Déployer sur les clients un script personnalisé qui met à jour les informations de port**. Si les clients ne peuvent pas communiquer avec un site en raison d’une modification du port, vous ne pouvez pas utiliser Configuration Manager pour déployer ce script. Vous pouvez par exemple utiliser la Stratégie de groupe.  

**Scénarios de déploiement de contenu** : quand vous créez du contenu sur un site et que vous déployez ce contenu vers un autre site de la hiérarchie, le site récepteur doit être capable de vérifier la signature des données du contenu signé. Cela nécessite un accès à la clé publique du site source dans lequel vous créez ces données. Quand vous étendez le schéma Active Directory pour Configuration Manager, la clé publique d’un site est rendue disponible à tous les sites de la hiérarchie.  

-   **Solutions de contournement :** si vous n’étendez pas le schéma, utilisez l’outil de maintenance de hiérarchie, **preinst.exe**, pour échanger les informations de la clé sécurisées entre les sites.  

     Par exemple, si vous pensez créer du contenu sur un site principal pour le déployer vers un site secondaire inférieur à un site principal différent, vous devez soit étendre le schéma Active Directory pour permettre au site secondaire d'obtenir la clé publique de la source des sites principaux, ou utiliser preinst.exe pour partager les clés directement entre les deux sites.  

## <a name="active-directory-attributes-and-classes"></a>Classes et attributs Active Directory  
Quand vous étendez le schéma pour System Center Configuration Manager, les classes et les attributs suivants sont ajoutés au schéma et sont accessibles à tous les sites Configuration Manager dans cette forêt Active Directory.  

-   Attributs :  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-Ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Boundaries  
        sur  

    -   cn=MS-SMS-Site-Boundaries  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   Classes :  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]  
>  Les extensions de schéma peuvent inclure des attributs et des classes issus de versions précédentes du produit, qui ne sont plus utilisés par Configuration Manager 2015. Exemple :  
>   
>  -   Attribut : cn=MS-SMS-Site-Boundaries  
> -   Classe : cn=MS-SMS-Server-Locator-Point  

Vous pouvez vous assurer que les listes précédentes sont à jour en consultant le fichier **ConfigMgr_ad_schema.LDF**, situé dans le dossier **\SMSSETUP\BIN\x64** du support d’installation de System Center Configuration Manager.  



<!--HONumber=Dec16_HO3-->


