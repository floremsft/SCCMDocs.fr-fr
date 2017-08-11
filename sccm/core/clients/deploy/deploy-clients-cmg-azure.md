---
title: "Installer et attribuer le client à partir d’internet | Microsoft Docs"
description: "Installez et attribuez le client System Center Configuration Manager à partir d’internet."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: 14
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: f604557d208b2dda9dc1c6b4c4d27d896d47695e
ms.contentlocale: fr-fr
ms.lasthandoff: 07/29/2017

---

# <a name="install-and-assign-configuration-manager-clients-from-the-internet-using-azure-ad-for-authentication"></a>Installer et attribuer des clients Configuration Manager à partir d’Internet à l’aide d’Azure AD pour l’authentification

Vous pouvez utiliser les services cloud de Configuration Manager avec Azure AD pour prendre en charge les scénarios suivants :

- Installer manuellement le client Configuration Manager à partir d’internet et l’affecter à un site Configuration Manager (nécessite le rôle de système de site de passerelle de gestion cloud).
- Utiliser Azure AD pour authentifier les clients sur Internet pour l’accès à vos sites Configuration Manager. Azure AD élimine le besoin de configurer et d’utiliser des certificats d’authentification client.
- Découvrez les utilisateurs Azure AD dans votre site à utiliser dans des regroupements, et d’autres opérations de Configuration Manager.

Utilisez les étapes suivantes pour vous aider à effectuer cette opération :

- **Étape 1 : Configurer la passerelle de gestion cloud**
- **Étape 2 : Configurer l’application de services Azure dans les services cloud de Configuration Manager**
- **Étape 3 : Configurer les paramètres client pour inscrire des appareils Windows 10 auprès d’Azure AD**
- **Étape 4 : Installer et inscrire le client Configuration Manager à l’aide de l’identité Azure Active Directory**


## <a name="before-you-start"></a>Avant de commencer

- Vous devez disposer d’un client Azure AD.
- Vos appareils doivent exécuter Windows 10 et être joints à Azure AD. Les clients peuvent également être joints à un domaine en plus d’Azure AD).
- Outre les [prérequis existants](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) pour le rôle de système de site du point de gestion, vous devez vérifier que l’option **ASP.NET 4.5** (et toute autre option sélectionnée automatiquement) sont activées sur l’ordinateur qui héberge ce rôle de système de site.
- Pour utiliser Configuration Manager pour déployer le client :
    - Configurez au moins un point de gestion pour le mode HTTPS.
    - Configurez une passerelle de gestion cloud.

## <a name="step-1-set-up-the-cloud-management-gateway"></a>Étape 1 : Configurer la passerelle de gestion cloud

Configurez la passerelle de gestion cloud pour permettre aux clients d’accéder à votre site Configuration Manager à partir d’Internet sans utiliser de certificats. Vous trouverez de l’aide dans les rubriques suivantes : 

- [Configurer la passerelle de gestion cloud dans Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurer la passerelle de gestion cloud pour Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Surveiller la passerelle de gestion cloud dans Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

## <a name="step-2-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Étape 2 : Configurer l’application de services Azure dans les services cloud de Configuration Manager

Cela connecte votre site Configuration Manager à Azure AD et est requis pour toutes les autres opérations de cette section. 

La découverte des utilisateurs Azure AD est configurée dans le cadre de la *gestion cloud*. La procédure à suivre est détaillée à l’étape **6** de la procédure [Créer l’application web Azure à utiliser avec Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) dans la rubrique *Configurer les services Azure à utiliser avec Configuration Manager*.
    
Une fois la procédure terminée, vous avez connecté votre site Configuration Manager à Azure AD. 

## <a name="step-3-configure-client-settings-to-register-windows-10-devices-with-azure-ad"></a>Étape 3 : Configurer les paramètres client pour inscrire des appareils Windows 10 auprès d’Azure AD

1.  Configurer la section suivante de paramètres client (figurant dans les services cloud) en utilisant les informations dans [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings).
    - **Inscrire automatiquement les nouveaux appareils joints à un domaine Windows 10 avec Azure Active Directory** : réglez sur**Oui** (valeur par défaut) ou **Non**.
    - **Permettre aux clients d’utiliser une passerelle de gestion cloud** : réglez sur **Oui** (valeur par défaut) ou **Non**.
2.  Déployez les paramètres client sur la collection requise d’appareils.

Pour confirmer que l’appareil est joint à Azure AD, exécutez la commande **dsregcmd.exe /status** dans une fenêtre d’invite de commandes. Le champ **AzureAdjoined** dans les résultats indique **OUI** si l’appareil est joint à Azure AD.


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>Étape 4 : Installer et inscrire le client Configuration Manager à l’aide de l’identité Azure Active Directory

Avant de commencer, assurez-vous que les fichiers sources d’installation client sont stockés localement sur l’appareil sur lequel vous souhaitez installer le client. Ensuite, suivez les instructions du [Guide pratique pour déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) en utilisant la ligne de commande d’installation suivante : 

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso AADCLIENTAPPID= AADRESOURCEURI=https://contososerver**

- **/NoCrlCheck** : si votre point de gestion ou votre passerelle de gestion cloud utilise un certificat de serveur non public, le client peut ne pas être en mesure d’atteindre l’emplacement de la liste de révocation de certificats.
- **/Source** : dossier local : emplacement des fichiers d’installation du client.
- **CCMHOSTNAME** : nom de votre point de gestion Internet. Vous pouvez le trouver en exécutant **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** à partir d’une invite de commandes sur un client géré.
- **SMSMP** : nom de votre point de gestion de recherche. Il peut se trouver sur votre intranet.
- **SMSSiteCode** : code de site de votre site Configuration Manager.
- **AADTENANTID**, **AADTENANTNAME** : ID et nom du locataire Azure AD que vous avez lié à Configuration Manager. Vous pouvez les trouver en exécutant dsregcmd.exe /status à partir d’une invite de commandes sur un appareil à Azure AD.
- **AADCLIENTAPPID** : ID d’application du client Azure AD. Pour vous aider à le trouver, consultez [Utiliser le portail pour créer une application Azure Active Directory et un principal de service pouvant accéder aux ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri** : URI de l’identificateur de l’application de serveur Azure AD intégrée.


## <a name="next-steps"></a>Étapes suivantes

Une fois terminé, vous pouvez continuer à [surveiller et gérer les clients](/sccm/core/clients/manage/monitor-clients).

