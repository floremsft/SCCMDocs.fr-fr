---
title: "Protéger des applications à l’aide de stratégies de gestion des applications mobiles | System Center Configuration Manager"
description: "Modifiez les fonctionnalités des applications que vous déployez pour qu’elles respectent les stratégies de sécurité et de conformité de votre entreprise."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b7936-a5ca-45c5-8bef-10424eb2e091
caps.latest.revision: 13
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: dfbf6b2001e3259abb7246ab463682b0ead4f4e8


---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>Protéger des applications à l’aide de stratégies de gestion des applications mobiles dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les stratégies de gestion des applications System Center Configuration Manager vous permettent de modifier les fonctionnalités des applications que vous déployez pour qu’elles respectent les stratégies de conformité et de sécurité de votre entreprise. Par exemple, vous pouvez restreindre les opérations Couper, Copier et Coller au sein d’une application limitée, ou configurer une application pour ouvrir tous les liens web dans Managed Browser. Les stratégies de gestion des applications prennent en charge :  

-   les appareils qui exécutent Android 4 et versions ultérieures ;  

-   les appareils qui exécutent iOS 7 et versions ultérieures.  

Outre les appareils gérés, vous pouvez utiliser des stratégies de gestion des applications mobiles pour protéger des applications sur des appareils non gérés par Intune. Grâce à cette nouvelle fonctionnalité, vous pouvez appliquer des stratégies de gestion des applications mobiles pour les applications se connectant aux services Office 365. Ces stratégies ne sont pas prises en charge pour les applications se connectant à Exchange sur site ou SharePoint.  
Pour utiliser cette nouvelle fonctionnalité, vous devez utiliser le portail Azure en version préliminaire. Les rubriques suivantes peuvent vous aider dans la prise en main :  
-   [Prise en main des stratégies de gestion des applications mobiles dans le portail Azure](https://technet.microsoft.com/library/mt627830.aspx)  
-   [Créer et déployer des stratégies de gestion des applications mobiles à l’aide de Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  

Contrairement aux éléments de configuration et aux bases de référence dans Configuration Manager, vous ne déployez pas une stratégie de gestion des applications directement. Au lieu de cela, vous associez la stratégie au type de déploiement d’application que vous voulez restreindre. Quand le type de déploiement d’application est déployé et installé sur les appareils, les paramètres que vous spécifiez prennent effet.  

Pour appliquer des restrictions à une application, celle-ci doit intégrer le Kit de développement logiciel (SDK) d’application Microsoft Intune. Il existe deux méthodes pour obtenir ce type d'application :  

-   **Utiliser une application gérée par une stratégie** (Android et iOS) : intègre le Kit de développement logiciel (SDK) d’application. Pour ajouter ce type d'application, spécifiez un lien vers l'application à partir d'un magasin d'applications tel que l'iTunes Store ou Google Play. Aucun traitement supplémentaire n'est nécessaire pour ce type d'application. Pour obtenir une liste des applications gérées par une stratégie qui sont disponibles pour les appareils iOS et Android, consultez [Applications gérées pour les stratégies de gestion des applications mobiles Microsoft Intune](https://technet.microsoft.com/en-us/library/dn708489.aspx).  

-   **Utiliser une application « encapsulée »** (Android et iOS) : applications repackagées pour inclure le Kit de développement logiciel (SDK) d’application à l’aide de l’ **outil de création de package de restrictions d’application Microsoft Intune**. On utilise généralement cet outil pour traiter les applications d'entreprise qui ont été créées en interne. Vous ne pouvez pas l'utiliser pour traiter les applications qui ont été téléchargées à partir du magasin d'applications. Consultez [Préparer des applications Android pour la gestion des applications mobiles avec l'outil de création de package de restrictions d'application Microsoft Intune](https://technet.microsoft.com/en-us/library/dn878028.aspx) et [Préparer des applications iOS pour la gestion des applications mobiles avec l'outil de création de package de restrictions d'application Microsoft Intune](https://technet.microsoft.com/en-us/library/mt147413.aspx).  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>Créer et déployer une application avec une stratégie de gestion des applications mobiles  
  
##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>Étape 1 : obtenir le lien vers une application gérée par une stratégie ou créer une application encapsulée  

-   **Pour obtenir un lien vers une application gérée par une stratégie** : à partir du magasin d'applications, recherchez et notez l'URL de l'application gérée par une stratégie que vous souhaitez déployer.  

     Par exemple, l’URL de l’application Microsoft Word pour iPad est **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  

-   **Pour créer une application encapsulée** - Utilisez les informations fournies dans les rubriques [Préparer des applications iOS pour la gestion des applications mobiles avec l’outil de création de package de restrictions d’application Microsoft Intune](https://technet.microsoft.com/en-us/library/dn878028.aspx) et [Préparer des applications Android pour la gestion des applications mobiles avec l’outil de création de package de restrictions d’application Microsoft Intune](https://technet.microsoft.com/en-us/library/mt147413.aspx) pour créer une application encapsulée.  

     L'outil crée une application traitée et un fichier manifeste associé. Vous utiliserez ces fichiers quand vous créerez une application Configuration Manager contenant l’application.  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>Étape 2 : créer une application Configuration Manager qui contient une application  
 La procédure de création de l’application Configuration Manager diffère selon que vous utilisez une application gérée par une stratégie (lien externe) ou une application qui a été créée avec l’outil de création de package de restrictions d’application Microsoft Intune pour iOS (package d’application pour iOS). Utilisez l’une des procédures suivantes pour créer l’application Configuration Manager.  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une application** pour ouvrir l'Assistant Création d'une application.  

4.  Sous l'onglet **Général** , sélectionnez **Détecter automatiquement les informations de cette application à partir des fichiers d'installation**.  

5.  Dans la liste déroulante **Type**, sélectionnez **Package d’application pour iOS (\*fichier *.ipa)**.  

6.  Cliquez sur **Parcourir** pour sélectionner le package d'application à importer, puis cliquez sur **Suivant**.  

7.  Sur la page **Informations générales** , entrez le texte descriptif et les informations de catégorie que vous souhaitez montrer aux utilisateurs sur le portail d'entreprise.  

8.  Effectuez toutes les étapes de l'Assistant.  

 La nouvelle application s'affiche dans le nœud **Applications** de l'espace de travail **Bibliothèque de logiciels** .  
  
### <a name="create-an-application-containing-a-link-to-a-policy-managed-app"></a>Créer une application contenant un lien vers une application gérée par une stratégie  
  
1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  
  
3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une application** pour ouvrir l'Assistant Création d'une application.  

4.  Sous l'onglet **Général** , sélectionnez **Détecter automatiquement les informations de cette application à partir des fichiers d'installation**.  

5.  Dans la liste déroulante **Type** , sélectionnez l'un des éléments suivants :  

    -   Pour iOS : **Package d’application pour iOS dans l’App Store**  

    -   Pour Android : **Package d’application pour Android sur Google Play**  

6.  Entrez l'URL de l'application (obtenue à l'étape 1), puis cliquez sur **Suivant**.  

7.  Sur la page **Informations générales** , entrez le texte descriptif et les informations de catégorie que vous souhaitez montrer aux utilisateurs sur le portail d'entreprise.  

8.  Effectuez toutes les étapes de l'Assistant.  

 La nouvelle application s'affiche dans le nœud **Applications** de l'espace de travail **Bibliothèque de logiciels** .  

##  <a name="step-3-create-an-application-management-policy"></a>Étape 3 : créer une stratégie de gestion d’application  
 Ensuite, vous allez créer une stratégie de gestion d'application que vous associerez à l'application. Vous pouvez créer une stratégie générale ou Managed Browser.  
  
1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Stratégies de gestion d’application**.  
3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une stratégie de gestion d'application**.  

4.  Dans la page **Général** , entrez le nom et la description de la stratégie, puis cliquez sur **Suivant**.  

5.  Dans la page **Type de stratégie** , sélectionnez la plateforme et le type de cette stratégie, puis cliquez sur **Suivant**. Les types de stratégies suivants sont disponibles :  

    -   **Général**: le type de stratégie Général permet de modifier les fonctionnalités des applications que vous déployez pour les adapter aux stratégies de sécurité et de conformité de votre entreprise. Par exemple, vous pouvez limiter les opérations Couper, Copier et Coller dans une application restreinte.  

    -   **Managed Browser**: spécifiez s’il faut autoriser ou empêcher Managed Browser d’ouvrir une liste d’URL. Le type de stratégie Managed Browser vous permet de modifier les fonctionnalités de l'application Intune Managed Browser. Il s'agit d'un navigateur web qui vous permet de gérer les actions que les utilisateurs peuvent effectuer, y compris les sites qu'ils peuvent visiter et le mode d'ouverture des liens vers du contenu dans le navigateur. En savoir plus sur l’  [application Intune Managed Browser pour iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) et [l’application Intune Managed Browser pour Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).  

6.  Dans la page **Stratégie iOS** ou **Stratégie Android** , configurez les valeurs suivantes selon les besoins, puis cliquez sur **Suivant**. Les options peuvent différer selon le type d'appareil pour lequel vous configurez la stratégie.  

|Valeur|Plus d'informations|  
|-----------|----------------------|  
|**Afficher le contenu web uniquement dans Managed Browser**|Quand ce paramètre est activé, tous les liens dans l'application sont ouverts dans Managed Browser. Pour que cette option fonctionne, vous devez avoir déployé cette application sur des appareils.|  
|**Interdire les sauvegardes Android** ou **Interdire les sauvegardes iTunes et iCloud**|Désactive la sauvegarde de toutes les informations à partir de l'application.|  
|**Autoriser l'application à transférer des données vers d'autres applications**|Spécifie les applications auxquelles cette application peut envoyer des données. Vous pouvez choisir de n'autoriser le transfert de données vers aucune application, d'autoriser le transfert vers d'autres applications restreintes ou d'autoriser le transfert vers toute application.<br /><br /> Pour les appareils iOS, pour empêcher le transfert de documents entre les applications gérées et non gérées, vous devez aussi configurer et déployer une stratégie de sécurité d'appareil mobile qui désactive le paramètre **Autoriser les documents gérés dans d'autres applications non gérées**.<br /><br /> Si vous choisissez d'autoriser uniquement le transfert vers d'autres applications restreintes, les visionneuses d'images et PDF Intune (si elles sont déployées) seront utilisées pour ouvrir le contenu des types respectifs.|  
|**Autoriser l'application à recevoir des données d'autres applications**|Spécifie les applications à partir desquelles cette application peut recevoir des données. Vous pouvez choisir de n’autoriser le transfert de données à partir d’aucune application, d’autoriser le transfert uniquement à partir d’autres applications restreintes, ou d’autoriser le transfert à partir de toute application.|  
|**Interdire « Enregistrer sous »**|Désactive l'utilisation de l'option **Enregistrer sous** dans toute application qui utilise cette stratégie.|  
|**Restreindre les opérations couper, copier et coller avec d'autres applications**|Spécifie comment les opérations couper, copier et coller peuvent être utilisées avec l'application. Choisissez parmi :<br /><br /> **Bloqué** : ne pas autoriser les opérations couper, copier et coller entre cette application et d'autres applications.<br /><br /> **Applications gérées par la stratégie** : autoriser uniquement les opérations couper, copier et coller entre cette application et les autres applications restreintes.<br /><br /> **Applications gérées par la stratégie avec Coller dans** : autoriser le collage de données coupées ou copiées à partir de cette application uniquement dans d'autres applications restreintes. Autoriser le collage dans cette application de données coupées ou copiées à partir de n'importe quelle application.<br /><br /> **N'importe quelle application** : aucune restriction pour les opérations couper, copier et coller vers ou à partir de cette application.|  
|**Demander un code confidentiel simple pour l'accès**|Oblige l'utilisateur à entrer un code confidentiel qu'il spécifie pour utiliser cette application. L'utilisateur sera invité à définir ce code lors de la première exécution de l'application.|  
|**Nombre de tentatives avant réinitialisation du code confidentiel**|Spécifiez le nombre de tentatives de saisie du code confidentiel qui peuvent être effectuées avant que l'utilisateur soit obligé de réinitialiser le code confidentiel.|  
|**Exiger des informations d'identification d'entreprise pour l'accès**|Exige que l'utilisateur entre ses informations d'ouverture de session d'entreprise pour accéder à l'application.|  
|**Exiger la conformité à la stratégie d'entreprise pour l'accès**|Autorise l'utilisation de l'application uniquement si l'appareil n'est pas jailbroken ou rooté.|  
|**Revérifier les exigences d'accès après (minutes)**|Dans le champ **Délai** , indiquez le délai au bout duquel les conditions d'accès pour l'application sont revérifiées après son démarrage.<br /><br /> Dans le champ **Période de grâce hors connexion** , si l'appareil est hors connexion, spécifiez le délai au bout duquel les conditions d'accès pour l'application sont revérifiées.|  
|**Chiffrer les données de l'application**|Spécifie que toutes les données associées à cette application seront chiffrées, y compris les données stockées en externe, telles que les cartes SD.<br /><br /> **Chiffrement pour iOS**<br /><br /> Pour les applications associées à une stratégie de gestion des applications mobiles Configuration Manager, les données sont chiffrées au repos à l’aide du chiffrement au niveau de l’appareil fourni par le système d’exploitation. Cette option est activée via la stratégie de code confidentiel d'appareil qui doit être définie par l'administrateur informatique. Quand un code confidentiel est nécessaire, les données sont chiffrées selon les paramètres de la stratégie de gestion des applications mobiles. Comme indiqué dans la documentation Apple, [les modules utilisés par iOS 7 sont certifiés FIPS 140-2](http://support.apple.com/en-us/HT202739).<br /><br /> **Chiffrement pour Android**<br /><br /> Pour les applications associées à une stratégie de gestion des applications mobiles Configuration Manager, le chiffrement est fourni par Microsoft. Les données sont chiffrées de manière synchrone durant les opérations d'E/S de fichier conformément au paramètre indiqué dans la stratégie de gestion des applications mobiles. Les applications gérées sur Android utilisent le chiffrement AES-128 en mode CBC, avec utilisation des bibliothèques de chiffrement de plateforme. La méthode de chiffrement n'est pas certifiée FIPS 140-2. Le contenu sur le stockage de l'appareil est toujours chiffré.|  
    |**Bloquer la capture d'écran** (appareils Android uniquement)|Spécifie que les fonctionnalités de capture d'écran de l'appareil sont bloquées lors de l'utilisation de cette application.|  

7.  Dans la page **Managed Browser** , indiquez si Managed Browser est autorisé à ouvrir uniquement les URL figurant dans la liste ou si vous souhaitez l'empêcher d'ouvrir les URL figurant dans la liste, gérez les URL de la liste, puis cliquez sur **Suivant**.  

    > [!WARNING]  
    >  Pour plus d’informations, consultez [Gérer l’accès à Internet à l’aide de stratégies Managed Browser](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).  
  
8.  Effectuez toutes les étapes de l'Assistant.  

 La nouvelle stratégie s'affiche dans le nœud **Stratégies de gestion d'application** de l'espace de travail **Bibliothèque de logiciels** .  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>Étape 4 : associer la stratégie de gestion d’application à un type de déploiement  
 
 Quand un type de déploiement est créé pour une application qui nécessite une stratégie de gestion d’application, Configuration Manager reconnaît qu’une stratégie de gestion d’application doit être liée à ce type de déploiement quand l’application associée est déployée et vous invite à en associer une. Pour Managed Browser, vous devrez associer une stratégie Général et une stratégie Managed Browser. Pour plus d’informations, consultez [Créer des applications](../../apps/deploy-use/create-applications.md).  
  
> [!IMPORTANT]  
>  Si l'application est déjà déployée, le déploiement du nouveau type de déploiement échouera tant que cette association n'aura pas été effectuée. Vous pouvez créer l'association dans les **Propriétés** de l'application, sous l'onglet **Gestion des applications** .  

> [!IMPORTANT]  
>  Pour les appareils qui exécutent des systèmes d'exploitation antérieurs à iOS 7.1, les stratégies associées ne sont pas supprimées lors de la désinstallation de l'application.  
>   
>  Si l’inscription de l’appareil dans Configuration Manager est annulée, les stratégies ne sont pas supprimées des applications. Les applications pour lesquelles des stratégies étaient appliquées conservent les paramètres de stratégie après la désinstallation et la réinstallation de l'application.  

##  <a name="step-5-monitor-the-app-deployment"></a>Étape 5 : surveiller le déploiement de l’application  
 Une fois que vous avez créé et déployé une application associée à une stratégie de gestion des applications mobiles, vous pouvez analyser l'application et résoudre les éventuels conflits de stratégie.  
  
1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Vue d’ensemble** > **Déploiements**.  
  
3.  Sélectionnez le déploiement et, sous l'onglet **Accueil** , cliquez sur **Propriétés**.  

4.  Dans le volet de détails du déploiement, cliquez sur **Stratégies de gestion d'application** sous **Objets associés**.  

 Pour plus d’informations sur la surveillance des applications, consultez [Surveiller des applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

##  <a name="how-policy-conflicts-are-resolved"></a>Résolution des conflits de stratégie  
 En cas de conflit de stratégie de gestion des applications mobiles lors du premier déploiement vers l'utilisateur ou l'appareil, la valeur de paramètre spécifique en conflit est supprimée de la stratégie déployée vers l'application et celle-ci utilise une valeur de conflit intégrée.  

 En cas de conflit de stratégie de gestion des applications mobiles lors de déploiements ultérieurs vers l'application ou l'utilisateur, la valeur de paramètre spécifique en conflit n'est pas mise à jour sur la stratégie de gestion des applications mobiles déployée vers l'application et celle-ci utilise la valeur existante pour ce paramètre.  

 Dans les cas où l'appareil ou l'utilisateur reçoit deux stratégies en conflit, le comportement suivant s'applique :  

-   Si une stratégie a déjà été déployée sur l'appareil, les paramètres de stratégie existants ne sont pas remplacés.  

-   Si aucune stratégie n'a encore été déployée sur l'appareil et que deux paramètres en conflit sont déployés, le paramètre par défaut intégré à l'appareil est utilisé.  

##  <a name="available-policy-managed-apps"></a>Applications gérées par une stratégie disponibles  
 Pour obtenir la liste des applications gérées par une stratégie disponibles pour les appareils iOS et Android, consultez [Partenaires d’application Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune-partners).  



<!--HONumber=Nov16_HO1-->


