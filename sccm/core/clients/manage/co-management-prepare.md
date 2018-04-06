---
title: Préparer les appareils Windows 10 pour la cogestion
description: Découvrez comment préparer vos appareils Windows 10 pour la cogestion.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 61aef0351e32ef6cf31911a8dfd27e86de82f38c
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2018
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Préparer les appareils Windows 10 pour la cogestion
Vous pouvez activer la cogestion sur les appareils Windows 10 qui sont joints à AD et à Azure AD, inscrits à Intune et clients dans Configuration Manager. Pour les nouveaux appareils Windows 10 et pour ceux qui sont déjà inscrits à Intune, installez le client Configuration Manager avant de pouvoir les cogérer. Pour les appareils Windows 10 qui sont déjà des clients Configuration Manager, inscrivez-les à Intune et activez la cogestion dans la console Configuration Manager.

> [!IMPORTANT]
> Les appareils mobiles Windows 10 ne prennent pas en charge la cogestion.

## <a name="command-line-to-install-configuration-manager-client"></a>Ligne de commande pour installer un client Configuration Manager
Créez une application dans Intune pour les appareils Windows 10 qui ne sont pas encore des clients Configuration Manager. Lors de la création de l’application dans les sections suivantes, utilisez cette ligne de commande :

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*URL du point de terminaison de l’authentification mutuelle pour la passerelle de gestion cloud*&#62;/ CCMHOSTNAME=&#60;*URL du point de terminaison de l’authentification mutuelle pour la passerelle de gestion cloud*&#62; SMSSiteCode=&#60;*Codesite*&#62; SMSMP=https:&#47;/&#60;*Nom de domaine complet du point de gestion*&#62; AADTENANTID=&#60;*ID du locataire AAD*&#62; AADTENANTNAME=&#60;*Nom du locataire*&#62; AADCLIENTAPPID=&#60;*ID de l’application serveur pour l’intégration AAD*&#62; AADRESOURCEURI=https:&#47;/&#60;*ID de la ressource*&#62;”

Par exemple, si vous aviez les valeurs suivantes :

- **URL du point de terminaison de l’authentification mutuelle pour la passerelle de gestion cloud** : https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Utilisez la valeur **MutualAuthPath** dans la vue SQL **vProxy_Roles** pour la valeur **URL du point de terminaison de l’authentification mutuelle pour la passerelle de gestion cloud**.

- **Nom de domaine complet du point de gestion** : sccmmp.corp.contoso.com    
- **CodeSite** : PS1    
- **ID du locataire Azure AD** : 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Nom du locataire Azure AD** : contoso    
- **ID de l’application cliente Azure AD** : bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI de l’ID de la ressource AAD** : ConfigMgrServer    

  > [!Note]    
  > Utilisez la valeur **IdentifierUri** trouvée dans la vue SQL **vSMS_AAD_Application_Ex** pour la valeur **URI de l’ID de la ressource AAD**.

Vous utiliseriez la ligne de commande suivante :

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer”

> [!Tip]
> Pour trouver les paramètres de ligne de commande pour votre site, effectuez les étapes suivantes :     
> 1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Cogestion**.  
> 2. Sous l’onglet Accueil, dans le groupe Gérer, choisissez  **Configurer la cogestion** pour ouvrir l’Assistant Intégration de la cogestion.    
> 3. Dans la page Abonnement, cliquez sur **Se connecter** et connectez-vous à votre locataire Intune, puis cliquez sur **Suivant**.    
> 4. Dans la page Activation, cliquez sur **Copier** dans la section **Appareils inscrits dans Intune** pour copier la ligne de commande dans le Presse-papiers et l’enregistrer ensuite pour vous en servir ultérieurement dans la procédure de création de l’application.  
> 5. Cliquez sur **Annuler** pour quitter l’Assistant.

> [!Important]    
> Si vous personnalisez la ligne de commande pour installer le client Configuration Manager, vérifiez qu’elle ne dépasse pas 1 024 caractères. Quand la ligne de commande fait plus de 1024 caractères, l’installation du client échoue.


## <a name="new-windows-10-devices"></a>Nouveaux appareils Windows 10
Pour les nouveaux appareils Windows 10, vous pouvez utiliser le service Autopilot pour configurer le mode OOBE (Out Of Box Experience) qui inclut la jonction de l’appareil à AD et à Azure AD, ainsi que son inscription dans Intune. Ensuite, créez une application dans Intune pour déployer le client Configuration Manager.  
1. Activez AutoPilot pour les nouveaux appareils Windows 10. Pour plus d’informations, consultez [Présentation de Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).    

   > [!NOTE]   
   > À compter de la version 1802, utilisez Configuration Manager pour collecter et signaler les informations des appareils nécessaires à Microsoft Store pour Entreprises et Éducation. numéro de série, identificateur de produit Windows et identificateur matériel. Dans l’espace de travail **Monitoring** de la console de Configuration Manager, développez le nœud **Création de rapports**, puis **Rapports**, et sélectionnez le nœud **Matériel – Général**. Exécutez le nouveau rapport, **Informations sur les appareils Windows AutoPilot**, et affichez les résultats. Dans la visionneuse de rapports, cliquez sur l’icône **Exporter**, puis sélectionnez l’option **CSV (délimité par des virgules)**. Après avoir enregistré le fichier, chargez les données dans Microsoft Store pour Entreprises et Éducation. Pour plus d’informations, consultez la page [Ajouter des appareils dans Microsoft Store pour Entreprises et Éducation](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).

2. Configurez l’inscription automatique dans Azure AD pour que vos appareils soient inscrits automatiquement à Intune. Pour plus d’informations, consultez  [Inscrire des appareils Windows pour Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Créez une application dans Intune avec le package du client Configuration Manager et déployez l’application sur les appareils Windows 10 que vous souhaitez gérer conjointement. Utilisez la [ligne de commande pour installer un client Configuration Manager](#command-line-to-install-configuration-manager-client) lorsque vous suivez les étapes permettant d’[installer des clients à partir d’Internet avec Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Appareils Windows 10 non inscrits à Intune ou non-clients Configuration Manager
Pour les appareils Windows 10 qui ne sont pas inscrits à Intune ou qui n’ont pas le client Configuration Manager, vous pouvez utiliser l’inscription automatique pour les inscrire dans Intune. Ensuite, créez une application dans Intune pour déployer le client Configuration Manager.
1. Configurez l’inscription automatique dans Azure AD pour que vos appareils soient inscrits automatiquement à Intune. Pour plus d’informations, consultez  [Inscrire des appareils Windows pour Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Créez une application dans Intune avec le package du client Configuration Manager et déployez l’application sur les appareils Windows 10 que vous souhaitez gérer conjointement. Utilisez la [ligne de commande pour installer un client Configuration Manager](#command-line-to-install-configuration-manager-client) lorsque vous suivez les étapes permettant d’[installer des clients à partir d’Internet avec Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).

## <a name="windows-10-devices-enrolled-in-intune"></a>Appareils Windows 10 inscrits à Intune
Pour les appareils Windows 10 qui sont déjà inscrits à Intune, créez une application dans Intune pour déployer le client Configuration Manager. Utilisez la [ligne de commande pour installer un client Configuration Manager](#command-line-to-install-configuration-manager-client) lorsque vous suivez les étapes permettant d’[installer des clients à partir d’Internet avec Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

## <a name="next-steps"></a>Étapes suivantes
[Basculer les charges de travail de Configuration Manager sur Intune](co-management-switch-workloads.md)