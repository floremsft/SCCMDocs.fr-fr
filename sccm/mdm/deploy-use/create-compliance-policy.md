---
title: "Créer et déployer une stratégie de conformité d’appareil | Microsoft Docs"
description: "Apprenez à créer et déployer des stratégie de conformité d’appareil dans System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 6832bb6c6a26be76720938154942a5eb99022785
ms.lasthandoff: 03/27/2017

---

# <a name="create-and-deploy-a-device-compliance-policy"></a>Créer et déployer une stratégie de conformité d’appareil

*S’applique à : System Center Configuration Manager (Current Branch)*


## <a name="create-a-compliance-policy"></a>Créer une stratégie de conformité

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.

2.  Dans l'espace de travail **Ressources et Conformité** , développez **Paramètres de compatibilité**, puis cliquez sur **Stratégies de conformité**.

3. Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une stratégie de conformité**.

4. Dans la page **Général** de l' **Assistant Création d'élément de configuration**, spécifiez les informations suivantes :

  * **Nom** : attribuez un nom unique à la stratégie de conformité. Vous pouvez utiliser jusqu'à 256 caractères.
  * **Description** : entrez une description qui donne un aperçu du profil VPN et permette son identification dans la console Configuration Manager. Vous pouvez utiliser jusqu'à 256 caractères.
  * **Type de stratégie de conformité** : sélectionnez le type de stratégie à créer selon que l’appareil est géré ou non par Configuration Manager. **Cela s’applique à la version ou à une version ultérieure**.<br /><br /> Pour les appareils gérés par Intune, optez pour les **règles de conformité applicables aux appareils gérés sans client Configuration Manager** .  Cette option vous permet également de sélectionner le type de plateforme auquel appliquer cette stratégie.
  * **Gravité de non-compatibilité pour les rapports** : spécifiez le niveau de gravité signalé si cette stratégie de conformité est évaluée comme étant non conforme. Les niveaux de gravité disponibles sont les suivants :<br /><br />
    * **Aucun** : les appareils qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec pour les rapports Configuration Manager.
    *  **Informations** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations** pour les rapports Configuration Manager.   
    * **Avertissement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement** pour les rapports Configuration Manager.
    * **Critique** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager.
    * **Critique avec événement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager. Ce niveau de gravité est aussi enregistré comme événement Windows dans le journal des événements des applications.|      

5.  Dans la page **Plateformes prises en charge** , choisissez les plateformes d'appareils qui seront évaluées par cette stratégie de conformité, ou cliquez sur **Sélectionner tout** pour choisir toutes les plateformes d'appareils. Les plateformes prises en charge sont les suivantes : Windows 7, 8.1, 10, Windows Server 2008 R2, 2012, 2012 R2 et 2016.

6.  Dans la page **Règles** , vous définissez une ou plusieurs règles qui définissent la configuration dont les appareils doivent disposer pour être évalués comme étant conformes. Quand vous créez une stratégie de conformité, certaines règles sont activées par défaut, mais vous pouvez les modifier ou les supprimer. Pour obtenir la liste complète de toutes les règles, consultez la section **Règles de stratégie de conformité** plus loin dans cette rubrique.

> [!NOTE]  
>  Sur les PC Windows, la version du système d’exploitation Windows 8.1 apparaît comme étant la version 6.3 au lieu de 8.1.    Si la règle de la version du système d’exploitation est définie sur Windows 8.1 pour Windows, l’appareil sera signalé comme non conforme, même si l’appareil a le système d’exploitation Windows 8.1. Assurez-vous que vous définissez la version **signalée** correcte de Windows pour les règles de version minimale et maximale du système d’exploitation. Le numéro de version doit correspondre à la version retournée par la commande winver. Les téléphones Windows Phone n’ont pas ce problème, car la version signalée est 8.1 comme prévu. Pour les PC Windows avec le système d’exploitation Windows 10, la version doit être définie comme étant « 10.0 » + le numéro de version du système d’exploitation renvoyé par la commande **winver**.

7.  Dans la page **Résumé** de l'Assistant, passez en revue les paramètres que vous avez définis, puis fermez l'Assistant.

 La nouvelle stratégie s'affiche sous le nœud **Stratégies de conformité** de l'espace de travail **Ressources et Conformité** .

