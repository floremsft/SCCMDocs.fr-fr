---
title: "Options de ligne de commande pour le programme d’installation| System Center Configuration Manager"
description: "Utilisez les informations de cet article pour configurer des scripts ou installer System Center Configuration Manager à partir d’une ligne de commande."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7d1f55786a42650395fcb66ee4917434feecb630

---
# <a name="command-line-options-for-setup-for-system-center-configuration-manager"></a>Options de ligne de commande pour le programme d’installation pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 Utilisez les informations des tableaux suivants quand vous configurez des scripts ou installez System Center Configuration Manager à partir d’une ligne de commande.  

##  <a name="a-namebkmksetupa-command-line-options-for-setup"></a><a name="bkmk_setup"></a> Options de ligne de commande pour le programme d’installation  
 **/DEINSTALL**  
 Désinstalle le site. Vous devez exécuter le programme d'installation à partir de l'ordinateur sur lequel est installé le serveur de site.  

 **/DONTSTARTSITECOMP**  
 Installe un site, mais empêche le démarrage du service Gestionnaire de composant de site. Tant que le service Gestionnaire de composant de site n'a pas démarré, le site n'est pas actif. Le Gestionnaire de composant de site est responsable de l'installation et du démarrage du service SMS_Executive, ainsi que d'autres processus au niveau du site. Une fois l'installation du site terminée, lorsque vous démarrez le service Gestionnaire de composant de site, ce dernier installe alors le service SMS_Executive et d'autres processus nécessaires au fonctionnement du site.  

 **/HIDDEN**  
 Masque l'interface utilisateur pendant l'installation. Cette option doit être utilisée conjointement avec l’option **/SCRIPT** , et le fichier de script sans assistance doit fournir toutes les options requises, sans quoi l’installation échoue.  

 **/NOUSERINPUT**  
 Désactive l'entrée utilisateur pendant l'installation, mais affiche l'interface de l' **Assistant Installation** . Cette option doit être utilisée conjointement avec l’option **/SCRIPT** , et le fichier de script sans assistance doit fournir toutes les options requises, sans quoi l’installation échoue.  

 **/RESETSITE**  
 Effectue une réinitialisation du site qui permet de réinitialiser la base de données et les comptes de service du site. Vous devez exécuter le programme d’installation à partir de **&lt;CheminInstallationConfigMgr\>\BIN\X64** sur le serveur de site. Pour plus d’informations sur la réinitialisation du site, consultez la section [Exécuter une réinitialisation de site](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) de la rubrique [Modifier votre infrastructure System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/TESTDBUPGRADE &lt;*nom_instance/nom_base_de_données*>**  
 Effectue un test sur une sauvegarde de la base de données du site pour vérifier qu'elle peut être mise à niveau. Vous devez fournir le nom d'instance et le nom de base de données pour la base de données de site. Si vous spécifiez uniquement le nom de la base de données, le programme d'installation utilise le nom de l'instance par défaut.  

> [!IMPORTANT]  
>  L'exécution de cette option de ligne de commande sur la base de données de votre site de production n'est pas prise en charge. Cette opération mettrait à niveau la base de données du site et risquerait de rendre votre site inutilisable.  

 **/UPGRADE**  
 Exécute une mise à niveau sans assistance d’un site. Lorsque vous utilisez /UPGRADE, vous devez également spécifier la clé du produit, y compris les tirets (-). En outre, vous devez spécifier le chemin d'accès aux fichiers de configuration requise du programme d'installation que vous avez téléchargés précédemment.  

 Exemple : **setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx &lt;chemin vers les fichiers du composant externe\>**  

 Pour plus d’informations sur les fichiers requis par le programme d’installation, consultez la section  [Téléchargeur d’installation](#bkmk_SetupDownloader) dans cette rubrique.  

 **/SCRIPT &lt;*chemin_script_programme_installation*>**  
 Effectue des installations sans assistance. Un fichier d’initialisation du programme d’installation est nécessaire quand vous utilisez l’option **/SCRIPT**. Pour plus d’informations sur l’exécution du programme d’installation sans assistance, consultez [Installer des sites à l’aide d’une ligne de commande](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/SDKINST &lt;*nom_domaine_complet*>**  
 Installe le fournisseur SMS sur l'ordinateur spécifié. Vous devez fournir le nom de domaine complet pour l'ordinateur du fournisseur SMS. Pour plus d’informations sur le fournisseur SMS, consultez [Planifier le fournisseur SMS pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/SDKDEINST &lt;*nom_domaine_complet*>**  
 Désinstalle le fournisseur SMS sur l'ordinateur spécifié. Vous devez fournir le nom de domaine complet pour l'ordinateur du fournisseur SMS.  

 **/MANAGELANGS &lt;*chemin_script_langue*>**  
 Gère les langues installées sur un site installé précédemment. Pour utiliser cette option, vous devez exécuter le programme d’installation à partir de **&lt;CheminInstallationConfigMgr\>\BIN\X64** sur le serveur de site et spécifier l’emplacement du fichier de script de langue contenant les paramètres de langue. Pour plus d’informations sur les options de langue disponibles dans le fichier de jeu de caractères, consultez la section [Options de ligne de commande pour gérer les langues](#bkmk_Lang) dans cette rubrique.  

##  <a name="a-namebkmklanga-command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a> Options de ligne de commande pour gérer les langues  
 **Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** ManageLanguages  

    -   **Détails :** gère la prise en charge des langues de serveur, de client et de client mobile d’un site.  

**Options**  

-   **Nom de clé :** AddServerLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** spécifie les langues de serveur qui seront disponibles pour la console Configuration Manager, les rapports et les objets Configuration Manager. L'anglais est disponible par défaut.  

-   **Nom de clé :** AddClientLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** spécifie les langues qui seront disponibles sur les ordinateurs clients. L'anglais est disponible par défaut.  

-   **Nom de clé :** DeleteServerLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** spécifie les langues à supprimer qui ne seront plus disponibles pour la console Configuration Manager, les rapports et les objets Configuration Manager. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** DeleteClientLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** spécifie les langues à supprimer qui ne seront plus disponibles sur les ordinateurs clients. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** MobileDeviceLanguage  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si les langues du client d’appareil mobile sont installées.  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = téléchargement  

         1 = déjà téléchargé  

    -   **Détails :** spécifie si les fichiers d’installation prérequis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur 0, le programme d'installation télécharge les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*chemin_fichiers_requis_programme_installation*>  

    -   **Détails :** spécifie le chemin vers les fichiers d’installation prérequis. Selon la valeur **PrerequisiteComp** , le programme d'installation utilise ce chemin d'accès pour stocker les fichiers téléchargés ou pour localiser des fichiers précédemment téléchargés.  

##  <a name="a-namebkmkunattendeda-unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a> Clés du fichier de script d’installation sans assistance  
 Utilisez les sections suivantes pour vous aider à créer votre script d'installation sans assistance. Les tableaux répertorient les clés de script d'installation disponibles ainsi que leurs valeurs correspondantes, indiquent si elles sont obligatoires ou non, le type d'installation pour lequel elles sont utilisées, ainsi qu'une brève description de la clé.  

### <a name="unattended-install-for-a-central-administration-site"></a>Installation sans assistance d’un site d’administration centrale  
 Utilisez les détails suivants pour installer un site d’administration centrale à l’aide d’un fichier de script d’installation sans assistance.  

**Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** InstallCAS  

    -   **Détails :** installe un site d’administration centrale.  

**Options**  

-   **Nom de clé :** ProductID  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *Eval*  

    -   **Détails :** Spécifie la clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  

-   **Nom de clé :** SiteCode  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*code_site*>  

    -   **Détails :** spécifie les trois caractères alphanumériques qui identifient le site de manière unique dans votre hiérarchie.  

-   **Nom de clé :** SiteName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*nom_site*>  

    -   **Détails :** spécifie le nom de ce site.  

-   **Nom de clé :** SMSInstallDir  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *CheminInstallationConfigMgr*  

    -   **Détails :** spécifie le dossier d’installation des fichiers programmes de Configuration Manager.  

-   **Nom de clé :** SDKServer  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*nom de domaine complet du fournisseur SMS*>  

    -   **Détails :** spécifie le FQDN du serveur qui héberge le fournisseur SMS.  
        Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale.  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = téléchargement  

         1 = déjà téléchargé  

    -   **Détails :** spécifie si les fichiers d’installation prérequis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur 0, le programme d'installation va télécharger les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*chemin_fichiers_requis_programme_installation*>  

    -   **Détails :** spécifie le chemin vers les fichiers d’installation prérequis. Selon la valeur PrerequisiteComp, le programme d'installation utilise ce chemin d'accès pour stocker les fichiers téléchargés ou localiser des fichiers téléchargés précédemment.  

-   **Nom de clé :** AdminConsole  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si la console Configuration Manager doit ou non être installée.  

-   **Nom de clé :** JoinCEIP  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas joindre  

         1 = joindre  

    -   **Détails :** spécifie si vous voulez vous joindre au programme d’amélioration de l’expérience utilisateur.  

-   **Nom de clé :** AddServerLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** spécifie les langues de serveur qui seront disponibles pour la console Configuration Manager, les rapports et les objets Configuration Manager. L'anglais est disponible par défaut.  

-   **Nom de clé :** AddClientLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** spécifie les langues qui seront disponibles sur les ordinateurs clients. L'anglais est disponible par défaut.  

-   **Nom de clé :** DeleteServerLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** modifie un site après son installation.  
        Spécifie les langues à supprimer qui ne seront plus disponibles pour la console Configuration Manager, les rapports et les objets Configuration Manager. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** DeleteClientLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** modifie un site après son installation.  
        Spécifie les langues à supprimer qui ne seront plus disponibles pour les ordinateurs clients. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** MobileDeviceLanguage  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si les langues du client d’appareil mobile sont installées.  

**SQLConfigOptions**  

-   **Nom de clé :** SQLServerName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *SQLServerName*  

    -   **Détails :** spécifie le nom du serveur ou le nom de l’instance en cluster exécutant SQL Server. Il hébergera la base de données de site.  

-   **Nom de clé :** DatabaseName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *&lt;nom_base_de_données_site\>* ou *&lt;nom_instance\>\&lt;nom_base_de_données_site\>*  

    -   **Détails :**  

         Spécifie le nom de la base de données SQL Server à créer ou utiliser pour installer la base de données du site d'administration centrale.  

        > [!IMPORTANT]  
        >  Si vous n'utilisez pas l'instance par défaut, vous devez spécifier le nom d'instance et le nom de base de données de site.  

-   **Nom de clé :** SQLSSBPort  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*numéro_port_SSB*>  

    -   **Détails :** spécifie le port SQL Server Service Broker (SSB) que SQL Server utilise. Généralement, SSB est configuré pour utiliser le port TCP 4022, mais d'autres ports sont pris en charge.  

-   **Nom de clé :** SQLDataFilePath  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*chemin d’accès au fichier .MDB de la base de données*>  

    -   **Détails :** spécifie un autre emplacement pour créer le fichier .MDB de la base de données.  

-   **Nom de clé :** SQLLogFilePath  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*chemin d’accès au fichier .LDF de la base de données*>  

    -   **Détails :** spécifie un autre emplacement pour créer le fichier .LDF de la base de données.  

**CloudConnectorOptions**  

-   **Nom de clé :** CloudConnector  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si vous voulez installer un point de connexion de service sur ce site. Étant donné que le point de connexion de service peut uniquement être installé sur le site de niveau supérieur d’une hiérarchie, cette valeur doit être 0 pour un site principal enfant.  

-   **Nom de clé :** CloudConnectorServer  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** &lt;*nom de domaine complet du serveur de point de connexion de service*>  

    -   **Détails :** spécifie le nom de domaine complet du serveur qui hébergera le rôle de système de site de point de connexion de service.  

-   **Nom de clé :** UseProxy  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** indique si le point de connexion de service utilisera un serveur proxy.  

-   **Nom de clé :** ProxyName  

    -   **Obligatoire :** obligatoire quand UseProxy est égal à 1  

    -   **Valeurs :** &lt;*nom de domaine complet du serveur proxy*>  

    -   **Détails :** spécifie le nom de domaine complet du serveur proxy qui sera utilisé par le rôle de système de site de point de connexion de service.  

-   **Nom de clé :** ProxyPort  

    -   **Obligatoire :** obligatoire quand UseProxy est égal à 1  

    -   **Valeurs :** &lt;*numéro_port*>  

    -   **Détails :** spécifie le numéro de port à utiliser.  

### <a name="unattended-install-for-a-primary-site"></a>Installation sans assistance d’un site principal  
Utilisez les détails suivants pour installer un site principal à l’aide d’un fichier de script d’installation sans assistance.  

Utilisez les détails suivants pour installer un site d’administration centrale à l’aide d’un fichier de script d’installation sans assistance.  

**Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** InstallPrimarySite  

    -   **Détails :** installe un site principal.  

**Options**  

-   **Nom de clé :** ProductID  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *Eval*  

    -   **Détails :** Spécifie la clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  

-   **Nom de clé :** SiteCode  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*code_site*>  

    -   **Détails :** spécifie les trois caractères alphanumériques qui identifient le site de manière unique dans votre hiérarchie.  

-   **Nom de clé :** SiteName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*nom_site*>  

    -   **Détails :** spécifie le nom de ce site.  

-   **Nom de clé :** SMSInstallDir  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *CheminInstallationConfigMgr*  

    -   **Détails :** spécifie le dossier d’installation des fichiers programmes de Configuration Manager.  

-   **Nom de clé :** SDKServer  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*nom de domaine complet du fournisseur SMS*>  

    -   **Détails :** spécifie le FQDN du serveur qui héberge le fournisseur SMS.  
        Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale.  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = téléchargement  

         1 = déjà téléchargé  

    -   **Détails :** spécifie si les fichiers d’installation prérequis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur 0, le programme d'installation va télécharger les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*chemin_fichiers_requis_programme_installation*>  

    -   **Détails :** spécifie le chemin vers les fichiers d’installation prérequis. Selon la valeur **PrerequisiteComp** , le programme d'installation utilise ce chemin d'accès pour stocker les fichiers téléchargés ou pour localiser des fichiers précédemment téléchargés.  

-   **Nom de clé :** AdminConsole  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si la console Configuration Manager doit ou non être installée.  

-   **Nom de clé :** JoinCEIP  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas joindre  

         1 = joindre  

    -   **Détails :** spécifie si vous voulez vous joindre au programme d’amélioration de l’expérience utilisateur.  

-   **Nom de clé :** ManagementPoint  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*nom de domaine complet du serveur de site du point de gestion*>  

    -   **Détails :** spécifie le nom de domaine complet du serveur qui hébergera le rôle de système de site de point de gestion.  

-   **Nom de clé :** ManagementPointProtocol  

    -   **Obligatoire :** non  

    -   **Valeurs :** HTTPS ou HTTP  

    -   **Détails :** spécifie le protocole à utiliser pour le point de gestion.  

-   **Nom de clé :** DistributionPoint  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*nom de domaine complet du serveur de site du point de distribution*>  

    -   **Détails :** spécifie le protocole à utiliser pour le point de gestion.  

-   **Nom de clé :** DistributionPointProtocol  

    -   **Obligatoire :** non  

    -   **Valeurs :** HTTPS ou HTTP  

    -   **Détails :** spécifie le protocole à utiliser pour le point de distribution.  

-   **Nom de clé :** RoleCommunicationProtocol  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** EnforceHTTPS ou HTTPorHTTPS  

    -   **Détails :** spécifie s’il convient de configurer tous les systèmes de site pour n’accepter que les communications HTTPS à partir de clients ou pour la méthode de communication à configurer pour chaque rôle de système de site. Lorsque vous sélectionnez **EnforceHTTPS**, l'ordinateur client doit disposer d'un certificat PKI valide pour l'authentification du client.  

-   **Nom de clé :** ClientsUsePKICertificate  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas utiliser  

         1 = utiliser  

    -   **Détails :** spécifie si les clients utiliseront un certificat PKI de client pour communiquer avec les rôles de système de site.  

-   **Nom de clé :** AddServerLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** spécifie les langues de serveur qui seront disponibles pour la console Configuration Manager, les rapports et les objets Configuration Manager. L'anglais est disponible par défaut.  

-   **Nom de clé :** AddClientLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** spécifie les langues qui seront disponibles sur les ordinateurs clients. L'anglais est disponible par défaut.  

-   **Nom de clé :** DeleteServerLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** modifie un site après son installation.  
        Spécifie les langues à supprimer qui ne seront plus disponibles pour la console Configuration Manager, les rapports et les objets Configuration Manager. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** DeleteClientLanguages  

    -   **Obligatoire :** non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** modifie un site après son installation.  
        Spécifie les langues à supprimer qui ne seront plus disponibles pour les ordinateurs clients. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** MobileDeviceLanguage  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si les langues du client d’appareil mobile sont installées.  

**SQLConfigOptions**  

-   **Nom de clé :** SQLServerName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *SQLServerName*  

    -   **Détails :** spécifie le nom du serveur ou le nom de l’instance en cluster exécutant SQL Server. Il hébergera la base de données de site.  

-   **Nom de clé :** DatabaseName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *&lt;nom_base_de_données_site\>* ou *&lt;nom_instance\>\&lt;nom_base_de_données_site\>*  

    -   **Détails :**  

         Spécifie le nom de la base de données SQL Server à créer ou utiliser pour installer la base de données du site principal.  

        > [!IMPORTANT]  
        >  Si vous n'utilisez pas l'instance par défaut, vous devez spécifier le nom d'instance et le nom de base de données de site.  

-   **Nom de clé :** SQLSSBPort  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*numéro_port_SSB*>  

    -   **Détails :** spécifie le port SQL Server Service Broker (SSB) que SQL Server utilise. Généralement, SSB est configuré pour utiliser le port TCP 4022, mais d'autres ports sont pris en charge.  

-   **Nom de clé :** SQLDataFilePath  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*chemin d’accès au fichier .MDB de la base de données*>  

    -   **Détails :** spécifie un autre emplacement pour créer le fichier .MDB de la base de données.  

-   **Nom de clé :** SQLLogFilePath  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*chemin d’accès au fichier .LDF de la base de données*>  

    -   **Détails :** spécifie un autre emplacement pour créer le fichier .LDF de la base de données.  

**HierarchyExpansionOption**  

-   **Nom de clé :** CCARSiteServer  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*nom de domaine complet du site d’administration centrale*>  

    -   **Détails :** spécifie le site d’administration centrale auquel un site principal s’attache quand il rejoint la hiérarchie Configuration Manager. Vous devez spécifier le site d'administration centrale lors de l'installation.  

-   **Nom de clé :** CASRetryInterval  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*intervalle*>  

    -   **Détails :** spécifie l’intervalle (en minutes) avant une nouvelle tentative de connexion au site d’administration centrale après un échec de connexion. Par exemple, en cas d'échec de la connexion au site d'administration centrale, le site principal attend le nombre de minutes que vous avez spécifié pour CASRetryInterval et essaie de nouveau d'établir une connexion.  

-   **Nom de clé :** WaitForCASTimeout  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*délai d’attente*>  

         Valeur de 0 à 100.  

    -   **Détails :** spécifie la valeur maximale du délai d’attente (en minutes) d’un site principal qui se connecte au site d’administration centrale. Par exemple, si un site principal ne parvient pas à se connecter à un site d'administration centrale, le site principal essaie de nouveau d'établir une connexion en fonction de la valeur de CASRetryInterval jusqu'à ce que le délai WaitForCASTimeout soit atteint. Vous pouvez spécifier une valeur de 0 à 100.  

**CloudConnectorOptions**  

-   **Nom de clé :** CloudConnector  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si vous voulez installer un point de connexion de service sur ce site. Étant donné que le point de connexion de service peut uniquement être installé sur le site de niveau supérieur d’une hiérarchie, cette valeur doit être 0 pour un site principal enfant.  

-   **Nom de clé :** CloudConnectorServer  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** &lt;*nom de domaine complet du serveur de point de connexion de service*\>  

    -   **Détails :** spécifie le nom de domaine complet du serveur qui hébergera le rôle de système de site de point de connexion de service.  

-   **Nom de clé :** UseProxy  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** indique si le point de connexion de service utilisera un serveur proxy.  

-   **Nom de clé :** ProxyName  

    -   **Obligatoire :** obligatoire quand UseProxy est égal à 1  

    -   **Valeurs :** &lt;*nom de domaine complet du serveur proxy*>  

    -   **Détails :** spécifie le nom de domaine complet du serveur proxy qui sera utilisé par le rôle de système de site de point de connexion de service.  

-   **Nom de clé :** ProxyPort  

    -   **Obligatoire :** obligatoire quand UseProxy est égal à 1  

    -   **Valeurs :** &lt;*numéro_port*>  

    -   **Détails :** spécifie le numéro de port à utiliser.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Récupération sans assistance d’un site d’administration centrale  
 Utilisez les détails suivants pour récupérer un site d’administration centrale à l’aide d’un fichier de script d’installation sans assistance.  

**Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** RecoverCCAR  

    -   **Détails :** récupère un site d’administration centrale.  

**RecoveryOptions**  

-   **Nom de clé :** ServerRecoveryOptions  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 1, 2 ou 4  

         1 = Serveur de site de récupération et SQL Server.  

         2 = Récupérer le serveur de site uniquement.  

         4 = Récupérer SQL Server uniquement.  

    -   **Détails :** spécifie si le programme d’installation doit récupérer le serveur de site, SQL Server ou les deux. Les clés associées sont requises lorsque vous définissez la valeur suivante pour le paramètre ServerRecoveryOptions :  

        -   Valeur = 1 : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site à l’aide d’une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

        -   Valeur = 2 : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site à l’aide d’une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

        -   Valeur = 4 : la clé **BackupLocation** est obligatoire si vous attribuez la valeur **10** à la clé **DatabaseRecoveryOptions** afin de restaurer la base de données du site à partir d’une sauvegarde.  

-   **Nom de clé :** DatabaseRecoveryOptions  

    -   **Obligatoire :** cette clé est obligatoire quand la valeur du paramètre ServerRecoveryOptions est **1** ou **4**.  

    -   **Valeurs :** 10, 20, 40, 80  

         10 = Restaurer la base de données du site à partir d'une sauvegarde.  

         20 = Utiliser une base de données de site qui a été récupérée manuellement à l'aide d'une autre méthode.  

         40 = Créer une nouvelle base de données de site. Utilisez cette option lorsqu'aucune sauvegarde de base de données de site n'est disponible. Les données globales et de site sont récupérées via la réplication à partir d'autres sites.  

         80 = Ignorer la récupération de base de données.  

    -   **Détails :** spécifie comment le programme d’installation récupère la base de données du site dans SQL Server.  

-   **Nom de clé :** ReferenceSite  

    -   **Obligatoire :** cette clé est obligatoire quand la valeur du paramètre **DatabaseRecoveryOptions** est **40**.  

    -   **Valeurs :** &lt;*nom_domaine_complet_site_référence*>  

    -   **Détails :** spécifie le site principal de référence que le site d’administration centrale utilise pour récupérer des données globales si la sauvegarde de la base de données est antérieure à la période de rétention du suivi des modifications ou quand vous récupérez le site sans sauvegarde.  

         Lorsque vous ne spécifiez pas de site de référence et que la sauvegarde est antérieure à la période de rétention du suivi des modifications, tous les sites principaux sont réinitialisés avec les données restaurées à partir du site d'administration centrale.  

         Lorsque vous ne spécifiez pas de site de référence et que la sauvegarde est comprise dans la période de rétention du suivi des modifications, seules les modifications apportées après la sauvegarde sont répliquées à partir des sites principaux. Lorsqu'il existe des conflits entre des modifications issues de différents sites principaux, le site d'administration centrale utilise la première modification reçue.  

-   **Nom de clé :** SiteServerBackupLocation  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*chemin_vers_jeu_sauvegarde_serveur_site*>  

    -   **Détails :** spécifie le chemin vers le jeu de sauvegarde du serveur de site. Cette clé est optionnelle lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **2**. Spécifiez une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l'aide d'une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

-   **Nom de clé :** BackupLocation  

    -   **Obligatoire :** cette clé est obligatoire quand vous configurez la valeur **1** ou **4** pour la clé **ServerRecoveryOptions**, et la valeur **10** pour la clé **DatabaseRecoveryOptions**.  

    -   **Valeurs :** &lt;*chemin_vers_jeu_sauvegarde_base_de_données_site*>  

    -   **Détails :** spécifie le chemin d’accès au jeu de sauvegarde de la base de données du site.  

**Options**  

-   **Nom de clé :** ProductID  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *Eval*  

    -   **Détails :** Spécifie la clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  

-   **Nom de clé :** SiteCode  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*code_site*>  

    -   **Détails :** spécifie les trois caractères alphanumériques qui identifient le site de manière unique dans votre hiérarchie. Vous devez spécifier le code de site que le site utilisait avant la défaillance. Pour plus d’informations sur les restrictions de code de site, consultez la section [À propos des noms de site et des codes de site](#bkmk_codes) dans cette rubrique.  

-   **Nom de clé :** SiteName  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*nom_site*>  

    -   **Détails :** spécifie le nom de ce site.  

-   **Nom de clé :** SMSInstallDir  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*CheminInstallationConfigMgr*>  

    -   **Détails :** spécifie le dossier d’installation des fichiers programmes de Configuration Manager.  

-   **Nom de clé :** SDKServer  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*nom de domaine complet du fournisseur SMS*>  

    -   **Détails :** spécifie le FQDN du serveur qui héberge le fournisseur SMS. Vous devez spécifier le serveur qui hébergeait le fournisseur SMS avant la défaillance.  

         Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale. Pour plus d’informations sur le fournisseur SMS, consultez [Planifier le fournisseur SMS pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = téléchargement  

         1 = déjà téléchargé  

    -   **Détails :** spécifie si les fichiers d’installation prérequis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur **0**, le programme d’installation télécharge les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*chemin_fichiers_requis_programme_installation*>  

    -   **Détails :** spécifie le chemin vers les fichiers d’installation prérequis. Selon la valeur **PrerequisiteComp** , le programme d'installation utilise ce chemin d'accès pour stocker les fichiers téléchargés ou pour localiser des fichiers précédemment téléchargés.  

-   **Nom de clé :** AdminConsole  

    -   **Obligatoire :** cette clé est obligatoire sauf quand le paramètre **ServerRecoveryOptions** a la valeur **4**.  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si la console Configuration Manager doit ou non être installée.  

-   **Nom de clé :** JoinCEIP  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas joindre  

         1 = joindre  

    -   **Détails :** spécifie si vous voulez vous joindre au programme d’amélioration de l’expérience utilisateur.  

**SQLConfigOptions**  

-   **Nom de clé :** SQLServerName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *SQLServerName*  

    -   **Détails :** spécifie le nom du serveur ou le nom de l’instance en cluster exécutant SQL Server qui hébergera la base de données du site. Vous devez spécifier le serveur qui a hébergé la base de données de site avant la défaillance.  

-   **Nom de clé :** DatabaseName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *&lt;nom_base_de_données_site\>* ou *&lt;nom_instance\>\&lt;nom_base_de_données_site\>*  

    -   **Détails :**  

         Spécifie le nom de la base de données SQL Server à créer ou utiliser pour installer la base de données du site d'administration centrale. Vous devez spécifier le nom de base de données qui était utilisé avant la défaillance.  

        > [!IMPORTANT]  
        >  Si vous n'utilisez pas l'instance par défaut, vous devez spécifier le nom d'instance et le nom de base de données de site.  

-   **Nom de clé :** SQLSSBPort  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*numéro_port_SSB*>  

    -   **Détails :** spécifie le port SQL Server Service Broker (SSB) que SQL Server utilise. Généralement, SSB est configuré pour utiliser le port TCP 4022. Vous devez définir le même port SSB utilisé avant la défaillance.  

-   **Nom de clé :** SQLDataFilePath  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*chemin d’accès au fichier .MDB de la base de données*>  

    -   **Détails :** spécifie un autre emplacement pour créer le fichier .MDB de la base de données.  

-   **Nom de clé :** SQLLogFilePath  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*chemin d’accès au fichier .LDF de la base de données*>  

    -   **Détails :** spécifie un autre emplacement pour créer le fichier .LDF de la base de données.  

**CloudConnectorOptions**  

-   **Nom de clé :** CloudConnector  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si vous voulez installer un point de connexion de service sur ce site. Étant donné que le point de connexion de service peut uniquement être installé sur le site de niveau supérieur d’une hiérarchie, cette valeur doit être 0 pour un site principal enfant.  

-   **Nom de clé :** CloudConnecorServer  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** &lt;*nom de domaine complet du serveur de point de connexion de service*>  

    -   **Détails :** spécifie le nom de domaine complet du serveur qui hébergera le rôle de système de site de point de connexion de service.  

-   **Nom de clé :** UseProxy  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** indique si le point de connexion de service utilisera un serveur proxy.  

-   **Nom de clé :** ProxyName  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** &lt;*nom de domaine complet du serveur proxy*>  

    -   **Détails :** spécifie le nom de domaine complet du serveur proxy qui sera utilisé par le rôle de système de site de point de connexion de service.  

-   **Nom de clé :** ProxyPort  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** &lt;*numéro_port*>  

    -   **Détails :** spécifie le numéro de port à utiliser.  

### <a name="unattended-recovery-for-a-primary-site"></a>Récupération sans assistance d’un site principal  
 Utilisez les détails suivant pour récupérer un site principal à l’aide d’un fichier de script d’installation sans assistance.  

**Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** site_principal_à_récupérer  

    -   **Détails :** récupère un site principal.  

**RecoveryOptions**  

-   **Nom de clé :** ServerRecoveryOptions  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 1, 2 ou 4  

         1 = Serveur de site de récupération et SQL Server.  

         2 = Récupérer le serveur de site uniquement.  

         4 = Récupérer SQL Server uniquement.  

    -   **Détails :** spécifie si le programme d’installation doit récupérer le serveur de site, SQL Server ou les deux. Les clés associées sont requises lorsque vous définissez la valeur suivante pour le paramètre ServerRecoveryOptions :  

        -   Valeur = 1 : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site à l’aide d’une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

        -   Valeur = 2 : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site à l’aide d’une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

        -   Valeur = 4 : la clé **BackupLocation** est obligatoire si vous attribuez la valeur **10** à la clé **DatabaseRecoveryOptions** afin de restaurer la base de données du site à partir d’une sauvegarde.  

-   **Nom de clé :** DatabaseRecoveryOptions  

    -   **Obligatoire :** cette clé est obligatoire quand la valeur du paramètre ServerRecoveryOptions est **1** ou **4**.  

    -   **Valeurs :** 10, 20, 40, 80  

         10 = Restaurer la base de données du site à partir d'une sauvegarde.  

         20 = Utiliser une base de données de site qui a été récupérée manuellement à l'aide d'une autre méthode.  

         40 = Créer une nouvelle base de données de site. Utilisez cette option lorsqu'aucune sauvegarde de base de données de site n'est disponible. Les données globales et de site sont récupérées via la réplication à partir d'autres sites.  

         80 = Ignorer la récupération de base de données.  

    -   **Détails :** spécifie comment le programme d’installation récupère la base de données du site dans SQL Server.  

-   **Nom de clé :** SiteServerBackupLocation  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*chemin_vers_jeu_sauvegarde_serveur_site*>  

    -   **Détails :**  

         Spécifie le chemin d'accès au jeu de sauvegarde du serveur de site. Cette clé est facultative si le paramètre **ServerRecoveryOptions** a la valeur **1** ou **2**. Spécifiez une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l'aide d'une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

-   **Nom de clé :** BackupLocation  

    -   **Obligatoire :** cette clé est obligatoire quand vous configurez la valeur **1** ou **4** pour la clé **ServerRecoveryOptions**, et la valeur **10** pour la clé **DatabaseRecoveryOptions**.  

    -   **Valeurs :** &lt;*chemin_vers_jeu_sauvegarde_base_de_données_site*>  

    -   **Détails :** spécifie le chemin d’accès au jeu de sauvegarde de la base de données du site.  

**Options**  

-   **Nom de clé :** ProductID  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *Eval*  

    -   **Détails :** Spécifie la clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  

-   **Nom de clé :** SiteCode  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*code_site*>  

    -   **Détails :** spécifie les trois caractères alphanumériques qui identifient le site de manière unique dans votre hiérarchie. Vous devez spécifier le code de site que le site utilisait avant la défaillance. Pour plus d’informations sur les restrictions de code de site, consultez la section [À propos des noms de site et des codes de site](#bkmk_codes) dans cette rubrique.  

-   **Nom de clé :** SiteName  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*nom_site*>  

    -   **Détails :** spécifie le nom de ce site.  

-   **Nom de clé :** SMSInstallDir  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*CheminInstallationConfigMgr*>  

    -   **Détails :** spécifie le dossier d’installation des fichiers programmes de Configuration Manager.  

-   **Nom de clé :** SDKServer  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*nom de domaine complet du fournisseur SMS*>  

    -   **Détails :** spécifie le FQDN du serveur qui héberge le fournisseur SMS. Vous devez spécifier le serveur qui hébergeait le fournisseur SMS avant la défaillance. Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale. Pour plus d’informations sur le fournisseur SMS, consultez [Planifier le fournisseur SMS pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = téléchargement  

         1 = déjà téléchargé  

    -   **Détails :** spécifie si les fichiers d’installation prérequis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur **0**, le programme d’installation télécharge les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*chemin_fichiers_requis_programme_installation*>  

    -   **Détails :** spécifie le chemin vers les fichiers d’installation prérequis. Selon la valeur **PrerequisiteComp** , le programme d'installation utilise ce chemin d'accès pour stocker les fichiers téléchargés ou pour localiser des fichiers précédemment téléchargés.  

-   **Nom de clé :** AdminConsole  

    -   **Obligatoire :** cette clé est obligatoire sauf quand le paramètre **ServerRecoveryOptions** a la valeur **4**.  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si la console Configuration Manager doit ou non être installée.  

-   **Nom de clé :** JoinCEIP  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas joindre  

         1 = joindre  

    -   **Détails :** spécifie si vous voulez vous joindre au programme d’amélioration de l’expérience utilisateur.  

**SQLConfigOptions**  

-   **Nom de clé :** SQLServerName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *SQLServerName*  

    -   **Détails :** spécifie le nom du serveur ou le nom de l’instance en cluster exécutant SQL Server qui hébergera la base de données du site. Vous devez spécifier le serveur qui a hébergé la base de données de site avant la défaillance.  

-   **Nom de clé :** DatabaseName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*nom_base_de_données_site*\> ou &lt;*nom_instance*\>\\&lt;*nom_base_de_données_site*\>

    -   **Détails :**  

         Spécifie le nom de la base de données SQL Server à créer ou utiliser pour installer la base de données du site d'administration centrale. Vous devez spécifier le nom de base de données qui était utilisé avant la défaillance.  

        > [!IMPORTANT]  
        >  Si vous n'utilisez pas l'instance par défaut, vous devez spécifier le nom d'instance et le nom de base de données de site.  

-   **Nom de clé :** SQLSSBPort  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*numéro_port_SSB*>  

    -   **Détails :** spécifie le port SQL Server Service Broker (SSB) que SQL Server utilise. Généralement, SSB est configuré pour utiliser le port TCP 4022. Vous devez définir le même port SSB utilisé avant la défaillance.  

-   **Nom de clé :** SQLDataFilePath  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*chemin d’accès au fichier .MDB de la base de données*>  

    -   **Détails :** spécifie un autre emplacement pour créer le fichier .MDB de la base de données.  

-   **Nom de clé :** SQLLogFilePath  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*chemin d’accès au fichier .LDF de la base de données*>  

    -   **Détails :** spécifie un autre emplacement pour créer le fichier .LDF de la base de données.  

**HierarchyExpansionOptions**  

-   **Nom de clé :** CCARSiteServer  

    -   **Obligatoire :** afficher les détails.  

    -   **Valeurs :** &lt;*code_site_pour_site_administration_centrale*>  

    -   **Détails :** spécifie le site d’administration centrale auquel un site principal s’attache quand il rejoint la hiérarchie Configuration Manager. Ce paramètre est requis si le site principal était attaché à un site d'administration centrale avant la défaillance. Vous devez spécifier le code de site qui était utilisé pour le site d'administration centrale avant la défaillance.  

-   **Nom de clé :** CASRetryInterval  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*intervalle*>  

    -   **Détails :** spécifie l’intervalle (en minutes) avant une nouvelle tentative de connexion au site d’administration centrale après un échec de connexion. Par exemple, en cas d'échec de la connexion au site d'administration centrale, le site principal attend le nombre de minutes que vous avez spécifié pour **CASRetryInterval**et essaie de nouveau d'établir une connexion.  

-   **Nom de clé :** WaitForCASTimeout  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*délai d’attente*>  

    -   **Détails :** spécifie la valeur maximale du délai d’attente (en minutes) d’un site principal qui se connecte au site d’administration centrale. Par exemple, si un site principal ne parvient pas à se connecter à un site d'administration centrale, le site principal essaie de nouveau d'établir une connexion en fonction de la valeur de **CASRetryInterval** jusqu'à ce que le délai **WaitForCASTimeout** soit atteint. Vous pouvez spécifier une valeur de 0 à 100.  

**CloudConnectorOptions**  

-   **Nom de clé :** CloudConnector  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si vous voulez installer un point de connexion de service sur ce site. Étant donné que le point de connexion de service peut uniquement être installé sur le site de niveau supérieur d’une hiérarchie, cette valeur doit être 0 pour un site principal enfant.  

-   **Nom de clé :** CloudConnecorServer  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** &lt;*nom de domaine complet du serveur de point de connexion de service*>  

    -   **Détails :** spécifie le nom de domaine complet du serveur qui hébergera le rôle de système de site de point de connexion de service.  

-   **Nom de clé :** UseProxy  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** indique si le point de connexion de service utilisera un serveur proxy.  

-   **Nom de clé :** ProxyName  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** &lt;*nom de domaine complet du serveur proxy*>  

    -   **Détails :** spécifie le nom de domaine complet du serveur proxy qui sera utilisé par le rôle de système de site de point de connexion de service.  

-   **Nom de clé :** ProxyPort  

    -   **Obligatoire :** obligatoire quand CloudConnector est égal à 1  

    -   **Valeurs :** &lt;*numéro_port*>  

    -   **Détails :** spécifie le numéro de port à utiliser.  



<!--HONumber=Nov16_HO1-->


