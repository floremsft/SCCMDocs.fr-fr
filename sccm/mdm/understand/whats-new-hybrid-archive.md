---
title: "Archive | Nouveautés de la gestion des appareils mobiles hybride | Microsoft Intune | System Center Configuration Manager"
description: "Archive des précédentes fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec System Center Configuration Manager et Intune."
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: bfc4baefbdddc5125c38272f2087d214151c91d5
ms.openlocfilehash: 4c0910ae365e1fda7b9747b79e13782a6056c0da

---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Précédentes fonctionnalités hybrides avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit des informations sur les précédentes fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec System Center Configuration Manager et Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilité avec les versions de Configuration Manager  

 Chaque section de cet article répertorie les fonctionnalités hybrides sous 3 catégories différentes. Utilisez les indications suivantes pour déterminer la compatibilité des fonctionnalités dans chaque catégorie avec différentes versions de Configuration Manager :  

|Catégories de fonctionnalités|
|-|  
|**Nouveautés de Microsoft Intune** : en général, toutes les fonctionnalités répertoriées dans cette catégorie doivent fonctionner avec toutes les versions de Configuration Manager, notamment les versions de System Center 2012 R2 Configuration Manager, dans la mesure où ces fonctionnalités nécessitent uniquement le service Intune et pas de fonctionnalités supplémentaires dans Configuration Manager.<br /><br /> **Nouveautés de Configuration Manager Technical Preview** : toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version d’évaluation technique spécifiée. Pour tester ces fonctionnalités, vous devez installer la version d’évaluation technique spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Nouveautés de Configuration Manager (Current Branch)** : toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version spécifiée de Configuration Manager (Current Branch), telle que la version 1511 ou 1602. Si vous utilisez une version antérieure de Configuration Manager pour votre déploiement hybride, vous devez effectuer la mise à niveau vers la version de Configuration Manager (Current Branch) spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Mettre à niveau vers System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## <a name="new-hybrid-features-in-june-2016"></a>Nouvelles fonctionnalités hybrides en juin 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune
Les fonctionnalités Intune suivantes introduites en juin 2016 fonctionnent dans les déploiements hybrides.

