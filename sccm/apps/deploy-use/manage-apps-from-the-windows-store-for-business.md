---
title: "Gérer les applications à partir du Windows Store pour Entreprises | System Center Configuration Manager"
description: "Gérez et déployez les applications à partir du Windows Store pour Entreprises en utilisant System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e293b2ec4debf7a8513f1e3544ac234616f04d7

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Gérer les applications à partir du Windows Store pour Entreprises avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le [Windows Store pour Entreprises](https://www.microsoft.com/business-store) vous donne accès à des applications Windows pour votre organisation que vous pouvez acheter individuellement ou en volume. En connectant le Windows Store à Configuration Manager, vous pouvez synchroniser la liste des applications que vous avez achetées avec Configuration Manager, les afficher dans la console Configuration Manager et les déployer comme n’importe quelle autre application.


## <a name="online-and-offline-apps"></a>Applications en ligne et hors connexion

Le Windows Store pour Entreprises prend en charge deux types d’application :

- **En ligne** : ce type de licence exige que les utilisateurs et les appareils se connectent au Windows Store pour obtenir une application et sa licence. Les appareils Windows 10 doivent être joints au domaine Azure Active Directory.
- **Hors connexion** : les organisations peuvent mettre en cache les applications et les licences à déployer directement dans leur réseau local, sans avoir à se connecter au Windows Store ni à disposer d’une connexion Internet.

[En savoir](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview) plus sur le Windows Store pour Entreprises.

Configuration Manager prend en charge la gestion des applications du Windows Store pour Entreprises sur les appareils Windows 10 exécutant le client Configuration Manager, ainsi que sur les appareils Windows 10 inscrits auprès de Microsoft Intune (ce que l’on appelle une configuration hybride). Les fonctionnalités offertes par Configuration Manager pour les applications en ligne et hors connexion sont répertoriées ci-dessous.

> [!IMPORTANT]
> Pour utiliser cette fonctionnalité, les appareils Windows 10 doivent exécuter la version de novembre 2015 (1511) ou une version ultérieure.

|Fonctionnalité|Applications hors connexion|Applications en ligne|
|------------|------------|------------|
|Synchronisation des données d’application dans Configuration Manager<br>(la synchronisation a lieu toutes les 24 heures)|Oui|Oui|
|Création d’applications Configuration Manager à partir d’applications du Windows Store|Oui|Oui|
|Prise en charge des applications gratuites du Windows Store|Oui|Oui|
|Prise en charge des applications payantes du Windows Store|Non|Non|
|Prise en charge des déploiements obligatoires sur les regroupements d’utilisateurs ou d’appareils|Oui|Oui<sup>1</sup>|
|Prise en charge des déploiements disponibles sur les regroupements d’utilisateurs ou d’appareils|Oui<sup>3</sup>|Non<sup>2</sup>|

<sup>1</sup>Prend en charge les appareils gérés par Intune uniquement. Bien qu’il ne vous soit pas interdit de créer une application en ligne dans la console Configuration Manager et de la déployer sur un appareil géré par le client Configuration Manager, elle ne fonctionnera pas. L’utilisateur final sera dirigé vers la page correspondante du magasin d’applications d’où il devra installer l’application manuellement.

<sup>2</sup>Les applications en ligne peuvent être déployées comme étant disponibles pour les regroupements d’utilisateurs ou d’appareils gérés par le client Configuration Manager uniquement mais, quand l’utilisateur final sélectionne une application de ce type dans le Centre logiciel, il est dirigé vers le Windows Store pour Entreprises d’où il doit installer l’application manuellement. Les déploiements disponibles sur les appareils inscrits auprès de Microsoft Intune ne sont pas pris en charge.

<sup>3</sup>Non pris en charge pour les appareils gérés par Intune.

> [!IMPORTANT]
> Dans cette version, si vous possédez une hiérarchie Configuration Manager contenant un site d’administration centrale et au moins un site principal, le déploiement d’applications hors connexion du Windows Store pour Entreprises vers des appareils gérés par Intune se soldera par un échec.


## <a name="activate-the-windows-store-for-business-capability"></a>Activer la fonctionnalité Windows Store pour Entreprises
S’agissant d’une fonctionnalité en version préliminaire, pour pouvoir connecter Configuration Manager au Windows Store pour Entreprises, vous devez effectuer les opérations suivantes :

**Donnez votre accord pour utiliser les fonctionnalités en version préliminaire**
1. Dans l’espace de travail **Administration** de la console Configuration Manager, cliquez sur **Configuration du site** > **Sites**.
2. Sélectionner le site de niveau supérieur de votre hiérarchie, puis ouvrez **Paramètres de hiérarchie**.
3. Dans la boîte de dialogue **Propriétés des paramètres de hiérarchie**, cochez la case **Accepter d’utiliser les fonctionnalités en version préliminaire**.
4. Cliquez sur **OK**.

**Activez la fonctionnalité Windows Store pour Entreprises**
1. Dans l’espace de travail **Administration** de la console Configuration Manager, cliquez sur **Services cloud** > **Mises à jour et maintenance** > **Fonctionnalités**.
2. Sélectionnez **Windows Store pour l’intégration professionnelle** puis, sous l’onglet **Accueil**, dans le groupe **Fonctionnalités**, cliquez sur **Activer**.
3. Fermez et rouvrez la console Configuration Manager.
4. Le nœud **Windows Store pour Entreprises** figure désormais dans l’espace de travail **Administration**, sous **Services cloud**.

## <a name="set-up-windows-store-for-business-synchronization"></a>Configurer la synchronisation du Windows Store pour Entreprises

**Dans Azure Active Directory, inscrivez Configuration Manager en tant qu’outil de gestion « Application web et/ou API web ». Vous obtenez alors un ID de client dont vous aurez besoin par la suite.**
1. Dans le nœud Active Directory de [https://manage.windowsazure.com](https://manage.windowsazure.com), sélectionnez votre Azure Active Directory, puis cliquez sur **Applications** > **Ajouter**.
2.  Cliquez sur **Ajouter une application développée par mon organisation**.
3.  Attribuez un nom à l’application, sélectionnez **Application web** et/ou **API web**, puis cliquez sur la flèche **Suivant**.
4.  Entrez la même URL pour **URL de connexion** et pour **URI ID d’application**. L’URL peut être une chaîne quelconque qui ne doit pas nécessairement correspondre à une adresse réelle. Par exemple, vous pouvez entrer *https://votredomaine/sccm*.
5.  Effectuez toutes les étapes de l'Assistant.

**Dans Azure Active Directory, créez une clé de client pour l’outil de gestion inscrit**.
1.  Sélectionnez l’application que vous venez de créer, puis cliquez sur **Configurer**.
2.  Sous **Clés**, sélectionnez une durée dans la liste, puis cliquez sur **Enregistrer**. Cela a pour effet de créer une nouvelle clé de client. Ne quittez pas cette page tant que vous n’avez pas correctement intégré Windows Store pour Entreprises à Configuration Manager.

**Dans le Windows Store pour Entreprises, configurez Configuration Manager en tant qu’outil de gestion de magasin**.
1.  Ouvrez [https://businessstore.microsoft.com/fr-fr/managementtools](https://businessstore.microsoft.com/en-us/managementtools) et connectez-vous si vous y êtes invité.
2.  Acceptez les conditions d’utilisation si cela vous est demandé.
3.  Sous **Outils de gestion**, cliquez sur **Ajouter un outil de gestion**.
4.  Dans **Rechercher l’outil par son nom**, tapez le nom de l’application que vous avez créée précédemment dans AAD, puis cliquez sur **Ajouter**.
5.  Cliquez sur **Activer** en regard de l’application que vous venez d’importer.
6.  Dans la page **Gérer > Informations de compte**, sélectionnez **Afficher les applications sous licence hors connexion** si vous souhaitez autoriser l’achat d’applications sous licence hors connexion.

**Ajouter le compte Windows Store à Configuration Manager**

1. Vérifiez que vous avez acheté au moins une application sur le Windows Store pour Entreprises. Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis cliquez sur **Windows Store pour Entreprises**.
2.  Sous l’onglet **Accueil**, dans le groupe **Windows Store pour Entreprises**, cliquez sur **Ajouter un compte Windows Store pour Entreprises**.
3.  Ajoutez vos ID de locataire, ID de client et clé de client à partir d’Azure Active Directory, puis fermez l’Assistant.
4. À la fin de l’opération, le compte que vous avez configuré figure dans la liste **Windows Store pour Entreprises** de la console Configuration Manager.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Créer et déployer une application Configuration Manager à partir d’une application du Windows Store pour Entreprises
1.  Dans l’espace de travail **Bibliothèque de logiciels** de la console Configuration Manager, développez **Gestion des applications**, puis cliquez sur **Informations de licence pour les applications du Store**.
2.  Choisissez l’application que vous voulez déployer, puis, sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Créer une application**.
Une application Configuration Manager contenant l’application du Windows Store pour Entreprises est alors créée. Vous pouvez ensuite déployer et surveiller cette application comme n’importe quelle autre application Configuration Manager.

> [!IMPORTANT]
> Pour les appareils inscrits auprès d’Intune, les applications déployées sont uniquement accessibles à l’utilisateur qui est à l’origine de l’inscription de l’appareil. Aucun autre utilisateur ne peut accéder à l’application.

## <a name="monitor-windows-store-for-business-apps"></a>Surveiller des applications du Windows Store pour Entreprises

Dans l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications**, puis cliquez sur **Informations de licence pour les applications du Store**.

Pour chaque application du Windows Store que vous gérez, vous pouvez afficher des informations la concernant, notamment le nom, la plateforme et le nombre de licences que vous possédez pour l’application, ainsi que le nombre de licences disponibles.



<!--HONumber=Nov16_HO1-->


