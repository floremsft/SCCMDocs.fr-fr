---
title: "Guide pratique pour créer des éléments de configuration pour les appareils Windows Phone gérés sans le client System Center Configuration Manager | System Center Configuration Manager"
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fae7f9e0-d5e7-422f-a6ed-6f6d73f6a617
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: b558c137668b7319c2b9f43f6084fa367b54cd1e


---
# <a name="how-to-create-configuration-items-for-windows-phone-devices-managed-without-the-system-center-configuration-manager-client"></a>Comment créer des éléments de configuration pour des appareils Windows Phone gérés sans le client System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’élément de configuration System Center Configuration Manager **Windows Phone** pour gérer les paramètres des appareils Windows Phone qui sont inscrits dans Microsoft Intune ou gérés localement par Configuration Manager.  

## <a name="create-a-windows-phone-configuration-item"></a>Créer un élément de configuration Windows Phone  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Éléments de configuration**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un élément de configuration**.  

4.  Dans la page **Général** page de l’ **Assistant Création d’élément de configuration**, spécifiez un nom et une éventuelle description pour l’élément de configuration.  

5.  Sous **Spécifier le type d’élément de configuration que vous voulez créer**, sélectionnez **Windows Phone**.  

6.  Cliquez sur **Catégories** si vous créez et attribuez des catégories pour faciliter la recherche et le filtrage des éléments de configuration dans la console Configuration Manager.  

7.  Dans la page **Plateformes prises en charge**, sélectionnez les plateformes Windows Phone spécifiques chargées d’évaluer l’élément de configuration.  

