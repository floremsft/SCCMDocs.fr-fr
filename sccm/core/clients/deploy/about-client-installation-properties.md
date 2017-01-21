---
title: "Propriétés d’installation du client | System Center Configuration Manager"
description: "Découvrez les propriétés d’installation du client dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: 15
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 3987e6a66f9c0f52da8ce9a8c29e35836d2a2bcb

---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>À propos des propriétés d’installation du client dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez la commande CCMSetup.exe de System Center Configuration Manager pour installer manuellement le logiciel client Configuration Manager sur les ordinateurs de votre entreprise.  

##  <a name="a-nameaboutccmsetupa-about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> À propos de CCMSetup.exe  
 La commande CCMSetup.exe télécharge tous les fichiers nécessaires à l’installation du client à partir d’un point de gestion ou d’un emplacement source spécifiés. Ces fichiers peuvent inclure :  

-   Le package Windows Installer Client.msi qui installe le logiciel client Configuration Manager.  

-   Les fichiers d'installation du service BITS (Background Intelligent Transfer Service) de Microsoft, s'ils sont requis.  

-   Les fichiers d'installation de Windows Installer, s'ils sont requis.  

-   Les mises à jour et correctifs du client Configuration Manager, s’ils sont requis.  

> [!NOTE]  
>  Dans Configuration Manger, vous ne pouvez pas exécuter le Fichier Client.msi directement.  

 CCMSetup.exe fournit plusieurs propriétés de ligne de commande permettant de personnaliser le comportement d'installation. De plus, vous pouvez également spécifier des propriétés pour modifier le comportement de Client.msi sur la ligne de commande CCMSetup.exe.  

> [!IMPORTANT]  
>  Vous devez spécifier toutes les propriétés CCMSetup requises avant d'indiquer les propriétés pour Client.msi.  

 CCMSetup.exe et ses fichiers de prise en charge résident sur le serveur de site Configuration Manager dans le sous-dossier **Client** du dossier d’installation de Configuration Manager. Ce dossier est partagé sur le réseau sous **&lt;Nom_Serveur_Site\>\SMS_&lt;Code_Site\>\Client**.  

 À l'invite de commandes, la commande CCMSetup.exe utilise le format suivant :  

 **CCMSetup.exe [&lt;propriétés Ccmsetup\>] [&lt;propriétés d’installation client.msi>]**  

 Exemple :  

 **CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01**  

 Cet exemple de commande effectue les actions suivantes :  

-   Force le point de gestion SMSMP01 à demander la liste des points de distribution afin de télécharger les fichiers source d'installation du client.  

-   Indique que l’installation doit s’arrêter si une version du client Configuration Manager existe déjà sur l’ordinateur.  

-   Ordonne à client.msi d'attribuer le client au code de site S01.  

-   Ordonne à client.msi d'utiliser le point d'état de secours nommé SMSFP01.  

> [!NOTE]  
>  Si une propriété contient des espaces, placez-la entre guillemets (" ").  

 Les propriétés décrites dans le tableau suivant sont disponibles pour modifier le comportement d'installation de CCMSetup.exe.  

> [!IMPORTANT]  
>  Si vous avez étendu le schéma Active Directory pour Configuration Manager, de nombreuses propriétés d’installation du client sont publiées dans les services de domaine Active Directory et automatiquement lues par le client Configuration Manager. Pour obtenir la liste des propriétés d’installation du client publiées dans les services de domaine Active Directory, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory dans System Center Configuration Manager](about-client-installation-properties-published-to-active-directory-domain-services.md).  

##  <a name="a-namebkmkccmsetupcommandlinea-ccmsetupexe-command-line-properties"></a><a name="BKMK_CCMSetupCommandLine"></a> Propriétés de ligne de commande CCMSetup.exe  

-   **/?**  

     Ouvre la boîte de dialogue **CCMSetup** affichant les propriétés de ligne de commande pour ccmsetup.exe.  

     Exemple : **ccmsetup.exe /?**  

-   **/source:&lt;Chemin\>**  

     Indique l'emplacement à partir duquel télécharger les fichiers d'installation. Vous pouvez indiquer un chemin d'installation local ou UNC. Les fichiers sont téléchargés à l'aide du protocole SMB (server message block).  

    > [!NOTE]  
    >  Vous pouvez utiliser la propriété **/source** plusieurs fois sur la ligne de commande pour indiquer d'autres emplacements à partir desquels télécharger les fichiers d'installation.  

    > [!IMPORTANT]  
    >  Pour utiliser la propriété de ligne de commande **/source** , le compte d'utilisateur Windows utilisé pour l'installation du client doit disposer d'autorisations de lecture sur l'emplacement d'installation.  

     Exemple : **ccmsetup.exe /source:"\\\ordinateur\dossier"**  

