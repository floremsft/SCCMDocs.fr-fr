---
title: "Créer des éléments de configuration pour des appareils iOS et Mac OS X gérés sans le client System Center Configuration Manager | Microsoft Docs"
description: "L’élément de configuration System Center Configuration Manager iOS et Mac OS X permet de gérer les paramètres des appareils iOS et Mac OS X."
ms.custom: na
ms.date: 12/14/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c378e0f7-be49-4b96-a46b-7c5d9638bd96
caps.latest.revision: 15
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: d023df79e0bcb7d5583224802976a5059c4ee753
ms.openlocfilehash: ea4024aaa07d40781663725127d64388055c6501


---
# <a name="create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-system-center-configuration-manager-client"></a>Créer des éléments de configuration pour des appareils iOS et Mac OS X gérés sans le client System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’élément de configuration System Center Configuration Manager **iOS et Mac OS X** pour gérer les paramètres des appareils iOS et Mac OS X qui sont inscrits dans Microsoft Intune ou gérés localement par Configuration Manager.  

## <a name="to-create-an-ios-and-mac-os-x-configuration-item"></a>Pour créer un élément de configuration iOS et Mac OS X  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Éléments de configuration**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un élément de configuration**.  

4.  Dans la page **Général** de l’ **Assistant Création d’élément de configuration**, spécifiez un nom et une description éventuelle pour l’élément de configuration.  

5.  Sous **Spécifier le type d’élément de configuration que vous voulez créer**, sélectionnez **iOS et Mac OS X**.  

6.  Cliquez sur **Catégories** si vous créez et attribuez des catégories pour faciliter la recherche et le filtrage des éléments de configuration dans la console Configuration Manager.  

7.  Dans la page **Plateformes prises en charge**, sélectionnez les plateformes iOS ou Mac OS X spécifiques chargées d’évaluer l’élément de configuration.  

