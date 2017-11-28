---
title: "Changer l’autorité MDM pour des utilisateurs spécifiques (autorité MDM mixte)"
titleSuffix: Configuration Manager
description: "Découvrez comment changer l’autorité MDM en passant de MDM hybride à la version autonome d’Intune pour certains utilisateurs."
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/14/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 31d1d84c225d041f644669f0d3279e6bcd3f75ba
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2017
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Changer l’autorité MDM pour des utilisateurs spécifiques (autorité MDM mixte) 

*S’applique à : System Center Configuration Manager (Current Branch)*    

Vous pouvez configurer une autorité MDM mixte dans le même locataire en choisissant de gérer certains utilisateurs dans Intune et d’autres avec MDM hybride (Intune intégré à Configuration Manager). Cette rubrique fournit des informations sur la façon de commencer à déplacer les utilisateurs vers la version autonome d’Intune autonome et part du principe que vous avez terminé les étapes suivantes :
- Utilisation de l’outil d’importation de données pour [importer des objets Configuration Manager dans Intune](migrate-import-data.md) (facultatif).
- [préparer Intune à la migration des utilisateurs](migrate-prepare-intune.md) pour que les utilisateurs et leurs appareils restent gérés après la migration ;

> [!Note]    
> Si vous décidez d’effectuer une réinitialisation complète de votre locataire, ce qui supprimera toutes les stratégies, applications et inscriptions d’appareils, appelez le support pour obtenir de l’aide.

Les utilisateurs qui ont migré et leurs appareils sont gérés dans Intune tandis que les autres appareils continuent d’être gérés dans Configuration Manager. Vous allez commencer avec un petit groupe d’utilisateurs de test pour vérifier que tout fonctionne comme prévu. Ensuite, vous allez faire migrer progressivement les autres groupes d’utilisateurs jusqu’à ce que vous soyez prêt à faire basculer l’autorité MDM au niveau du locataire depuis Configuration Manager vers la version autonome d’Intune. 

## <a name="things-to-know-before-you-migrate-users"></a>Éléments à connaître avant de lancer la migration des utilisateurs
- Lors de la migration en plusieurs phases, toutes les stratégies ou applications MDM existantes dans Configuration Manager continuent à s’appliquer aux appareils MDM hybrides.
- Les utilisateurs sont ajoutés à un groupe AAD que vous désignez comme votre groupe de migration. Tous les appareils associés aux utilisateurs inclus dans le groupe de migration sont gérées dans Intune.
- Si des appareils sont ajoutés au groupe AAD, ils sont ignorés, sauf s’ils n’ont pas d’utilisateur associé.
- Les utilisateurs non inclus dans un groupe AAD marqués pour la migration héritent automatiquement de l’autorité MDM au niveau du locataire (Configuration Manager).
- Lorsque vous faites migrer un utilisateur vers Intune, ses appareils et lui apparaissent dans Intune dans le portail Azure à l’issue de 15 minutes environ.  
- Lorsque vous faites migrer des utilisateurs vers la version autonome d’Intune, continuez à gérer les paramètres suivants à partir de Configuration Manager pour les appareils MDM hybrides et de la version autonome d’Intune :
    - [Certificat Apple Push Notification Service (APNs)](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)
    - [Programme d’inscription des appareils](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)
    - Profils d’inscription
    - [Licences du programme d’achat en volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)
    - Identificateurs d’entreprise 
    - [Certificats de signature de code](/sccm/mdm/deploy-use/enroll-hybrid-windows)
    - [Catégories d’appareils](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)
    - [Gestionnaires d’inscription](/sccm/mdm/plan-design/device-enrollment-methods)
    - Conditions générales
    - SLK Windows
    - Personnalisation du portail d’entreprise    
      
> [!Important]    
  > Continuez à modifier les stratégies au niveau du locataire à l’aide de la console Configuration Manager. Après avoir [remplacé votre autorité MDM au niveau du locataire](change-mdm-authority.md) par Intune, vous allez gérer ces stratégies dans Intune sur Azure. 
- Nous vous recommandons de ne pas faire migrer des comptes d’utilisateur qui ont été ajoutés en tant que gestionnaires d’inscription d’appareil dans Configuration Manager. Plus tard, quand vous remplacerez votre autorité MDM au niveau du locataire par Intune, ces comptes d’utilisateur migreront correctement. Si vous faites migrer le compte d’utilisateur gestionnaire d’inscription d’appareil avant de modifier l’autorité MDM au niveau du locataire, vous devez ajouter manuellement l’utilisateur en tant que gestionnaire d’inscription d’appareil dans Intune sur Azure. Toutefois, les appareils inscrits à l’aide d’un gestionnaire d’inscription d’appareil ne migrent pas correctement. Vous devez appeler le support technique pour faire migrer ces appareils. Pour plus d’informations, consultez [Ajouter un gestionnaire d’inscription d’appareil](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).
- Les appareils inscrits à l’aide d’un gestionnaire d’inscription d’appareil et les appareils auxquels aucun utilisateur n’est associé ne migrent pas vers la nouvelle autorité MDM. Pour ces appareils, vous devez appeler le support technique pour obtenir de l’aide. Ne permettez pas au support technique d’effectuer une réinitialisation de l’autorité MSM, sans quoi les données seront effacées dans Intune. Vous devez [modifier votre autorité MDM](migrate-change-mdm-authority.md) à partir de la console Configuration Manager.