-   **/mp:&lt;Ordinateur\>**  

     Spécifie un point de gestion source auquel les ordinateurs peuvent se connecter pour trouver le point de distribution le plus proche afin d'y télécharger les fichiers d'installation du client. En l'absence de point de distribution ou si les ordinateurs ne peuvent pas télécharger les fichiers auprès des points de distribution au terme d'un délai de quatre heures, les clients téléchargent les fichiers auprès du point de gestion spécifié.  

     Les ordinateurs téléchargent les fichiers via une connexion HTTP ou HTTPS, selon la configuration du rôle de système de site des connexions client. Le téléchargement utilise la limitation BITS, si cette fonctionnalité est configurée. Si tous les points de distribution et de gestion sont configurés uniquement pour les connexions client HTTPS, vous devez vérifier que l'ordinateur client possède un certificat client d'infrastructure à clé publique (PKI) valide.  

    > [!NOTE]  
    >  Vous pouvez utiliser la propriété de ligne de commande **/mp** pour spécifier plusieurs points de gestion : dans ce cas, si l'ordinateur ne parvient pas à se connecter au premier point de gestion, il essaie de se connecter au deuxième, et ainsi de suite. Lorsque vous spécifiez plusieurs points de gestion, séparez les valeurs par des points-virgules.  

    > [!IMPORTANT]  
    >  Cette propriété est utilisée uniquement pour spécifier un point de gestion initial, afin de permettre aux ordinateurs de trouver la source la plus proche en vue de télécharger les fichiers d'installation du client. Elle n'indique pas le point de gestion auquel le client sera affecté après l'installation. Vous pouvez spécifier n’importe quel point de gestion Configuration Manager de n’importe quel site pour fournir aux ordinateurs une liste de points de distribution auprès desquels ils peuvent télécharger les fichiers d’installation du client.  

     Exemple utilisant le nom de l’ordinateur : **ccmsetup.exe /mp:SMSMP01**  

     Exemple utilisant le nom de domaine complet : **ccmsetup.exe /mp:smsmp01.contoso.com**  

    > [!TIP]  
    >  Si le client se connecte à un point de gestion via le protocole HTTPS, vous devez en général spécifier le nom de domaine complet plutôt que le nom de l'ordinateur. La valeur que vous spécifiez doit être indiquée dans le nom d'objet ou dans l'autre nom d'objet du certificat d'infrastructure à clé publique du point de gestion. Même si Configuration Manager prend uniquement en charge un nom d’ordinateur dans ce certificat PKI pour les connexions intranet, il est recommandé d’utiliser un nom de domaine complet pour plus de sécurité.  

-   **/retry:&lt;Minutes\>**  

     Indique l'intervalle entre les tentatives si CCMSetup.exe ne parvient pas à télécharger les fichiers d'installation. La valeur par défaut est **10** minutes. CCMSetup renouvelle les tentatives jusqu'à atteindre la limite indiquée dans la propriété d'installation **downloadtimeout** .  

     Exemple : **ccmsetup.exe /retry:20**  

-   **/noservice**  

     Empêche l'exécution de CCMSetup en tant que service. Lorsque CCMSetup est exécuté en tant que service, il s'exécute dans le contexte du compte système local de l'ordinateur, qui peut ne pas disposer des droits suffisants pour accéder aux ressources réseau requises dans le cadre du processus d'installation. Lorsque vous spécifiez l'option **/noservice** , CCMSetup.exe s'exécute dans le contexte du compte d'utilisateur que vous utilisez pour démarrer le processus d'installation. En outre, si vous utilisez un script pour exécuter CCMSetup.exe avec la propriété **/service** , le processus CCMSetup.exe s'arrête dès le démarrage du service et risque de ne pas renvoyer correctement les détails sur l'installation, car le service CCMSetup s'occupe de l'installation du client. Si cette propriété de ligne de commande n'est pas spécifiée, par défaut, **/service** sera utilisé.  

     Exemple : **ccmsetup.exe /noservice**  

-   **/service**  

     Indique que CCMSetup doit s'exécuter comme un service qui utilise le compte système local.  

     Exemple : **ccmsetup.exe /service**  

-   **/uninstall**  

     Indique que le logiciel client Configuration Manager doit être désinstallé. Pour plus d'informations, voir [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md).  

     Exemple : **ccmsetup.exe /uninstall**  

-   **/logon**  

     Indique que l’installation du client doit s’arrêter si une version de Configuration ou du client Configuration Manager est déjà installée.  

     Exemple : **ccmsetup.exe /logon**  

-   **/forcereboot**  

     Indique que CCMSetup doit forcer l'ordinateur client à redémarrer si nécessaire pour terminer l'installation du client. Si cette option n'est pas spécifiée, CCMSetup se ferme lorsqu'un redémarrage est nécessaire et continue après le prochain redémarrage manuel.  

     Exemple : **CCMSetup.exe /forcereboot**  

-   **/BITSPriority:&lt;Priorité\>**  

     Indique la priorité de téléchargement lorsque les fichiers d'installation du client sont téléchargés via une connexion HTTP. Les valeurs possibles sont les suivantes :  

    -   FOREGROUND (avant-plan)  

    -   HIGH (élevée)  

    -   NORMAL (normale)  

    -   LOW (faible)  

     La valeur par défaut est NORMAL.  

     Exemple : **ccmsetup.exe /BITSPriority:HIGH**  

-   **/downloadtimeout:&lt;Minutes\>**  

     Indique la durée, en minutes, pendant laquelle CCMSetup essaie de télécharger les fichiers d'installation du client avant d'abandonner. La valeur par défaut est **1 440** minutes (1 jour).  

     Exemple : **ccmsetup.exe /downloadtimeout:100**  