8.  Dans la page **Paramètres de l’appareil**, sélectionnez le groupe de paramètres à configurer. Pour plus d’informations, consultez [Informations de référence sur les paramètres d’élément de configuration Windows Phone](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client#windows-phone-configuration-item-settings-reference) dans cette rubrique, puis cliquez sur **Suivant**.  

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

 Vous pouvez afficher le nouvel élément de configuration dans le nœud **Éléments de configuration** de l’espace de travail **Ressources et conformité** .  

##  <a name="windows-phone-configuration-item-settings-reference"></a>Informations de référence sur les paramètres d’élément de configuration Windows Phone  

### <a name="password"></a>Mot de passe  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  

|Paramètre|Détails|  
|-------------|-------------|  
|**Exiger des paramètres de mot de passe sur les appareils**|Exigez un mot de passe sur les appareils pris en charge.|  
|**Longueur minimale du mot de passe (caractères)**|Longueur minimale du mot de passe.|  
|**Expiration du mot de passe en jours**|Nombre de jours avant qu'un mot de passe ne doive être modifié.|  
|**Nombre de mots de passe mémorisés**|Empêche la réutilisation des mots de passe déjà utilisés.|  
|**Nombre d'échecs de tentative de connexion avant que l'appareil soit réinitialisé**|Réinitialise l'appareil si le nombre d'échecs de tentative de est atteint.|
|**Durée d’inactivité avant le verrouillage de l’appareil**|Spécifie la durée pendant laquelle un appareil doit rester inactif avant le verrouillage automatique de l’écran.|  
|**Complexité du mot de passe**|Choisissez si vous pouvez spécifier un code confidentiel tel que « 1234 » ou si vous devez fournir un mot de passe fort.|
|**Autoriser les mots de passe simples**|Spécifie que des mots de passe simples comme « 0000 » et « 1234 » peuvent être utilisés.|
|**Envoyer le code PIN de récupération du mot de passe au serveur Exchange Server**|-|  

### <a name="device"></a>Appareil  

|Paramètre|Détails|  
|-------------|-------------|  
|**Capture d'écran**|Autorisez l’utilisateur à prendre une capture d’écran de l’affichage de l’appareil.<br /><br /> (Windows Phone 8.1 uniquement)|  
|**Envoi des données de diagnostic**|Autorisez l'envoi des journaux d'application.|  
|**Géolocalisation**|Autorisez l'appareil à utiliser les informations des services d'emplacement.<br /><br /> (Windows Phone 8.1 uniquement)|  
|**Copier et coller**|Utilisez le copier-coller pour transférer des données entre les applications.<br /><br /> (Windows Phone 8.1 uniquement)|  
|**BlueTooth**|Autorisez l’utilisation de la fonctionnalité Bluetooth de l’appareil.|  

### <a name="email-management"></a>Gestion de la messagerie  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  

|Paramètre|Détails|  
|-------------|-------------|  
|**Messagerie POP et IMAP**|Autorise la connexion à des comptes de messagerie qui utilisent les normes POP et IMAP.|  
|**Durée de conservation maximum des courriers électroniques**|Durée de conservation des courriers électroniques avant qu'ils ne soient supprimés du serveur.|  
|**Formats de message autorisés**|Spécifiez si les courriers électroniques des utilisateurs peuvent être au format HTML ou au format texte brut uniquement.|  
|**Taille maximale des messages en texte brut (téléchargés automatiquement)**|Contrôle la taille maximale des courriers électroniques en texte brut lorsqu'ils sont automatiquement téléchargés.|  
|**Taille maximale des messages HTML (téléchargés automatiquement)**|Contrôle la taille maximale des courriers électroniques HTML lorsqu'ils sont automatiquement téléchargés.|  
|**Taille maximum d'une pièce jointe (téléchargée automatiquement)**|Configure la taille maximale des courriers électroniques qui seront téléchargés automatiquement.|  
|**Synchronisation du calendrier**|Permet aux utilisateurs de synchroniser les rendez-vous du calendrier en plus des e-mails.|  
|**Compte de messagerie personnalisé**|Autorisez l'utilisation d'un compte non Microsoft sur l'appareil.|  
|**Rendre le compte Microsoft facultatif dans l'application Windows Mail**|-|  

### <a name="store"></a>Magasin  
 Ces paramètres s’appliquent aux appareils Windows Phone 8.1 uniquement.  

|Paramètre|Détails|  
|-------------|-------------|  
|**Boutique d'applications**|Permet d'accéder à l'App Store sur l'appareil.|  

### <a name="browser"></a>Navigateur  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  

|Paramètre|Détails|  
|-------------|-------------|  
|**Autoriser le navigateur web**|L'utilisateur peut modifier le navigateur Internet par défaut.|  
|**Remplissage automatique**|L'utilisateur peut modifier les paramètres de saisie semi-automatique dans le navigateur.|  
|**Active scripting**|Le navigateur peut exécuter des scripts, tels que les scripts ActiveX.|  
|**Plug-ins**|L'utilisateur peut ajouter des plug-ins à Internet Explorer.|  
|**Bloqueur de fenêtres publicitaires**|Active ou désactive le bloqueur de fenêtres publicitaires du navigateur.|  
|**Cookies**|Autorisez l'enregistrement des cookies sur l'appareil.|  
|**Avertissement de fraude**|Activez ou désactivez les avertissements des sites Web frauduleux potentiels.|  

### <a name="internet-explorer"></a>Internet Explorer  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  

|Paramètre|Détails|  
|-------------|-------------|  
|**Toujours envoyer un en-tête Aucun tracking**|Empêche que les informations d'exploration ne soient envoyées à des sites tiers.|  
|**Zone de sécurité intranet**|-|  
|**Niveau de sécurité de la zone Internet**|Configurez le niveau de sécurité pour la zone Internet.|  
|**Niveau de sécurité de la zone intranet**|Configurez le niveau de sécurité pour la zone intranet.|  
|**Niveau de sécurité de la zone Sites de confiance**|Configurez le niveau de sécurité pour la zone Sites de confiance.|  
|**Niveau de sécurité de la zone des sites sensibles**|Configurez le niveau de sécurité pour la zone des sites sensibles.|  
|**Espaces de noms pour la zone intranet**|-|  
|**Accéder à un site intranet pour une entrée à mot unique**|Active ou désactive le paramètre qui permet à Internet Explorer d'accéder automatiquement à un site Intranet si un nom de site valide est entré sans être précédé de HTTP :|  
|**Option de menu du mode entreprise**|Autorisez les utilisateurs à activer et désactiver le mode Entreprise à partir du menu **Outils** d’Internet Explorer.|  
|**Emplacement du rapport de journalisation (URL)**|Spécifiez une URL où les sites web visités sont enregistrés quand le Mode entreprise est actif.|  
|**Emplacement de la liste des sites en Mode entreprise (URL)**|Spécifiez l'emplacement de la liste des sites web qui utilisent le Mode entreprise quand il est actif.|  

### <a name="cloud"></a>Cloud  

|Paramètre|Détails|  
|-------------|-------------|  
|**Synchronisation des paramètres**|Permet la synchronisation des paramètres entre les appareils.|  
|**Synchronisation des informations d'identification**|Permet la synchronisation des informations d'identification entre les appareils.|  
|**Compte Microsoft**|Autorisez l'utilisation d'un compte Microsoft sur l'appareil.<br /><br /> (Windows Phone 8.1 uniquement)|  
|**Synchronisation des paramètres via des connexions limitées**|Autorisez la synchronisation des paramètres quand la connexion Internet est mesurée.|  

### <a name="security"></a>Sécurité  

|Paramètre|Détails|  
|-------------|-------------|  
|**Installation du fichier non signé**|Autorise le chargement des fichiers non signés.|  
|**Applications non signées**|Autorise le chargement des applications non signées.|  
|**Messagerie SMS et MMS**|Autorisez les messages SMS et MMS à partir de l'appareil.|  
|**Stockage amovible**|Autorisez l'utilisation du stockage amovible, comme une carte SD sur l'appareil.|  
|**Appareil photo**|Autorisez l'utilisation de l'appareil photo.|  
|**Communication en champ proche (NFC)**|Autorisez la communication à l'aide de NFC sur l'appareil.<br /><br /> (Windows Phone 8.1 uniquement)|
|**Autoriser la connexion USB**|Contrôle si les appareils peuvent accéder à des dispositifs de stockage externes via une connexion USB.|

### <a name="peak-synchronization"></a>Synchronisation de pointe  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  

|Paramètre|Détails|  
|-------------|-------------|  
|**Spécifier les heures de pointe**|Configurer la période de pointe pour la synchronisation des appareils mobiles.|  
|**Fréquence de synchronisation pendant les heures de pointe**|Configurer la fréquence à laquelle la synchronisation se produit pendant les heures de pointe que vous avez configurées.|  
|**Fréquence de synchronisation pendant les heures creuses**|Configurer la fréquence à laquelle la synchronisation se produit en dehors des heures de pointe que vous avez configurées.|  

### <a name="roaming"></a>Itinérant  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  

|Paramètre|Détails|  
|-------------|-------------|  
|**Gestion des appareils en itinérance**|Permet à l’appareil d’être géré par Configuration Manager en phase d’itinérance.|  
|**Téléchargement de logiciel en itinérance**|Permet de télécharger des applications et des logiciels lors de l'itinérance.|  
|**Téléchargement d'e-mails en itinérance**|Autorise les téléchargements de courrier électronique lors de l'itinérance.|  
|**Itinérance des données**|Autorisez l'itinérance entre réseaux lors de l'accès aux données.|  

### <a name="encryption"></a>Chiffrement  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  

|Paramètre|Détails|  
|-------------|-------------|  
|**Chiffrement de la carte de stockage**|Exigez le chiffrement des cartes de stockage utilisées avec l'appareil.|  
|**Chiffrement des fichiers sur l’appareil**|Requiert que les fichiers de l'appareil mobile soient chiffrés.|  
|**Demander la signature des courriers électroniques**|Requiert la signature des messages électroniques avant leur envoi.|  
|**Algorithme de signature**|Sélectionnez l’algorithme à utiliser pour signer les messages électroniques.|  
|**Demander le chiffrement des courriers électroniques**|Exigez le chiffrement des messages électroniques avant leur envoi.|  
|**Algorithme de chiffrement**|Sélectionnez l’algorithme à utiliser pour chiffrer les messages électroniques.|  

###  <a name="wireless-communications"></a>Communications sans fil  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Connexion réseau sans fil**|Activez ou désactivez la fonctionnalité Wi-Fi des appareils.|  
|**Connexion Wi-Fi**|Les utilisateurs peuvent utiliser leur appareil en tant que point d'accès sans fil mobile.|  
|**Décharger les données en Wi-Fi si possible**|Configurez cette option pour utiliser la connexion Wi-Fi sur le périphérique lorsque cela est possible.|  
|**Rapports de point d'accès Wi-Fi**|Envoie des informations sur les connexions Wi-Fi pour aider l’utilisateur à détecter les connexions à proximité.|  

#### <a name="to-configure-a-wireless-network-connection"></a>Pour configurer une connexion réseau sans fil  

1.  Dans la page **Configurer les paramètres de communication sans fil de l'appareil mobile** , cliquez sur **Ajouter**.  

2.  Dans la boîte de dialogue **Connexion réseau sans fil**, spécifiez les informations suivantes sur la connexion sans fil qui sera configurée sur les appareils mobiles, puis cliquez sur **OK** :

|Paramètre|Plus d'informations|  
|-------------|----------------------|  
|**Nom réseau (SSID)**|Entrez le nom du réseau Wi-Fi.|  
|**Connexion réseau**|Choisissez entre **Internet** et **Travail**.|  
|**Authentification**|Sélectionnez la méthode d'authentification de la connexion sans fil :<br><br>- **Ouvrir**<br>-                    **Partagé**<br>- **WPA**<br>- **WPA-PSK**<br>- **WPA2**<br>- **WPA2-PSK**|  
|**Chiffrement des données**|Choisissez la méthode de chiffrement utilisée par cette connexion. Les valeurs possibles varient en fonction de la méthode d' **Authentification** sélectionnée :<br><br>- **Désactivé**<br>- **WEP**<br>- **TKIP**<br>- **AES**|  
|**Index de clé**|Sélectionnez un index de clé entre **1** et **4** , qui sera utilisé avec un paramètre **Chiffrement des données** de **WEP**.|  
|**Ce réseau se connecte à Internet**|Sélectionnez cette option si vous souhaitez fournir des paramètres de proxy qui permettent aux appareils mobiles d'établir une connexion sans fil à Internet.|  
|**Paramètres du serveur proxy**|Spécifiez si nécessaire les paramètres **Serveur** et **Port** pour **HTTP**, **WAP** et **Sockets**.|  
|**Activer l'accès réseau 802.1X**|Sélectionnez cette option si vous souhaitez sécuriser la connexion en spécifiant un type EAP.|  
|**Type EAP**|Choisissez le type EAP à utiliser :<br><br>- **PEAP**<br>- **Carte à puce ou certificat**|  


###  <a name="certificates"></a>Certificats  
 Importez les certificats à installer sur les appareils mobiles.  

 Cliquez sur **Importer**, puis spécifiez les valeurs suivantes :  

-   **Fichier de certificat** : cliquez sur **Parcourir** , puis sélectionnez le fichier de certificat avec l'extension **.cer** que vous souhaitez importer.  

-   **Banque d'informations de destination** : choisissez une ou plusieurs banques de destination où le certificat importé sera ajouté sur l'appareil mobile :  

    -   **Racine**  

    -   **Autorité de certification**  

    -   **Normal**  

    -   **Privilégié**  

    -   **SPC**  

    -   **Homologue**  

-   **Rôle** : si **SPC** (Software Publisher Certificate) est sélectionné en tant que banque de destination, choisissez le rôle qui sera associé au certificat :  

    -   **Opérateur mobile**  

    -   **Gestionnaire**  

    -   **Utilisateur authentifié**  

    -   **Administrateur informatique**  

    -   **Utilisateur non authentifié**  

    -   **Serveur d’approvisionnement approuvé**  

### <a name="system-security"></a>Sécurité système  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  

|Paramètre|Détails|  
|-------------|-------------|  
|**Contrôle de compte d'utilisateur**|Active ou désactive le contrôle de compte d'utilisateur Windows sur l'appareil.|  
|**Pare-feu réseau**|Active ou désactive le pare-feu Windows.|  
|**Mises à jour**|Choisissez le mode de téléchargement des mises à jour logicielles Windows sur les ordinateurs. Par exemple, vous pouvez télécharger automatiquement les mises à jour, mais permettre à l'utilisateur de choisir à quel moment les installer.|  
|**Classification minimale des mises à jour**|Choisissez la classification minimale des mises à jour téléchargées sur les ordinateurs Windows : **Aucune**, **Importante**ou **Recommandée**.|  
|**SmartScreen**|Activez ou désactivez Windows SmartScreen.|  
|**Protection antivirus**|Assurez-vous que l’appareil est protégé par un logiciel antivirus.|  
|**Les signatures de la protection antivirus sont à jour**|Assurez-vous que les signatures antivirus sont à jour.|
|**Autoriser la désinscription manuelle**|-|  

### <a name="windows-server-work-folders"></a>Dossiers de travail du serveur Windows  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  

|Paramètre|Détails|  
|-------------|-------------|  
|**URL des dossiers de travail**|Configure l'emplacement d'un dossier de travail Windows Server auquel les utilisateurs peuvent se connecter à partir de leur appareil.|  

### <a name="windows-phone-allowed-and-blocked-apps-list-windows-phone-81-only"></a>Liste des applications autorisées et bloquées par Windows Phone (Windows Phone 8.1 uniquement)  
 Elle vous permet de spécifier la liste des applications Windows Phone conformes ou non conformes dans votre entreprise. Les applications que vous spécifiez comme bloquées ne peuvent pas être installées par les utilisateurs. Si vous spécifiez une liste d'applications autorisées, les utilisateurs peuvent installer uniquement les applications de la liste.  

 Vous ne pouvez pas spécifier à la fois des applications autorisées et bloquées dans le même élément de configuration.  

> [!IMPORTANT]  
>  Si vous spécifiez une liste d’applications autorisées, vous devez vous assurer que l’application du portail d’entreprise et toutes les applications déployées sur les appareils Windows Phone 8.1 figurent dans la liste **Applications autorisées** .  

#### <a name="to-specify-an-allowed-or-blocked-apps-list"></a>Pour spécifier une liste des applications autorisées ou bloquées  

1.  Dans la page **Liste des applications autorisées et bloquées (Windows Phone 8.1)** spécifiez les informations suivantes :  

|Paramètre|Plus d'informations|  
|-|-|  
|**Liste des applications bloquées**|Sélectionnez cette option si vous souhaitez spécifier une liste d'applications que les utilisateurs sont autorisés à installer.|  
|**Liste des applications autorisées**|Sélectionnez cette option si vous souhaitez spécifier une liste d'applications que les utilisateurs sont autorisés à installer.|  
|**Ajouter**|Ajoute une application à la liste sélectionnée. Spécifiez le nom de votre choix, éventuellement l’éditeur de l’application, ainsi que l’URL de l’application dans la boutique d’applications.<br /><br /> Pour spécifier l’URL, dans la page Windows Phone Store, recherchez l’application que vous voulez utiliser.<br /><br /> **Exemple :** recherchez l’application **Skype** dans le Store. L’URL que vous utilisez sera http://www.windowsphone.com/en-us/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51.<br /><br /> Pour l'application du portail d'entreprise, ou des applications métiers, il est inutile de spécifier une URL complète, le GUID de l'application suffit.|  
|**Éditer**|Vous permet de modifier le nom, l'éditeur et l'URL de l'application sélectionnée.|  
|**Supprimer**|Supprime l'application sélectionnée dans la liste.|  
|**Importerer**|Importe une liste d'applications que vous avez spécifiée dans un fichier de valeurs séparées par des virgules. Utilisez le format Nom de l'application, Éditeur, URL de l'application dans le fichier.|  



<!--HONumber=Dec16_HO3-->