## <a name="deploy-a-compliance-policy"></a>Déployer une stratégie de conformité

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.

2.  Dans l'espace de travail **Ressources et Conformité** , développez **Paramètres de compatibilité**, puis cliquez sur **Stratégies de conformité**.

3.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.

4.  Dans la boîte de dialogue **Déployer une stratégie de conformité** , cliquez sur **Parcourir** pour sélectionner le regroupement d'utilisateurs pour lesquels déployer la stratégie.

     En outre, vous pouvez sélectionner des options pour générer des alertes quand la stratégie n'est pas conforme et configurer le calendrier selon lequel cette stratégie sera évaluée pour la conformité.

5.  Une fois terminé, cliquez sur **OK**.

## <a name="monitor-the-compliance-policy"></a>Analyser la stratégie de conformité

### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Pour afficher les résultats de compatibilité dans la console Configuration Manager

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.

2.  Dans l'espace de travail **Surveillance** , cliquez sur **Déploiements**.

3.  Dans la liste **Déploiements** , sélectionnez le déploiement de la stratégie de conformité dont vous souhaitez vérifier les informations de conformité.

4.  Vous pouvez consulter un résumé des informations relatives à la conformité du déploiement de la stratégie dans la page principale. Pour afficher des informations plus détaillées, sélectionnez le déploiement, puis, sous l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Afficher l'état** pour ouvrir la page **État du déploiement** .

     La page **État du déploiement** contient les onglets suivants :

    -   **Conforme**: affiche la conformité de la stratégie en fonction du nombre de ressources affectées. Vous pouvez cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** ou **Périphériques** de l'espace de travail **Ressources et Conformité** , qui contient tous les utilisateurs ou appareils conformes à cette règle. Le volet **Détails du bien** affiche les utilisateurs ou les appareils conformes à la ligne de base de configuration. Double-cliquez sur un utilisateur ou un appareil de la liste pour afficher des informations supplémentaires.

    -   **Erreur**: affiche une liste de toutes les erreurs pour le déploiement de stratégie sélectionné en fonction du nombre de ressources affectées. Vous pouvez cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** ou **Périphériques** de l'espace de travail **Biens et conformité** , qui contient tous les utilisateurs ou appareils qui ont généré des erreurs avec cette règle. Lorsque vous sélectionnez un utilisateur ou un appareil, le volet **Détails du bien** affiche les utilisateurs ou les appareils qui sont affectés par le problème sélectionné. Double-cliquez sur un utilisateur ou un appareil de la liste pour afficher des informations supplémentaires sur le problème.

    -   **Non conforme**: affiche une liste de toutes les règles non conformes au sein de la stratégie en fonction du nombre de ressources affectées. Vous pouvez cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** ou **Périphériques** de l'espace de travail **Biens et conformité** , qui contient tous les utilisateurs ou appareils qui ne sont pas compatibles avec cette règle. Lorsque vous sélectionnez un utilisateur ou un appareil, le volet **Détails du bien** affiche les utilisateurs ou les appareils qui sont affectés par le problème sélectionné. Double-cliquez sur un utilisateur ou un appareil de la liste pour afficher d'autres informations sur le problème.

    -   **Inconnu**: affiche une liste de tous les utilisateurs et appareils qui n’ont pas signalé leur conformité pour le déploiement de stratégie sélectionné, ainsi que l’état du client actuel des appareils.

### <a name="to-monitor-the-individual-compliance-status"></a>Pour surveiller l’état de conformité individuel

Vous pouvez également afficher l’état de chaque appareil :

1.  Dans la console Configuration Manager, cliquez sur l’espace de travail **Actifs et conformité**.

2.  Cliquez sur **Appareils**.
3.  Cliquez avec le bouton droit sur une des colonnes pour en ajouter d’autres.

Vous pouvez ajouter les colonnes suivantes :

- **ID de l’appareil Azure Active Directory :** identificateur unique de l’appareil dans AAD.

- **Détails de l’erreur de conformité :** détails du message d’erreur en cas de problème avec le processus de bout en bout. Si cette colonne est vide, cela signifie qu’aucune erreur n’a été trouvée et que l’état de conformité a été correctement signalé.