-   **/UsePKICert**  

     Lorsque ce paramètre est spécifié, le client utilise un certificat PKI qui inclut l'authentification du client, s'il est disponible. Si aucun certificat valide n'est trouvé, le client se replie sur l'utilisation d'une connexion HTTP et un certificat auto-signé. Lorsque cette option n'est pas spécifiée, le client utilise un certificat auto-signé et toutes les communications vers les systèmes de site s'effectuent sur HTTP.  

    > [!NOTE]  
    >  Dans certains cas, il n'est pas nécessaire de spécifier cette propriété lorsque vous installez un client pour utiliser un certificat client PKI. Ces scénarios qui comprennent l'installation d'un client recourent à une installation poussée du client et à une installation basée sur le point de mise à jour logicielle. Toutefois, vous devez indiquer cette propriété à chaque fois que vous installez un client manuellement et utiliser la propriété **/mp** pour indiquer un point de gestion qui est configuré pour accepter uniquement les connexions client HTTPS. Vous devez également spécifier cette propriété lorsque vous installez un client pour la communication Internet uniquement, en utilisant la propriété CCMALWAYSINF=1 (conjointement avec les propriétés pour le point de gestion basé sur Internet et le code de site). Pour plus d’informations sur la gestion du client basée sur Internet, consultez [Éléments à prendre en considération pour les communications de clients à partir d’Internet ou d’une forêt non approuvée](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) dans [Communications entre points de terminaison dans System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

     Exemple : **CCMSetup.exe /UsePKICert**  