8.  Dans la page **Paramètres de l’appareil**, sélectionnez le groupe de paramètres à configurer. Consultez [Informations de référence sur les paramètres d’élément de configuration iOS et Mac OS X](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client#ios-and-mac-os-x-configuration-item-settings-reference) dans cette rubrique pour plus d’informations, puis cliquez sur **Suivant**.  

    > [!TIP]  
    >  Si le paramètre souhaité n’est pas répertorié, cochez la case **Configurer d’autres paramètres qui ne se trouvent pas dans les groupes de paramètres par défaut**.  

9. Dans chaque page de paramètres, configurez les paramètres dont vous avez besoin et indiquez si vous voulez les corriger quand ils ne sont pas conformes sur des périphériques (quand cela est pris en charge).  

10. Pour chaque groupe de paramètres, vous pouvez aussi spécifier la gravité signalée dans les rapports Configuration Manager quand un élément de configuration est évalué comme non conforme :  

    -   **Aucun** : les appareils qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec.  

    -   **Informations** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations**.  

    -   **Avertissement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement**.  

    -   **Critique** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique**.  

    -   **Critique avec événement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique**.  

11. Dans la page **Condition d’application de la plateforme**, passez en revue tous les paramètres qui ne sont pas conformes avec les plateformes prises en charge que vous avez sélectionnées précédemment. Vous pouvez revenir sur ces paramètres et les supprimer, ou vous pouvez continuer.  

    > [!TIP]  
    >  La conformité des paramètres non pris en charge n’est pas évaluée.  

12. Effectuez toutes les étapes de l'Assistant.  

 Vous pouvez afficher le nouvel élément de configuration dans le nœud **Éléments de configuration** de l’espace de travail **Ressources et Conformité** .  

##  <a name="ios-and-mac-os-x-configuration-item-settings-reference"></a>Informations de référence sur les paramètres d’élément de configuration iOS et Mac OS X  

###  <a name="password"></a>Mot de passe  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Demander des paramètres de mot de passe sur les appareils mobiles**|Exigez un mot de passe sur les appareils pris en charge.|  
|**Longueur minimale du mot de passe (caractères)**|Longueur minimale du mot de passe.|  
|**Expiration du mot de passe en jours**|Nombre de jours avant qu'un mot de passe ne doive être modifié.|  
|**Nombre de mots de passe mémorisés**|Empêche la réutilisation des mots de passe déjà utilisés.|  
|**Nombre d'échecs de tentative de connexion avant que l'appareil soit réinitialisé**|Réinitialise l'appareil si le nombre d'échecs de tentative de est atteint.<br>(iOS uniquement)| 
|**Durée d’inactivité avant le verrouillage de l’appareil**|Spécifie le nombre de minutes d’inactivité avant que l’appareil soit automatiquement verrouillé.|
|**Complexité du mot de passe**|Indiquez si vous pouvez spécifier un code confidentiel tel que « 1234 » ou si vous devez fournir un mot de passe fort.|
|**Autoriser les mots de passe simples**|Spécifie que des mots de passe simples comme « 0000 » et « 1234 » peuvent être utilisés.|
|**Empreinte digitale pour le déverrouillage**|Autorise l’utilisation d’une empreinte digitale pour déverrouiller l’appareil.|

###  <a name="device"></a>Appareil  
 Ces paramètres s’appliquent aux appareils iOS et Mac OS X.  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Numérotation vocale**|Autorise l'utilisation de la fonctionnalité de numérotation vocale sur l'appareil.|  
|**Assistant vocal**|Autorise l'utilisation d'une application d'assistance vocale comme Siri.|  
|**Assistant vocal lors du verrouillage**|Autorise l'utilisation d'une application d'assistance vocale comme Siri lorsque l'appareil est verrouillé.|  
|**Capture d'écran**|Permet de prendre une capture d'écran de l'affichage de l'appareil.|  
|**Client chat vidéo**|Autorise l’utilisation des applications de conversation vidéo comme Facetime.|  
|**Ajouter des amis du centre de jeux**|Permet d'ajouter des amis de l'application du centre de jeux.|  
|**Jeux multijoueur**|Permet de jouer avec d'autres joueurs sur Internet.|  
|**Logiciel de portefeuille personnel lors du verrouillage**|Autorise l'utilisation d'un logiciel de portefeuille personnel comme Passbook.|  
|**Envoi des données de diagnostic**|Autorisez l'envoi des journaux d'application.|  

###  <a name="store"></a>Magasin  
 Ces paramètres s'appliquent aux appareils iOS uniquement.  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Boutique d'applications**|Permet d'accéder à l'App Store sur l'appareil.|  
|**Entrer un mot de passe pour accéder à la boutique d'applications**|Les utilisateurs doivent entrer un mot de passe pour accéder à l'App Store.|  
|**Achats dans l'application**|Autorise les utilisateurs à effectuer des achats dans l'application.|  

###  <a name="browser"></a>Navigateur  
 Ces paramètres s'appliquent aux appareils iOS uniquement.  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Autoriser le navigateur web**|L’utilisateur peut utiliser le navigateur web par défaut de l’appareil.|  
|**Remplissage automatique**|L'utilisateur peut modifier les paramètres de saisie semi-automatique dans le navigateur.|  
|**Active scripting**|Le navigateur peut exécuter des scripts, tels que les scripts ActiveX.|  
|**Bloqueur de fenêtres publicitaires**|Active ou désactive le bloqueur de fenêtres publicitaires du navigateur.|  
|**Cookies**|Autorisez l'enregistrement des cookies sur l'appareil.|  
|**Avertissement de fraude**|Activez ou désactivez les avertissements des sites Web frauduleux potentiels.|  

###  <a name="content-rating"></a>Contrôle d’accès au contenu  
 Ces paramètres s'appliquent aux appareils iOS uniquement.  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Contenu explicite dans la boutique multimédia**|Spécifiez si vous autorisez que le contenu pour adultes soit accessible à partir de l'App Store.|  
|**Région des classifications**|Spécifie le pays pour lequel vous souhaitez appliquer des restrictions de classifications.|  
|**Classification des films**|Spécifiez la classification maximale de contenu vidéo que vous souhaitez autoriser.|  
|**Classification des émissions de télévision**|Spécifiez la classification maximale de contenu d'émission de télévision que vous souhaitez autoriser.|  
|**Classification des applications**|Spécifiez la classification maximale de contenu d'application que vous souhaitez autoriser.|  

> [!NOTE]  
>  Les classifications que vous pouvez sélectionner varient en fonction de la **Région des classifications** sélectionnée.  

###  <a name="cloud"></a>Cloud  
 Ces paramètres s'appliquent aux appareils iOS uniquement.  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Sauvegarde cloud**|Autorisez les sauvegardes sur un service cloud comme iCloud.|  
|**Sauvegarde chiffrée**|Autorisez le chiffrement des sauvegardes sur un service cloud.|  
|**Synchronisation de documents**|Autorisez la synchronisation des documents sur un service cloud.|  
|**Synchronisation des photos**|Autorisez la synchronisation des photos sur un service cloud.|  

###  <a name="security"></a>Sécurité  
 Ces paramètres s'appliquent aux appareils iOS uniquement.  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Appareil photo**|Autorisez l'utilisation de l'appareil photo.|  

###  <a name="roaming"></a>Itinérant  
 Ces paramètres s'appliquent aux appareils iOS uniquement.  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Itinérance vocale**|Autorise les appels vocaux lors de l'itinérance.|  
|**Synchronisation automatique lors de l’itinérance**|Permet à l'appareil de se synchroniser automatiquement lors de l'itinérance.|  
|**Itinérance des données**|Autorisez l'itinérance entre réseaux lors de l'accès aux données.|  

###  <a name="system-security"></a>Sécurité système  
 Ces paramètres s'appliquent aux appareils iOS uniquement.  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**L’utilisateur doit accepter les certificats TLS non approuvés**|Si **Autorisé**, l'utilisateur peut accepter les certificats. Si **Interdit**, les certificats non approuvés sont automatiquement rejetés.|
|**Autoriser le verrou d’activation (mode supervisé uniquement)**|Utilisez ce paramètre pour activer le verrou d’activation iOS sur les appareils iOS **supervisés** que vous gérez. Pour plus d’informations sur le verrou d’activation, consultez [Gérer le verrou d’activation iOS](../../mdm/deploy-use/manage-ios-activation-lock.md).
|**Centre de contrôle sur l’écran de verrouillage**|Détermine si l'application de centre de contrôle est accessible lorsque l'appareil est verrouillé.|  
|**Affichage des notifications sur l’écran de verrouillage**|Détermine si les notifications peuvent s'afficher lorsque l'appareil est verrouillé.|  
|**Affichage journée sur l’écran de verrouillage**|Détermine si la vue Aujourd'hui peut s'afficher lorsque l'appareil est verrouillé.|   

###  <a name="data-protection"></a>Protection des données  
 Ces paramètres s'appliquent aux appareils iOS uniquement.  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Ouvrir les documents des applications gérés dans d’autres applications non gérées**|Pour une utilisation avec les applications gérées par les stratégies de gestion des applications Configuration Manager.|  
|**Ouvrir les documents des applications non gérées dans d’autres applications gérées**|Pour une utilisation avec les applications gérées par les stratégies de gestion des applications Configuration Manager.|  

###  <a name="compliant-and-noncompliant-apps-ios"></a>Applications conformes et non conformes (iOS)  
 Permet de spécifier une liste d’applications iOS conformes ou non conformes dans votre entreprise. Vous pouvez ensuite utiliser des rapports pour afficher les appareils sur lesquels sont installées des applications non conformes et l'utilisateur associé.  

 Vous ne pouvez pas spécifier à la fois les applications conformes et non conformes dans le même élément de configuration.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Pour spécifier la liste des applications conformes ou non conformes  

1.  Dans la page **Applications conformes et non conformes (iOS)** , spécifiez les informations suivantes :  

    -   **Liste des applications non conformes** - Sélectionnez cette option si vous souhaitez spécifier une liste d’applications qui seront signalées comme non conformes en cas d’installation par des utilisateurs.  

    -   **Liste des applications conformes** - Sélectionnez cette option si vous souhaitez spécifier une liste d’applications que les utilisateurs sont autorisés à installer. Toutes les autres applications installées sont signalées comme non conformes.  

    -   **Ajouter** - Ajoute une application à la liste sélectionnée. Spécifiez un nom de votre choix, éventuellement l'éditeur de l'application, et l'URL de l'application dans le magasin d'applications.  

         Pour spécifier l'URL, à partir de l'iTunes App Store, recherchez l'application que vous voulez utiliser.  

         Ouvrez la page de l'application, puis copiez l'URL dans le Presse-papiers. Vous pouvez maintenant utiliser cette URL dans la liste des applications conformes ou non conformes.  

         **Exemple :** recherchez l’application **Microsoft Word pour iPad** dans le Store. L'URL que vous utilisez sera **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  

    -   **Modifier** - Permet de modifier le nom, l’éditeur et l’URL de l’application sélectionnée.  

    -   **Supprimer** - Supprime l’application sélectionnée dans la liste.  

    -   **Importer** - Importe une liste d’applications que vous avez spécifiée dans un fichier de valeurs séparées par des virgules. Utilisez le format Nom de l'application, Éditeur, URL de l'application dans le fichier.  

2.  Lorsque vous avez terminé, cliquez sur **Suivant**.  

 Vous pouvez utiliser l’un des rapports suivants pour surveiller les applications conformes et non conformes :  

-   **Liste des applications et des appareils non conformes d'un utilisateur spécifié** : affiche des informations sur les utilisateurs et les appareils sur lesquels sont installées des applications non conformes avec une stratégie que vous avez spécifiée.  

-   **Résumé des utilisateurs ayant des applications non conformes** : affiche des informations sur les utilisateurs qui ont installé des applications non conformes avec une stratégie que vous avez spécifiée.  

 Pour plus d’informations sur la façon d’utiliser les rapports, consultez [Rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  

###  <a name="compliant-and-noncompliant-apps-mac-os-x"></a>Applications conformes et non conformes (Mac OS X)  
 Permet de spécifier une liste d’applications Mac OS X conformes ou non conformes dans votre entreprise. Vous pouvez ensuite utiliser des rapports pour afficher les appareils sur lesquels sont installées des applications non conformes et l'utilisateur associé.  

 Vous ne pouvez pas spécifier à la fois les applications conformes et non conformes dans le même élément de configuration.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Pour spécifier la liste des applications conformes ou non conformes  

1.  Dans la page **Applications conformes et non conformes (Mac OS X)** , spécifiez les informations suivantes :  

    -   **Liste des applications non conformes** - Sélectionnez cette option si vous souhaitez spécifier une liste d’applications qui seront signalées comme non conformes en cas d’installation par des utilisateurs.  

    -   **Liste des applications conformes** - Sélectionnez cette option si vous souhaitez spécifier une liste d’applications que les utilisateurs sont autorisés à installer. Toutes les autres applications installées sont signalées comme non conformes.  

    -   **Ajouter** - Ajoute une application à la liste sélectionnée. Spécifiez un nom de votre choix, éventuellement l’éditeur de l’application, et l’ID d’offre groupée de l’application.  

        > [!TIP]  
        >  Pour rechercher l’ID d’offre groupée d’une application, effectuez les étapes suivantes sur un ordinateur Mac où l’application est installée :  
        >   
        >  1.  Ouvrez le dossier dans lequel l’application est installée (par exemple, **/Applications**)  
        > 2.  Sélectionnez l’offre groupée *<Nom de l’application\>***.app** et choisissez **Afficher le contenu du package**.  
        > 3.  Ouvrez le fichier **Info.plist**  
        > 4.  Vérifiez la valeur associée à la clé **CFBundleIdentifier**  
        >   
        >  L’ID d’offre groupée se présente ainsi : **com.contoso.nomapp**  

    -   **Modifier** - Permet de modifier le nom, l’éditeur et l’ID d’offre groupée de l’application sélectionnée.  

    -   **Supprimer** - Supprime l’application sélectionnée dans la liste.  

    -   **Importer** - Importe une liste d’applications que vous avez spécifiée dans un fichier de valeurs séparées par des virgules. Utilisez le format, le nom de l’application, l’éditeur et l’ID d’offre groupée dans le fichier.  

2.  Lorsque vous avez terminé, cliquez sur **Suivant**. Les éléments de configuration contenant des paramètres d’application conformes et non conformes doivent être déployés sur des regroupements d’utilisateurs.

 Vous pouvez utiliser l’un des rapports suivants pour surveiller les applications conformes et non conformes :  

-   **Liste des applications et des appareils non conformes d'un utilisateur spécifié** : affiche des informations sur les utilisateurs et les appareils sur lesquels sont installées des applications non conformes avec une stratégie que vous avez spécifiée.  

-   **Résumé des utilisateurs ayant des applications non conformes** : affiche des informations sur les utilisateurs qui ont installé des applications non conformes avec une stratégie que vous avez spécifiée.  

 Pour plus d’informations sur la façon d’utiliser les rapports, consultez [Rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="ios-and-mac-os-x-custom-profile-settings"></a>Paramètres du profil personnalisé iOS et Mac OS X  
 Utilisez des **Profils personnalisés iOS et Mac OS X** pour déployer les paramètres que vous avez créés à l’aide de l’ [outil Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) sur des appareils iOS et Mac OS X. Cet outil vous permet de créer plusieurs paramètres qui contrôlent le fonctionnement de ces appareils et de les exporter vers un profil de configuration. Vous pouvez ensuite importer ce profil de configuration dans un profil personnalisé iOS et Mac OS X et déployer les paramètres pour les utilisateurs et les appareils de votre organisation.  

> [!NOTE]  
>  Vérifiez que les paramètres que vous exportez à partir de l’outil Apple Configurator sont compatibles avec la version d’iOS ou de Mac OS X des appareils sur lesquels vous déployez le profil. Pour plus d'informations sur la résolution des paramètres incompatibles, recherchez Configuration Profile Reference et Mobile Device Management Protocol Reference sur le site web [Apple Developer](https://developer.apple.com/) .  

### <a name="to-create-an-ios-and-mac-os-x-custom-profile"></a>Pour créer un profil personnalisé iOS et Mac OS X  

1.  Dans la page **Configurer les paramètres du profil personnalisé iOS et Mac OS X** de l’ **Assistant Création d’élément de configuration**, spécifiez les informations suivantes :  

    -   **Nom du profil de configuration personnalisé (celui présenté aux utilisateurs)** - Entrez le nom de la stratégie tel qu’il sera affiché sur l’appareil et dans les rapports Configuration Manager.  

    -   **Importer** - Choisissez un fichier que vous avez exporté à partir de l’outil Apple Configurator.  

    -   **Détails du profil de configuration** - Affiche le code XML du profil de configuration que vous avez importé.  

    -   **Corriger les paramètres non conformes** -  

         Sélectionnez si vous souhaitez corriger les paramètres de configuration non conformes (quand ils sont pris en charge).  

    -   **Gravité de non-compatibilité pour les rapports** - Spécifiez le niveau de gravité signalé si cette stratégie de conformité est évaluée comme non conforme. Les niveaux de gravité disponibles sont les suivants :  

        > [!NOTE]  
        >  Quand un appareil Mac OS X est en mode veille, il n’est pas possible de remettre ou d’inventorier les stratégies et les profils. La console Configuration Manager peut donc afficher temporairement l’état Paramètres de stratégie erronés jusqu’à ce que l’appareil sorte du mode veille.  

        -   **Aucun** : les appareils qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec pour les rapports Configuration Manager.  

        -   **Informations** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations** pour les rapports Configuration Manager.  

        -   **Avertissement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement** pour les rapports Configuration Manager.  

        -   **Critique** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager.  

        -   **Critique avec événement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager. Ce niveau de gravité est également enregistré comme événement Windows dans le journal des événements des applications.  

## <a name="how-to-create-a-configuration-profile-file"></a>Création d’un fichier de profil de configuration  
 Vous pouvez créer le fichier de profil de configuration utilisé par la stratégie personnalisée de deux manières :  

-   Exportez le fichier (avec l’extension **.mobileconfig**) à partir de l’outil Apple Configurator.  

-   Créez le fichier en utilisant le schéma approprié fourni dans la [référence des clés de profil de configuration](https://developer.apple.com/library/ios/featuredarticles/iPhoneConfigurationProfileRef/Introduction/Introduction.html).  

###  <a name="kiosk-mode-ios"></a>Mode kiosque (iOS)  
 Le mode kiosque vous permet de verrouiller un appareil pour n'autoriser que le fonctionnement de certaines fonctionnalités. Par exemple, vous pouvez autoriser un appareil à exécuter seulement une application gérée que vous spécifiez ou vous pouvez désactiver les boutons de volume sur un appareil. Ces paramètres peuvent être utilisés pour un modèle de démonstration d'un appareil ou pour un appareil dédié à l'exécution d'une seule fonction, par exemple dans un point de vente.  

#### <a name="to-configure-kiosk-mode-for-ios-devices"></a>Pour configurer le mode kiosque pour des appareils iOS  

1.  Dans la page **Configurer les paramètres du mode kiosque pour les appareils iOS** de l' **Assistant Création d'élément de configuration**, spécifiez les informations suivantes :  

    -   **Sélectionner une application** - Sélectionnez l’application qui sera autorisée à s’exécuter quand l’appareil est en mode plein écran. Aucune autre application ne pourra s'exécuter sur l'appareil. Choisissez parmi :  

        -   **Application gérée** : cliquez sur Parcourir, puis sélectionnez une application gérée.  

        -   **Application du Store** : spécifiez l'URL d'une application de l'App Store, puis cliquez sur **Obtenir l'ID de l'application** pour remplir le champ **ID de l'application** .  

         Pour trouver l'URL de l'application :  

        -   À l'aide d'un moteur de recherche, recherchez l'application à utiliser dans l'App Store iTunes, puis ouvrez la page de l'application.  

        -   Copiez l'URL de la page et utilisez-la en tant qu'URL pour spécifier l'application que vous souhaitez exécuter en mode kiosque.  

        -   **Exemple :** recherchez **Microsoft Word pour iPad**. L'URL que vous utilisez sera **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  

    -   **Tactile** - Active ou désactive l’écran tactile sur l’appareil.  

    -   **Rotation écran** - Active ou désactive la modification de l’orientation de l’écran quand vous faites pivoter l’appareil.  

    -   **Boutons de volume** - Active ou désactive l’utilisation des boutons de volume sur l’appareil.  

    -   **Fonction de sonnerie** - Active ou désactive le commutateur de sonnerie (désactivation du son) sur l’appareil.  

    -   **Bouton de mise en veille et en éveil de l’écran** - Active ou désactive le bouton Veille/sortie de veille de l’écran sur l’appareil.  

    -   **Verrouillage automatique** - Active ou désactive le verrouillage automatique de l’appareil.  

    -   **Audio mono** - Active ou désactive le paramètre d’accessibilité **Audio mono**.  

    -   **VoiceOver** - Active ou désactive le paramètre d’accessibilité **VoiceOver** qui lit à haute voix le texte sur l’affichage de l’appareil.  

    -   **Réglages des commentaires audio** - Active ou désactive les réglages VoiceOver qui vous permettent de régler la fonction VoiceOver (par exemple la vitesse de lecture à haute voix du texte à l’écran).  

    -   **Zoom** - Active ou désactive le paramètre d’accessibilité **Zoom** qui vous permet d’utiliser la fonctionnalité tactile pour agrandir l’affichage de l’appareil.  

    -   **Réglage du zoom** - Active ou désactive les réglages du zoom qui vous permettent de régler la fonction de zoom.  

    -   **Inverser les couleurs** - Active ou désactive le paramètre d’accessibilité **Inverser les couleurs** qui ajuste l’affichage pour aider les utilisateurs ayant des troubles visuels.  

    -   **Réglage de l’inversion des couleurs** - Active ou désactive les réglages de couleurs inversées qui vous permettent d’ajuster la fonction de couleurs inversées.  

    -   **Assistance tactile** - Active ou désactive le paramètre d’accessibilité **Assistance tactile** qui aide les utilisateurs à effectuer des gestes à l’écran qui peuvent être difficiles à effectuer.  

    -   **Réglages de l’assistance tactile** - Active ou désactive les réglages d’assistance tactile qui vous permettent de régler la fonction tactile d’assistance.  

    -   **Sélection de la reconnaissance vocale** - Active ou désactive les paramètres d’accessibilité **Sélection Speak** qui peuvent lire à haute voix le texte que vous sélectionnez.  

    -   **Résoudre les paramètres non compatibles** - Sélectionnez si vous souhaitez corriger les paramètres de configuration non conformes (si cela est pris en charge).  

    -   **Gravité de non-compatibilité pour les rapports** - Spécifiez le niveau de gravité signalé (dans les rapports Configuration Manager) si cette stratégie de conformité est évaluée comme non conforme. Les degrés de gravité disponibles sont les suivants :  

        -   **Aucun** : les appareils qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec.  

        -   **Informations** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations**.  

        -   **Avertissement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement**.  

        -   **Critique** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique**.  

        -   **Critique avec événement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique**.  



<!--HONumber=Dec16_HO3-->


