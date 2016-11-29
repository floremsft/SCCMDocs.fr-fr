---
title: "Synchroniser les données | Microsoft Operations Management Suite | System Center Configuration Manager"
description: "Synchronisez les données de System Center Configuration Manager vers Microsoft Operations Management Suite."
ms.custom: na
ms.date: 10/13/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: 5786f0734ce186601f5173003b9b133ed6ae8b11

---
# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Synchroniser les données de System Center Configuration Manager vers Microsoft Operations Management Suite

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser le connecteur Microsoft Operations Management Suite (OMS) pour synchroniser les données, comme vos regroupements, de System Center Configuration Manager vers OMS. Les données de votre déploiement Configuration Manager deviennent alors visibles dans OMS.

## <a name="add-an-oms-connection-to-configuration-manager"></a>Ajouter une connexion OMS à Configuration Manager

Pour ajouter une connexion OMS, votre environnement Configuration Manager doit d’abord configurer un [point de connexion de service](../../../core/servers/deploy/configure/about-the-service-connection-point.md) dans un [mode en ligne](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/). Quand vous ajoutez une connexion OMS à votre environnement, Microsoft Monitoring Agent est également installé sur l’ordinateur exécutant ce rôle de système de site.
1.  Dans l’espace de travail **Administration**, sélectionnez **Connecteur OMS**. Dans le ruban, cliquez sur « Créer une connexion à Operations Management Suite ». L’**Assistant Connexion à Operation Management Suite** s’ouvre. Sélectionnez **Suivant**.
2.  Dans l’écran **Général**, vérifiez que vous disposez des informations suivantes, puis sélectionnez **Suivant**.

    * Configuration Manager inscrit en tant qu’outil de gestion « Application web et/ou API web » et présence de l’[ID de client résultant de cette inscription](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
    * Clé de client créée pour l’outil de gestion inscrit dans Azure Active Directory.
    * Dans le portail de gestion Azure, application web inscrite disposant d’une autorisation d’accès à OMS, comme décrit dans [Accorder à Configuration Manager les autorisations d’accès à OMS](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

3.  Dans l’écran **Azure Active Directory**, configurez vos paramètres de connexion à OMS en renseignant les champs **Locataire**, **ID Client** et **Clé secrète du client**, puis sélectionnez **Suivant**.
4.  Dans l’écran **Configuration de la connexion OMS**, définissez vos paramètres de connexion en renseignant les champs **Abonnement Azure**, **Groupe de ressources Azure** et **Espace de travail Operations Management Suite**.
5.  Vérifiez vos paramètres de connexion dans l’écran **Résumé**, puis sélectionnez **Suivant**. L’écran **Progression** indique l’état de connexion, puis **Terminé**.

> [!NOTE]
> Vous devez connecter OMS au site de niveau supérieur de votre hiérarchie. Si vous connectez OMS à un site principal autonome et que vous ajoutez ensuite un site d’administration centrale à votre environnement, vous devez supprimer et recréer la connexion OMS au sein de la nouvelle hiérarchie.

Après avoir lié Configuration Manager à OMS, vous pouvez ajouter ou supprimer des regroupements et afficher les propriétés de la connexion OMS.

## <a name="viewing-microsoft-operations-management-suite-connection-properties-in-configuration-manager"></a>Affichage des propriétés de connexion de Microsoft Operations Management Suite dans Configuration Manager

1.  Accédez à **Services cloud**, puis sélectionnez **Connecteur OMS** pour ouvrir la page **Propriétés de connexion OMS**.
2.  Cette page contient deux onglets :
  * L’onglet **Azure Active Directory** affiche votre **Locataire**, l’**ID Client**, l’**Expiration de la clé secrète client** et vous permet de **vérifier** votre **Clé secrète client** si elle a expiré.
  * L’onglet **Propriétés de connexion OMS** affiche votre **Abonnement Azure**, votre **Groupe de ressources Azure**, l’**Espace de travail Operations Management Suite**, ainsi que la liste des **Regroupements d’appareils pour lesquels Operations Management Suite peut obtenir des données**. Utilisez les boutons **Ajouter** et **Supprimer** pour modifier les collections autorisées.



<!--HONumber=Nov16_HO1-->