- **Emplacement de l’erreur de conformité :** fournit des informations détaillées sur l’emplacement où la conformité a échoué. Si cette colonne est vide, cela signifie qu’aucune erreur n’a été trouvée et que l’état de conformité a été correctement signalé. Exemples d’emplacements où le processus de conformité est susceptible d’échouer : 
    - Client ConfigMgr
    - Point de gestion
    - Intune
    - Azure Active Directory
<br></br>
- **Heure d’évaluation de la conformité :** heure de la dernière vérification de la conformité.

- **Heure définie de la conformité :** dernière fois où la conformité a été mise à jour vers Azure Active Directory.

- **Conforme à l’accès conditionnel :** indique si l’ordinateur est conforme ou non aux stratégies d’accès conditionnel.

> [!IMPORTANT]
> Par défaut, ces colonnes ne sont pas affichées.

### <a name="to-view-intune-compliance-policies-charts"></a>Pour afficher les graphiques de stratégies de conformité Intune
1. À compter de la version 1610 de Configuration Manager, dans la console Configuration Manager, cliquez sur **Analyse**.
2. Dans l’espace de travail **Analyse**, accédez à **Vue d’ensemble** > **Paramètres de compatibilité** >  **Stratégies de conformité**.
3. Les graphiques suivants s’affichent :
    - **Conformité globale des appareils** : affiche la conformité globale des appareils pour toutes les stratégies de conformité.
    - **Raisons principales de non-conformité** : affiche les principales stratégies non respectées par les appareils.
4. Cliquez sur une section dans l’un des deux graphiques pour afficher la liste des appareils dans cette catégorie.

### <a name="to-view-a-health-attestation-report"></a>Pour afficher un rapport d’attestation d’intégrité

1.  **À compter de la version 1602 de Configuration Manager**, dans la console Configuration Manager, cliquez sur **Analyse**.

2.  Pour afficher un rapport de synthèse sur l’état de conformité actuel des appareils, cliquez sur **Sécurité**. Cliquez ensuite sur **Attestation d’intégrité**.

3.  Pour afficher un rapport qui répertorie tous les appareils et tous les attributs d’attestation d’intégrité, cliquez sur **Sécurité**. Cliquez ensuite sur **Attestation d’intégrité**.

## <a name="compliance-policy-rules"></a>Règles de stratégie de conformité
* **Exiger des paramètres de mot de passe sur les appareils mobiles** : exigez de la part des utilisateurs qu’ils entrent un mot de passe pour pouvoir accéder à leur appareil.

  **Pris en charge sur :**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
* **Demander un mot de passe pour déverrouiller un appareil inactif (mise à jour 1602)** : exigez de la part des utilisateurs qu’ils entrent un mot de passe pour accéder à un appareil verrouillé.

  **Pris en charge sur :**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minutes d’inactivité avant qu’un mot de passe soit demandé (mise à jour 1602)** : indique la durée d’inactivité avant que l’utilisateur soit contraint d’entrer à nouveau son mot de passe. Choisissez l’une des valeurs suivantes : **1 minute**, **5 minutes**, **15 minutes**, **30 minutes**, **1 heure**.

  Cette règle doit être utilisée avec l’option **Exiger un mot de passe pour déverrouiller un appareil inactif**. La valeur définie ici détermine à quel moment l’appareil est considéré comme inactif et verrouillé, et à quel moment l’option  **Exiger un mot de passe pour déverrouiller un appareil inactif** est définie sur **True**et exige donc que l’utilisateur entre un mot de passe pour accéder à l’appareil verrouillé.

  **Pris en charge sur :**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Exiger les mises à jour automatiques (mise à jour 1602)** : vous pouvez imposer une installation automatique des mises à jour sur les appareils équipés de Windows 8.1 ou d’une version ultérieure et spécifier la classe des mises à jour.

  La valeur doit être définie sur **Aucun** pour empêcher l’installation automatique, sur **Recommandé** pour installer automatiquement tous les mises à jour recommandées, ou sur **Important** pour installer uniquement les mises à jour classées comme importantes.

  **Pris en charge sur :**
  * Windows Phone 8+

