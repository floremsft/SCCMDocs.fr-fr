---
title: "Configurer des applications iOS avec des stratégies de configuration d’application | Microsoft Docs"
description: "Évitez les problèmes de configuration sur les appareils exécutant iOS 8 ou version ultérieure en déployant des stratégies de configuration des applications sur les appareils avant que les utilisateurs exécutent les applications."
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
ms.sourcegitcommit: 72157aa0e94b99eb947fdd9891b7e91c1001ea22
ms.openlocfilehash: 64964834b63167e1f78c44410396b8e18735875e


---
# <a name="apply-settings-to-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Appliquer des paramètres aux applications iOS à l’aide de stratégies de configuration d’application dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Vous pouvez utiliser des stratégies de configuration des applications disponibles dans System Center Configuration Manager (Configuration Manager) pour distribuer les paramètres pouvant être nécessaires quand un utilisateur exécute une application. Par exemple, une application peut exiger qu’un utilisateur spécifie les détails suivants :
- Un numéro de port personnalisé
- Paramètres de langue
- Paramètres de sécurité
- Paramètres de personnalisation, comme le logo de l’entreprise

Si l’utilisateur entre les paramètres incorrectement, il est de la responsabilité du support technique de les corriger, ce qui ralentit le déploiement de l’application.
Pour éviter ces problèmes, vous pouvez utiliser des stratégies de configuration d’application pour déployer les paramètres obligatoires sur les utilisateurs avant qu’ils n’exécutent l’application. Les paramètres sont automatiquement associés à un utilisateur. Aucune intervention de la part de l’utilisateur n’est nécessaire.
Pour utiliser une stratégie de configuration d’application dans Configuration Manager au lieu de déployer les stratégies de configuration directement sur des utilisateurs et des appareils, associez une stratégie à un type de déploiement quand vous déployez l’application. Les paramètres de stratégie sont appliqués chaque fois que l’application les vérifie (en général, lors de sa première exécution).

Les stratégies de configuration des applications ne sont actuellement disponibles que sur les appareils exécutant iOS 8 et versions ultérieures, et pour les types d’application suivants :

- **package d’application pour iOS (*fichier .ipa)**
- **Package d’application pour iOS de l’App Store**

Pour plus d’informations sur les types d’installation d’application, consultez [Introduction à la gestion des applications](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Créer une stratégie de configuration des applications

1. Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Stratégies de configuration des applications**.
2. Sous l’onglet **Accueil**, dans le groupe **Stratégies de configuration des applications**, choisissez **Créer une stratégie de configuration d’applications**.
3. Dans la page **Général** de l’Assistant Création d’une stratégie de configuration d’applications, définissez les informations de cette stratégie :
  - **Nom**. Entrez un nom unique pour la stratégie.
  - **Description**. (Facultatif) Pour identifier plus facilement la stratégie, vous pouvez ajouter une description.
  - **Catégories attribuées pour améliorer la recherche et le filtrage**. (Facultatif) Pour créer et attribuer des catégories à la stratégie, choisissez **Catégories**. L’utilisation de catégories facilite le tri et la recherche d’éléments dans la console Configuration Manager.
4. Dans la page **Stratégie iOS**, choisissez de quelle façon les informations sur la stratégie de configuration sont définies :
  - **Spécifier des paires nom/valeur**. Vous pouvez utiliser cette option pour les fichiers de liste de propriétés simples sans imbrication.

      *Pour spécifier une paire nom/valeur*
        1. Pour ajouter une nouvelle paire, choisissez **Nouveau**.
        2. Dans la boîte de dialogue **Ajouter une paire nom/valeur**, spécifiez les éléments suivants :
            - **Type**. Dans la liste, sélectionnez le type de valeur que vous souhaitez spécifier.
            - **Nom**. Entrez le nom de la clé de liste de propriétés pour laquelle vous voulez spécifier une valeur.
            - **Valeur**. Entrez la valeur à appliquer à la clé spécifiée.

  - **Accéder à un fichier de liste de propriétés**. Utilisez cette option si vous avez déjà un fichier XML de configuration d’applications, ou pour les fichiers de liste de propriétés plus complexes avec imbrication.

    *Pour accéder à un fichier de liste de propriétés*

      1.  Dans le champ **Stratégie de configuration des applications**, entrez les informations de la liste de propriétés au format XML correct.

      Pour en savoir plus sur les listes de propriétés XML, consultez [Understanding XML Property Lists](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) (Présentation des listes de propriétés XML) sur le site iOS Developer Library.

        The format of the XML property list varies depending on the app you are configuring. Contact the app supplier for details about the format to use.
        Intune supports the following data types in a property list:

            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
    Pour plus d’informations sur les types de données, consultez [About Property Lists](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) (À propos des listes de propriétés) sur le site iOS Developer Library.
    De plus, Intune prend en charge les types de jeton suivants dans la liste des propriétés :
    
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

      2.  Pour importer un fichier XML créé précédemment, choisissez **Sélectionner le fichier**.
6. Choisissez **Suivant**. Si le code XML contient des erreurs, vous devez le corriger avant de continuer.
7. Terminez les étapes de l’Assistant.

La nouvelle stratégie de configuration des applications s’affiche dans le nœud **Stratégies de configuration des applications** de l’espace de travail **Bibliothèque de logiciels**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associer une stratégie de configuration des applications à une application de Configuration Manager

Pour associer une stratégie de configuration des applications au déploiement d’une application iOS, déployez l’application comme vous le faites habituellement, en suivant la procédure décrite dans la rubrique [Déployer des applications](/sccm/apps/deploy-use/deploy-applications).

Dans la page **Stratégies de configuration d’application** de l’Assistant Déploiement logiciel, choisissez **Nouveau**. Dans la boîte de dialogue **Sélectionner la stratégie de configuration des applications**, choisissez un type de déploiement d’application et la stratégie de configuration des applications à laquelle l’associer.
Quand le type de déploiement est installé, les paramètres de la stratégie de configuration des applications sont automatiquement appliqués.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Exemple de format pour le fichier XML de configuration des applications mobiles

Quand vous créez un fichier de configuration des applications mobiles, vous pouvez utiliser ce format pour spécifier une ou plusieurs des valeurs suivantes :

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



<!--HONumber=Feb17_HO3-->


