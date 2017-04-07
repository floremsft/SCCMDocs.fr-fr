---
title: "Créer des éléments de configuration pour les appareils Android et Samsung KNOX Standard gérés via Microsoft Intune | Microsoft Docs"
description: "Utilisez l’élément de configuration Android et Samsung KNOX Standard de System Center Configuration Manager pour gérer les paramètres des appareils."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: a8682db0d1def583413e59cf2251a48c6afbdb53
ms.lasthandoff: 03/27/2017


---
# <a name="how-to-create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>Comment créer des éléments de configuration pour des appareils Android et Samsung KNOX gérés sans le client System Center Configuration Manager

Utilisez l’élément de configuration **Android et Samsung KNOX** de System Center Configuration Manager pour gérer les paramètres des appareils Android et Samsung KNOX qui sont inscrits dans Microsoft Intune ou gérés localement par Configuration Manager.  

### <a name="to-create-an-android-and-samsung-knox-configuration-item"></a>Pour créer un élément de configuration Android et Samsung KNOX  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , développez **Paramètres de compatibilité**, puis cliquez sur **Éléments de configuration**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un élément de configuration**.  

4.  Dans la page **Général** de l’ **Assistant Création d’élément de configuration**, spécifiez un nom et une description éventuelle pour l’élément de configuration.  

5.  Sous **Spécifier le type d’élément de configuration que vous voulez créer**, sélectionnez **Android et Samsung KNOX**.  

6.  Cliquez sur **Catégories** si vous créez et attribuez des catégories pour faciliter la recherche et le filtrage des éléments de configuration dans la console Configuration Manager.  

7.  Dans la page **Plateformes prises en charge** de l’Assistant, sélectionnez les plateformes Android ou Samsung KNOX spécifiques chargées d’évaluer l’élément de configuration.  

