---
title: "Nouveautés de la gestion des appareils mobiles hybride | Microsoft Intune | System Center Configuration Manager"
description: "Découvrez les nouvelles fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec System Center Configuration Manager et Intune."
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f13b38fcc4e7c55f05dbf6a7d8f516643939ba92
ms.openlocfilehash: 3525fba1b75196bddebc89e49f40cbfd3c75d9d0

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Nouveautés de la gestion hybride des appareils mobiles avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit des informations sur les nouvelles fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec System Center Configuration Manager et Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilité avec les versions de Configuration Manager  

 Chaque section de cet article répertorie les fonctionnalités hybrides sous 3 catégories différentes. Utilisez les indications suivantes pour déterminer la compatibilité des fonctionnalités dans chaque catégorie avec différentes versions de Configuration Manager :  

|Catégories de fonctionnalités|
|-|  
|**Nouveautés de Microsoft Intune** : en général, toutes les fonctionnalités répertoriées dans cette catégorie doivent fonctionner avec toutes les versions de Configuration Manager, notamment les versions de System Center 2012 R2 Configuration Manager, dans la mesure où ces fonctionnalités nécessitent uniquement le service Intune et pas de fonctionnalités supplémentaires dans Configuration Manager.<br /><br /> **Nouveautés de Configuration Manager Technical Preview** : toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version d’évaluation technique spécifiée. Pour tester ces fonctionnalités, vous devez installer la version d’évaluation technique spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Nouveautés de Configuration Manager (Current Branch)** : toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version spécifiée de Configuration Manager (Current Branch), telle que la version 1511 ou 1602. Si vous utilisez une version antérieure de Configuration Manager pour votre déploiement hybride, vous devez effectuer la mise à niveau vers la version de Configuration Manager (Current Branch) spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Mettre à niveau vers System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## <a name="new-hybrid-features-in-october-2016"></a>Nouvelles fonctionnalités hybrides en octobre 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en octobre 2016 fonctionnent dans les déploiements hybrides.

- **Accès conditionnel pour la gestion des applications mobiles**

  Vous pouvez restreindre l’accès à Exchange Online afin que l’accès soit fourni uniquement à partir d’applications qui prennent en charge les stratégies de gestion des applications mobiles Intune, telles qu’Outlook. [Cette nouvelle fonctionnalité](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) s’associe parfaitement aux stratégies de gestion des applications mobiles (GAM) Intune, car vous pouvez bloquer l’accès aux clients de messagerie intégrés ou à d’autres applications qui n’ont pas été configurées avec les stratégies GAM Intune. Cela garantit que vos utilisateurs accèdent aux données de votre organisation avec des applications qui peuvent être protégées à l’aide de la GAM Intune. Vous pouvez bien démarrer avec la gestion des applications mobiles Intune à l’aide du portail Azure. Recherchez la nouvelle section Accès conditionnel dans le panneau « Paramètres ».

-   **Outil de création de package de restrictions d’application Intune pour Android**

  Vous pouvez activer vos applications pour utiliser les stratégies de gestion des applications mobiles (MAM) Intune à l’aide de l’outil de création de package de restrictions d’application Intune.

- **Compatibilité d’Android Samsung KNOX avec Intune**

  Certains modèles de téléphone Samsung Galaxy Ace ne peuvent pas être gérés par Intune comme les appareils Samsung KNOX. Quand vous inscrivez ces appareils auprès d’Intune, ils sont gérés comme des appareils Android standard.

  Les numéros de modèle concernés sont les suivants :

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  Vous et vos utilisateurs finaux n’avez aucune action supplémentaire à effectuer. Pour plus d’informations, visitez le site web de Samsung KNOX.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Nouveautés de Configuration Manager Technical Preview 1610

Les nouvelles fonctionnalités hybrides suivantes ont été introduites en octobre 2016 pour Configuration Manager Technical Preview 1610.

