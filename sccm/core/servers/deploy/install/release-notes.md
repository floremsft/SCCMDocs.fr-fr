---
title: "Notes de publication - Configuration Manager | Microsoft Docs"
description: "Consultez ces notes pour les problèmes urgents qui ne sont pas encore résolus dans le produit ou traités dans un article de la Base de connaissances Microsoft."
ms.custom: na
ms.date: 3/27/27
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
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: aca3525fc143b281f41c3d9bd20bb93b1d91f6ce
ms.lasthandoff: 03/27/2017


---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notes de publication de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec System Center Configuration Manager, les notes de publication de produit sont limitées aux problèmes urgents qui n’ont pas encore été résolus dans le produit (disponibles par le biais d’une mise à jour dans la console) ou détaillés dans un article de la Base de connaissances Microsoft.  

 Pour les problèmes connus qui affectent des scénarios de base, ces informations sont transmises dans la documentation du produit en ligne accessible dans la bibliothèque de documentation de System Center Configuration Manager.  

> [!TIP]  
>  Cette rubrique contient les notes de publication de la branche CB (Current Branch) de System Center Configuration Manager. Pour la préversion technique de System Center Configuration Manager, consultez [Technical Preview pour System Center Configuration Manager](../../../../core/get-started/technical-preview.md).  

## <a name="setup-and-upgrade"></a>Installation et mise à niveau  

### <a name="after-you-update-a-configuration-manager-console-using-consolesetupexe-from-the-site-server-folder-recent-language-pack-changes-are-not-available"></a>Après avoir mis à jour une console Configuration Manager à l’aide du fichier ConsoleSetup.exe du dossier du serveur de site, les dernières modifications du pack linguistique ne sont pas disponibles
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
Après avoir exécuté une mise à jour sur place sur la console à l’aide du fichier ConsoleSetup.exe d’un dossier d’installation de serveurs de site, les packs linguistiques récemment installés peuvent ne pas être disponibles. Cela se produit lorsque :
- Votre site exécute la version 1610 ou 1702.
- La console est mise à jour sur place à l’aide du fichier ConsoleSetup.exe du dossier d’installation du serveur de site.

Lorsque ce problème se produit, la console réinstallée n’utilise pas la dernière série de modules linguistiques qui ont été configurés. Aucune erreur n’est retournée, mais les packs linguistiques disponibles dans la console n’auront pas changé.  

**Solution de contournement :** désinstallez la console actuelle et réinstallez la console en tant que nouvelle installation. Vous pouvez utiliser le fichier ConsoleSetup.exe du dossier d’installation des serveurs de site. Pendant l’installation, veillez à sélectionner les fichiers du pack linguistique que vous souhaitez utiliser.


### <a name="with-version-1702-the-default-site-boundary-group-is-configured-for-use-for-site-assignment"></a>Avec la version 1702, le groupe de limites de site par défaut est configuré pour une utilisation dans le cadre d’une attribution de site
<!--  SMS 486380   Applicability should only be to 1702. -->
Avec la version 1702, l’onglet Référence des groupes de limites de site par défaut affiche une coche pour l’option **Utiliser ce groupe de limites pour l'attribution de site**, répertorie le site en tant que **site attribué** et apparaît en grisé indiquant que la configuration ne peut pas être modifiée ou supprimée.

**Solution de contournement :** aucune. Vous pouvez ignorer ce paramètre. Même si le groupe est activé pour l’attribution de site, le groupe de limites de site par défaut n’est pas utilisé pour l’attribution de site. Avec la version 1702, cette configuration garantit que le groupe de limites de site par défaut est associé au site approprié.



### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Quand vous installez un site Long-Term Service Branch à l’aide de la version 1606, un site Current Branch est installé
<!-- Consider move to core content  -->
Quand vous utilisez le média de base de référence de la version 1606 publiée en octobre 2016 pour installer un site Long-Term Servicing Branch (LTSB), le programme d’installation installe un site Current Branch à la place. Cela se produit car l’option d’installation d’un point de connexion de service avec l’installation du site n’est pas sélectionnée.

 - Bien qu’un point de connexion ne soit pas obligatoire, son installation doit être sélectionnée pendant l’installation d’un site LTSB.

Une fois l’installation terminée, vous pouvez désinstaller le point de connexion de service.  Toutefois, vous devez disposer d’un point de connexion de service en mode hors connexion ou en ligne pour envoyer les données de télémétrie et obtenir des mises à jour de sécurité pour les sites Current Branch et LTSB.

