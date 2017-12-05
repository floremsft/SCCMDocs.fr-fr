---
title: Assistant Services Azure
titleSuffix: Configuration Manager
description: "À propos de l’Assistant Services Azure pour System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 7646e8bc368e5c01ddef41592c513f7bd1643cdb
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurer les services Azure à utiliser avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

À compter de Current Branch version 1706, l’**Assistant Services Azure** est utilisé pour simplifier le processus de configuration des services Azure que vous utilisez avec Configuration Manager.

Cet Assistant fournit une expérience de configuration commune en utilisant une **inscription d’application web Azure AD** pour fournir des détails d’abonnement et de configuration et authentifier les communications avec Azure AD. Grâce à cette application web, vous n’avez pas besoin d’entrer ces mêmes informations chaque fois que vous configurez un nouveau composant ou service Configuration Manager avec Azure.

Les services Azure suivants peuvent être configurés à l’aide de l’Assistant Services Azure :
-   **Gestion cloud**   
    [Permettez aux clients de s’authentifier à l’aide d’Azure Active Directory](/sccm/core/clients/deploy/deploy-clients-cmg-azure) (Azure AD). Vous pouvez également [configurer la découverte des utilisateurs Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
-   **Connecteur OMS**
    [Connectez-vous à Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS) et synchronisez les données telles que les collections avec OMS Log Analytics.
-   **Upgrade Readiness**
    [Connectez-vous à Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) et consultez les données de compatibilité de mise à niveau des clients.
-   **Microsoft Store pour Entreprises** Connectez-vous à [Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) et obtenez des applications pour votre organisation que vous pouvez déployer avec Configuration Manager.

Quand vous utilisez l’Assistant pour configurer un service, plusieurs actions courantes sont disponibles.
À savoir :
-   *Configurer l’environnement Azure* : dans la page **Application** de l’Assistant, sélectionnez l’**environnement Azure** que vous utilisez. Consultez le contenu associé à chaque service afin de savoir si celui-ci prend en charge uniquement le cloud Azure public, ou s’il peut prendre en charge un cloud privé.
-   *Créer ou importer une application serveur* : dans la page **Application** de l’Assistant, vous pouvez **créer** et **importer** des métadonnées d’inscription d’application web Azure. Les options disponibles dépendent du service que vous configurez. En outre, certains services peuvent nécessiter une application supplémentaire. Par exemple, le service de **gestion cloud** requiert une **application cliente native** qui permet aux clients d’authentifier directement les communications avec les services Azure.


Pour obtenir des informations sur les applications web, consultez [Authentification et autorisation dans Azure App Service](/azure/app-service/app-service-authentication-overview) et [Vue d’ensemble des applications web](/azure/app-service-web/app-service-web-overview).


## <a name="webapp"></a> Créer ou importer une inscription d’application web Azure Active Directory à utiliser avec Configuration Manager

L’inscription d’application web des services Azure connecte votre site Configuration Manager à Azure AD et est un prérequis pour utiliser les services Azure avec votre infrastructure. Pour cela :

1.  Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis cliquez sur **Services Azure**.
2.  Sur l’onglet **Accueil**, sous le groupe **Services Azure**, cliquez sur **Configurer les services Azure**.
3.  Sur la page **Services Azure** de l’Assistant Services Azure, sélectionnez le service Azure que vous souhaitez connecter à Configuration Manager.
4.  Sur la page **Général** de l’assistant, spécifiez un nom et une description pour votre service Azure.
5.  Sur la page **Application** de l’assistant, sélectionnez votre environnement Azure dans la liste, puis cliquez sur **Parcourir** pour sélectionner *l’application web* et *l’application cliente native* (uniquement si nécessaire) qui permettront de configurer le service Azure.

    **Application web :** ouvre la fenêtre Application serveur.    
      Dans la fenêtre **Server App**, sélectionnez l’application serveur à utiliser, puis cliquez sur **OK**. Les applications serveur sont des inscriptions d’applications web Azure AD qui contiennent les configurations pour votre compte Azure, notamment l’ID de locataire, l’ID de client et une clé secrète pour les clients.
    Si aucune application n’est disponible, choisissez l’une des méthodes suivantes :

    - **Créer** : automatisez la création d’une inscription d’application web Azure AD en fonction des informations que vous entrez dans la console Configuration Manager. Entrez un nom convivial pour l’application, l’URL de la page d’accueil, l’URI de l’ID d’application et la période de validité de la clé secrète. Par défaut, la période de validité de la clé secrète est un an.
        
        Un utilisateur doit ensuite se connecter à l’aide de ses informations d’identification Azure AD pour terminer la création de l’application web dans Azure. Le compte que vous utilisez pour vous connecter à Azure n’a pas besoin d’être le même que celui qui exécute l’Assistant Services Azure. Une fois établie la connexion à Azure, Configuration Manager crée l’application web dans Azure, notamment l’ID de client et la clé secrète à utiliser avec l’application web. Ces informations sont ensuite disponibles dans le portail Azure.

        Quand vous utilisez *Créer* pour configurer une application web, Configuration Manager peut créer l’application web pour vous dans Azure AD.
    
    - **Importer** : entrez les informations sur une inscription d’application web Azure AD déjà créée dans le **portail Azure** pour importer les métadonnées relatives à cette inscription dans Configuration Manager. Indiquez un nom convivial pour l’application et le locataire, puis spécifiez l’ID de locataire, l’ID de client et la clé secrète de l’application web Azure que Configuration Manager doit utiliser. Après avoir vérifié les informations, cliquez sur **OK** pour continuer.
        > [!NOTE]
        > Avant de pouvoir effectuer l’**importation**, une inscription d’application Azure AD de type *application web / API* doit être créée dans le [portail Azure](https://portal.azure.com). Pour en savoir plus sur la création d’une inscription d’application, consultez [Inscrire votre application avec un client Azure Active Directory](/azure/active-directory/active-directory-app-registration). Pour la configuration d’Upgrade Readiness ou d’Operations Management Suite, vous devrez également accorder à l’application web que vous venez d’inscrire des autorisations de *contributeur* sur le groupe de ressources qui contient l’espace de travail OMS approprié pour que Configuration Manager puisse accéder à cet espace de travail. Pour ce faire, vous devrez rechercher le nom de l’inscription d’application dans le panneau **Ajouter des utilisateurs** au moment d’attribuer l’autorisation. Il s’agit du même processus que celui à suivre pour [accorder à Configuration Manager les autorisations d’accès à OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) pour les connexions à [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm). Ces autorisations doivent être attribuées avant que l’application soit importée dans Configuration Manager.


    **Application cliente native :** ouvre la fenêtre Application cliente.  
     Dans la fenêtre **Application cliente**, sélectionnez l’application cliente à utiliser, puis cliquez sur **OK**.

     Si aucune application cliente n’est disponible, choisissez l’une des méthodes suivantes :
     - **Créer** : pour créer une application cliente, cliquez sur **Créer**. Fournissez ensuite un nom convivial pour l’application et l’URI de redirection.

         Un utilisateur doit ensuite se connecter à l’aide de ses informations d’identification Azure AD pour terminer la création de l’application web dans Azure. Le compte que vous utilisez pour vous connecter à Azure n’a pas besoin d’être le même que celui qui exécute l’Assistant Services Azure. Une fois établie la connexion à Azure, Configuration Manager crée l’application cliente native dans Azure AD, notamment l’ID de client et la clé secrète. Ces informations sont ensuite disponibles dans le [portail Azure](https://portal.azure.com). 

     - **Importer** : utilisez une application cliente qui existe déjà dans votre abonnement Azure. Fournissez un nom convivial pour l’application et l’ID du client. Ensuite, cliquez sur **OK**.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  (Uniquement durant la configuration du service de **gestion cloud**) Dans la page **Découverte** de l’Assistant, cliquez sur **Activer la découverte d’utilisateurs Azure Active Directory**, puis sur **Paramètres**.
Dans la boîte de dialogue **Paramètres de découverte d’utilisateurs Azure AD**, configurez une planification pour déterminer quand la détection survient. Vous pouvez également activer la découverte delta, qui vérifie uniquement les comptes nouveaux ou modifiés dans Azure AD. Explorez la [découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

7.  Effectuez toutes les étapes de l'Assistant.

À ce stade, vous avez terminé la configuration d’un service Azure dans le Configuration Manager. Vous pouvez répéter ce processus pour configurer d’autres services Azure.

## <a name="view-the-configuration-of-an-azure-service"></a>Afficher la configuration d’un service Azure
Vous pouvez afficher les propriétés d’un service Azure que vous avez configuré en vue de son utilisation.

Dans la console, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Services Azure**. Ensuite, choisissez le service que vous souhaitez afficher ou modifier, puis cliquez sur **Propriétés**.