-   **/NoCRLCheck**  

     Spécifie qu'un client ne doit pas vérifier pas la liste de révocation de certificats (CRL) lorsqu'il communique sur HTTPS à l'aide d'un certificat PKI.  

     Lorsque cette option n'est pas spécifiée, le client vérifie la liste de révocation de certificats avant d'établir une connexion HTTPS à l'aide de certificats PKI.  

     Pour plus d’dansformations sur la vérification de la liste de révocation des certificats clients, consultez [Planndansg for PKI certificate revocation](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) dans[Plan for security dans System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

     Exemple : **CCMSetup.exe /UsePKICert /NoCRLCheck**  

-   **/config:&lt;fichier de configuration\>**  

     Indique le nom d'un fichier texte contenant les propriétés d'installation du client. À moins que vous spécifiiez la propriété CCMSetup **/noservice**, ce fichier doit se trouver dans le dossier CCMSetup, c’est-à-dire dans %Windir%\\Ccmsetup pour les systèmes d’exploitation 32 bits et 64 bits. Si vous spécifiez la propriété **/noservice** , ce fichier doit se trouver dans le dossier à partir duquel vous exécutez CCMSetup.exe.  

     Exemple : **CCMSetup.exe /config:&lt;Nom_Fichier_Configuration.txt\>**  

     Utilisez le fichier mobileclienttemplate.tcf dans le dossier &lt;Répertoire_Configuration Manager\>\\bin\\&lt;plateforme\> sur l’ordinateur serveur de site pour fournir le format approprié du fichier. Ce fichier contient également des informations au format commentaire sur les sections et leur utilisation. Spécifiez les propriétés d'installation du client dans la section [Client Install], à la suite du texte ci-après : **Install=INSTALL=ALL**.  

     Exemple d'entrée de section [Client Install] : **Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100**  

-   **/skipprereq:&lt;nom_fichier\>**

     Indique que CCMSetup.exe ne doit pas installer le programme prérequis spécifié pendant l’installation du client Configuration Manager.  

     Exemples : **CCMSetup.exe /skipprereq:silverlight.exe** ou **CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe**  

    > [!NOTE]  
    >  Cette propriété accepte plusieurs valeurs. Pour séparer chaque valeur, utilisez le point-virgule (;).  

-   **/forceinstall**  

     Force la désinstallation du client existant avant l'installation du nouveau client.  

-   **/ExcludeFeatures:&lt;fonctionnalité\>**  

     Indique que CCMSetup.exe n’installera pas la fonctionnalité spécifiée pendant l’installation du client Configuration Manager.  

     Exemple : **CCMSetup.exe /ExcludeFeatures:ClientUI** n’installera pas le Centre logiciel sur le client.  

    > [!NOTE]  
    >  Pour cette version, **ClientUI** est la seule valeur prise en charge avec la propriété **/ExcludeFeatures** .  

##  <a name="a-nameccmsetupreturncodesa-ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> Codes de retour de CCMSetup.exe  
 La commande CCMSetup.exe fournit les codes de retour suivants une fois son exécution est terminée. Pour résoudre les problèmes d’exécution de la commande, examinez le fichier ccmsetup.log sur l’ordinateur client afin de déterminer le contexte et des détails supplémentaires sur les problèmes de code de retour.  

|Code de retour|Signification|  
|-----------------|-------------|  
|0|Opération réussie|  
|6|Erreur|  
|7|Redémarrage obligatoire|  
|8|Programme d’installation déjà en cours d’exécution|  
|9|Échec d’évaluation de condition préalable|  
|10|Échec de validation de hachage de manifeste de configuration|  

##  <a name="a-nameclientmsipropsa-clientmsi-properties"></a><a name="clientMsiProps"></a> Propriétés de Client.msi  
 Les propriétés suivantes peuvent modifier le comportement d’installation de client.msi. Si vous utilisez la méthode d'installation push du client, vous pouvez également spécifier les propriétés sous l'onglet **Client** de la boîte de dialogue **Propriétés de l'installation push du client** .  

-   **CCMALWAYSINF**  

     À définir sur 1 pour indiquer que le client sera toujours basé sur Internet et ne se connectera jamais à l'intranet. Le type de connexion du client affiche **Toujours Internet**.  

     Cette propriété doit être utilisée avec CCMHOSTNAME, qui indique le nom de domaine complet du point de gestion basé sur Internet. Elle doit également être utilisée avec la propriété CCMSetup /UsePKICert et avec le code de site.  

     Pour plus d’informations sur la gestion du client basée sur Internet, consultez [Éléments à prendre en considération pour les communications de clients à partir d’Internet ou d’une forêt non approuvée](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) dans [Communications entre points de terminaison dans System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

     Exemple : **CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC**  

-   **CCMCERTISSUERS**  

     Spécifie la liste des émetteurs de certificats, qui est une liste de certificats issus d’autorités de certification racines de confiance que le site Configuration Manager a approuvées.  

     Pour plus d’informations sur la liste des émetteurs de certificats et sur la façon dont les clients l’utilisent lors du processus de sélection de certificat, consultez [Planning for PKI client certificate selection](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) dans [Plan for security dans System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

     Il s'agit d'une correspondance qui respecte la casse pour les attributs d'objet qui se trouvent dans le certificat d'autorité de certification racine. Les attributs peuvent être séparés par une virgule (,) ou un point-virgule (;). Plusieurs certificats d'autorité de certification racine peuvent être spécifiés à l'aide d'une barre de séparation. Exemple :  

     **CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &amp;#124; CN=Litware Corporate Root CA; O=Litware, Inc.”**  

    > [!TIP]  
    >  Faites référence au fichier mobileclient.tcf dans le dossier &lt;répertoire_Configuration_Manager\>\bin\\&lt;plateforme\> sur l’ordinateur de serveur de site pour copier les **CertificateIssuers=&lt;chaîne\>** configurés pour le site.  

-   **CCMCERTSEL**  

     Indique les critères de sélection des certificats si le client possède plusieurs certificats qui peuvent être utilisés pour la communication HTTPS (un certificat valide incluant des fonctions d'authentification du client).  

     Vous pouvez rechercher une correspondance exacte (utilisez **Subject:**) ou une correspondance partielle (utilisez **SubjectStr:)**dans le nom d'objet ou l'autre nom de l'objet. Exemples :  

     **CCMCERTSEL="Subject:computer1,contoso.com"** recherche un certificat avec une correspondance exacte au nom d'ordinateur « computer1,contoso.com » dans le nom d'objet ou l'autre nom de l'objet.  

     **CCMCERTSEL="SubjectStr:contoso.com"** recherche un certificat contenant « contoso.com » dans le nom d'objet ou l'autre nom de l'objet.  

     Vous pouvez également utiliser un identificateur d'objet (OID) ou des attributs de nom unique dans les attributs du nom d'objet ou de l'autre nom de l'objet, par exemple :  

     **CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"** recherche l'attribut d'unité organisationnelle exprimé en tant qu'identificateur d'objet et nommé Computers.  

     **CCMCERTSEL="SubjectAttr:OU = Computers"** recherche l’attribut d’unité organisationnelle exprimé en tant que nom unique et nommé Computers.  

    > [!IMPORTANT]  
    >  Si vous utilisez la zone Nom d’objet, le processus de correspondance pour la valeur des critères de sélection **Subject:** respecte la casse, tandis que le processus de correspondance pour la valeur des critères de sélection **SubjectStr:** ne la respecte pas.  
    >   
    >  Si vous utilisez la zone Autre nom de l’objet, le processus de correspondance pour la valeur des critères de sélection **Subject:** et pour la valeur des critères de sélection **SubjectStr:** ne respecte pas la casse.  

     La liste complète des attributs que vous pouvez utiliser pour la sélection de certificat figure dans [Valeurs d'attribut prises en charge pour les critères de sélection de certificat PKI](#BKMK_attributevalues).  

     Si plusieurs certificats correspondent à la recherche et si la propriété que CCMFIRSTCERT a été définie sur 1, le certificat dont la période de validité est la plus longue est sélectionné.  

-   **CCMCERTSTORE**  

     Indique un autre nom de magasin de certificats si le certificat du client à utiliser pour la communication HTTPS ne se trouve pas dans le magasin de certificats par défaut de **Personnel** du magasin Ordinateur.  

     Exemple : **CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"**  

-   **CCMFIRSTCERT**  

     Si la valeur est définie sur 1, cette propriété spécifie que le client doit sélectionner le certificat PKI dont la période de validité est la plus longue. Ce paramètre peut être requis si vous utilisez un mécanisme d'application de protection d'accès réseau avec la contrainte IPsec.  

     Exemple : **CCMSetup.exe /UsePKICert CCMFIRSTCERT=1**  

-   **CCMHOSTNAME**  

     Indique le nom de domaine complet du point de gestion basé sur Internet, si le client est géré sur Internet.  

     N'attribuez pas la propriété d'installation SMSSITECODE=AUTO à cette option. Vous devez directement attribuer les clients Internet à leur site Internet.  

     Exemple : **CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"**  

-   **CCMHTTPPORT**  

     Indique le port que le client doit utiliser lors de la communication sur HTTP avec des serveurs de système de site.  

     Si vous ne spécifiez pas le port, la valeur par défaut (80) est utilisée.  

     Exemple : **CCMSetup.exe CCMHTTPPORT=80**  

-   **CCMHTTPSPORT**  

     Indique le port que le client doit utiliser lors de la communication sur HTTPS avec des serveurs de système de site. Si le port n'est pas spécifié, la valeur par défaut de 443, sera utilisée.  

     Exemple : **CCMSetup.exe /UsePKICert CCMHTTPSPORT=443**  

-   **SMSPUBLICROOTKEY**  

     Indique la clé racine approuvée de Configuration Manager lorsque celle-ci ne peut pas être récupérée à partir des services de domaine Active Directory. Cette propriété s'applique aux clients qui utilisent la communication client HTTP et HTTPS. Pour plus d’informations, consultez [Planification de la clé racine approuvée](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) dans [Planifier la sécurité dans System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

     Exemple : **CCMSetup.exe SMSPUBLICROOTKEY=&lt;clé\>**  

-   **SMSROOTKEYPATH**  

     Utilisée pour réinstaller la clé racine approuvée de Configuration Manager. Indique le chemin d'accès complet et le nom de fichier d'un fichier contenant la clé racine approuvée. Cette propriété s'applique aux clients qui utilisent la communication client HTTP et HTTPS. Pour plus d’informations, consultez [Planification de la clé racine approuvée](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) dans [Planifier la sécurité dans System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

     Exemple : CCMSetup.exe **SMSROOTKEYPATH=&lt;chemin_complet_et_nom_de_fichier\>**  

-   **RESETKEYINFORMATION**  

     Si un client Configuration Manager possède la mauvaise clé racine approuvée de Configuration Manager et ne peut pas contacter de point de gestion approuvé pour recevoir une copie valide de la nouvelle clé racine approuvée, vous devez supprimer manuellement l’ancienne clé racine approuvée à l’aide de cette propriété. Cette situation se produit couramment lorsque vous déplacez un client d'une hiérarchie de site à une autre. Cette propriété s'applique aux clients qui utilisent la communication client HTTP et HTTPS.  

     Exemple : **CCMSetup.exe RESETKEYINFORMATION=TRUE**  

-   **CCMDEBUGLOGGING**  

     Active l’enregistrement du débogage dans le journal (journalisation). Les valeurs peuvent être définies sur 0 (désactivée) ou 1 (activée). La valeur par défaut est 0. Dans ce cas, le client enregistre dans le journal des informations détaillées qui peuvent être utiles pour le dépannage. Nous vous recommandons d'éviter d'utiliser cette propriété dans des sites en production, car une journalisation excessive peut alors se produire et compliquer la recherche d'informations pertinentes dans les fichiers journaux. CCMENABLELOGGING doit être définie sur TRUE pour activer la journalisation du débogage.  

     Exemple : **CCMSetup.exe CCMDEBUGLOGGING=1**  

-   **CCMENABLELOGGING**  

     Active l’enregistrement dans le journal (journalisation) si cette propriété est définie à TRUE (VRAI). Par défaut, la journalisation est activée. Les fichiers journaux sont stockés dans le dossier **Logs** du dossier d’installation du client Configuration Manager. Par défaut, ce dossier est %Windir%\CCM\Logs.  

     Exemple : **CCMSetup.exe CCMENABLELOGGING=TRUE**  

-   **CCMLOGLEVEL**  

     Indique la quantité de détails à écrire dans les fichiers journaux de Configuration Manager. Spécifiez un entier entre 0 et 3, où 0 représente la journalisation la plus abondante et où 3 ne consigne que les erreurs. La valeur par défaut est 1.  

     Exemple : **CCMSetup.exe CCMLOGLEVEL=3**  

-   **CCMLOGMAXHISTORY**  

     Quand la taille d’un fichier journal de Configuration Manager atteint 250 000 octets (ou la valeur indiquée par la propriété CCMLOGMAXSIZE), le fichier est renommé pour sauvegarde et un nouveau fichier journal est créé.  

     Cette propriété indique combien conserver de versions précédentes du fichier journal. La valeur par défaut est 1. Si la valeur est définie sur 0, aucun ancien fichier journal n'est conservé.  

     Exemple : **CCMSetup.exe CCMLOGMAXHISTORY=0**  

-   **CCMLOGMAXSIZE**  

     Spécifie la taille maximale du fichier journal en octets. Quand un journal atteint la taille spécifiée, il est renommé comme fichier d’historique et un nouveau fichier est créé. Cette propriété doit être définie sur 10 000 octets au moins. La valeur par défaut est 250 000 octets.  

     Exemple : **CCMSetup.exe CCMLOGMAXSIZE=300000**  

-   **CCMALLOWSILENTREBOOT**  

     Spécifie que l'ordinateur est autorisé à redémarrer après l'installation du client, si cela est nécessaire.  

    > [!IMPORTANT]  
    >  L'ordinateur redémarre sans avertissement, même si un utilisateur est actuellement connecté.  

     Exemple : **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

-   **DISABLESITEOPT**  

     Si cette propriété a la valeur TRUE, elle empêche les utilisateurs finaux disposant d’informations d’identification administratives sur l’ordinateur client de modifier le site attribué au client Configuration Manager à l’aide de Configuration Manager dans le Panneau de configuration de l’ordinateur client.  

     Exemple : **CCMSetup.exe DISABLESITEOPT=TRUE**  

-   **DISABLECACHEOPT**  

     Si cette propriété a la valeur TRUE, elle empêche les utilisateurs finaux disposant d’informations d’identification administratives sur l’ordinateur client de modifier les paramètres du dossier du cache client pour le client Configuration Manager à l’aide de Configuration Manager dans le Panneau de configuration de l’ordinateur client.  

     Exemple : **CCMSetup.exe DISABLECACHEOPT=TRUE**  

-   **SMSCACHEDIR**  

     Spécifie l'emplacement du dossier de cache du client sur l'ordinateur client, qui stocke les fichiers temporaires. Par défaut, l'emplacement est *%Windir\ccmcache*.  

     Exemple : **CCMSetup.exe SMSCACHEDIR="C:\Temp"**  

     Cette propriété peut être utilisée avec la propriété SMSCACHEFLAGS pour contrôler davantage l'emplacement du dossier mis en mémoire cache du client.  

     Exemple : **CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE** installe le dossier de mémoire cache du client sur le lecteur de disque le plus volumineux disponible du client.  

-   **SMSCACHEFLAGS**  

     Configure le dossier de cache de Configuration Manager, qui stocke les fichiers temporaires. Vous pouvez utiliser les propriétés de SMSCACHEFLAGS individuellement ou en combinaison, séparées par des points-virgules. Si cette propriété n’est pas spécifiée, le dossier mis dans la mémoire cache du client est installé conformément à la propriété SMSCACHEDIR, il n'est pas compressé et la valeur de SMSCACHESIZE est utilisée pour sa taille en Mo.  

     Spécifie davantage les détails d'installation pour le dossier mis dans la mémoire cache du client. Les propriétés suivantes peuvent être indiquées :  

    -   PERCENTDISKSPACE : indique la taille du dossier sous forme de pourcentage de l’espace disque total. Si vous indiquez cette propriété, vous devez également indiquer la propriété SMSCACHESIZE comme valeur de pourcentage à utiliser.  

    -   PERCENTFREEDISKSPACE : indique la taille du dossier sous forme de pourcentage de l’espace disque disponible. Si vous indiquez cette propriété, vous devez également indiquer la propriété SMSCACHESIZE comme valeur de pourcentage à utiliser. Par exemple, si le disque dispose de 10 Mo libres et que SMSCACHESIZE indique 50, cela signifie que la taille du dossier est définie sur 5 Mo. Vous ne pouvez pas utiliser cette propriété avec la propriété PERCENTDISKSPACE.  

    -   MAXDRIVE : indique que le dossier doit être installé sur le disque le plus volumineux disponible. Cette valeur sera ignorée si un chemin a été spécifié avec la propriété SMSCACHEDIR.  

    -   MAXDRIVESPACE : indique que le dossier doit être installé sur le lecteur de disque possédant l’espace disponible le plus important. Cette valeur sera ignorée si un chemin a été spécifié avec la propriété SMSCACHEDIR.  

    -   NTFSONLY : indique que le dossier ne peut être installé que sur des lecteurs de disques formatés avec le système de fichiers NTFS. Cette valeur sera ignorée si un chemin a été spécifié avec la propriété SMSCACHEDIR.  

    -   COMPRESS : indique que le dossier doit être conservé sous une forme compressée.  

    -   FAILIFNOSPACE : indique que le logiciel client doit être supprimé si l’espace est insuffisant pour installer le dossier.  

    > [!NOTE]  
    >  Vous pouvez indiquer plusieurs propriétés pour celle-ci, en les séparant par un point-virgule.  

     Si cette propriété n'est pas spécifiée, le dossier temporaire mis dans la mémoire cache du client sera créé conformément à la propriété SMSCACHEDIR, il ne sera pas compressé et sa taille sera celle indiquée dans la propriété SMSCACHESIZE.  

     Exemple : **CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS**  

    > [!NOTE]  
    >  Ce paramètre est ignoré lorsque vous mettez à niveau un client existant.  

-   **SMSCACHESIZE**  

     > [!IMPORTANT]
     > Dans Configuration Manager version 1606, de nouveaux paramètres client sont disponibles pour spécifier la taille du dossier du cache du client. L’ajout de ces paramètres du client remplace l’utilisation de SMSCACHESIZE comme propriété client.msi pour spécifier la taille du cache du client. Pour plus d’informations, consultez les [paramètres du client pour la taille du cache](about-client-settings.md#client-cache-settings).  

     Pour la version 1602 et antérieure, SMSCACHESIZE indique la taille du dossier mis dans la mémoire cache du client en mégaoctets (Mo) ou sous forme de pourcentage quand elle est utilisée avec la propriété PERCENTDISKSPACE ou PERCENTFREEDISKSPACE. Si cette propriété n’est pas définie, la taille maximale du dossier est par défaut de 5120 Mo. La valeur la plus basse que vous pouvez spécifier est 1 Mo.  

    > [!NOTE]  
    >  Si un nouveau package qui doit être téléchargé peut provoquer le dépassement de la taille maximale du dossier et que le dossier ne peut pas être purgé pour libérer un espace suffisant, le téléchargement du package échoue et le programme ou l'application ne s'exécute pas.  

     Ce paramètre est ignoré lorsque vous mettez à niveau un client existant et lorsque le client télécharge les mises à jour logicielles.  

     Exemple : **CCMSetup.exe SMSCACHESIZE=100**  

    > [!NOTE]  
    >  Si vous réinstallez un client, vous ne pouvez pas utiliser les propriétés d'installation SMSCACHESIZE ou SMSCACHEFLAGS pour définir une taille de cache inférieure à la taille de cache précédente. Si vous essayez d'effectuer cette opération, votre valeur est ignorée et la taille du cache est automatiquement définie sur la dernière taille enregistrée.  
    >   
    >  Par exemple, si vous installez le client en utilisant la taille de cache par défaut (5 120 Mo), puis que vous le réinstallez en utilisant une taille de cache de 100 Mo, la taille du dossier du cache sur le client réinstallé sera de 5 120 Mo.  


-   **SMSCONFIGSOURCE**  

     Indique l’emplacement et l’ordre dans lesquels le programme d’installation de Configuration Manager vérifie les paramètres de configuration. La propriété est une chaîne contenant un ou plusieurs caractères, chacun définissant une source de configuration spécifique. Utilisez les valeurs caractère R, P, M et U, seules ou en combinaison, comme indiqué dans les exemples suivants :  

    -   R : vérification des paramètres de configuration dans le Registre.  

         Cliquez ici pour obtenir [plus d’informations sur le stockage des propriétés d’installation du client dans le Registre](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision).  

    -   P : vérification des paramètres de configuration dans les propriétés d’installation fournies à l’invite de commandes.  

    -   M : vérification des paramètres existants à l’occasion de la mise à niveau d’un ancien client avec le logiciel client Configuration Manager.  

    -   U : mise à niveau du client installé vers une version plus récente (et utilisation du code de site attribué).  

     Par défaut, l’installation du client utilise `PU` pour vérifier d’abord les propriétés d’installation, puis les paramètres existants.  

     Exemple : **CCMSetup.exe SMSCONFIGSOURCE=RP**  

-   **SMSDIRECTORYLOOKUP**  

     Indique si le client peut utiliser les services WINS (Windows Internet Name Service) pour trouver un point de gestion qui accepte les connexions HTTP. Les clients utilisent cette méthode lorsqu'ils ne peuvent pas trouver de point de gestion dans les services de domaine Active Directory ou dans DNS.  

     Cette propriété est indépendante de l'utilisation du service WINS par le client pour la résolution de noms.  

     Vous pouvez configurer deux modes différents pour cette propriété :  

    -   NOWINS : il s’agit du paramètre le plus sûr pour cette propriété et il empêche les clients de trouver un point de gestion dans le service WINS.  Lorsque vous utilisez ce paramètre, les clients doivent disposer d'une autre méthode de localisation d'un point de gestion sur l'Intranet, telle que les services de domaine Active Directory ou en utilisant la publication DNS.  

    -   WINSSECURE : dans ce mode, un client qui utilise la communication HTTP peut utiliser WINS pour trouver un point de gestion. Toutefois, le client doit disposer d'une copie de la clé racine approuvée avant de pouvoir se connecter correctement au point de gestion. Pour plus d’informations, consultez [Planification de la clé racine approuvée](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) dans [Planifier la sécurité dans System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

     Si cette propriété n'est pas spécifiée, la valeur par défaut de WINSSECURE est utilisée.  

     Exemple : **CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS**  

-   **SMSSIGNCERT**  

     Spécifie le chemin d'accès complet et le nom de fichier .cer du certificat auto-signé exporté sur le serveur de site.  

     Ce certificat est stocké dans le magasin de certificats **SMS** et porte le nom d'objet **Serveur de site** et le nom convivial **Certificat de signature du serveur de site**.  

     Exemple : **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;chemin _complet_et_nom_de_fichier\>**  

-   **SMSMP**  

     Spécifie un point de gestion initial à utiliser par le client Configuration Manager.  

    > [!IMPORTANT]  
    >  Si le point de gestion accepte uniquement les connexions clientes sur HTTPS (et n’autorise donc pas les connexions clientes HTTP), vous devez ajouter le préfixe https:// au nom du point de gestion.  

     Exemple : **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

     Exemple : **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

     Exemple : **CCMSetup.exe SMSMP=https://smsmp01.contoso.com**  

-   **SMSSITECODE**  

     Indique le site Configuration Manager auquel attribuer le client Configuration Manager. Il peut s'agir d'un code de site à trois caractères ou du mot AUTO. Si AUTO est spécifié ou si cette propriété n’est pas spécifiée, le client tente de déterminer son affectation de site Configuration Manager à partir des services de domaine Active Directory ou d’un point de gestion spécifié.  

    > [!NOTE]  
    >  N'utilisez pas AUTO si vous spécifiez également le point de gestion basé sur Internet (CCMHOSTNAME). Dans ce cas, vous devez directement attribuer le client à son site.  

     Exemple : **CCMSetup.exe SMSSITECODE=XZY**  

-   **CCMINSTALLDIR**  

     Indique le dossier dans lequel les fichiers du client Configuration Manager sont installés. Si cette propriété n’est pas définie, le logiciel client est installé dans le dossier *%Windir%*\CCM. Quel que soit l'emplacement d'installation de ces fichiers, le fichier Ccmcore.dll est toujours installé dans le dossier *%Windir%\System32* . De plus, sur les systèmes d’exploitation 64 bits, une copie du fichier Ccmcore.dll est toujours installée dans le dossier *%Windir%*\SysWOW64 pour prendre en charge les applications 32 bits qui utilisent la version 32 bits des API du client Configuration Manager à partir du Kit de développement logiciel (SDK) Configuration Manager.  

     Exemple : **CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"**  

-   CCMADMINS  

     Indique un ou plusieurs groupes ou comptes d'utilisateurs Windows auxquels accorder l'accès aux paramètres et stratégies du client. Cette propriété est utile si l’administrateur de Configuration Manager ne dispose pas d’informations d’identification administratives locales sur l’ordinateur client. Vous pouvez indiquer une liste de comptes qui sont séparés par un point-virgule.  

     Exemple : **CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"**  

-   **FSP**  

     Indique le point d’état de secours qui reçoit et traite les messages d’état envoyés par les ordinateurs clients Configuration Manager.  

     Pour plus d’informations sur le point d’état de secours, consultez [Déterminer si vous avez besoin d’un point d’état de secours](plan/determine-the-site-system-roles-for-clients.md#BKMK_Determine_FSP) dans [Déterminer les rôles de système de site pour les clients System Center Configuration Manager](plan/determine-the-site-system-roles-for-clients.md).  

     Exemple : **CCMSetup.exe FSP=SMSFP01**  

-   **DNSSUFFIX**  

     Spécifie un domaine DNS pour que les clients localisent les points de gestion qui sont publiés dans DNS. Lorsqu'un point de gestion est localisé, il indique au client d'autres points de gestion dans la hiérarchie. Cela signifie qu'il n'est pas nécessaire que le point de gestion qui est localisé à l'aide de la publication DNS provienne du site du client, et il peut s'agir de n'importe quel point de gestion de la hiérarchie.  

    > [!NOTE]  
    >  Vous n'êtes pas tenu de spécifier cette propriété si le client se trouve dans le même domaine qu'un point de gestion publié. Dans ce cas, le domaine du client est automatiquement utilisé pour chercher des points de gestion dans DNS.  

     Pour plus d’informations sur la publication DNS comme méthode d’emplacement du service pour les clients Configuration Manager, consultez [Emplacement du service et façon dont les clients déterminent leur point de gestion attribué](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) dans [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

    > [!NOTE]  
    >  Par défaut, la publication DNS n’est pas activée dans Configuration Manager.  

     Exemple : **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com**  

-   **CCMEVALINTERVAL**  

     Spécifie la fréquence lors de l'exécution de l'outil d'évaluation de l'intégrité du client (ccmeval.exe). Vous pouvez spécifier une valeur comprise entre **1** et **1440** minutes. Si vous ne spécifiez pas cette propriété, ni une valeur incorrecte, l'évaluation sera exécutée une fois par jour.  

-   **CCMEVALHOUR**  

     Spécifiez l'heure d'exécution de l'outil d'évaluation de l'intégrité du client (ccmeval.exe). Vous pouvez spécifier une valeur comprise entre **0** (minuit) et **23** (11 pm). Si vous ne spécifiez pas cette propriété, ni une valeur incorrecte, l'évaluation sera exécutée à minuit.  

-   **IGNOREAPPVVERSIONCHECK**  

     Spécifie que l'existence de la version minimale requise de Microsoft Application Virtualization (App-V) n'est pas cochée avant que le client soit installé.  

    > [!IMPORTANT]  
    >  Si vous installez le client Configuration Manager sans installer App-V, vous ne pouvez pas déployer des applications virtuelles.  

     Exemple : **CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE**  

-   **NOTIFYONLY**  

     Indique que l’état du client sera signalé, mais que les problèmes détectés au niveau du client Configuration Manager ne seront pas corrigés.  

     Exemple : **CCMSetup.exe NOTIFYONLY=TRUE**  

     Pour plus d’informations, voir [Comment configurer l’état du client dans System Center Configuration Manager](configure-client-status.md).  

##  <a name="a-namebkmkattributevaluesa-supported-attribute-values-for-the-pki-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> Valeurs d'attribut prises en charge pour les critères de sélection de certificat PKI  
 Configuration Manager prend en charge les valeurs d’attribut suivantes pour les critères de sélection de certificat PKI :  

|Attribut d'OID|Attribut de nom unique|Définition de l'attribut|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Composant de domaine|  
|1.2.840.113549.1.9.1|E ou E-mail|Adresse de messagerie|  
|2.5.4.3|CN|Nom commun|  
|2.5.4.4|SN|Nom d'objet|  
|2.5.4.5|SERIALNUMBER|Numéro de série|  
|2.5.4.6|C|Code du pays|  
|2.5.4.7|L|Localité|  
|2.5.4.8|S ou ST|Nom de département/province|  
|2.5.4.9|STREET|Adresse|  
|2.5.4.10|O|Nom de l'organisation|  
|2.5.4.11|OU|Unité d'organisation|  
|2.5.4.12|T ou Title|Titre|  
|2.5.4.42|G ou GN ou GivenName|Prénom|  
|2.5.4.43|I ou Initials|Initiales|  
|2.5.29.17|(aucune valeur)|Autre nom de l'objet|  



<!--HONumber=Nov16_HO1-->


