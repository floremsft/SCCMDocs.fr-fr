---
title: "Synchroniser les données | Microsoft Docs | Microsoft Operations Management Suite "
description: "Synchronisez les données de System Center Configuration Manager vers Microsoft Operations Management Suite."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 3acfaa2cf8c64ece5cef65b80372067336d6a815
ms.lasthandoff: 03/27/2017

---


# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Synchroniser les données de System Center Configuration Manager vers Microsoft Operations Management Suite


*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser le connecteur Microsoft Operations Management Suite (OMS) pour synchroniser les données, comme vos regroupements, de System Center Configuration Manager vers OMS Log Analytics dans Microsoft Azure. Les données de votre déploiement Configuration Manager deviennent alors visibles dans OMS.
> [!TIP]
> La fonctionnalité Connecteur OMS est une préversion. Pour plus d’informations, consultez [Utiliser des fonctionnalités de préversion des mises à jour](/sccm/core/servers/manage/pre-release-features).

Depuis la version 1702, vous pouvez utiliser le connecteur OMS pour vous connecter à un espace de travail OMS figurant sur le Microsoft Azure Government Cloud. Pour cela, vous devez modifier un fichier de configuration avant d’installer le connecteur OMS. Consultez la section [Utiliser le connecteur OMS avec Azure Government Cloud](#fairfaxconfig) dans cette rubrique.

## <a name="prerequisites"></a>Prérequis
- Avant d’installer le connecteur OMS dans Configuration Manager, vous devez accorder à Configuration Manager les autorisations d’accès à OMS. Plus précisément, vous devez accorder un *accès Contributeur* au *groupe de ressources* Azure qui contient l’espace de travail OMS Log Analytics. Les procédures à suivre sont documentées dans le contenu Log Analytics. Consultez la rubrique [Accorder à Configuration Manager les autorisations d’accès à OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) dans la documentation OMS.

- Le connecteur OMS doit être installé sur l’ordinateur qui héberge un [point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point) se trouvant en [mode en ligne](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

  Si vous avez connecté OMS à un site principal autonome et que vous prévoyez d’ajouter un site d’administration centrale à votre environnement, vous devez supprimer la connexion actuelle puis reconfigurer le connecteur sur le nouveau site d’administration centrale.

- Vous devez installer un Microsoft Monitoring Agent pour OMS sur le point de connexion de service ainsi que le connecteur OMS.  L’agent et le connecteur OMS doivent être configurés pour utiliser le même **espace de travail OMS**. Pour installer l’agent, consultez [Télécharger et installer l’agent](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) dans la documentation OMS.

- Après avoir installé le connecteur et l’agent, vous devez configurer OMS pour utiliser les données Configuration Manager.  Pour ce faire, dans le portail OMS, [importez des regroupements Configuration Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).



## <a name="install-the-oms-connector"></a>Installer le connecteur OMS  
1. Dans la console Configuration Manager, configurez votre [hiérarchie pour utiliser les fonctionnalités de la version préliminaire](/sccm/core/servers/manage/pre-release-features), puis activez l’utilisation du connecteur OMS.  

2. Ensuite, accédez à **Administration** > **Services de cloud** > **Connecteur OMS**. Dans le ruban, cliquez sur « Créer une connexion à Operations Management Suite ». L’**Assistant Connexion à Operation Management Suite** s’ouvre. Sélectionnez **Suivant**.  


3.    Dans la page **Général**, vérifiez que vous disposez des informations suivantes, puis sélectionnez **Suivant**.  
  - Configuration Manager inscrit en tant qu’outil de gestion « Application web et/ou API web » et présence de l’[ID de client résultant de cette inscription](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).  
  - Clé de client créée pour l’outil de gestion inscrit dans Azure Active Directory.  

  - Dans le portail de gestion Azure, application web inscrite disposant d’une autorisation d’accès à OMS, comme décrit dans [Accorder à Configuration Manager les autorisations d’accès à OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).  

4.    Dans la page **Azure Active Directory**, configurez vos paramètres de connexion à OMS en renseignant les champs **Locataire**, **ID Client** et **Clé secrète du client**, puis sélectionnez **Suivant**.  

5.    Dans la page **Configuration de la connexion OMS**, définissez vos paramètres de connexion en renseignant les champs **Abonnement Azure**, **Groupe de ressources Azure** et **Espace de travail Operations Management Suite**.  L’espace de travail doit correspondre à l’espace de travail configuré pour Microsoft Management Agent installé sur le point de connexion de service.  

6.    Vérifiez vos paramètres de connexion dans la page **Résumé**, puis sélectionnez **Suivant**. La page **Progression** indique l’état de connexion, puis **Terminé**.

Après avoir lié Configuration Manager à OMS, vous pouvez ajouter ou supprimer des regroupements et afficher les propriétés de la connexion OMS.

## <a name="verify-the-oms-connector-properties"></a>Vérifiez les propriétés du connecteur OMS
1.    Dans la console Configuration Manager, accédez à **Administration** > **Services cloud**, puis sélectionnez **Connecteur OMS** afin d’ouvrir la page **Connexion OMS****.
2.    Cette page contient deux onglets :
  - **Azure Active Directory :**   
    Cet onglet affiche votre **Llcataire**, l’**ID client**, l’**expiration de la clé secrète client** et vous permet de vérifier si votre clé secrète client a expiré.

  - **Propriétés de connexion OMS :**  
    Cet onglet affiche votre **Abonnement Azure**, votre **Groupe de ressources Azure**, l’**Espace de travail Operations Management Suite**, ainsi que la liste des **Regroupements d’appareils pour lesquels Operations Management Suite peut obtenir des données**. Utilisez les boutons **Ajouter** et **Supprimer** pour modifier les collections autorisées.

## <a name="fairfaxconfig"> </a> Utiliser le connecteur OMS avec Azure Government Cloud


1.  Sur les ordinateurs où est installée la console Configuration Manager, modifiez le fichier de configuration suivant pour qu’il pointe vers Azure Government Cloud : ***&lt;Chemin d’installation de Configuration Manager>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Modifications :**

    Modifiez la valeur du nom de paramètre *FairFaxArmResourceID* pour qu’elle corresponde à « https://management.usgovcloudapi.net/ »

   - **Avant modification :**
      &lt;nom du paramètre="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Après modification :**     
      &lt;nom du paramètre="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Modifiez la valeur du nom de paramètre *FairFaxAuthorityResource* pour qu’elle corresponde à « https://login.microsoftonline.com/ »

  - **Avant modification :**
    &lt;nom de paramètre="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **Après modification :**
    &lt;nom du paramètre="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.com/&lt;/value>

2.    Après avoir apporté ces deux modifications et enregistré le fichier, redémarrez la console Configuration Manager sur le même ordinateur, puis utilisez cette console pour installer le connecteur OMS. Pour installer le connecteur, utilisez les informations situées sous [Synchroniser les données de System Center Configuration Manager vers Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), puis sélectionnez l’**Espace de travail Operations Management Suite** qui se trouve dans Microsoft Azure Government Cloud.

3.    Une fois le connecteur OMS installé, une connexion à Azure Government Cloud est disponible lorsque vous utilisez une console se connectant au site.

