---
title: Notes de publication | System Center Configuration Manager
description: "Consultez ces notes pour les problèmes urgents qui ne sont pas encore résolus dans le produit ou traités dans un article de la Base de connaissances Microsoft."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 0b6c49f3c5e817f1dbd40b40c78d89c4a018e0f1


---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notes de publication de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec System Center Configuration Manager, les notes de publication de produit sont limitées aux problèmes urgents qui n’ont pas encore été résolus dans le produit (disponibles par le biais d’une mise à jour dans la console) ou détaillés dans un article de la Base de connaissances Microsoft.  

 Pour les problèmes connus qui affectent des scénarios de base, ces informations sont transmises dans la documentation du produit en ligne accessible dans la bibliothèque de documentation de System Center Configuration Manager.  

> [!TIP]  
>  Cette rubrique contient les notes de publication de la branche CB (Current Branch) de System Center Configuration Manager. Pour la préversion technique de System Center Configuration Manager, consultez [Technical Preview pour System Center Configuration Manager](../../../../core/get-started/technical-preview.md).  

## <a name="setup-and-upgrade"></a>Installation et mise à niveau  



### <a name="the-sql-server-backup-model-in-use-by-configuration-manager-can-change-from-full-to-simple"></a>Le modèle de sauvegarde SQL Server utilisé par Configuration Manager peut basculer de « complète » à « simple »  
 Quand vous mettez à niveau System Center Configuration Manager vers la version 1511, le modèle de sauvegarde SQL Server utilisé par Configuration Manager peut passer du modèle de sauvegarde complète au modèle de sauvegarde simple.  

-   Si vous utilisez une tâche de sauvegarde SQL Server personnalisée avec le modèle de sauvegarde complète (à la place de la tâche de sauvegarde intégrée pour Configuration Manager), la mise à niveau peut convertir votre modèle de sauvegarde complète en modèle de sauvegarde simple.  

**Solution de contournement**: après la mise à niveau vers la version 1511, vérifiez la configuration de SQL Server et restaurez le modèle de sauvegarde complète si nécessaire.  

### <a name="when-you-add-a-service-window-to-a-new-site-server-service-windows-that-were-configured-for-another-site-server-are-deleted"></a>Quand vous ajoutez une fenêtre de service à un nouveau serveur de site, les fenêtres de service qui étaient configurées pour un autre serveur de site sont supprimées.  
 Quand vous utilisez des fenêtres de service avec System Center Configuration Manager version 1511, vous ne pouvez configurer des fenêtres de service que pour un seul serveur de site dans une hiérarchie. Après avoir configuré des fenêtres de service sur un serveur, quand vous configurez une fenêtre de service sur un second serveur de site, les fenêtres de service sur le premier serveur de site sont supprimées de manière silencieuse, sans aucun avertissement ni erreur.  

