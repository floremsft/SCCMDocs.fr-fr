---
title: "Gérer les applications à partir du Windows Store pour Entreprises | Microsoft Docs"
description: "Gérez et déployez les applications à partir du Windows Store pour Entreprises en utilisant System Center Configuration Manager."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f955b5aadfc617e08d5d933dee8e42de838f83c0
ms.openlocfilehash: bf2937f5ba86db19d9cb40e2c98cbb8ba365f7eb

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Gérer les applications à partir du Windows Store pour Entreprises avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le [Windows Store pour Entreprises](https://www.microsoft.com/business-store) vous donne accès à des applications Windows pour votre organisation que vous pouvez acheter individuellement ou en volume. En connectant le Windows Store à Configuration Manager, vous pouvez synchroniser la liste des applications que vous avez achetées avec Configuration Manager, les afficher dans la console Configuration Manager et les déployer comme n’importe quelle autre application.


## <a name="online-and-offline-apps"></a>Applications en ligne et hors connexion

Le Windows Store pour Entreprises prend en charge deux types d’application :

- **En ligne** : ce type de licence exige que les utilisateurs et les appareils se connectent au Windows Store pour obtenir une application et sa licence. Les appareils Windows 10 doivent être joints au domaine Azure Active Directory.
- **Hors connexion** : les organisations peuvent mettre en cache les applications et les licences à déployer directement dans leur réseau local, sans avoir à se connecter au Windows Store ni à disposer d’une connexion Internet.

En savoir plus sur le [Windows Store pour Entreprises](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview).

Configuration Manager prend en charge la gestion des applications du Windows Store pour Entreprises sur les appareils Windows 10 exécutant le client Configuration Manager, ainsi que sur les appareils Windows 10 inscrits auprès de Microsoft Intune (configuration hybride). Les fonctionnalités offertes par Configuration Manager pour les applications en ligne et hors connexion sont répertoriées ci-dessous.

> [!IMPORTANT]
> Pour utiliser ces fonctionnalités, les appareils Windows 10 doivent exécuter la version de novembre 2015 (1511) ou une version ultérieure.

|Fonctionnalité|Applications hors connexion|Applications en ligne|
|------------|------------|------------|
|Synchroniser des données d’application dans Configuration Manager<br>(la synchronisation se produit toutes les 24 heures, ou vous pouvez lancer une synchronisation immédiate)|Oui|Oui|
|Création d’applications Configuration Manager à partir d’applications du Windows Store|Oui|Oui|
|Prise en charge des applications gratuites du Windows Store|Oui|Oui<sup>1</sup>|
|Prise en charge des applications payantes du Windows Store|Non|Oui<sup>1</sup>|
|Prise en charge des déploiements obligatoires sur les regroupements d’utilisateurs ou d’appareils|Oui|Oui<sup>1</sup>|
|Prise en charge des déploiements disponibles sur les regroupements d’utilisateurs ou d’appareils|Oui<sup>2</sup>|Non|

<sup>1</sup>Prise en charge des appareils gérés par Intune uniquement. Il ne vous est pas interdit de créer une application en ligne dans la console Configuration Manager ni de la déployer sur un appareil géré par le client Configuration Manager, mais le déploiement échouera. Les utilisateurs seront dirigés vers la page correspondante de l’App Store d’où ils devront installer l’application manuellement.

<sup>2</sup>Prise en charge des appareils gérés par le client Configuration Manager uniquement.

<!--- ## Activate the Windows Store for Business capability
Because this is a pre-release feature, before you can connect Configuration Manager to the Windows Store for Business, you must take the following steps:

**Give your consent to use pre-release features**
1. In the **Administration** workspace of the Configuration Manager console, choose **Site Configuration** > **Sites**.
2. Select the top-level site in your hierarchy, then, open **Hierarchy Settings**.
3. In the **Hierarchy Settings Properties** dialog box, check the box, **Consent to use Pre-Release** features.
4. Choose **OK**.

**Activate the Windows Store for Business capability**
1. In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Features**.
2. Select **Windows Store for Business Integration**, and then in the **Home** tab, in the **Features** group, choose **Turn on**.
3. Close and re-open the Configuration Manager console.
4. You'll now see the node **Windows Store for Business** in the **Administration** workspace under **Cloud Services**. --->

## <a name="set-up-windows-store-for-business-synchronization"></a>Configurer la synchronisation du Windows Store pour Entreprises

> [!IMPORTANT]
> Quand vous configurez une connexion entre Configuration Manager et le Windows Store pour Entreprises, vous devez fournir un dossier où le contenu d’application synchronisé à partir du Windows Store sera conservé.
Pour vous assurer que ce dossier est sécurisé et que son contenu peut être déployé sur des appareils, vérifiez que les autorisations suivantes sont en place :
-    L’ordinateur sur lequel vous installez le rôle de système de site de point de connexion de service (le site de niveau supérieur dans la hiérarchie) doit disposer d’autorisations en lecture et en écriture sur le dossier que vous avez spécifié lors de l’utilisation du compte **Computer$**.
-    L’auteur de l’application doit avoir des autorisations en lecture sur le dossier spécifié.
-    Le compte **Computer$** de chaque ordinateur qui héberge une instance du fournisseur SMS doit être en mesure d’utiliser le dossier spécifié.


Dans Azure Active Directory, inscrivez Configuration Manager comme outil de gestion Application web ou API web. Vous obtenez ainsi un ID de client dont vous aurez besoin ultérieurement.
1. Dans le nœud Active Directory [https://manage.windowsazure.com](https://manage.windowsazure.com), sélectionnez votre Azure Active Directory, puis choisissez **Applications** > **Ajouter**.
2.  Choisissez **Ajouter une application développée par mon organisation**.
3.  Attribuez un nom à l’application, sélectionnez **Application web** et/ou **API web**, puis choisissez **Suivant**.
4.  Entrez la même URL tant pour **URL de connexion** que pour **URI ID d’application**. L’URL peut être une chaîne quelconque qui ne doit pas nécessairement correspondre à une adresse réelle. Par exemple, vous pouvez entrer *https://votredomaine/sccm*.
5.  Fermez l'Assistant.

Dans Azure Active Directory, créez une clé de client pour l’outil de gestion inscrit.
1.  Sélectionnez l’application que vous venez de créer, puis choisissez **Configurer**.
2.  Sous **Clés**, sélectionnez une durée dans la liste, puis choisissez **Enregistrer**. Cela a pour effet de créer une nouvelle clé de client. Ne quittez pas cette page tant que vous n’avez pas correctement intégré le Windows Store pour Entreprises à Configuration Manager.

Dans le Windows Store pour Entreprises, configurez Configuration Manager comme outil de gestion du Windows Store.
1.  Ouvrez [https://businessstore.microsoft.com/fr-fr/managementtools](https://businessstore.microsoft.com/en-us/managementtools) et connectez-vous si vous y êtes invité.
2.  Acceptez les conditions d’utilisation si cela vous est demandé.
3.  Sous **Outils de gestion**, choisissez **Ajouter un outil de gestion**.
4.  Dans **Rechercher l’outil par son nom**, tapez le nom de l’application que vous avez créée précédemment dans Azure Active Directory, puis choisissez **Ajouter**.
5.  Choisissez **Activer** en regard de l’application que vous venez d’importer.
6.  Dans la page **Gérer > Informations de compte**, sélectionnez **Afficher les applications sous licence hors connexion** si vous souhaitez autoriser l’achat d’applications sous licence hors connexion.

> [!Note]
> Si vous utilisez plusieurs outils de gestion pour déployer des applications Windows Store pour Entreprises, vous ne pouviez auparavant en associer qu’un à Windows Store pour Entreprises. Maintenant, vous pouvez associer plusieurs outils de gestion au magasin, par exemple, Intune et Configuration Manager.

Ajoutez le compte Windows Store à Configuration Manager.

1. Vérifiez que vous avez acheté au moins une application sur le Windows Store pour Entreprises. Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis choisissez **Windows Store pour Entreprises**.
2.  Sous l’onglet **Accueil**, dans le groupe **Windows Store pour Entreprises**, choisissez **Ajouter un compte Windows Store pour Entreprises**.
3.  Ajoutez vos ID de locataire, ID de client et clé secrète de client à partir d’Azure Active Directory, puis terminez l’Assistant.
4. À la fin de l’opération, le compte que vous avez configuré figure dans la liste **Windows Store pour Entreprises** de la console Configuration Manager.

Modifiez les langues d’application qui seront affichées dans le catalogue d’applications pour être téléchargées par les utilisateurs.

1.    Dans l’espace de travail **Administration** de la console Configuration Manager, choisissez **Services cloud** > **Mises à jour et maintenance** > **Windows Store pour Entreprises**.
2.    Sélectionnez votre compte Windows Store pour Entreprises, puis choisissez **Propriétés**.
3.    Sélectionnez l’onglet **Langue**.
4.    Ajoutez ou supprimez les langues qui seront affichées dans le catalogue d’applications. Sélectionnez la langue du catalogue d’applications par défaut qui sera mise à la disposition des utilisateurs.

>[!IMPORTANT]
>Dans cette version, si vous modifiez les langues qui seront synchronisées, vous devez redémarrer le service SMS Executive sur le serveur de site avant que les paramètres de langue ne prennent effet.


Modifiez la clé secrète du client à partir d’Azure Active Directory.

1.    Dans l’espace de travail **Administration** de la console Configuration Manager, choisissez **Services cloud** > **Mises à jour et maintenance** > **Windows Store pour Entreprises**.
2.    Sélectionnez votre compte Windows Store pour Entreprises, puis choisissez **Propriétés**.
3.    Dans la boîte de dialogue **Windows Store for Business Account Properties** (Propriétés du compte Windows Store pour Entreprises), entrez une nouvelle clé dans le champ **Clé secrète du client**, puis choisissez **Vérifier**. Une fois la vérification effectuée, choisissez **Appliquer**, puis fermez la boîte de dialogue.

## <a name="sync-apps-from-the-store-with-configuration-manager"></a>Synchroniser des applications du Windows Store à Configuration Manager

La synchronisation se produit toutes les 24 heures, ou vous pouvez lancer une synchronisation immédiate en procédant comme suit :

1. Dans l’espace de travail **Administration** de la console Configuration Manager, choisissez **Services cloud** > **Mises à jour et maintenance** > **Windows Store pour Entreprises**.
3.    Sous l’onglet **Accueil**, dans le groupe **Synchroniser**, choisissez **Synchroniser maintenant**.
4.    L’application que vous avez achetée apparaît dans le nœud **Informations de licence pour les applications du Store** de l’espace de travail **Gestion des applications**.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Créer et déployer une application Configuration Manager à partir d’une application du Windows Store pour Entreprises

Cette procédure suppose que vous avez acquis au moins une application gratuite ou acheté au moins une applications sous licence en ligne payante sur le Windows Store pour Entreprises.

1.  Dans l’espace de travail **Bibliothèque de logiciels** de la console Configuration Manager, développez **Gestion des applications**, puis choisissez **Informations de licence pour les applications du Store**.
2.  Choisissez l’application que vous voulez déployer puis, sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une application**.
Une application Configuration Manager contenant l’application du Windows Store pour Entreprises est alors créée. Vous pouvez ensuite déployer et surveiller cette application comme n’importe quelle autre application Configuration Manager.

> [!IMPORTANT]
> Pour les appareils inscrits auprès d’Intune, les applications déployées sont uniquement accessibles à l’utilisateur qui est à l’origine de l’inscription de l’appareil. Aucun autre utilisateur ne peut utiliser l’application.

## <a name="monitor-windows-store-for-business-apps"></a>Surveiller des applications du Windows Store pour Entreprises

Dans l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications**, puis choisissez **Informations de licence pour les applications du Store**.

Pour chaque application du Windows Store que vous gérez, vous pouvez afficher des informations la concernant, notamment le nom, la plateforme et le nombre de licences que vous possédez pour l’application, ainsi que le nombre de licences disponibles.



<!--HONumber=Feb17_HO3-->