- **Demander une synchronisation de la stratégie à partir de la console d’administration**

  Vous pouvez demander une synchronisation de la stratégie sur un appareil mobile inscrit à partir de la console Configuration Manager, au lieu d’avoir à demander la synchronisation dans l’application Portail d’entreprise sur l’appareil lui-même. Il s’agit d’une nouvelle action appelée **Envoyer une demande de synchronisation** dans le menu Actions de l’appareil à distance, qui s’affiche dans le ruban quand un appareil mobile est sélectionné dans le nœud Périphériques.

- **Paramètres de configuration de Windows Defender**

  Vous pouvez maintenant configurer les paramètres du client Windows Defender sur des ordinateurs Windows 10 inscrits auprès d’Intune à l’aide d’éléments de configuration de la console Configuration Manager. Il existe un nouveau groupe de paramètres nommé **Windows Defender** dans l’Assistant Nouvel élément de configuration. Notez que ces paramètres sont pris en charge uniquement sur Windows 10 version 1511 et versions ultérieures.


### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

Aucune nouvelle fonctionnalité hybride n’a été introduite en août 2016 pour Configuration Manager (Current Branch).

## <a name="new-hybrid-features-in-september-2016"></a>Nouvelles fonctionnalités hybrides en septembre 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en septembre 2016 fonctionnent dans les déploiements hybrides.