* **Autoriser les mots de passe simples** : permet aux utilisateurs de créer des mots de passe simples, comme « 1234 » ou « 1111 ». Ce paramètre est **désactivé par défaut**.

  **Pris en charge sur :**
  * Windows Phone 8+
  * iOS 6+

* **Longueur minimale du mot de passe** : spécifie le nombre minimal de chiffres ou de caractères que le mot de passe de l’utilisateur doit contenir (**6** par défaut).

  **Pris en charge sur :**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  >[!NOTE]
  >Pour les appareils qui exécutent Windows et qui sont sécurisés avec un compte Microsoft, la stratégie de conformité n’est pas évaluée correctement si l’option **Longueur minimale du mot de passe** a une valeur supérieure à 8 caractères ou si l’option **Nombre minimum de jeux de caractères** a une valeur supérieure à 2.

* **Chiffrement des fichiers sur le périphérique mobile** : impose le chiffrement de l’appareil pour la connexion aux ressources. Les appareils qui exécutent **Windows Phone 8** sont **chiffrés automatiquement**. Les appareils qui exécutent **iOS** sont chiffrés quand vous configurez le paramètre **Exiger des paramètres de mot de passe sur les appareils mobiles** (activé par défaut).

  **Pris en charge sur :**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **L’appareil ne doit pas être jailbroken ou rooté** : si cette option est activé, les appareils jailbroken (iOS) ou rootés (Android) ne sont pas conformes (désactivé par défaut).

  **Pris en charge sur :**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Le profil de messagerie doit être géré par Intune** : quand cette option est définie sur Oui, l’appareil doit utiliser le profil de messagerie déployé sur l’appareil. L’appareil est considéré comme non conforme si le profil d’e-mail n’est pas déployé sur le groupe d’utilisateurs ciblé par la stratégie de conformité.

  De même, l’appareil n’est pas conforme si l’utilisateur a déjà configuré sur l’appareil un compte e-mail qui correspond au profil d’e-mail Intune déployé sur l’appareil. Dans ce cas, Intune ne peut pas remplacer le profil configuré par l’utilisateur et ne peut donc pas le gérer. L’utilisateur peut mettre l’appareil en conformité en supprimant les paramètres d’e-mail existants, ce qui permet à Intune d’installer le profil d’e-mail géré.

  Pour plus d'informations sur les profils de messagerie, consultez [Activer l'accès à la messagerie professionnelle à l'aide de profils de messagerie avec Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Ce paramètre est désactivé par défaut.

  **Pris en charge sur :**
  * iOS 6+

* **Profil de messagerie** : si l’option **Le compte de messagerie doit être géré par Intune** est sélectionnée, cliquez sur **Sélectionner** pour choisir le profil de messagerie que doit gérer les appareils. Le profil de messagerie doit être présent sur l'appareil.

  **Pris en charge sur :**
  * iOS 6+