**Solution de contournement** : installez le correctif à partir de la page de [l’article 3142341 de la Base de connaissances Microsoft](http://support.microsoft.com/kb/3142341). Ce problème est également résolu quand vous installez la mise à jour 1602 pour System Center Configuration Manager.  

### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Une mise à jour est bloquée avec un état Téléchargement dans le nœud Mises à jour et maintenance de la console Configuration Manager  
Pendant le téléchargement automatique des mises à jour par un point de connexion de service en ligne, une mise à jour peut se trouver bloquée avec un état Téléchargement. Lorsque le téléchargement d’une mise à jour est bloqué, des entrées similaires aux suivantes apparaissent dans les fichiers journaux indiqués :  

DMPdownloader.log :  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log :  

-   Error: failed to verify ’d:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi’ authenticode signature.  

-   Error: file signature check failed for ’d:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Solution de contournement** : sur le serveur de site, modifiez la clé de Registre suivante comme ci-après, puis redémarrez le service SMS_Executive ou attendez jusqu’à 24 heures le prochain cycle de téléchargement automatique.  

-   **Clé à modifier** : HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valeur de l’état** : définie sur **146944** décimal ou sur **0x00023e00** hexadécimal  

### <a name="pre-release-features-introduced-in-system-center-configuration-manager-1602"></a>Fonctionnalités en préversion introduites dans System Center Configuration Manager 1602  

Des fonctionnalités en préversion sont incluses dans le produit à des fins de test anticipé en environnement de production, mais ne doivent pas être considérées comme prêtes pour une utilisation en production.  

À partir de la mise à jour 1606, vous devez donner votre consentement avant de pouvoir utiliser les fonctionnalités en préversion. Pour plus d’informations, consultez [Utiliser des fonctionnalités de préversions de mises à jour](../../../../core/servers/manage/install-in-console-updates.md).

System Center Configuration Manager version 1602 introduit deux fonctionnalités de la version préliminaire :  

-   Accès conditionnel pour les PC gérés par System Center Configuration Manager. Pour plus d’informations, consultez [Gérer l’accès aux services O365 des PC gérés par System Center Configuration Manager](../../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).
    - Après avoir installé la mise à jour 1602, le type de fonctionnalité s’affiche comme commercialisé même s’il s’agit d’une préversion.
    - Si vous mettez ensuite à jour la version 1602 vers la version 1606, le type de fonctionnalité s’affiche comme commercialisé même s’il reste en préversion.
    - Si vous mettez à jour la version 1511 directement vers la version 1606, le type de fonctionnalité s’affiche en tant que préversion.


-   Maintenance d’un regroupement adapté aux clusters. Pour plus d’informations, consultez [Maintenance de groupe de serveurs](../../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups) dans [Capabilities in Technical Preview 1605 for System Center Configuration Manager](../../../../core/get-started/capabilities-in-technical-preview-1605.md) (Capacités de la version Technical Preview 1605 pour System Center Configuration Manager).  




### <a name="recovery-options-for-a-secondary-site-are-not-available-in-the-console"></a>Les options de récupération pour un site secondaire ne sont pas disponibles dans la console  
Après l’échec de la récupération d’un site secondaire, l’option **Récupérer le site secondaire** risque de ne plus être disponible dans la console Configuration Manager.  

Ce problème concerne System Center Configuration Manager versions 1511 et 1602, et devrait être résolu dans une prochaine mise à jour.  

**Solution de contournement**: utilisez l’une des méthodes suivantes pour récupérer (réinstaller) le site secondaire :  

-   Utilisez **Preinst.exe** et la commande **/delsite** pour supprimer le site secondaire, puis réinstallez le site secondaire. Pour plus d’informations sur preinst.exe, consultez [Outil de maintenance hiérarchique (Preinst.exe) pour System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)  

-   Exécutez le script suivant pour commencer la récupération du site secondaire. Vous exécutez ce script sur la base de données sur le site principal parent du site secondaire à récupérer :  

    ```  
    declare @SiteCode NVARCHAR(3)=N'<replace with secondary site code>'   

    UPDATE Sites SET Status = 9  
                    , DetailedStatus = 3  
    FROM Sites WHERE SiteCode = @SiteCode  

    UPDATE SCP SET SCP.Value1 = 9  
                    , SCP.Value2 = N'3'  
    FROM SC_SiteDefinition_Property SCP INNER JOIN SC_SiteDefinition SC ON SC.SiteNumber = SCP.SiteNumber  
    WHERE SC.SiteCode = @SiteCode AND SCP.[Name] = N'Requested Status'  
  ```  

###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>Le programme d’installation échoue lors de l’utilisation de fichiers redist à partir du dossier CD.Latest avec une erreur de vérification du manifeste
Quand vous exécutez le programme d’installation à partir d’un dossier CD.Latest créé pour la version 1606 et que vous utilisez les fichiers redist inclus avec ce dossier CD.Latest, le programme d’installation échoue avec les erreurs suivantes dans le journal d’installation de Configuration Manager :

  - ERROR: File hash check failed for defaultcategories.dll (ERREUR : Échec de la vérification du hachage de fichier pour defaultcategories.dll)
  - ERROR: Manifest verification failed. Wrong version of manifest? (ERREUR : Échec de la vérification du manifeste. Version de manifeste incorrecte ?)

**Solution de contournement :** procédez de l’une des manières suivantes :
 - Pendant l’installation, téléchargez les fichiers redist les plus récents de Microsoft à utiliser à la place de ceux figurant dans le dossier CD.Latest.
 - Supprimez manuellement le dossier *cd.latest\redist\languagepack\zhh*, puis réexécutez le programme d’installation.

## <a name="backup-and-recovery"></a>Sauvegarde et récupération
### <a name="pre-production-client-is-not-available-after-a-site-restore"></a>Aucun client de préproduction n’est disponible après une restauration de site
Avec la version 1602, quand vous utilisez des clients de préproduction et que vous restaurez le site de niveau supérieur de votre hiérarchie à partir d’une sauvegarde, la version du client de préproduction n’est pas disponible après la restauration du site.  

**Solution de contournement :** après avoir restauré le site de niveau supérieur de votre hiérarchie, vous devez copier manuellement les fichiers du client de préproduction afin que Configuration Manager puisse les traiter et les restaurer, et qu’ils puissent être utilisés :
1. Sur l’ordinateur du serveur de site de niveau supérieur, copiez le contenu du dossier *&lt;Emplacement_Installation_CM\>\\Client* dans le dossier *&lt;Emplacement_Installation_CM\>\\Client_préproduction*.

2. Créez un fichier vide nommé **client.acu**, puis copiez ou collez ce fichier dans le dossier *&lt;Emplacement_Installation_CM\>\\Boîtes de réception\\hman.box* sur le serveur de site. (Ce fichier peut être un fichier texte qui a été renommé, tant qu’il n’a plus l’extension txt). Une fois que ce fichier est placé dans le dossier hman.box, le Gestionnaire de hiérarchie sur le serveur de site démarre et traite les fichiers du client, et restaure les fichiers du client de préproduction à utiliser.

Ce problème est résolu dans la version 1606.


## <a name="client-deployment-and-upgrade"></a>Mise à niveau et déploiement du client  

### <a name="expansion-to-central-administration-site-stops-automatic-client-upgrades"></a>L’extension à un site d’administration centrale arrête les mises à niveau automatiques de clients  
Dans la version 1511 uniquement, vous ne pouvez pas exécuter des mises à niveau automatiques de clients pour un site principal étendu à un site d’administration centrale. Lors de l’extension du site, le site faisant autorité sur le package de mise à jour du client n’est pas correctement défini sur le nouveau site d’administration centrale, ce qui empêche l’exécution correcte des mises à niveau automatiques des clients. Ce problème se pose uniquement pour la version 1511. Il est résolu dans la version 1602 et les versions ultérieures.  

**Solution de contournement :** exécutez le script SQL suivant sur la base de données du site d’administration centrale. Après exécution du script, les mises à niveau automatiques des clients doivent commencer à fonctionner normalement.  

  ```  
  DECLARE @RootSite AS NVARCHAR(3)  
  DECLARE @SourceServer AS NVARCHAR(255)  
  DECLARE @FullClientPkgSource AS NVARCHAR(255)  
  DECLARE @UpgradePkgSource AS NVARCHAR(255)  

  SELECT @RootSite = SiteCode, @SourceServer = SiteServer  
  FROM sites  
  WHERE ISNULL(ReportToSite, N'') = N''  

  SELECT @FullClientPkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\Client'  
  SELECT @UpgradePkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\ClientUpgrade'  

  UPDATE SMSPackages_G  
  SET Source = @FullClientPkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT FullPackageID FROM ClientDeploymentSettings)  

  UPDATE SMSPackages_G  
  SET Source = @UpgradePkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT UpgradePackageID FROM ClientDeploymentSettings)  

  UPDATE ProgramOffers_G  
  SET SourceSite = @RootSite  
  WHERE OfferID IN  
      (SELECT UpgradeAdvertisementID FROM ClientDeploymentSettings)  
  ```  

## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation  

### <a name="issue-with-the-windows-adk-for-windows-10-version-1511"></a>Problème avec Windows ADK pour Windows 10, version 1511  
Quand vous exécutez, à partir du Centre logiciel, une séquence de tâches qui utilise une image de démarrage Windows PE v.10.0.10586 de Windows ADK 10 version 1511, quand l’ordinateur redémarre dans Windows PE, le redémarrage échoue à l’étape « Initialisation des périphériques matériels... » avec l’erreur suivante : **Échec de l’initialisation de Windows PE avec le code d’erreur 0x80220014**.  

**Solution de contournement**: utilisez la version de Windows 10 ADK d’origine. Pour plus d’informations, consultez le blog suivant de l’équipe System Center Configuration Manager : [Issue with the Windows ADK for Windows 10](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx)  

### <a name="dynamic-application-installation-fails-during-task-sequence-which-successfully-completes"></a>L’installation d’applications dynamiques échoue pendant une séquence de tâches qui se termine avec succès  
Quand vous déployez une séquence de tâches qui utilise l’option **Installer les applications en fonction de la liste de variables dynamiques**et que l’installation de l’une des applications échoue pour une raison quelconque, la séquence de tâches signale qu’elle s’est terminée correctement. Cela se produit quelle que soit la façon dont vous configurez les options suivantes :  

-   **Continuer en cas d’erreur** (sous l’onglet Options de l’étape Installer l’application)  

-   **Si l’installation d’une application échoue, continuer d’installer les autres applications de la liste** (sous l’onglet Propriétés de l’étape Installer l’application)  

Vous pouvez afficher le fichier smsts.log pour déterminer si l’installation d’une application a échoué.  

**Solution de contournement**: utilisez la variable **_TSAppInstallStatus** comme condition lors des étapes suivantes dans une séquence de tâches, en spécifiant que la séquence de tâches doit échouer si une erreur s’est produit au niveau de l’une des applications dynamiques.  

### <a name="smb-might-not-work-properly-after-you-use-a-task-sequence-to-install-windows-10"></a>SMB peut ne pas fonctionner correctement après utilisation d’une séquence de tâches pour installer Windows 10  
Lorsque vous utilisez une séquence de tâches pour installer une image de Windows 10, il se peut que SMB ne fonctionne pas correctement après l’installation du client Configuration Manager. Par exemple, les étapes de séquence de tâches suivantes peuvent échouer :  

-   Restauration de l’état d’utilisateur en cas d’utilisation avec un point de migration d’état  

-   Connexion à un dossier réseau  

À partir d’une invite de commandes d’administrateur F8, vous pouvez toujours, par exemple, effectuer un test PING de l’ordinateur, mais le trafic réseau SMB (par exemple, NET USE à partir d’une invite de commandes) peut échouer en générant l’erreur 1231 - L’emplacement réseau ne peut pas être atteint.  

**Solution de contournement** :  
ajoutez une étape de séquence de tâches Exécuter la ligne de commande après l’étape de séquence de tâches Configurer Windows et ConfigMgr afin d’arrêter, puis de démarrer le service Station de travail comme suit :    
**net stop workstation /y & net start workstation**  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Les plans de maintenance créent un grand nombre de groupes et de déploiements de mises à jour logicielles en double  
Par défaut, l’Assistant Créer un plan de maintenance s’exécute actuellement après chaque synchronisation des mises à jour logicielles. Chaque fois que l’Assistant s’exécute, il crée un groupe et un déploiement de mises à jour logicielles. Par exemple, si vous avez une planification de la synchronisation des mises à jour logicielles qui s’exécute plusieurs fois par jour, l’Assistant Créer un plan de maintenance génère quotidiennement plusieurs groupes et déploiements de mises à jour logicielles, probablement identiques.  

**Solution de contournement** :    
après avoir créé un plan de maintenance, ouvrez les propriétés de celui-ci, accédez à l’onglet **Calendrier d’évaluation**, sélectionnez **Exécuter la règle dans un calendrier**, cliquez sur **Personnaliser**, puis créez un calendrier personnalisé. Par exemple, vous pouvez faire en sorte que le plan de maintenance s’exécute tous les 60 jours.  

## <a name="mobile-device-management"></a>Gestion des appareils mobiles  

### <a name="cannot-create-an-enrollment-profile-on-a-primary-site"></a>Impossible de créer un profil d’inscription sur un site principal  
Un administrateur ne peut pas créer de profil d’inscription qui se connecte à un site principal dans la console d’administration de System Center Configuration Manager. Lors de la tentative d’inscription, un message d’erreur « Le jeton DEP n’a pas été chargé. Chargez un jeton DEP » s’affiche à l’administrateur dans l’Assistant Profil d’inscription. Cette erreur se produit même si un jeton DEP valide a été chargé vers le site d’administration centrale.  

**Solution de contournement**: créez, dans la console System Center Configuration Manager, un profil d’inscription qui se connecte au site d’administration centrale.  

### <a name="dep-cannot-use-non-alpha-numeric-characters-in-enrollment-profiles"></a>DEP ne peut pas utiliser de caractères non alphanumériques dans les profils d’inscription  
Les profils d’inscription associés à Apple DEP (Device Enrollment Profile) ne peuvent pas utiliser de caractères non alphanumériques dans les champs **Nom**, **Description**, **Service** et **Numéro de téléphone** pour le profil d’inscription quand DEP est activé. L’utilisation de caractères non alphanumériques dans ces champs crée un profil d’inscription, mais celui-ci ne peut pas être chargé vers Apple. Aucun message d’erreur ou d’avertissement n’est fourni par le serveur Apple, et les profils ne sont pas déployés sur les appareils gérés par DEP.  

**Solution de contournement** : aucune.

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>Une réinitialisation complète désactive les appareils Windows 10 avec moins de 4 Go de RAM

L’exécution d’une réinitialisation complète sur les appareils Windows 10 RTM (versions antérieures à la version 1511) avec moins de 4 Go de RAM peut rendre l’appareil inutilisable. Après une tentative de réinitialisation de l’appareil, il ne peut pas démarrer et ne répond pas.

**Solution de contournement** : vérifiez que les PC Windows 10 RTM ont au moins 4 Go de RAM disponible avant d’effectuer une réinitialisation complète de l’appareil. Pour afficher le numéro de version des appareils Windows 10, entrez « winver » à partir d’une invite de commandes. Si l’appareil a déjà été réinitialisé et n’est plus réactif, utilisez un lecteur USB Windows 10 démarrable pour démarrer et récupérer l’accès à l’appareil.

### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Quand un utilisateur appartient à plusieurs regroupements d’utilisateurs pour lesquels une stratégie de conditions générales est déployée, l’utilisateur voit plusieurs ensembles des mêmes conditions générales  

Quand un administrateur déploie un ensemble de conditions générales dans plusieurs regroupements d’utilisateurs et qu’un utilisateur est membre de plusieurs de ces regroupements, plusieurs copies identiques des conditions générales lui sont présentées quand il ouvre le portail d’entreprise.  Par exemple, si un utilisateur nommé « Exemple_Utilisateur » est membre de deux regroupements d’utilisateurs différents, l’un nommé « EmployésSociétéFTE » et l’autre « EmployésSociétéNA », et que les conditions générales nommées « ConditionsGénérales » sont déployées vers EmployésSociétéFTE et vers EmployésSociétéNA, Exemple_Utilisateur verra deux ensembles identiques de ConditionsGénérales dans la page d’acceptation des conditions générales. Étant donné que les utilisateurs peuvent uniquement accepter ou refuser toutes les conditions générales, il n’existe aucun risque d’être dans un état d’acceptation ambigu (où l’utilisateur aurait à la fois accepté et refusé les conditions générales). Le rapport d’acceptation des conditions générales comprend une seule ligne par ensemble de conditions générales et par utilisateur. Il ne contient donc aucune erreur. La seule conséquence est que l’utilisateur verra deux ensembles de conditions générales dans la page d’acceptation.  

**Solution de contournement**: assurez-vous que chaque utilisateur appartient à un seul regroupement où les conditions générales sont déployées.  

## <a name="reports-and-monitoring"></a>Rapports et analyse  

### <a name="the-health-attestation-report-is-empty-even-though-health-attestation-data-was-previously-collected"></a>Le rapport d’attestation d’intégrité est vide, alors que des données d’attestation d’intégrité ont été collectées  
Quand un utilisateur administratif ayant un rôle de sécurité incluant l’autorisation **Lecture** sur le groupe d’autorisations **Attestation d’intégrité** consulte le rapport d’attestation d’intégrité, celui-ci est vide. Cela est dû au fait que les autorisations d’afficher les données du rapport d’attestation d’intégrité sont liées au groupe d’autorisations **Affinité entre utilisateur et périphérique** au lieu du groupe d’autorisations Attestation d’intégrité.  

Ce problème concerne System Center Configuration Manager avec la mise à jour 1602, et devrait être résolu dans une prochaine mise à jour.  

**Solution de contournement** : affectez à l’utilisateur administratif un groupe de sécurité incluant l’autorisation **Lecture** sur le groupe d’autorisations **Affinités des périphériques d’utilisateur**.  

### <a name="conditional-access"></a>Accès conditionnel  

#### <a name="the-same-user-collection-is-not-blocked-from-being-added-to-both-exempted-and-targeted-collections"></a>L’ajout du même regroupement d’utilisateurs aux regroupements Exemptés et Ciblés n’est pas bloqué.  
Cela se produit uniquement quand vous ajoutez le même **regroupement d’utilisateurs** à la page **Regroupements exemptés** **avant** de l’ajouter à la page **Regroupements ciblés**.  Si vous ajoutez un **regroupement d’utilisateurs** d’abord à la page **Regroupements ciblés**, puis essayez d’ajouter le même **regroupement d’utilisateurs** à la page **Regroupements exemptés**, vous devriez voir s’afficher le message de blocage normal.  

Ce problème affecte l’accès conditionnel de System Center Configuration Manager pour **Exchange sur site** avec la mise à jour 1602, et devrait être résolu dans une prochaine mise à jour.  

**Solution de contournement :** ajoutez le **regroupement d’utilisateurs** à la page **Regroupements ciblés** avant de sélectionner le **regroupement d’utilisateurs** dans la page **Regroupements exemptés**, ou assurez-vous que vous n’ajoutez pas le même **regroupement d’utilisateurs** aux regroupements ciblés et exemptés.



<!--HONumber=Nov16_HO1-->