- **Ajout de « Notifications » au portail d’entreprise pour Android**

  Une nouvelle icône Notifications a été ajoutée sur la page d’accueil du portail d’entreprise pour Android. Appuyez sur cette icône pour accéder à la page Notifications, ce qui affiche à vos utilisateurs finaux tous les éléments qui nécessitent votre attention dans l’application Portail d’entreprise, comme la non-conformité de l’appareil, la mise à jour de l’inscription et l’activation de l’inscription. L’application Portail d’entreprise iOS bénéficie déjà de cette expérience de notifications. Grâce à cette nouvelle page Notifications, la page Configuration de l’accès à l’entreprise ne s’affichera plus à l’utilisateur chaque fois qu’il lancera ou reprendra le portail d’entreprise tant que l’appareil est déjà inscrit. Si vous créez votre propre aide pour les utilisateurs finaux, vous pouvez mettre à jour votre documentation pour refléter cette modification. Des captures d’écran mises à jour sont disponibles [ici](https://aka.ms/androidcpupdate).

- **Modifications en termes de prise en charge de l’application Portail d’entreprise iOS**

  Tous les utilisateurs de l’application Portail d’entreprise Microsoft Intune pour iOS sont maintenant tenus d’utiliser sa version la plus récente. Les nouveaux utilisateurs ne peuvent télécharger que la dernière version, et les utilisateurs actuels sont tenus d’effectuer une mise à jour vers celle-ci. La dernière version exige iOS 8.0 ou une version ultérieure. Par conséquent, les appareils exécutant des versions d’iOS plus anciennes ne peuvent pas utiliser le portail d’entreprise ou s’inscrire tant qu’ils n’ont pas effectué une mise à jour de leur appareil vers iOS 8.0 ou une version ultérieure, puis une mise à jour de l’application Portail d’entreprise vers la dernière version. Les appareils inscrits qui exécutent des versions antérieures à iOS 8.0 continueront à être gérés et répertoriés dans la console d’administration Intune.

- **Bouton d’envoi de commentaires ajouté à l’application Portail d’entreprise Windows Phone 8.1**

  L’application Portail d’entreprise Windows Phone 8.1 permet aux utilisateurs finaux d’envoyer des commentaires concernant l’application à l’aide d’un nouveau bouton « Envoyer des commentaires ». Pour trouver ce bouton, les utilisateurs appuient sur le menu « points de suspension » situé en bas à droite de l’écran de l’application Portail d’entreprise, puis sélectionnent **Envoyer des commentaires**. Les commentaires collectés anonymement permettent à Microsoft d’améliorer l’expérience d’application Portail d’entreprise des utilisateurs.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Nouveautés de Configuration Manager Technical Preview 1609

Les nouvelles fonctionnalités hybrides suivantes ont été introduites en septembre 2016 pour Configuration Manager Technical Preview 1609.

- **Paramètres supplémentaires et expérience améliorée pour les paramètres d’élément de configuration**

  De nouveaux paramètres ont été ajoutés pour Android, iOS et Windows, et seuls les paramètres qui s’appliquent aux plateformes que vous sélectionnez dans la page Plateformes prises en charge s’affichent dans l’Assistant. Pour plus d’informations, consultez [Nouveaux paramètres de compatibilité pour les éléments de configuration dans TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items).

- **Paramètres supplémentaires pour les profils DEP**

  TouchID, ApplePay et Zoom ont été ajoutés en tant que paramètres configurables dans les profils DEP pour les appareils iOS.

- **Applications payantes dans le Windows Store pour Entreprises**

  Vous pouvez maintenant ajouter des applications payantes et des applications gratuites au Windows Store pour Entreprises, et les déployer auprès des utilisateurs de votre organisation. Pour plus d’informations, consultez [Améliorations apportées au Windows Store pour Entreprises dans TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager).

- **Types de connexion natifs pour les profils VPN Windows 10**

  Vous pouvez maintenant créer des profils VPN Windows 10 pour la gestion des appareils mobiles avec des types de connexion Microsoft Automatic, IKEv2 et PPTP dans la console Configuration Manager sans utiliser de paramètre OMA-URI.

- **Graphiques de conformité Intune**

  Vous pouvez obtenir un aperçu rapide de la compatibilité globale des appareils et les principales raisons de non-compatibilité à l’aide de nouveaux graphiques sous l’espace de travail Analyse. Pour plus d’informations, consultez [Graphiques de conformité Intune dans TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

La nouvelle fonctionnalité suivante introduite en septembre 2016 est disponible dans les déploiements hybrides avec Microsoft Intune et Configuration Manager version 1606 (Current Branch).

- **Prise en charge d’iOS 10**

  Si vous avez des profils ou des éléments de configuration destinés à toutes les plateformes iOS, ils feront également l’objet d’un push vers iOS 10. Nous avons également publié une mise à jour vers Configuration Manager version 1606 qui vous permet de cibler des profils et des éléments de configuration sur des plateformes iOS individuelles, notamment iOS 10. Vous pouvez installer la mise à jour avec la console d’administration Configuration Manager dans **Administration > Vue d’ensemble > Services cloud > Mises à jour et maintenance**. Des informations supplémentaires relatives à la mise à jour sont disponible à l’adresse [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="new-hybrid-features-in-august-2016"></a>Nouvelles fonctionnalités hybrides en août 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en août 2016 fonctionnent dans les déploiements hybrides.

- **Prise en charge d’Android 7 dans l’application Portail d’entreprise**

  L’application Portail d’entreprise Intune pour Android fournit une prise en charge au « jour 0 » pour le prochain système d’exploitation Android 7.0 pour les appareils mobiles.

- **Suppression, par Google, de la capacité de réinitialisation à distance des codes secrets sur les appareils Android 7.0**

  Google supprime la possibilité, pour les utilisateurs finaux et les administrateurs informatiques, de réinitialiser à distance le code secret des appareils Android 7.0. Auparavant, les administrateurs informatiques pouvaient réinitialiser à distance le code secret d’un utilisateur, et les utilisateurs finaux pouvaient réinitialiser leurs codes secrets à partir du site web du portail d’entreprise.

- **Stratégie d’applications autorisées et bloquées pour les appareils Samsung KNOX**

  Vous pouvez maintenant configurer une stratégie personnalisée pour appareils Samsung KNOX qui vous permet de créer l’un des éléments suivants :

  - Une liste d’applications dont l’exécution sur l’appareil est bloquée. Même si elle est installée, une application définie dans la liste bloquée ne peut pas être activée sur l’appareil.
  - Une liste d’applications que les utilisateurs de l’appareil sont autorisés à installer à partir de Google Play Store. Aucune autre application ne peut être installée à partir du Store.

  Ces paramètres ne peuvent être utilisés que par des appareils qui exécutent Samsung KNOX. Pour plus d’informations, consultez [Utiliser des stratégies personnalisées pour autoriser et bloquer des applications pour les appareils Samsung KNOX](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Lien Commentaires du portail d’entreprise vers Microsoft**

   Le site web du portail d’entreprise permet aux utilisateurs finaux d’appuyer sur un nouveau lien « Commentaires », situé en bas de la page, pour envoyer des commentaires à Microsoft concernant leur expérience avec le site. Les commentaires collectés anonymement permettent à Microsoft d’améliorer l’expérience du site web du portail d’entreprise pour les utilisateurs.

- **Version minimale de Managed Browser iOS mise à jour vers 8.0**

  L’application Microsoft Intune Managed Browser pour iOS a été mise à jour pour prendre en charge les appareils exécutant iOS 8.0 ou version ultérieure. Même si les appareils iOS 7.1 peuvent toujours utiliser l’application Managed Browser existante, encouragez vos utilisateurs à effectuer la mise à jour vers iOS 8.0 ou une version ultérieure pour tirer pleinement parti des nouvelles fonctionnalités de Managed Browser.

### <a name="new-in-configuration-manager-technical-preview"></a>Nouveautés de Configuration Manager Technical Preview

Aucune nouvelle fonctionnalité hybride n’a été introduite en août 2016 pour Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

Aucune nouvelle fonctionnalité hybride n’a été introduite en août 2016 pour Configuration Manager (Current Branch).

## <a name="new-hybrid-features-in-july-2016"></a>Nouvelles fonctionnalités hybrides en juillet 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en juillet 2016 fonctionnent dans les déploiements hybrides.

- **Le composant Xamarin pour les applications Intune est disponible**

  Le composant Xamarin du SDK de l’application Intune vous permet d’activer les fonctionnalités de gestion des applications mobiles Intune dans vos applications iOS et Android mobiles avec Xamarin. Ce composant est disponible dans le [Store Xamarin](https://components.xamarin.com/view/Microsoft.Intune.MAM) ou dans la [page Github Microsoft Intune](https://github.com/msintuneappsdk).

- **Amélioration de l’expérience utilisateur final lors de l’inscription d’appareils Windows**

  Quand vous utilisez l’accès conditionnel, les étapes d’inscription pour Windows 8.1, Windows 10 Desktop et Windows 10 Mobile ont été clarifiées dans le site web Portail d’entreprise. Les utilisateurs verront à présent des étapes **Inscription de l’appareil** et **Jonction d’espace de travail** distinctes, ce qui leur permet de voir plus facilement l’état de leur appareil et de terminer le processus s’ils rencontrent un échec de jonction d’espace de travail. Les étapes distinctes sont également supposées simplifier le processus de dépannage pour les administrateurs informatiques. Auparavant, quand les utilisateurs finaux tentaient d’effectuer une inscription et que toutes les étapes d’inscription réussissaient à l’exception de la jonction d’espace de travail, l’appareil inscrit n’apparaissait pas dans la liste des appareils pour être identifiés par les utilisateurs, ce qui est une source de confusion pour les utilisateurs.

 - **Réinitialisation complète désormais disponible pour les appareils Windows 10**

    Les PC Windows 10 et les ordinateurs portables inscrits en tant qu’appareils mobiles peuvent être réinitialisés pour rétablir les paramètres d’usine de l’appareil. Pour plus d’informations, consultez [Guide pratique pour protéger vos appareils avec la réinitialisation à distance](/sccm/mdm/deploy-use/wipe-lock-reset).

- **Modifications apportées aux comptes Gestionnaires d’inscription d’appareil dans l’application Portail d’entreprise iOS**

  Pour des performances et une évolutivité optimales, Intune n’affiche plus tous les appareils gestionnaires d’inscription d’appareil dans le volet Mes appareils de l’application Portail d’entreprise iOS. Seul l’appareil local exécutant l’application est affiché, et uniquement s’il est inscrit à l’aide de l’application Portail d’entreprise.

  L’utilisateur d’un gestionnaire d’inscription d’appareil peut effectuer des actions sur l’appareil local, mais la gestion à distance d’autres appareils inscrits ne peut être effectuée qu’à partir de la console d’administration Intune. De plus, Intune déprécie l’utilisation de comptes gestionnaires d’inscription d’appareil avec le programme d’inscription des appareils Apple ou l’outil Configurateur Apple. Ces deux méthodes d’inscription prennent déjà en charge l’inscription sans utilisateur pour les appareils iOS partagés.

  Utilisez uniquement des comptes gestionnaires d’inscription d’appareil quand l’inscription sans utilisateur pour les appareils partagés n’est pas disponible. Pour plus d’informations, consultez [Inscrire des appareils d’entreprise avec le Gestionnaire d’inscription d’appareil dans Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md).

- **Changements apportés à l’application Portail d’entreprise Android**

  Si les utilisateurs finaux Android voient un message d’erreur indiquant qu’un certificat nécessaire pour leur appareil est manquant, ils peuvent appuyer sur un bouton « Comment résoudre ce problème » pour connaître la procédure d’installation du certificat manquant. Si les utilisateurs effectuent ces étapes, mais qu’un autre message d’erreur « Certificat manquant » s’affiche, ils sont invités à contacter leur administrateur informatique et de fournir ce lien, qui contient les étapes que les administrateurs informatiques peuvent utiliser pour résoudre le problème de certificat.

- **Limiter les installations d’applications à chargement indépendant sur des appareils Android inscrits**

  Les appareils Android ne peuvent plus installer d’applications via le site web Portail d’entreprise, sauf si les appareils ont été inscrits dans Intune à l’aide de l’application Portail d’entreprise Intune pour Android.


### <a name="new-in-configuration-manager-technical-preview"></a>Nouveautés de Configuration Manager Technical Preview

Aucune nouvelle fonctionnalité hybride n’a été introduite en juillet 2016 pour Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

Les fonctionnalités suivantes qui étaient précédemment disponibles dans les versions Configuration Manager Technical Preview sont maintenant disponibles dans les déploiements hybrides avec Intune et Configuration Manager (Current Branch) version 1606.

* Rechercher, gérer et distribuer des applications du Windows Store pour Entreprises pour des appareils Windows 10 à partir de la console Configuration Manager ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   Paramètre SmartLock pour les appareils Android ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   VPN déclenché par les applications pour les appareils Windows 10 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Nouvelle expérience pour les actions d’appareils distants ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Applications du Windows Store pour Entreprises ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Améliorations générales pour les applications achetées en volume ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Protection des informations Windows (WIP) ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Prédéclarer des appareils d’entreprise avec numéro IMEI ou numéro de série iOS ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Classer automatiquement des appareils dans des regroupements ([1606](whats-new-hybrid-archive.md#new-in-1606-technical-preview))

Pour plus d’informations sur les nouvelles fonctionnalités, consultez la documentation de la version Technical Preview spécifiée.

## <a name="notices"></a>Remarques

- **25 octobre 2016 : Chargement du portail d’entreprise Windows Phone 8 déprécié**

  La possibilité de charger une application Portail d’entreprise signée a été supprimée de la console Configuration Manager, car le support technique Intune est déprécié pour Windows 8, Windows Phone 8 et Windows RT, le support pour le portail d’entreprise Windows Phone 8 se termine au mois de novembre.  Les appareils Windows 8, Windows Phone 8 et Windows RT qui sont déjà inscrits continueront à être pris en charge, mais l’inscription d’appareils supplémentaires auprès de ces plateformes ne sera pas prise en charge.


### <a name="see-also"></a>Voir aussi

- [Anciennes fonctionnalités de gestion des appareils mobiles hybride](whats-new-hybrid-archive.md)
- [Nouveautés de MDM dans System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)



<!--HONumber=Nov16_HO1-->


