---
title: "Installer et attribuer le client à partir d’internet | Microsoft Docs"
description: "Installez et attribuez le client System Center Configuration Manager à partir d’internet."
ms.custom: na
ms.date: 8/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: "14"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 7bbcece8a7a745b3b6cc9bbd8aa283963e2b738d
ms.sourcegitcommit: 49add91eebfeaba6d1d203d3cf9927b9cacdfc8e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/08/2017
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Installer et affecter des clients Windows 10 Configuration Manager à l’aide d’Azure AD à des fins d’authentification

Vous pouvez utiliser les services cloud de Configuration Manager avec Azure AD pour prendre en charge les scénarios suivants :

- Installez manuellement le client Gestionnaire de configuration sur des appareils Windows 10 par Internet, et affectez-le à un site Configuration Manager (nécessite le rôle de système de site de la Passerelle de gestion cloud).
- Utilisez Azure AD pour authentifier les clients de façon à leur donner accès à vos sites Configuration Manager. Azure AD élimine le besoin de configurer et d’utiliser des certificats d’authentification client.
- Découvrez les utilisateurs Azure AD dans votre site à utiliser dans des regroupements, et d’autres opérations de Configuration Manager.

Utilisez les étapes suivantes pour vous aider à effectuer cette opération :

- **Étape 1 : Configurer l’application de services Azure dans les Services cloud Configuration Manager et configurer la découverte d’utilisateurs Azure AD**
- **Étape 2 : Configurer la Passerelle de gestion cloud** (facultatif pour les clients locaux)
- **Étape 3 : Configurer les paramètres clients pour joindre des appareils Windows 10 à Azure AD et permettre aux clients d’utiliser la Passerelle de gestion cloud**
- **Étape 4 : Installer et inscrire le client Configuration Manager à l’aide de l’identité Azure Active Directory**


## <a name="before-you-start"></a>Avant de commencer

- Vous devez disposer d’un client Azure AD.
- Vos appareils doivent exécuter Windows 10, être joints à Azure AD et être connecté à l’aide d’une identité Azure AD. Les clients peuvent également être joints à un domaine en plus d’Azure AD).
- Outre les [prérequis existants](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) pour le rôle de système de site du point de gestion, vous devez vérifier que l’option **ASP.NET 4.5** (et toute autre option sélectionnée automatiquement) sont activées sur l’ordinateur qui héberge ce rôle de système de site.
- Pour utiliser Configuration Manager pour déployer le client :
    - Configurez au moins un point de gestion pour le mode HTTPS si vous souhaitez utiliser Azure AD pour l’authentification plutôt que des certificats clients.
        Si vous utilisez des certificats clients plutôt que la Passerelle de gestion cloud, le point de gestion HTTPS est facultatif mais recommandé. Si vous utilisez Azure AD pour l’authentification, que ce soit pour des clients locaux ou Internet, le point de gestion HTTPS est requis.
    - Configurez une Passerelle de gestion cloud si vous souhaitez déployer des clients Internet. Pour les clients locaux que vous authentifiez auprès d’Azure AD, vous n’avez pas besoin de configurer la Passerelle de gestion cloud.


## <a name="step-1-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Étape 1 : Configurer l’application de services Azure dans les Services cloud Configuration Manager

Cela connecte votre site Configuration Manager à Azure AD et est requis pour toutes les autres opérations de cette section. 

La découverte des utilisateurs Azure AD est configurée dans le cadre de la *gestion cloud*. La procédure à suivre est détaillée à l’étape **6** de la procédure [Créer l’application web Azure à utiliser avec Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) dans la rubrique *Configurer les services Azure à utiliser avec Configuration Manager*.
    
Une fois la procédure terminée, vous avez connecté votre site Configuration Manager à Azure AD. 

## <a name="step-2-set-up-the-cloud-management-gateway"></a>Étape 2 : Configurer la Passerelle de gestion cloud

Configurez la Passerelle de gestion cloud pour pouvoir mettre en place les scénarios de gestion cloud décrits dans cette rubrique. Vous trouverez de l’aide dans les rubriques suivantes : 

- [Configurer la passerelle de gestion cloud dans Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurer la passerelle de gestion cloud pour Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Surveiller la passerelle de gestion cloud dans Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

## <a name="step-3-configure-client-settings-to-join-windows-10-devices-with-azure-ad-and-enable-clients-to-use-the-cloud-management-gateway"></a>Étape 3 : Configurer les paramètres clients pour joindre des appareils Windows 10 à Azure AD et permettre aux clients d’utiliser la Passerelle de gestion cloud

1.  Configurez les paramètres clients suivants (figurant dans la section **Services cloud**) suivant les informations du [Guide pratique pour configurer les paramètres clients](/sccm/core/clients/deploy/configure-client-settings).
    - **Autoriser l’accès au point de distribution cloud** : activez ce paramètre afin que les appareils Internet puissent obtenir le contenu requis pour installer le client Gestionnaire de configuration. Si le contenu n’est pas disponible sur le point de distribution cloud, les appareils peuvent récupérer le contenu à partir d’un point de gestion connecté à la Passerelle de gestion cloud.
    - **Inscrire automatiquement les nouveaux appareils joints à un domaine Windows 10 avec Azure Active Directory** : réglez sur**Oui** (valeur par défaut) ou **Non**.
    - **Permettre aux clients d’utiliser une passerelle de gestion cloud** : réglez sur **Oui** (valeur par défaut) ou **Non**.
2.  Déployez les paramètres client sur la collection requise d’appareils. Ne déployez pas ces paramètres sur des regroupements d’utilisateurs.

Pour confirmer que l’appareil est joint à Azure AD, exécutez la commande **dsregcmd.exe /status** dans une fenêtre d’invite de commandes. Le champ **AzureAdjoined** dans les résultats indique **OUI** si l’appareil est joint à Azure AD.


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>Étape 4 : Installer et inscrire le client Configuration Manager à l’aide de l’identité Azure Active Directory

Pour installer le client, suivez les instructions du [Guide pratique pour déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) en utilisant la ligne de commande d’installation suivante : 

**ccmsetup.exe /mp&#58; https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=DFD SMSMP=https://SCCMDFPSS.contoso.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011DB47 AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d17026 AADRESOURCEURI=https://contososerver**

- **/MP** : source de téléchargement. Peut être défini sur CMG en cas d’amorçage par Internet.
- **CCMHOSTNAME** : nom de votre point de gestion Internet. Vous pouvez le trouver en exécutant **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** à partir d’une invite de commandes sur un client géré.
- **SMSSiteCode** : code de site de votre site Configuration Manager.
- **SMSMP** : nom de votre point de gestion de recherche. Il peut se trouver sur votre intranet.
- **AADTENANTID**, **AADTENANTNAME** : ID et nom du locataire Azure AD que vous avez lié à Configuration Manager. Vous pouvez les trouver en exécutant dsregcmd.exe /status à partir d’une invite de commandes sur un appareil à Azure AD.
- **AADCLIENTAPPID** : ID d’application du client Azure AD. Pour vous aider à le trouver, consultez [Utiliser le portail pour créer une application Azure Active Directory et un principal de service pouvant accéder aux ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri** : URI de l’identificateur de l’application de serveur Azure AD intégrée. Pour plus d’informations, consultez l’article [Configurer les services Azure à utiliser avec Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).




## <a name="next-steps"></a>Étapes suivantes

Une fois terminé, vous pouvez continuer à [surveiller et gérer les clients](/sccm/core/clients/manage/monitor-clients).