* **Système d’exploitation minimal requis** : quand un appareil ne satisfait pas à la condition de version minimale du système d’exploitation, il est signalé comme étant non conforme. Un lien avec des informations sur la mise à niveau s’affiche. L’utilisateur final peut choisir de mettre à niveau son appareil. Une fois cette opération effectuée, il peut accéder aux ressources de l’entreprise.

  **Pris en charge sur :**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Version maximale autorisée du système d’exploitation** : quand un appareil utilise une version du système d’exploitation ultérieure à celle spécifiée dans la règle, l’accès aux ressources de l’entreprise est bloqué et l’utilisateur est invité à contacter son administrateur. Jusqu’à ce qu’il y ait une modification de la règle pour autoriser la version du système d’exploitation, cet appareil ne peut pas être utilisé pour accéder aux ressources de l’entreprise.

  **Pris en charge sur :**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Exiger que les appareils soient signalés sains (mise à jour 1602)** : vous pouvez définir une règle exigeant que les appareils Windows 10 soient signalés comme intègres dans les stratégies de conformité nouvelles ou existantes. Si ce paramètre est activé, les appareils Windows 10 sont évalués via le service d’attestation de l’intégrité (HAS, Health Attestation Service) pour les points de données suivants :
 - **BitLocker est activé** : quand Bitlocker est activé, l’appareil peut protéger les données stockées sur le lecteur contre tout accès non autorisé, en cas de mise hors tension ou de mise en veille prolongée du système.

   Le chiffrement de lecteur BitLocker Windows chiffre toutes les données stockées sur le volume hébergeant le système d’exploitation Windows. BitLocker utilise le Module de plateforme sécurisée (TPM) pour protéger le système d’exploitation Windows et les données utilisateur. Il contribue également à prévenir toute falsification d’un ordinateur, même si celui-ci est laissé sans assistance, perdu ou volé.<br />Si l’ordinateur est équipé d’un TPM compatible, BitLocker utilise celui-ci pour verrouiller les clés de chiffrement qui protègent les données. Par conséquent, les clés sont inaccessibles tant que le TPM n’a pas vérifié l’état de l’ordinateur.
  - **L’intégrité du code est activée** : l’intégrité du code est une fonctionnalité qui valide l’intégrité d’un pilote ou d’un fichier système chaque fois qu’il est chargé en mémoire. L’intégrité du code détecte si un pilote ou un fichier système non signés sont chargés dans le noyau, ou si un fichier système a été modifié par un logiciel malveillant exécuté par un compte d’utilisateur disposant de privilèges d’administrateur.
  - **Le démarrage sécurité est activé** : quand le démarrage sécurisé est activé, le système est contraint de démarrer dans un état approuvé par défaut. En outre, lorsque le démarrage sécurisé est activé, les composants principaux utilisés pour démarrer la machine doivent avoir des signatures de chiffrement appropriées, approuvées par le fabricant de l’appareil. Le microprogramme UEFI vérifie cela avant de laisser la machine démarrer. Si des fichiers ont été falsifiés, avec pour effet d’annuler leur signature, le système ne démarre pas.
  - **Logiciel anti-programme malveillant à lancement anticipé (ce paramètre concerne uniquement les PC)** : le logiciel anti-programme malveillant à lancement anticipé assure la protection des ordinateurs de votre réseau au démarrage et avant l’initialisation de pilotes tiers.<br />Cette règle est désactivée par défaut.

  Pour plus d’informations sur le fonctionnement du service HAS, consultez [Health Attestation CSP](https://msdn.microsoft.com/library/dn934876.aspx)(Fournisseur de services de configuration pour l’attestation de l’intégrité).
  **Pris en charge sur :**
  * Windows 10 et Windows 10 Mobile

- **Applications qui ne peuvent pas être installées sur l’appareil :** si les utilisateurs installent une application à partir de la liste des applications non conformes de l’administrateur, ils seront bloqués lorsqu’ils tenteront d’accéder à la messagerie de l’entreprise et à d’autres ressources de l’entreprise qui prennent en charge l’accès conditionnel. Cette règle requiert le nom de l’application et l’ID de l’application lors de l’ajout d’une application à la liste des applications non conformes définies par l’administrateur. L’éditeur de l’application peut également être ajouté, mais ce n’est pas obligatoire.
    - **Pris en charge sur :**
      * iOS 6+
      * Android 4.0+
      * Samsung KNOX Standard 4.0+

#### <a name="whats-app-id"></a>Qu’est-ce que l’ID de l’application ?

L’ID de l’application est un identificateur qui identifie de façon unique l’application dans les services d’application Apple et Google. Par exemple, com.contoso.myapp.

#### <a name="find-app-ids"></a>Trouver les ID d’applications

- **Android**
    - Vous trouverez l’ID de l’application dans l’URL Google Play Store utilisée pour créer l’application :
        - Exemple d’ID de l’application : ***…?id=com.companyname.appname&hl=en***

- **iOS**
    - Dans l’URL iTunes Store, recherchez le **numéro d’ID**, par exemple : ***/id875948587?mt=8***.
    - Dans un navigateur web, accédez à l’URL suivante, en remplaçant le nombre par le numéro d’ID trouvé : 
        - https://itunes.apple.com/lookup?id=875948587
    - Téléchargez et ouvrez le fichier texte.
    - Recherchez le texte « *bundleid* ».
    - Exemple d’ID de l’application : « *bundleId*":"*com.companyname.appname* » 