- Les informations sur l’**état du service Intune** pour Intune ont été déplacées vers un emplacement central avec d’autres services Microsoft. Vous trouverez maintenant ces informations dans le portail de gestion Office 365 sous État du service. Pour plus d’informations, consultez ce [billet de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Expérience de configuration de la stratégie de données d’entreprise Windows 10 améliorée**

  Intune propose maintenant une expérience améliorée pour la configuration de la stratégie Protection des informations Windows 10. Les améliorations comprennent de meilleures méthodes pour créer des règles d’application et spécifier la définition des limites réseau ainsi que d’autres paramètres de la Protection des informations Windows. Pour en savoir plus, consultez [Créer une stratégie Protection des informations Windows (WIP) à l’aide de Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Stratégie de contrôle d’accès réseau Cisco ISE pour Intune**

  Les clients qui utilisent Cisco ISE (Identity Service Engine) 2.1 et aussi Microsoft Intune peuvent définir une stratégie de contrôle d’accès réseau dans ISE. À l’aide de cette stratégie, les appareils qui doivent se connecter au réseau Wi-Fi ou VPN doivent respecter les conditions suivantes avant que l’accès ne leur soit accordé :

  - Ils doivent être gérés par Intune
  - Ils doivent être conformes à toutes les stratégies de conformité Intune déployées

  Les utilisateurs finaux d’appareils non conformes sont invités à les inscrire et corriger tout problème de conformité pour obtenir l’accès.

- **Accès conditionnel pour le navigateur**

  Vous pouvez définir une stratégie d’accès conditionnel pour Exchange Online et SharePoint Online afin qu’ils soient seulement accessibles à partir de navigateurs web pris en charge sur des appareils iOS et Android gérés et conformes. Les utilisateurs finaux qui essaient de se connecter aux sites OWA (Outlook Web Access) et SharePoint avec des appareils iOS et Android sont invités à inscrire leurs appareils avec Intune, ainsi qu’à résoudre les problèmes de non-conformité avant de se connecter. Pour plus d'informations, voir

  * [Restreindre l’accès à la messagerie Exchange Online et Exchange Online Dedicated (nouvel environnement) avec Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restreindre l’accès à SharePoint Online avec Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online prend en charge l’accès conditionnel**

  Vous pouvez définir une stratégie d’accès conditionnel pour Dynamics CRM Online afin qu’il soit accessible uniquement par les appareils iOS et Android gérés et conformes. Les utilisateurs finaux qui essaient de se connecter à l’application mobile Dynamics CRM sur iOS et Android sont invités à inscrire leurs appareils avec Intune, ainsi qu’à résoudre les problèmes de non-conformité avant de se connecter. Pour plus d’informations, consultez [Restreindre l’accès à Dynamics CRM Online avec Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune).

- **Mises à jour apportées à l’application Portail d’entreprise Android**

  Intune comporte désormais les nouvelles stratégies suivantes qui affectent les utilisateurs de l’application Portail d’entreprise Android :   

  Stratégie  |Effet sur les utilisateurs  
  ---------|---------
  Exiger que les appareils interdisent l’installation des applications provenant de sources inconnues (Android 4.0+)     |  Les utilisateurs finaux équipés d’appareils Android 4.0 ou version ultérieure voient le message « L’installation à partir de sources inconnues doit être désactivée ». Les utilisateurs doivent accéder à **Paramètres > Sécurité** sur leurs appareils et désactiver l’option **Sources inconnues**. Un lien dans le message de compatibilité permet aux utilisateurs d’obtenir plus d’informations sur le message et de savoir pourquoi ils doivent désactiver le paramètre.
  Exiger que les appareils interdisent l’installation des applications provenant de sources inconnues (Android 4.0+)  |    Les utilisateurs finaux équipés d’appareils Android 4.0 ou version ultérieure voient le message « Rechercher les menaces de sécurité sur l’appareil ». Les utilisateurs doivent accéder à **Paramètres > Google > Sécurité** sur leurs appareils et activer l’option **Rechercher les menaces de sécurité sur l’appareil**. Un lien dans le message de compatibilité permet aux utilisateurs d’obtenir plus d’informations sur le message et de savoir pourquoi ils doivent activer le paramètre.     
  Exiger que le débogage USB soit désactivé (Android 4.2+)  | Les utilisateurs finaux équipés d’appareils Android 4.2 ou version ultérieure voient le message « Le débogage USB doit être désactivé ». Les utilisateurs doivent accéder à **Paramètres > Options pour développeurs** sur leurs appareils et désactiver l’option **Débogage USB**. Un lien dans le message de compatibilité permet aux utilisateurs d’obtenir plus d’informations sur le message et de savoir pourquoi ils doivent désactiver le paramètre.
  Niveau minimal du correctif de sécurité Android (Android 6.0+)  | Les utilisateurs finaux équipés d’appareils Android 6.0 ou version ultérieure voient le message « Cet appareil n’est pas au niveau minimal du correctif de sécurité Android ». Les utilisateurs doivent installer le correctif de sécurité requis. Un lien dans le message de compatibilité permet aux utilisateurs d’obtenir des informations sur la façon d’installer le correctif de sécurité requis et d’identifier le correctif de sécurité actuellement installé.

- **Mises à jour apportées à l’application Portail d’entreprise iOS**

  * Quand les utilisateurs finaux installent des applications métier, ils bénéficient désormais d’une expérience améliorée en termes d’installation d’applications. Si l’installation de l’application prend beaucoup de temps, les utilisateurs peuvent synchroniser manuellement leur appareil pour forcer la reprise du processus de synchronisation. Pour passer en revue les instructions pour l’utilisateur final, consultez Synchroniser manuellement votre appareil iOS.
  * L’application Portail d’entreprise Microsoft Intune pour iOS a été mise à jour pour prendre en charge iOS versions 8.0 et ultérieure. Cette mise à jour signifie que les utilisateurs finaux peuvent installer l’application Portail d’entreprise et inscrire de nouveaux appareils dans Intune uniquement si l’appareil exécute iOS version 8.0 ou ultérieure. Les utilisateurs qui ont déjà inscrit des appareils exécutant une version non prise en charge d'iOS peuvent continuer à utiliser l'application Portail d'entreprise qui figure sur leur appareil.


### <a name="new-in-1606-technical-preview"></a>Nouveautés de la version d’évaluation technique 1606
Les nouvelles fonctionnalités suivantes introduites en juin 2016 sont disponibles dans les déploiements hybrides avec Intune et Configuration Manager Technical Preview 1606.

- **Classer automatiquement des appareils dans des regroupements**

  Vous pouvez créer des catégories d’appareils, qui permettent de placer automatiquement les appareils dans des regroupements d’appareils quand vous utilisez Configuration Manager avec Intune. Les utilisateurs doivent ensuite choisir une catégorie d’appareils quand ils inscrivent un appareil dans Intune. Vous pouvez en outre modifier la catégorie d’un appareil à partir de la console Configuration Manager. Pour plus d’informations, consultez [Classer automatiquement des appareils dans des regroupements](/sccm/core/get-started/capabilities-in-technical-preview-1606.md#dmp_category) dans [Fonctionnalités de la version d’évaluation technique 1606 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606.md).

  > [!IMPORTANT]
  > Cette fonctionnalité est opérationnelle avec la version de juin 2016 de Microsoft Intune. Vérifiez que vous avez effectué la mise à jour vers cette version avant d’essayer ces procédures.

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)
Aucune nouvelle fonctionnalité hybride n’a été introduite en juin 2016 pour Configuration Manager (Current Branch).

##  <a name="new-hybrid-features-in-may-2016"></a>Nouvelles fonctionnalités hybrides en mai 2016  

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune  
 Les fonctionnalités Intune suivantes introduites en mai 2016 fonctionnent dans les déploiements hybrides.

- **SDK GAM : Prendre en charge la configuration de la longueur du code confidentiel**

  Vous pouvez désormais spécifier une longueur de code confidentiel pour les applications GAM semblable à un code confidentiel d’appareil. Cela nécessite que les utilisateurs finaux se conforment aux nouvelles restrictions que vous définissez. L’écran de saisie du code confidentiel est légèrement modifié pour tenir compte de l’entrée la plus longue. Pour plus d’informations, consultez [Paramètres de stratégie GAM pour Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings) et [Paramètres de stratégie GAM pour iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype Entreprise pour iOS et Android**

  Vous pouvez maintenant cibler Skype Entreprise avec [GAM sans stratégie d’inscription](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Une fois les utilisateurs connectés, les stratégies GAM sont appliquées.  

- **Nouvelles applications disponibles pour la gestion avec des stratégies GAM**

  Les applications Microsoft Word, Excel et PowerPoint pour Android peuvent maintenant être associées à des stratégies GAM sur les appareils qui ne sont pas inscrits avec Intune. Pour obtenir une liste complète des applications prises en charge, accédez à la galerie des applications mobiles Microsoft Intune dans la page [Partenaires d’application Microsoft Intune](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx).  

- **Application Portail d’entreprise Android : notifications toast pour l’utilisateur final**

  Les notifications toast de l’application Portail d’entreprise Android apparaissent quand les utilisateurs finaux inscrivent ou suppriment leurs appareils dans le portail d’entreprise.  

- **Site web du portail d’entreprise : la bannière d’identification de l’appareil fournit d’autres informations aux utilisateurs finaux**

  Les utilisateurs finaux peuvent désormais identifier plus facilement l’appareil qu’ils ont sélectionné quand ils utilisent le site web du portail d’entreprise. Si l’appareil choisi n’est pas correct, ils peuvent sélectionner l’appareil approprié en appuyant sur le lien **Appuyer ici** dans la bannière de la page d’accueil.  


### <a name="new-in-1605-technical-preview"></a>Nouveautés de la version d’évaluation technique 1605  
 Les nouvelles fonctionnalités suivantes introduites en mai 2016 sont disponibles dans les déploiements hybrides avec Intune et Configuration Manager Technical Preview 1605. Ces fonctionnalités exigent que vous utilisiez la console Configuration Manager pour les configurer et les gérer.  

- **VPN déclenché par les applications pour les appareils Windows 10**

  Pour les appareils Windows 10 gérés à l’aide de Configuration Manager avec Intune, vous pouvez ajouter une liste d’applications qui ouvrent automatiquement une connexion VPN que vous avez configurée via la console d’administration Configuration Manager. Pour plus d’informations, consultez [VPN déclenché par les applications pour les appareils Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1605) dans [Fonctionnalités de la version d’évaluation technique 1605 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **Nouvelle expérience pour les actions des appareils à distance**

  L’exécution des actions des appareils à distance à partir de la console Configuration Manager a été améliorée.

  Des actions courantes telles que **Mettre hors service/Réinitialiser**, **Réinitialisation du code secret**, **Verrouillage à distance** et **Contourner le verrou d’activation** figurent désormais dans le menu **Actions de l’appareil à distance** accessible à partir de l’espace de travail **Ressources et Conformité**

  Pour plus d’informations, consultez [Nouvelle expérience pour les actions des appareils à distance](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) dans [Fonctionnalités de la version d’évaluation technique 1605 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Applications du Windows Store pour Entreprises**

  Le [Windows Store pour Entreprises](https://www.microsoft.com/en-us/business-store) est l’emplacement où vous pouvez trouver et acheter des applications pour votre organisation, isolément ou en volume. En connectant le Store à Configuration Manager, vous pouvez gérer les applications achetées en volume à partir de la console Configuration Manager. Pour plus d’informations, consultez [Applications du Windows Store pour Entreprises](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) dans [Fonctionnalités de la version d’évaluation technique 1605 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Améliorations générales pour les applications achetées en volume**

  Les applications achetées en volume dans le Windows Store pour Entreprises et App Store iOS ont été consolidées dans une même vue, **Informations de licence pour les applications du Store**. En outre, la façon dont vous créez des applications achetées en volume pour iOS a été améliorée. Pour plus d’informations, consultez [Améliorations générales pour les applications achetées en volume](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) dans [Fonctionnalités de la version d’évaluation technique 1605 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Prédéclarer des appareils d’entreprise avec leur numéro IMEI ou leur numéro de série iOS**

  Vous pouvez désormais identifier des appareils d’entreprise en important leur numéro IMEI (International Mobile Equipment Identity). Vous pouvez charger un fichier de valeurs séparées par des virgules (.csv) contenant les numéros IMEI des appareils ou saisir manuellement les informations sur les appareils.  Vous pouvez également importer des numéros de série pour les appareils iOS.  Pour plus d’informations, consultez [Prédéclarer des appareils d’entreprise avec leur numéro IMEI ou leur numéro de série iOS](../../core/get-started/capabilities-in-technical-preview-1605.md#pre-declare-corporate-owned-devices-with-with-imei-or-ios-serial-number) dans [Fonctionnalités de la version d’évaluation technique 1605 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Protection des informations Windows (WIP)**

  Vous pouvez créer des éléments de configuration qui vous permettent de déployer vos stratégies Protection des informations Windows (WIP), notamment de choisir vos applications protégées, de définir le niveau de protection assuré par WIP et de rechercher des données d’entreprise sur le réseau. Pour plus d’informations sur WIP, consultez les rubriques suivantes :  

  -   [Protéger les données d’entreprise avec Protection des informations Windows (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Créer et déployer une stratégie Protection des informations Windows (WIP) à l’aide de System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)  
 Aucune nouvelle fonctionnalité hybride n’a été introduite en mai 2016 pour Configuration Manager (Current Branch).  

##  <a name="new-hybrid-features-in-april-2016"></a>Nouvelles fonctionnalités hybrides en avril 2016  

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune  
 Les fonctionnalités Intune suivantes introduites en avril 2016 fonctionnent dans les déploiements hybrides.  

- **Conformité des utilisateurs GAM**

  Vous pouvez désormais afficher l’état de vos stratégies de gestion des applications pour tous les utilisateurs dans votre client Azure Active Directory (AAD).  Pour plus d’informations, consultez [Analyser les stratégies de gestion des applications mobiles à l’aide de Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) dans la bibliothèque Intune.  

- **Contrôles GAM pour empêcher la synchronisation des contacts Outlook (Android)**

  Un nouveau paramètre est disponible, qui vous permet d’empêcher une application de synchroniser des contacts dans le carnet d’adresses natif sur les appareils Android. Ce nouveau paramètre est initialement pris en charge par l’application Outlook sur les appareils Android. Pour plus d’informations, consultez [Créer et déployer des stratégies de gestion des applications mobiles à l’aide de Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) dans la bibliothèque Intune.  

- **Améliorations apportées au site web du portail d’entreprise**

  Quand les utilisateurs Windows 10 Mobile et Windows Phone 8.1 installent des applications métier, ils voient à présent les nouveaux états suivants, qui leur fournissent plus de détails sur l’état de leur installation :  

  -   **En attente de la synchronisation de l’appareil** : l’utilisateur a appuyé sur Installer et l’appareil tente à présent la synchronisation avec l’infrastructure Intune. La synchronisation est nécessaire avant de procéder à l’installation. Le message « En attente de la synchronisation de l’appareil » est également un lien sur lequel les utilisateurs peuvent appuyer pour afficher des instructions sur la façon de synchroniser manuellement leur appareil avec Intune si le processus de synchronisation dure longtemps ou se bloque.  

  -   **Téléchargement** : la demande de téléchargement de l’utilisateur est en cours de traitement et l’appareil télécharge et installe l’application.  

- **Améliorations apportées à l’application Portail d’entreprise Android**

  Les utilisateurs qui n’ont pas inscrit leur appareil dans Intune et qui n’ont pas le bon certificat installé ne peuvent pas se connecter à l’application Portail d’entreprise Android et le message « Vous ne pouvez pas vous connecter, car il manque un certificat obligatoire à votre appareil. » s’affiche. Le message inclut un lien « Comment résoudre ce problème » sur lequel les utilisateurs peuvent appuyer pour afficher des instructions sur l’installation du certificat. Pour connaître les étapes que les utilisateurs finaux suivent pour résoudre ce problème, consultez [Un certificat obligatoire est manquant sur votre appareil](/intune/enduser/using-your-android-device-with-intune) dans la bibliothèque Intune.  

- **Améliorations apportées à l’application Portail d’entreprise iOS**

  La prise en charge de l’action Extraire pour actualiser a été ajoutée pour actualiser le contenu de l’écran d’accueil, qui inclut les applications répertoriées, les appareils répertoriés et les coordonnées du service informatique. L’action Extraire pour actualiser ne vérifie pas les informations de conformité ni de la stratégie ; cette vérification peut être effectuée en sélectionnant la vignette de votre appareil et en appuyant sur le bouton **Synchroniser**.  

- **Améliorations apportées à l’application Portail d’entreprise Windows 10 Mobile et Windows Phone 8.1**

  Quand les utilisateurs finaux installent des applications métier, ils bénéficient désormais d’une expérience améliorée en termes d’installation d’applications. Si l’installation de l’application prend beaucoup de temps, les utilisateurs peuvent synchroniser manuellement leur appareil pour forcer la reprise du processus de synchronisation. Pour passer en revue les instructions pour l’utilisateur final, consultez [Synchroniser votre appareil manuellement à l’aide du site web Portail d’entreprise](/intune/enduser/using-your-windows-device-with-intune) dans la bibliothèque Intune.  

###  <a name="new-in-1604-technical-preview"></a>Nouveautés de la version d’évaluation technique 1604
 Les nouvelles fonctionnalités suivantes introduites en avril 2016 sont disponibles dans les déploiements hybrides avec Intune et Configuration Manager Technical Preview 1604. Ces fonctionnalités exigent que vous utilisiez la console Configuration Manager pour les configurer et les gérer.  

- **Rechercher, gérer et distribuer des applications du Windows Store pour Entreprises pour des appareils Windows 10 à partir de la console Configuration Manager**


  La prise en charge du Windows Store pour Entreprises est disponible dans Configuration Manager Technical Preview 1604 pour vous aider à rechercher, gérer et distribuer des applications pour les appareils Windows 10 que vous gérez. Pour plus d’informations, consultez [Gérer les applications achetées en volume à partir du Windows Store pour Entreprises](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) dans [Fonctionnalités de la version d’évaluation technique 1604 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **Paramètre SmartLock pour les appareils Android**

  Un nouveau paramètre a été ajouté à l’élément de configuration Android et Samsung KNOX, qui vous permet de contrôler la fonctionnalité SmartLock sur les appareils Android compatibles.  Vous pouvez utiliser ce paramètre pour empêcher des utilisateurs finaux de configurer SmartLock. Consultez [Paramètre SmartLock pour les appareils Android](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) dans [Fonctionnalités de la version d’évaluation technique 1604 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md).  

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)  
 Aucune nouvelle fonctionnalité hybride n’a été introduite en avril 2016 pour Configuration Manager (Current Branch).  

##  <a name="new-hybrid-features-in-march-2016"></a>Nouvelles fonctionnalités hybrides en mars 2016  

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune  
 Les fonctionnalités Intune suivantes introduites en mars 2016 fonctionnent dans les déploiements hybrides.  

- **Contrôles GAM pour empêcher la synchronisation des contacts Outlook (iOS)**

  Un nouveau paramètre est disponible, qui vous permet d’empêcher une application de synchroniser des contacts dans le carnet d’adresses natif sur les appareils iOS. Ce nouveau paramètre est pris en charge par l’application Outlook sur les appareils iOS. Pour plus d’informations sur ce paramètre et d’autres paramètres, consultez [Créer et déployer des stratégies GAM](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) dans la bibliothèque Intune.  

- **Skype Entreprise Online prend en charge l’accès conditionnel**

  Vous pouvez définir une stratégie d’accès conditionnel pour Skype Entreprise Online afin qu’il soit accessible uniquement par les appareils iOS et Android gérés et conformes.  Pour plus d’informations, consultez [Gérer l’accès à Skype Entreprise Online](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) dans la bibliothèque Intune.  

- **Prise en charge d’iOS 9.3**

  Lundi 21 mars, Apple a annoncé la disponibilité d’iOS 9.3. Toutes les fonctionnalités Intune existantes actuellement disponibles pour la gestion des appareils iOS continuent de fonctionner en toute transparence quand les utilisateurs effectuent la mise à niveau de leurs appareils vers iOS 9.3.  

- **Packages d’application Windows disponibles directement depuis le site web du portail d’entreprise**

  Les utilisateurs de PC exécutant Windows RT, Windows 8 et Windows 8.1 peuvent désormais installer les packages d’application Windows (avec l’extension .appx) directement depuis le site web du portail d’entreprise. Auparavant, vous deviez déployer l’application Portail d’entreprise, ou les utilisateurs devaient l’installer sur leurs appareils, pour installer des applications.  

- **Les utilisateurs peuvent verrouiller à distance leurs appareils depuis le site web du portail d’entreprise**

  Une nouvelle option Verrouillage à distance a été ajoutée au site web du portail d’entreprise pour permettre aux utilisateurs de verrouiller à distance leur appareil depuis le portail s’il est perdu ou volé.  

- **Tirer parti de la fonctionnalité de gestion iOS Open In pour les appareils inscrits dans une solution de gestion des appareils mobiles tierce**

  Vous pouvez utiliser votre fournisseur de solution de gestion des appareils mobiles tierce pour tirer parti de la fonctionnalité de gestion iOS Open In. Vous pouvez définir les restrictions dans les paramètres de profil de configuration et déployer l’application à l’aide de votre logiciel de gestion des appareils mobiles. Quand l’utilisateur installe l’application gérée, les restrictions sont appliquées. Pour plus d’informations, consultez [Stratégies de gestion des applications mobiles Microsoft Intune et iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) dans la bibliothèque Intune.  

- **Applications Microsoft qui prennent en charge GAM**

  La liste des applications Microsoft que vous pouvez utiliser avec les stratégies de gestion des applications mobiles Intune a été mise à jour pour inclure les dernières applications (pour les appareils inscrits avec Intune uniquement).  

- **Déployer Adobe Reader pour Microsoft Intune sur des appareils iOS gérés par Intune dans votre entreprise**

  L’application Adobe Reader pour iOS peut maintenant être gérée sur les appareils inscrits avec la stratégie de gestion des applications mobiles Intune.  

- L’application de partage Rights Management est prise en charge pour Android

  Les administrateurs informatiques peuvent déployer des stratégies de gestion des applications mobiles afin que les utilisateurs finaux puissent afficher des images, des fichiers PDF et AV en toute sécurité, que le service informatique utilise ou non Intune pour gérer les appareils.  

- **Améliorations apportées à l’application Portail d’entreprise Android et iOS**

  -   Quand vos utilisateurs lancent une application qui est gérée par la gestion des applications mobiles (GAM), ils voient un message qui leur indique que l’application est gérée par leur société. Les utilisateurs peuvent désormais appuyer sur un lien « En savoir plus » pour obtenir plus d’informations ici sur ce que signifie « applications gérées ». Ils peuvent aussi appuyer sur « Ne plus afficher ce message » afin que le message ne s’affiche plus lors du lancement de l’application.  

  -   De nouveaux écrans ont été ajoutés pour guider les utilisateurs dans le processus d’inscription et fournir plus d’informations sur la raison pour laquelle les utilisateurs doivent s’inscrire ainsi que sur ce que les administrateurs informatiques peuvent et ne peuvent pas voir sur leurs appareils inscrits.  

  -   Des messages d’erreur d’inscription s’affichent maintenant dans l’application Portail d’entreprise.  

### <a name="new-in-configuration-manager-technical-preview"></a>Nouveautés de Configuration Manager Technical Preview  
 Aucune nouvelle fonctionnalité hybride n’a été introduite en mars 2016 pour Configuration Manager Technical Preview.  

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)  
 Les nouvelles fonctionnalités suivantes introduites en mars 2016 sont disponibles dans les déploiements hybrides avec Intune et Configuration Manager (Current Branch) version 1602. Ces fonctionnalités exigent que vous utilisiez la console Configuration Manager pour les configurer et les gérer.  

- **Stratégies de configuration d’applications iOS**

  Dans la version 1602 de Configuration Manager (Current Branch), vous pouvez utiliser des stratégies de configuration d’applications pour fournir des paramètres pouvant être requis si l’utilisateur exécute une application iOS. Pour plus d’informations, consultez [Configurer des applications iOS avec des stratégies de configuration des applications dans System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  

- **Gérer les applications iOS achetées en volume**

  Dans la version 1602 de Configuration Manager (Current Branch), vous pouvez déployer et gérer des applications que vous avez achetées en volume dans le cadre d’un Programme d’achat en volume (VPP) Apple, en important les informations de licence à partir de l’App Store et en suivant le nombre de licences que vous avez utilisées. Pour plus d’informations, consultez [Gérer les applications iOS achetées en volume avec System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Création automatique d’applications mobiles Office**

  Depuis la version 1602 de Configuration Manager (Current Branch), les applications mobiles Microsoft Office suivantes pour Android et iOS sont créées quand vous effectuez la mise à niveau à partir de la version 1511 :  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (iOS uniquement)  
  -   Microsoft Outlook  

  Vous trouverez ces applications dans le nœud Applications de la console Configuration Manager. Pour plus d’informations sur le déploiement d’applications, consultez [Comment déployer des applications avec System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Paramètres du mode plein écran pour les appareils Android Samsung KNOX**

  Le mode kiosque vous permet de verrouiller un appareil pour n'autoriser que le fonctionnement de certaines fonctionnalités.  Depuis la version 1602 de Configuration Manager (Current Branch), vous pouvez maintenant spécifier les paramètres du mode plein écran pour les appareils Samsung KNOX. Pour plus d’informations, consultez [Comment créer des éléments de configuration pour des appareils Android et Samsung KNOX gérés sans le client System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **Verrou d’activation iOS**

  Depuis la version 1602 de Configuration Manager (Current Branch), vous pouvez gérer le verrou d’activation iOS, fonctionnalité de l’application Rechercher mon iPhone pour les appareils iOS 7.1 et versions ultérieures. Le verrou d'activation est activé automatiquement quand l'application Rechercher mon iPhone est utilisée sur un appareil.  Pour plus d’informations, consultez [Gérer le contournement du verrou d’activation iOS pour System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock).  



<!--HONumber=Nov16_HO1-->