## <a name="migrate-users-to-intune"></a>Faire migrer des utilisateurs vers Intune
Pour tester si vos configurations Intune fonctionnent comme prévu, commencez par faire migrer un petit ensemble d’utilisateurs et leurs appareils. Ensuite, après avoir vérifié que tout fonctionne normalement, vous pouvez commencer la migration d’autres groupes AAD contenant davantage d’utilisateurs et leurs appareils.

## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Faire migrer un groupe d’utilisateurs de test vers la version autonome d’Intune
Les appareils des utilisateurs inclus dans le regroupement associé à l’abonnement Intune peuvent s’inscrire à la gestion hybride des appareils mobiles. Lorsque vous supprimez un utilisateur du regroupement, ses appareils inscrits migrent vers la version autonome d’Intune si une licence Intune lui est attribuée. Si vous n’avez pas déjà attribué des licences aux utilisateurs que vous envisagez de faire migrer, consultez [Affecter des licences Intune à vos comptes d’utilisateur](https://docs.microsoft.com/intune/licenses-assign). Dans le regroupement de l’abonnement Intune, vous pouvez exclure des regroupements d’utilisateurs de votre regroupement principal pour faire migrer les utilisateurs inclus dans le regroupement exclu. 

Dans l’exemple suivant, le regroupement d’utilisateurs hybrides contient tous les membres du regroupement de tous les utilisateurs. Ainsi, tout utilisateur peut inscrire un appareil à la gestion hybride des appareils mobiles. Pour faire migrer des utilisateurs vers la version autonome d’Intune, vous sélectionnez Exclure des regroupements et vous ajoutez un regroupement contenant les utilisateurs à faire migrer. Lorsque vous êtes prêt à faire migrer d’autres utilisateurs, vous pouvez ajouter d’autres regroupements exclus qui incluent ces utilisateurs. 

![Exclure des regroupements](../media/migrate-excludecollections.png)

> [!Note] 
> Lorsque le regroupement **Tous les utilisateurs** est sélectionné pour l’abonnement Intune, vous n’êtes pas autorisé à ajouter une règle pour exclure des regroupements. Créez un nouveau regroupement basé sur le regroupement **Tous les utilisateurs**, vérifiez que le regroupement contient les utilisateurs attendus, puis modifiez l’abonnement Intune pour utiliser le nouveau regroupement. Vous pouvez exclure des regroupements d’utilisateurs du nouveau regroupement pour faire migrer des utilisateurs. 

Pour faire migrer un groupe d’utilisateurs de test vers Intune, créez un regroupement d’utilisateurs contenant les utilisateurs à faire migrer, puis excluez le regroupement d’utilisateurs du regroupement utilisé pour l’abonnement Intune.   

Le diagramme suivant donne une vue d’ensemble du fonctionnement de la migration d’utilisateurs.

 ![Vue d’ensemble de l’autorité mixte](../media/migrate-mixedauthority.svg)

1. Vérifiez que l’utilisateur dispose d’une licence Intune/EMS. 
2. Créez un regroupement à exclure du regroupement de l’abonnement Intune. Dans cet exemple, le regroupement **Tous les utilisateurs hybrides** contient une règle pour exclure des utilisateurs du regroupement **Pilote de migration**. **User1** est membre du regroupement **Pilote de migration** et exclu du regroupement **Tous les utilisateurs hybrides**. 
3. Les appareils de **User1** sont désormais gérés à partir d’Intune dans le portail Azure. 
4. Tous les autres appareils continuent d’être gérés à partir de la console Configuration Manager. 

## <a name="verify-intune-standalone-functionality"></a>Vérifier la fonctionnalité de la version autonome d’Intune
Après avoir fait migrer un petit ensemble d’utilisateurs, vérifiez que leurs appareils sont répertoriés dans Intune. Accédez au panneau **Appareils** et sélectionnez **Tous les appareils**. 

Ensuite, vérifiez que vos stratégies, profils, applications, etc. fonctionnent comme prévu sur les appareils des utilisateurs.

## <a name="migrate-additional-users"></a>Faire migrer d’autres utilisateurs
Après avoir vérifié que la version autonome d’Intune fonctionne comme prévu, vous pouvez commencer la migration d’autres utilisateurs. Tout comme vous avez créé un regroupement avec un ensemble d’utilisateurs de test, créez des regroupements qui contiennent des utilisateurs à faire migrer et excluez ces regroupements du regroupement associé à l’abonnement Intune. Pour plus d’informations, consultez [Regroupement associé à votre abonnement Intune](#collection-associated-with-your-intune-subscription).

## <a name="next-steps"></a>Étapes suivantes
Après avoir fait migrer des utilisateurs et testé la fonctionnalité d’Intune, déterminez si vous êtes prêt à [faire passer l’autorité MDM](migrate-change-mdm-authority.md) de votre locataire Intune de Configuration Manager vers Intune. 