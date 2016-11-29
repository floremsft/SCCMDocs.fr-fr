---
title: "Configurer des applications iOS à l’aide de stratégies de configuration des applications | System Center Configuration Manager"
description: "Évitez les problèmes de configuration sur les appareils exécutant iOS 8 ou version ultérieure en déployant des stratégies de configuration des applications sur les appareils avant que les utilisateurs exécutent les applications."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-app
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74d5d776-e37d-45de-bdba-43541b03d12c
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9cbf28afbbe69f9a027ffad2a699b9d6b625e690


---
# <a name="configure-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Configurer des applications iOS à l’aide de stratégies de configuration des applications dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Utilisez les stratégies de configuration des applications disponibles dans Configuration Manager pour fournir les paramètres pouvant être nécessaires quand l’utilisateur exécute une application. Par exemple, une application peut nécessiter que l’utilisateur spécifie les paramètres suivants :
- Un numéro de port personnalisé
- Paramètres de langue
- Paramètres de sécurité
- Paramètres de personnalisation comme le logo de l’entreprise

Si ces paramètres ne sont pas correctement entrés par l’utilisateur, non seulement la charge du support technique est alourdie, mais l’adoption de nouvelles applications est également ralentie.
Les stratégies de configuration des applications peuvent vous aider à éliminer ces problèmes en vous permettant de déployer ces paramètres dans une stratégie avant que les utilisateurs exécutent l’application. Les paramètres sont ensuite fournis automatiquement, et l’utilisateur n’a aucune action à effectuer.
Vous ne déployez pas ces stratégies directement sur les appareils et utilisateurs. Au lieu de cela, vous associez la stratégie à un type de déploiement quand vous déployez l’application. Les paramètres de stratégie sont utilisés chaque fois que l’application les vérifie (en général, lors de sa première exécution).

Les stratégies de configuration des applications sont disponibles uniquement sur les appareils exécutant iOS 8 et versions ultérieures. Elles prennent en charge les types d’application suivants :

- **Package d’application pour iOS (*fichier .ipa)**
- **Package d’application pour iOS depuis App Store**

Pour plus d’informations sur les types d’installation d’application, consultez [Introduction à la gestion des applications](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Créer une stratégie de configuration des applications

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Stratégies de configuration des applications**.
3. Sous l’onglet **Accueil**, dans le groupe **Stratégies de configuration des applications**, cliquez sur **Créer une stratégie de configuration d’applications**.
4. Dans la page **Général** de l’**Assistant Création d’une stratégie de configuration d’applications**, spécifiez les informations suivantes :
    - **Nom** : spécifiez un nom unique pour la stratégie.
    - **Description** : (facultatif) spécifiez une description qui vous aide à identifier la stratégie.
    - **Catégories attribuées afin d’améliorer la recherche et le filtrage** : (facultatif) cliquez sur **Catégories** pour créer des catégories et les attribuer à la stratégie. L’utilisation de catégories facilite le tri et la recherche des éléments dans la console Configuration Manager.
5. Dans la page **Stratégie iOS**, choisissez de quelle façon vous allez spécifier les informations sur la stratégie de configuration :
    - **Spécifier des paires nom/valeur** : vous pouvez utiliser cette option pour les fichiers de liste de propriétés simples sans imbrication.
    Pour spécifier des paires nom/valeur
        - Pour ajouter une nouvelle paire, cliquez sur **Nouveau**.
        - Dans la boîte de dialogue **Ajouter une paire nom/valeur**, spécifiez les éléments suivants :
            - **Type** : dans la liste, choisissez le type de valeur que vous souhaitez spécifier.
            - **Nom** : entrez le nom de la clé de liste de propriétés pour laquelle vous voulez spécifier une valeur.
            - **Valeur** : entrez la valeur à appliquer à la clé spécifiée.
        - Accéder à un fichier de liste de propriétés : utilisez cette option si vous avez déjà un fichier XML de configuration d’applications, ou pour les fichiers de liste de propriétés plus complexes avec imbrication.
        Pour accéder à un fichier de liste de propriétés
            - Dans le champ **Stratégie de configuration des applications**, entrez les informations de la liste de propriétés au format XML correct.
            Pour en savoir plus sur les listes de propriétés XML, consultez [Understanding XML Property Lists](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) (Présentation des listes de propriétés XML) sur le site iOS Developer Library.
            Le format de la liste de propriétés XML varie en fonction de l’application que vous configurez. Pour plus d’informations sur le format exact à utiliser, contactez le fournisseur de l’application.
            Intune prend en charge les types de données suivants dans une liste de propriétés :
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
            Pour plus d’informations sur les types de données, consultez [About Property Lists](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) (À propos des listes de propriétés) sur le site iOS Developer Library.
            De plus, Intune prend en charge les types de jetons suivants dans la liste de propriétés :
            ```
            {{userprincipalname}} - (Example: John@contoso.com)
            {{mail}} - (Example: John@contoso.com)
            {{partialupn}} - (Example: John)
            {{accountid}} - (Example: fc0dc142-71d8-4b12-bbea-bae2a8514c81)
            {{deviceid}} - (Example: b9841cd9-9843-405f-be28-b2265c59ef97)
            {{userid}} - (Example: 3ec2c00f-b125-4519-acf0-302ac3761822)
            {{username}} - (Example: John Doe)
            {{serialnumber}} - (Example: F4KN99ZUG5V2) for iOS devices
            {{serialnumberlast4digits}} - (Example: G5V2) for iOS devices

            The {{ and }} characters are used by token types only and must not be used for other purposes.
            ```
            Vous pouvez également cliquer sur **Sélectionner le fichier** pour importer un fichier XML que vous avez créé précédemment.
6. Cliquez sur **Suivant**. Si le code XML contient des erreurs, vous devez le corriger avant de continuer.
6. Effectuez toutes les étapes de l'Assistant.

La nouvelle stratégie de configuration des applications s’affiche dans le nœud **Stratégies de configuration des applications** de l’espace de travail **Bibliothèque de logiciels**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associer une stratégie de configuration des applications à une application de Configuration Manager

Pour associer une stratégie de configuration des applications au déploiement d’une application iOS, déployez l’application comme vous le faites habituellement, en suivant la procédure décrite dans la rubrique [Déployer des applications](/sccm/apps/deploy-use/deploy-applications).
Dans la page **Stratégies de configuration des applications** de l’**Assistant Déploiement logiciel**, cliquez sur **Nouveau**. Ensuite, dans la boîte de dialogue **Sélectionner la stratégie de configuration des applications**, choisissez un type de déploiement d’application et une stratégie de configuration des applications à laquelle l’associer.
Quand le type de déploiement est installé, les paramètres de la stratégie de configuration des applications sont automatiquement appliqués.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Exemple de format pour le fichier XML de configuration des applications mobiles

Quand vous créez un fichier de configuration des applications mobiles, vous pouvez spécifier une ou plusieurs des valeurs suivantes en respectant le format ci-dessous :

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>
```



<!--HONumber=Nov16_HO1-->