Si votre site a été installé comme un site Current Branch alors que vous souhaitiez installer LTSB, vous pouvez désinstaller le site, puis le réinstaller. Vous pouvez également appeler le [Centre d’aide et de support Microsoft](http://go.microsoft.com/fwlink/?LinkId=243064) pour obtenir de l’aide.  

Pour vérifier quelle branche a été installée, dans la console, accédez à **Administration** > **Configuration du Site** > **Sites**, puis ouvrez **Paramètres de hiérarchie**. L’option permettant de convertir le site en site Current Branch est uniquement disponible quand le site exécute LTSB.  

**Solution de contournement :**  aucune.   



### <a name="the--sql-server-backup-model-in-use-by-configuration-manager-can-change-from-full-to-simple"></a>Le modèle de sauvegarde SQL Server utilisé par Configuration Manager peut basculer de « complète » à « simple »  
<!-- Confirm applicability for upgrade to later baselines. 1511 is out of support. 1606 is minmum supported baseline  -->

 Quand vous mettez à niveau System Center Configuration Manager vers la version 1511, le modèle de sauvegarde SQL Server utilisé par Configuration Manager peut passer du modèle de sauvegarde complète au modèle de sauvegarde simple.  

-   Si vous utilisez une tâche de sauvegarde SQL Server personnalisée avec le modèle de sauvegarde complète (à la place de la tâche de sauvegarde intégrée pour Configuration Manager), la mise à niveau peut convertir votre modèle de sauvegarde complète en modèle de sauvegarde simple.  

**Solution de contournement**: après la mise à niveau vers la version 1511, vérifiez la configuration de SQL Server et restaurez le modèle de sauvegarde complète si nécessaire.  



### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Une mise à jour est bloquée avec un état Téléchargement dans le nœud Mises à jour et maintenance de la console Configuration Manager  
<!-- Source bug pending. Consider move to core content.  -->
Pendant le téléchargement automatique des mises à jour par un point de connexion de service en ligne, une mise à jour peut se trouver bloquée avec un état Téléchargement. Lorsque le téléchargement d’une mise à jour est bloqué, des entrées similaires aux suivantes apparaissent dans les fichiers journaux indiqués :  

DMPdownloader.log :  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log :  

-   Error: failed to verify ’d:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi’ authenticode signature.  

-   Error: file signature check failed for ’d:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Solution de contournement** : sur le serveur de site, modifiez la clé de Registre suivante comme ci-après, puis redémarrez le service SMS_Executive ou attendez jusqu’à 24 heures le prochain cycle de téléchargement automatique.  

-   **Clé à modifier** : HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valeur de l’état** : définie sur **146944** décimal ou sur **0x00023e00** hexadécimal  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>Le programme d’installation échoue lors de l’utilisation de fichiers redist à partir du dossier CD.Latest avec une erreur de vérification du manifeste
<!-- Source bug pending  -->

Quand vous exécutez le programme d’installation à partir d’un dossier CD.Latest créé pour la version 1606 et que vous utilisez les fichiers redist inclus avec ce dossier CD.Latest, le programme d’installation échoue avec les erreurs suivantes dans le journal d’installation de Configuration Manager :

  - ERROR: File hash check failed for defaultcategories.dll (ERREUR : Échec de la vérification du hachage de fichier pour defaultcategories.dll)
  - ERROR: Manifest verification failed. Wrong version of manifest? (ERREUR : Échec de la vérification du manifeste. Version de manifeste incorrecte ?)

**Solution de contournement :** procédez de l’une des manières suivantes :
 - Pendant l’installation, téléchargez les fichiers redist les plus récents de Microsoft à utiliser à la place de ceux figurant dans le dossier CD.Latest.
 - Supprimez manuellement le dossier *cd.latest\redist\languagepack\zhh*, puis réexécutez le programme d’installation.

### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>L’outil de connexion de service lève une exception quand le serveur SQL Server est distant ou quand la mémoire partagée est désactivée
À compter de la version 1606, l’outil de connexion de service génère une exception si l’une des conditions suivantes s’applique :  
 -    Votre base de données de site est distante de l’ordinateur qui héberge le point de connexion de service et utilise un port non standard (autre que le port 1433)
 -     Votre base de données de site se trouve sur le même serveur que le point de connexion de service, mais l’option **Mémoire partagée** du protocole SQL est désactivée

L’exception est semblable à la suivante :
 - *Exception non prise en charge : System.Data.SqlClient.SqlException : Une erreur liée au réseau ou spécifique à l’instance s’est produite lors de l’établissement d’une connexion à SQL Server. Le serveur est introuvable ou n’est pas accessible. Vérifiez que le nom de l’instance est correct et que SQL Server est configuré pour autoriser les connexions distantes. (fournisseur : Fournisseur de canaux nommés, erreur : 40 - Impossible d’ouvrir une connexion à SQL Server) --*

**Solution de contournement** : quand vous utilisez l’outil, vous devez modifier le Registre du serveur qui héberge le point de connexion de service de manière à inclure des informations sur le port SQL Server :

   1.    Avant d’utiliser l’outil, modifiez la clé de Registre suivante et ajoutez le numéro du port utilisé au nom du serveur SQL Server :
    - Clé : HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - Valeur : &lt;nom du serveur SQL Server>
    - Ajoutez : **,&lt;PORT>**

    Par exemple, pour ajouter le port *15001* à un serveur nommé *testserver.test.net*, la clé résultante est la suivante : ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.    Une fois le port ajouté au Registre, l’outil doit fonctionner normalement.  

   3.    Quand vous avez terminé d’utiliser l’outil, pour les étapes **-connect** et **-import**, rétablissez la valeur d’origine de la clé de Registre.  




<!-- No current Backup and Recovery relenotes
## Backup and recovery
-->


<!-- No current  Client deployment and upgrade relenotes
## Client deployment and upgrade  
-->



## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation  

### <a name="issue-with-the-windows-adk-for-windows-10-version-1511"></a>Problème avec Windows ADK pour Windows 10, version 1511  
Quand vous exécutez, à partir du Centre logiciel, une séquence de tâches qui utilise une image de démarrage Windows PE v.10.0.10586 de Windows ADK 10 version 1511, quand l’ordinateur redémarre dans Windows PE, le redémarrage échoue à l’étape « Initialisation des périphériques matériels... » avec l’erreur suivante : **Échec de l’initialisation de Windows PE avec le code d’erreur 0x80220014**.  

**Solution de contournement**: utilisez la version de Windows 10 ADK d’origine. Pour plus d’informations, consultez le blog suivant de l’équipe System Center Configuration Manager : [Issue with the Windows ADK for Windows 10](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx)  

### <a name="dynamic-application-installation-fails-during-task-sequence-which-successfully-completes"></a>L’installation d’applications dynamiques échoue pendant une séquence de tâches qui se termine avec succès  
Quand vous déployez une séquence de tâches qui utilise l’option **Installer les applications en fonction de la liste de variables dynamiques**et que l’installation de l’une des applications échoue pour une raison quelconque, la séquence de tâches signale qu’elle s’est terminée correctement. Cela se produit quelle que soit la façon dont vous configurez les options suivantes :  

-   **Continuer en cas d’erreur** (sous l’onglet Options de l’étape Installer l’application)  

-   **Si l’installation d’une application échoue, continuer d’installer les autres applications de la liste** (sous l’onglet Propriétés de l’étape Installer l’application)  

Vous pouvez afficher le fichier smsts.log pour déterminer si l’installation d’une application a échoué.  

**Solution de contournement**: utilisez la variable **_TSAppInstallStatus** comme condition lors des étapes suivantes dans une séquence de tâches, en spécifiant que la séquence de tâches doit échouer si une erreur s’est produit au niveau de l’une des applications dynamiques.  

### <a name="smb-might-not-work-properly-after-you-use-a-task-sequence-to-install-windows-10"></a>SMB peut ne pas fonctionner correctement après utilisation d’une séquence de tâches pour installer Windows 10  
Lorsque vous utilisez une séquence de tâches pour installer une image de Windows 10, il se peut que SMB ne fonctionne pas correctement après l’installation du client Configuration Manager. Par exemple, les étapes de séquence de tâches suivantes peuvent échouer :  

-   Restauration de l’état d’utilisateur en cas d’utilisation avec un point de migration d’état  

-   Connexion à un dossier réseau  

À partir d’une invite de commandes d’administrateur F8, vous pouvez toujours, par exemple, effectuer un test PING de l’ordinateur, mais le trafic réseau SMB (par exemple, NET USE à partir d’une invite de commandes) peut échouer en générant l’erreur 1231 - L’emplacement réseau ne peut pas être atteint.  

**Solution de contournement** :  
ajoutez une étape de séquence de tâches Exécuter la ligne de commande après l’étape de séquence de tâches Configurer Windows et ConfigMgr afin d’arrêter, puis de démarrer le service Station de travail comme suit :    
**net stop workstation /y & net start workstation**  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Les plans de maintenance créent un grand nombre de groupes et de déploiements de mises à jour logicielles en double  
Par défaut, l’Assistant Créer un plan de maintenance s’exécute actuellement après chaque synchronisation des mises à jour logicielles. Chaque fois que l’Assistant s’exécute, il crée un groupe et un déploiement de mises à jour logicielles. Par exemple, si vous avez une planification de la synchronisation des mises à jour logicielles qui s’exécute plusieurs fois par jour, l’Assistant Créer un plan de maintenance génère quotidiennement plusieurs groupes et déploiements de mises à jour logicielles, probablement identiques.  

**Solution de contournement** :    
après avoir créé un plan de maintenance, ouvrez les propriétés de celui-ci, accédez à l’onglet **Calendrier d’évaluation**, sélectionnez **Exécuter la règle dans un calendrier**, cliquez sur **Personnaliser**, puis créez un calendrier personnalisé. Par exemple, vous pouvez faire en sorte que le plan de maintenance s’exécute tous les 60 jours.  

### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>Quand une boîte de dialogue de déploiement à haut risque est visible pour l’utilisateur, les boîtes de dialogue à haut risque ultérieures avec une échéance plus courte ne sont pas affichées
Une fois que vous avez créé et déployé un déploiement de tâches à haut risque sur les utilisateurs, une boîte de dialogue à haut risque s’affiche pour l’utilisateur. Si l’utilisateur ne ferme pas la boîte de dialogue et que vous créez et déployez un autre déploiement à haut risque avec une échéance plus courte que la première, l’utilisateur ne reçoit pas de boîte de dialogue mise à jour tant qu’il ne ferme pas la boîte de dialogue d’origine. Les déploiements continuent de s’exécuter selon les échéances configurées.

**Solution de contournement** :  
L’utilisateur doit fermer la boîte de dialogue pour que le premier déploiement à haut risque affiche la boîte de dialogue du déploiement à haut risque suivant.

## <a name="mobile-device-management"></a>Gestion des appareils mobiles  

### <a name="cannot-create-an-enrollment-profile-on-a-primary-site"></a>Impossible de créer un profil d’inscription sur un site principal  
Un administrateur ne peut pas créer de profil d’inscription qui se connecte à un site principal dans la console d’administration de System Center Configuration Manager. Lors de la tentative d’inscription, un message d’erreur « Le jeton DEP n’a pas été chargé. Chargez un jeton DEP » s’affiche à l’administrateur dans l’Assistant Profil d’inscription. Cette erreur se produit même si un jeton DEP valide a été chargé vers le site d’administration centrale.  

**Solution de contournement**: créez, dans la console System Center Configuration Manager, un profil d’inscription qui se connecte au site d’administration centrale.  

### <a name="dep-cannot-use-non-alpha-numeric-characters-in-enrollment-profiles"></a>DEP ne peut pas utiliser de caractères non alphanumériques dans les profils d’inscription  
Les profils d’inscription associés à Apple DEP (Device Enrollment Profile) ne peuvent pas utiliser de caractères non alphanumériques dans les champs **Nom**, **Description**, **Service** et **Numéro de téléphone** pour le profil d’inscription quand DEP est activé. L’utilisation de caractères non alphanumériques dans ces champs crée un profil d’inscription, mais celui-ci ne peut pas être chargé vers Apple. Aucun message d’erreur ou d’avertissement n’est fourni par le serveur Apple, et les profils ne sont pas déployés sur les appareils gérés par DEP.  

**Solution de contournement** : aucune.

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>Une réinitialisation complète désactive les appareils Windows 10 avec moins de 4 Go de RAM

L’exécution d’une réinitialisation complète sur les appareils Windows 10 RTM (versions antérieures à la version 1511) avec moins de 4 Go de RAM peut rendre l’appareil inutilisable. Après une tentative de réinitialisation de l’appareil, il ne peut pas démarrer et ne répond pas.

**Solution de contournement** : vérifiez que les PC Windows 10 RTM ont au moins 4 Go de RAM disponible avant d’effectuer une réinitialisation complète de l’appareil. Pour afficher le numéro de version des appareils Windows 10, entrez « winver » à partir d’une invite de commandes. Si l’appareil a déjà été réinitialisé et n’est plus réactif, utilisez un lecteur USB Windows 10 démarrable pour démarrer et récupérer l’accès à l’appareil.

### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Quand un utilisateur appartient à plusieurs regroupements d’utilisateurs pour lesquels une stratégie de conditions générales est déployée, l’utilisateur voit plusieurs ensembles des mêmes conditions générales  

Quand un administrateur déploie un ensemble de conditions générales dans plusieurs regroupements d’utilisateurs et qu’un utilisateur est membre de plusieurs de ces regroupements, plusieurs copies identiques des conditions générales lui sont présentées quand il ouvre le portail d’entreprise.  Par exemple, si un utilisateur nommé « Exemple_Utilisateur » est membre de deux regroupements d’utilisateurs différents, l’un nommé « EmployésSociétéFTE » et l’autre « EmployésSociétéNA », et que les conditions générales nommées « ConditionsGénérales » sont déployées vers EmployésSociétéFTE et vers EmployésSociétéNA, Exemple_Utilisateur verra deux ensembles identiques de ConditionsGénérales dans la page d’acceptation des conditions générales. Étant donné que les utilisateurs peuvent uniquement accepter ou refuser toutes les conditions générales, il n’existe aucun risque d’être dans un état d’acceptation ambigu (où l’utilisateur aurait à la fois accepté et refusé les conditions générales). Le rapport d’acceptation des conditions générales comprend une seule ligne par ensemble de conditions générales et par utilisateur. Il ne contient donc aucune erreur. La seule conséquence est que l’utilisateur verra deux ensembles de conditions générales dans la page d’acceptation.  

**Solution de contournement**: assurez-vous que chaque utilisateur appartient à un seul regroupement où les conditions générales sont déployées.  

## <a name="reports-and-monitoring"></a>Rapports et analyse  

### <a name="the-health-attestation-report-is-empty-even-though-health-attestation-data-was-previously-collected"></a>Le rapport d’attestation d’intégrité est vide, alors que des données d’attestation d’intégrité ont été collectées  
Quand un utilisateur administratif ayant un rôle de sécurité incluant l’autorisation **Lecture** sur le groupe d’autorisations **Attestation d’intégrité** consulte le rapport d’attestation d’intégrité, celui-ci est vide. Cela est dû au fait que les autorisations d’afficher les données du rapport d’attestation d’intégrité sont liées au groupe d’autorisations **Affinité entre utilisateur et périphérique** au lieu du groupe d’autorisations Attestation d’intégrité.  

Ce problème concerne System Center Configuration Manager avec la mise à jour 1602, et devrait être résolu dans une prochaine mise à jour.  

**Solution de contournement** : affectez à l’utilisateur administratif un groupe de sécurité incluant l’autorisation **Lecture** sur le groupe d’autorisations **Affinités des périphériques d’utilisateur**.  

### <a name="conditional-access"></a>Accès conditionnel  

#### <a name="the-same-user-collection-is-not-blocked-from-being-added-to-both-exempted-and-targeted-collections"></a>L’ajout du même regroupement d’utilisateurs aux regroupements Exemptés et Ciblés n’est pas bloqué.  
Cela se produit uniquement quand vous ajoutez le même **regroupement d’utilisateurs** à la page **Regroupements exemptés** **avant** de l’ajouter à la page **Regroupements ciblés**.  Si vous ajoutez un **regroupement d’utilisateurs** d’abord à la page **Regroupements ciblés**, puis essayez d’ajouter le même **regroupement d’utilisateurs** à la page **Regroupements exemptés**, vous devriez voir s’afficher le message de blocage normal.  

Ce problème affecte l’accès conditionnel de System Center Configuration Manager pour **Exchange sur site** avec la mise à jour 1602, et devrait être résolu dans une prochaine mise à jour.  

**Solution de contournement :** ajoutez le **regroupement d’utilisateurs** à la page **Regroupements ciblés** avant de sélectionner le **regroupement d’utilisateurs** dans la page **Regroupements exemptés**, ou assurez-vous que vous n’ajoutez pas le même **regroupement d’utilisateurs** aux regroupements ciblés et exemptés.

