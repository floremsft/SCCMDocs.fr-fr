---
title: Assistant Services Azure | Microsoft Docs
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
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 22203b358830903cf2e531c0532ae3111b8265fc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurer les services Azure à utiliser avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Depuis Current Branch version 1706, **l’Assistant Services Azure** est utilisé pour simplifier le processus de configuration des services Azure que vous utilisez avec Configuration Manager.

Cet Assistant fournit une expérience de configuration commune en utilisant une **application web Azure** pour fournir des détails d’abonnement et de configuration. Grâce à cette application web, vous n’avez pas besoin d’entrer ces mêmes informations chaque fois que vous configurez un nouveau composant ou service Configuration Manager avec Azure.

Les services Azure suivants sont configurés à l’aide de l’Assistant Configurer les services Azure :
-   **Gestion cloud**   
    [Permettez aux clients de s’authentifier à l’aide d’Azure Active Directory]() (Azure AD). Vous pouvez également [configurer la découverte des utilisateurs Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
-   **Connecteur OMS**
    [Connectez-vous à Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS) et synchronisez les données telles que les collections avec OMS Log Analytics.
-   **Upgrade Readiness**
    [Connectez-vous à Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) et consultez les données de compatibilité de mise à niveau des clients.
-   **Windows Store pour Entreprises** Connectez-vous à la boutique en ligne de [Windows Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) et obtenez des applications pour votre organisation que vous pouvez déployer avec Configuration Manager.

Quand vous utilisez l’Assistant pour configurer un service, plusieurs actions courantes sont disponibles.
à savoir :
-   Configurer l’environnement Azure : dans la page **Application** de l’Assistant, vous sélectionnez **l’environnement Azure** que vous utilisez. Consultez le contenu associé à chaque service afin de savoir si celui-ci prend en charge uniquement le cloud Azure public, ou s’il peut prendre en charge un cloud privé.
-   Créer ou importer une application serveur : dans la page **Application** de l’Assistant, vous pouvez **créer** et **importer** des applications web Azure. Les options disponibles dépendent du service que vous configurez.  En outre, certains services peuvent nécessiter une application supplémentaire. Par exemple, un service peut nécessiter également une **application cliente native**.


Pour obtenir des informations sur les applications web, consultez [Authentification et autorisation dans Azure App Service](/azure/app-service/app-service-authentication-overview) et [Vue d’ensemble des applications web](/azure/app-service-web/app-service-web-overview).


## <a name="webapp"></a> Créer l’application web Azure à utiliser avec Configuration Manager

L’application web des services Azure connecte votre site Configuration Manager à Azure AD et est un prérequis pour utiliser les services Azure avec votre infrastructure. Pour cela :

1.  Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis cliquez sur **Services Azure**.
2.  Sur l’onglet **Accueil**, sous le groupe **Services Azure**, cliquez sur **Configurer les services Azure**.
3.  Sur la page **Services Azure** de l’assistant de services Azure, sélectionnez **Gestion cloud** pour permettre aux clients de s’authentifier auprès de la hiérarchie à l’aide d’Azure AD.
4.  Sur la page **Général** de l’assistant, spécifiez un nom et une description pour votre service Azure.
5.  Dans la page **Application** de l’assistant, sélectionnez votre environnement Azure dans la liste, puis cliquez sur **Parcourir** pour sélectionner *l’application web* et *l’application cliente native* qui permettent de configurer le service Azure.     
    **Application web :** ouvre la fenêtre Application serveur.    
      Dans la fenêtre **Server App**, sélectionnez l’application serveur à utiliser, puis cliquez sur **OK**. Les applications serveur sont des applications web Azure qui contiennent les configurations pour votre compte Azure, notamment l’ID de locataire, l’ID de client et une clé secrète pour les clients.
    Si aucune application n’est disponible, choisissez l’une des méthodes suivantes :
        - **Créer** : pour créer une application serveur, cliquez sur **Créer**. Ensuite, entrez un nom convivial pour l’application, l’URL de la page d’accueil, l’URI de l’ID d’application et la période de validité de la clé secrète. Par défaut, la période de validité de la clé secrète est un an.

         Ensuite, une personne doit se connecter à Azure pour terminer la création de l’application web dans Azure. Le compte que vous utilisez pour vous connecter à Azure n’a pas besoin d’être le même que celui qui exécute l’Assistant Services Azure. Une fois établie la connexion à Azure, Configuration Manager crée l’application web dans Azure, notamment l’ID de client et la clé secrète à utiliser avec l’application web. Ces informations sont ensuite disponibles dans le portail Azure.

         Quand vous utilisez Créer pour configurer une application web, Configuration Manager peut créer l’application web pour vous dans Azure AD.
        - **Importer** : pour utiliser une application web qui existe déjà dans votre abonnement Azure, cliquez sur **Importer**. Indiquez un nom convivial pour l’application et le locataire, puis spécifiez l’ID de locataire, l’ID de client et la clé secrète de l’application web Azure que Configuration Manager doit utiliser. Après avoir vérifié les informations, cliquez sur **OK** pour continuer.

          Cette option n’est pas disponible pour tous les services que vous pouvez configurer.

   **Application cliente native :** ouvre la fenêtre Application cliente.  
     Dans la fenêtre **Application cliente**, sélectionnez l’application cliente à utiliser, puis cliquez sur **OK**.

     Si aucune application cliente n’est disponible, choisissez l’une des méthodes suivantes :
     - **Créer** : pour créer une application cliente, cliquez sur **Créer**. Ensuite, fournissez un nom convivial pour l’application et l’URL de réponse.

          Ensuite, une personne doit se connecter à Azure pour terminer la création de l’application cliente dans Azure. Le compte que vous utilisez pour vous connecter à Azure n’a pas besoin d’être le même que celui qui exécute l’Assistant Services Azure. Une fois établie la connexion à Azure, Configuration Manager crée l’application cliente native dans Azure, notamment l’ID de client à utiliser avec l’application web. Ces informations sont ensuite disponibles dans le portail Azure.
          Quand vous utilisez Créer pour configurer l’application, Configuration Manager peut créer l’application cliente native pour vous dans Azure AD.
     - **Importer** : pour utiliser une application cliente qui existe déjà dans votre abonnement Azure, cliquez sur **Importer**. Fournissez un nom convivial pour l’application et l’ID du client. Ensuite, cliquez sur **OK**.
           Cette option n’est pas disponible pour tous les services que vous pouvez configurer.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  Dans la page **Découverte** de l’Assistant, cliquez sur **Activer la découverte d’utilisateurs Azure Active Directory**, puis cliquez sur **Paramètres**.
Dans la boîte de dialogue **Paramètres de découverte d’utilisateurs Azure AD**, configurez une planification pour déterminer quand la détection survient. Vous pouvez également activer la découverte delta, qui vérifie uniquement les comptes nouveaux ou modifiés dans Azure AD. Explorez la [découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).
 
 7. Effectuez toutes les étapes de l'Assistant.

À ce stade, vous avez connecté votre site Configuration Manager à Azure AD.

## <a name="view-the-configuration-of-an-azure-service"></a>Afficher la configuration d’un service Azure
Vous pouvez afficher les propriétés d’un service Azure que vous avez configuré en vue de son utilisation.

Dans la console, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Services Azure**. Ensuite, choisissez le service que vous souhaitez afficher ou modifier, puis cliquez sur **Propriétés**.