8.  Dans la page **Paramètres de périphérique** de l’Assistant, sélectionnez le groupe de paramètres à configurer. Consultez [Informations de référence sur les paramètres d’élément de configuration Android et Samsung KNOX](#BKMK_setref) dans cette rubrique pour plus d’informations, puis cliquez sur **Suivant**.  

    > [!TIP]  
    >  Si le paramètre souhaité n’est pas répertorié, cochez la case **Configurer d’autres paramètres qui ne se trouvent pas dans les groupes de paramètres par défaut**.  

9. Dans chaque page de paramètres, configurez les paramètres dont vous avez besoin et indiquez si vous voulez les corriger quand ils ne sont pas conformes sur des périphériques (quand cela est pris en charge).  

10. Pour chaque groupe de paramètres, vous pouvez également configurer la gravité signalée quand un élément de configuration n’est pas conforme :  

    -   **Aucun** : les appareils qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec pour les rapports Configuration Manager.  

    -   **Informations** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations** pour les rapports Configuration Manager.  

    -   **Avertissement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement** pour les rapports Configuration Manager.  

    -   **Critique** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager.  

    -   **Critique avec événement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager. Ce niveau de gravité est également enregistré comme événement Windows dans le journal des événements des applications.  

11. Dans la page **Condition d’application de la plateforme** de l’Assistant, passez en revue tous les paramètres qui ne sont pas compatibles avec les plateformes prises en charge que vous avez sélectionnées précédemment. Vous pouvez revenir sur ces paramètres et les supprimer, ou vous pouvez continuer.  

    > [!TIP]  
    >  La conformité des paramètres non pris en charge n’est pas évaluée.  

12. Effectuez toutes les étapes de l'Assistant.  

 Vous pouvez afficher le nouvel élément de configuration dans le nœud **Éléments de configuration** de l’espace de travail **Ressources et Conformité** .  

##  <a name="android-and-samsung-knox-configuration-item-settings-reference"></a>Informations de référence sur les paramètres d’élément de configuration Android et Samsung KNOX  

### <a name="password"></a>Mot de passe  
 Ces paramètres s’appliquent aux périphériques Android et Samsung KNOX.  

|Paramètre|Détails|  
|-------------|-------------|  
|**Exiger des paramètres de mot de passe sur les appareils**|Exigez un mot de passe sur les appareils pris en charge.|  
|**Longueur minimale du mot de passe (caractères)**|Longueur minimale du mot de passe.|  
|**Expiration du mot de passe en jours**|Nombre de jours avant qu'un mot de passe ne doive être modifié.|  
|**Nombre de mots de passe mémorisés**|Empêche la réutilisation des mots de passe déjà utilisés.|  
|**Nombre d'échecs de tentative de connexion avant que l'appareil soit réinitialisé**|Réinitialise l'appareil si le nombre d'échecs de tentative de est atteint.|  
|**Durée d’inactivité avant le verrouillage de l’appareil**|Sélectionnez le laps de temps au bout duquel l’appareil est verrouillé en cas de non-utilisation.|
|**Qualité du mot de passe**|Sélectionnez le niveau de complexité du mot de passe requis et spécifiez si les appareils biométriques peuvent être utilisés.|  
|**Autoriser Smart Lock et d’autres agents de confiance**|Vous permet de contrôler la fonctionnalité Smart Lock sur les appareils Android compatibles. Cette fonctionnalité du téléphone, parfois appelée agents de confiance, vous permet de désactiver ou de contourner le mot de passe de l’écran de verrouillage de l’appareil si celui-ci se trouve dans un emplacement approuvé, comme quand il est connecté à un appareil Bluetooth spécifique, ou quand il se trouve à proximité d’une balise NFC. Vous pouvez utiliser ce paramètre pour empêcher les utilisateurs finaux de configurer Smart Lock.|
|**Empreinte digitale pour le déverrouillage (KNOX 5.0+)**|Autorise l’utilisation d’une empreinte digitale pour déverrouiller les appareils compatibles.|

###  <a name="device"></a>Appareil   

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Numérotation vocale**|Active ou désactive la fonctionnalité de numérotation vocale sur l’appareil.|
|**Assistant vocal**|Autorise l’utilisation du logiciel Assistant vocal sur l’appareil.|
|**Capture d'écran**|Permet à l’utilisateur de capturer le contenu de l’écran en tant qu’image.|
|**Envoi des données de diagnostic**|Autorise l’appareil à envoyer des informations de diagnostic à Google.|
|**Géolocalisation**|Autorise l’appareil à utiliser les informations d’emplacement.|
|**Copier et coller**|Autorise les fonctions Copier et Coller sur l’appareil.|
|**Réinitialisation aux paramètres d’usine**|Autorisez l'utilisateur à rétablir les paramètres d'usine sur l'appareil.|  |
|**Partage du Presse-papiers entre les applications**|Utilisez le Presse-papiers pour copier-coller entre les applications.|  |
|**BlueTooth**|Autorise l’utilisation de la fonction Bluetooth sur l’appareil.|

### <a name="store"></a>Magasin
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Boutique d'applications**|Autorise l’utilisateur à accéder à Google Play Store sur l’appareil.|

### <a name="browser"></a>Navigateur
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Autoriser le navigateur web**|Spécifie si le navigateur web par défaut de l’appareil peut être utilisé.|
|**Remplissage automatique**|Autorise l’utilisation de la fonction de remplissage automatique du navigateur web.|
|**Active scripting**|Autorise le navigateur web de l’appareil à utiliser Active Scripting.|
|**Bloqueur de fenêtres publicitaires**|Autorise l’utilisation du bloqueur de fenêtres publicitaires dans le navigateur web.|
|**Cookies**|Autorise le navigateur web de l’appareil à utiliser des cookies.|

### <a name="cloud"></a>Cloud  

|Paramètre|Détails|  
|-------------|-------------|  
|**Sauvegarde Google**|Autorise l’utilisation de la sauvegarde de Google.|  
|**Synchronisation automatique de compte Google**|Autorise la synchronisation automatique des paramètres du compte Google.|  

### <a name="security"></a>Sécurité  

|Paramètre|Détails|  
|-------------|-------------|  
|**Messagerie SMS et MMS**|Autorise l’utilisation des messages SMS et MMS sur l’appareil.|
|**Stockage amovible**|Autorise l’appareil à utiliser du stockage amovible, comme une carte SD.|
|**Appareil photo**|Autorise l’utilisation de l’appareil photo de l’appareil.<br /><br /> S’applique aux périphériques Android et Samsung KNOX.|
|**Communication en champ proche (NFC)**|Autorise les opérations qui utilisent la communication en champ proche si l’appareil la prend en charge.|
|**YouTube**|Autorise l'utilisation de l'application YouTube sur l'appareil.<br /><br /> S’applique uniquement aux périphériques Samsung KNOX.|  
|**Mise hors tension**|Autorise la mise hors tension de l'appareil.<br /><br /> S’applique uniquement aux périphériques Samsung KNOX.|  

### <a name="roaming"></a>Itinérant

|Paramètre|Détails|  
|-------------|-------------|  
|Itinérance vocale|Autorise l’itinérance vocale quand l’appareil se trouve sur un réseau cellulaire.|
|Itinérance des données|Autorise l’itinérance de données quand l’appareil se trouve sur un réseau cellulaire.|


### <a name="encryption"></a>Chiffrement  
 Ces paramètres s’appliquent aux périphériques Android et Samsung KNOX.  

|Paramètre|Détails|  
|-------------|-------------|  
|**Chiffrement de la carte de stockage**|Requiert le chiffrement de la carte de stockage de l’appareil.|
|**Chiffrement des fichiers sur l’appareil**|Requiert que les fichiers de l'appareil mobile soient chiffrés.|  

### <a name="wireless-communications"></a>Communications sans fil

|Paramètre|Détails|  
|-------------|-------------|  
|**Connexion réseau sans fil**|Autorise l’utilisation des fonctionnalités Wi-Fi de l’appareil.|
|**Connexion Wi-Fi**|Autorise l’utilisation de la connexion Wi-Fi sur l’appareil.|


###  <a name="compliant-and-noncompliant-apps-android"></a>Applications conformes et non conformes (Android)  
 Permet de spécifier une liste d'applications Android conformes ou non conformes dans votre entreprise. Vous pouvez ensuite utiliser des rapports pour afficher les appareils sur lesquels sont installées des applications non conformes et l'utilisateur associé.  

 Vous ne pouvez pas spécifier à la fois les applications conformes et non conformes dans le même élément de configuration.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Pour spécifier la liste des applications conformes ou non conformes  

Dans la page **Applications conformes et non conformes (Android)** , spécifiez les informations suivantes :  

|Paramètre|Plus d'informations|  
|-------------|----------------------|  
|**Liste des applications non conformes**|Sélectionnez cette option si vous souhaitez spécifier une liste d'applications qui seront signalées comme non conformes si elles sont installées par les utilisateurs.|  
|**Liste des applications conformes**|Sélectionnez cette option si vous souhaitez spécifier une liste d'applications que les utilisateurs sont autorisés à installer. Toutes les autres applications installées sont signalées comme non conformes.|  
|**Ajouter**|Ajoute une application à la liste sélectionnée. Spécifiez un nom de votre choix, éventuellement l'éditeur de l'application, et l'URL de l'application dans le magasin d'applications.<br /><br /> Pour spécifier l'URL, dans la [section Applications de Google Play](https://play.google.com/store/apps), recherchez l'application à utiliser.<br /><br /> Ouvrez la page de l'application, puis copiez l'URL dans le Presse-papiers. Vous pouvez maintenant utiliser cette URL dans la liste des applications conformes ou non conformes.<br /><br /> **Exemple :** recherchez Google Play pour **Microsoft Office Mobile**. L'URL que vous utilisez sera **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**.|  
|**Éditer**|Vous permet de modifier le nom, l'éditeur et l'URL de l'application sélectionnée.|  
|**Supprimer**|Supprime l'application sélectionnée dans la liste.|  
|**Importerer**|Importe une liste d'applications que vous avez spécifiée dans un fichier de valeurs séparées par des virgules. Utilisez le format Nom de l'application, Éditeur, URL de l'application dans le fichier.|  

## <a name="android-for-work-configuration-items"></a>Éléments de configuration Android for Work
Android for Work a deux groupes de paramètres pour les éléments de configuration :
-    Mot de passe : identique aux paramètres d’Android « classique »
- Profil de travail : active les paramètres Android for Work suivants :
  -    Autoriser le partage de données entre les profils personnels et professionnels
  - Masquer les notifications de profil professionnel lorsque l’appareil est verrouillé (Android 6.0+)
  -    Configurer la stratégie d’autorisation d’application par défaut (Android 6.0+)

Pour créer un élément de configuration dans le profil professionnel Android, choisissez **Android for Work** dans la page **Général** et configurez les paramètres pour chacun des groupes de paramètres, en ajoutant l’élément de configuration à une base de référence et en procédant au déploiement normalement. Ces paramètres s’appliqueront uniquement aux appareils inscrits comme Android for Work, et pas à ceux inscrits comme Android.

### <a name="kiosk-mode-samsung-knox-only"></a>Mode plein écran (Samsung KNOX uniquement)  
 Le mode plein écran vous permet de verrouiller un appareil pour n'autoriser que le fonctionnement de certaines fonctionnalités. Par exemple, vous pouvez autoriser un appareil à exécuter seulement une application gérée que vous spécifiez ou vous pouvez désactiver les boutons de volume sur un appareil. Ces paramètres peuvent être utilisés pour un modèle de démonstration d'un appareil ou pour un appareil dédié à l'exécution d'une seule fonction, par exemple dans un point de vente.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>Pour configurer le mode plein écran pour un appareil Samsung KNOX  

1.  Dans la page **Configurer les paramètres du mode plein écran pour les appareils Samsung KNOX** de l’**Assistant Création d’élément de configuration**, spécifiez les informations suivantes :  

|Paramètre|Plus d'informations|  
|-------------|----------------------|  
|**Sélectionner l’application**|Cliquez sur **Parcourir** pour sélectionner une application Android Configuration Manager (avec l’extension **.apk**) autorisée à s’exécuter quand l’appareil est en mode plein écran. Aucune autre application ne pourra s'exécuter sur l'appareil.|  
|**Boutons du volume**|Active ou désactive l'utilisation des boutons de volume sur l'appareil.|  
|**Bouton Veille et sortie de veille de l'écran**|Active ou désactive le bouton Veille/sortie de veille de l'écran sur l'appareil.|  



2.  Lorsque vous avez terminé, cliquez sur **Suivant**.  

 Vous pouvez utiliser l’un des rapports suivants pour surveiller les applications conformes et non conformes :  

-   **Liste des applications et des appareils non conformes d'un utilisateur spécifié** : affiche des informations sur les utilisateurs et les appareils sur lesquels sont installées des applications non conformes avec une stratégie que vous avez spécifiée.  

-   **Résumé des utilisateurs ayant des applications non conformes** : affiche des informations sur les utilisateurs qui ont installé des applications non conformes avec une stratégie que vous avez spécifiée.  

 Pour plus d’informations sur la façon d’utiliser les rapports, consultez [Rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="see-also"></a>Voir aussi  
 [Éléments de configuration pour les appareils gérés sans le client System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)

