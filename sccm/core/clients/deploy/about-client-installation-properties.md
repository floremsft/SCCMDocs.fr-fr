---
title: "Propriétés d’installation du client | Microsoft Docs"
description: "Découvrez les propriétés d’installation du client dans System Center Configuration Manager."
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: 15
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: afe0ecc4230733fa76e41bf08df5ccfb221da7c8
ms.openlocfilehash: fef330a14ad2a1f75d520eac0706a376953993e8
ms.contentlocale: fr-fr
ms.lasthandoff: 08/04/2017

---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>À propos des propriétés d’installation du client dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez la commande CCMSetup.exe de System Center Configuration Manager pour installer manuellement le client Configuration Manager.  

##  <a name="aboutCCMSetup"></a> À propos de CCMSetup.exe  
 La commande CCMSetup.exe télécharge les fichiers nécessaires pour installer le client à partir d’un point de gestion ou d’un emplacement source. Ces fichiers peuvent être les suivants :  

-   Le package Windows Installer Client.msi qui installe le logiciel client.  

-   Les fichiers d’installation du service BITS (Background Intelligent Transfer Service) de Microsoft.  

-   Les fichiers d’installation de Windows Installer.  

-   Les mises à jour et correctifs du client Configuration Manager.  

> [!NOTE]  
>  Dans Configuration Manger, vous ne pouvez pas exécuter le Fichier Client.msi directement.  

 CCMSetup.exe fournit des [propriétés de ligne de commande](#ccmsetup-exe-command-line-properties) permettant de personnaliser l’installation. Vous pouvez également spécifier des propriétés pour modifier le comportement de Client.msi sur la ligne de commande CCMSetup.exe.  

> [!IMPORTANT]  
>  Spécifiez les propriétés CCMSetup avant d’indiquer les propriétés pour Client.msi.  

 CCMSetup.exe et ses fichiers de prise en charge résident sur le serveur de site Configuration Manager dans le sous-dossier **Client** du dossier d’installation de Configuration Manager. Ce dossier est partagé sur le réseau sous **&lt;Nom_Serveur_Site\>\SMS_&lt;Code_Site\>\Client**.  

 À l'invite de commandes, la commande CCMSetup.exe utilise le format suivant :  

 `CCMSetup.exe [&lt;Ccmsetup properties\>] [&lt;client.msi setup properties>]`  

 Exemple :  

 « CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01 »  

 Cet exemple effectue les opérations suivantes :  

-   Force le point de gestion SMSMP01 à demander la liste des points de distribution pour télécharger les fichiers d’installation du client.  

-   Force l’arrêt de l’installation si une version du client existe déjà sur l’ordinateur.  

-   Ordonne à client.msi d'attribuer le client au code de site S01.  

-   Ordonne à client.msi d'utiliser le point d'état de secours nommé SMSFP01.  

> [!NOTE]  
>  Si une propriété contient des espaces, placez-la entre guillemets.  


> [!IMPORTANT]  
>  Si vous avez étendu le schéma Active Directory pour Configuration Manager, de nombreuses propriétés d’installation du client sont publiées dans les services de domaine Active Directory et automatiquement lues par le client Configuration Manager. Pour obtenir la liste des propriétés d’installation du client publiées dans les services de domaine Active Directory, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory dans System Center Configuration Manager](about-client-installation-properties-published-to-active-directory-domain-services.md).  

##  <a name="ccmsetupexe-command-line-properties"></a>Propriétés de ligne de commande CCMSetup.exe  

### <a name=""></a>/?  

Ouvre la boîte de dialogue **CCMSetup** affichant les propriétés de ligne de commande pour ccmsetup.exe.  

Exemple : **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;Chemin\>  

 Spécifie l’emplacement de téléchargement des fichiers. Utilisez un chemin local ou UNC. Les fichiers sont téléchargés à l'aide du protocole SMB (server message block).  Pour utiliser **/source**, le compte d’utilisateur Windows pour l’installation du client doit avoir les autorisations Lecture sur l’emplacement.

> [!NOTE]  
>  Vous pouvez utiliser la propriété **/source** plusieurs fois dans une ligne de commande pour spécifier d’autres emplacements de téléchargement.  

 Exemple : **ccmsetup.exe /source:"\\\ordinateur\dossier"**  

### <a name="mpltcomputer"></a>/mp:&lt;Ordinateur\>

 Spécifie un point de gestion source auquel les ordinateurs peuvent se connecter pour trouver le point de distribution le plus proche pour les fichiers d’installation. En l'absence de point de distribution ou si les ordinateurs ne peuvent pas télécharger les fichiers auprès des points de distribution au terme d'un délai de quatre heures, les clients téléchargent les fichiers auprès du point de gestion spécifié.  

> [!IMPORTANT]  
>  Cette propriété permet de spécifier un point de gestion initial utilisé par les ordinateurs qui recherchent une source de téléchargement. Cela peut être n’importe quel point de gestion sur n’importe quel site. Elle n’*affecte* pas le client à un point de gestion.   

 Les ordinateurs téléchargent les fichiers via une connexion HTTP ou HTTPS, selon la configuration du rôle de système de site des connexions client. Le téléchargement utilise la limitation BITS, si cette fonctionnalité est configurée. Si tous les points de distribution et de gestion sont configurés uniquement pour les connexions client HTTPS, vérifiez que l’ordinateur client possède un certificat client valide.  

Vous pouvez utiliser la propriété de ligne de commande **/mp** pour spécifier plusieurs points de gestion : dans ce cas, si l'ordinateur ne parvient pas à se connecter au premier point de gestion, il essaie de se connecter au deuxième, et ainsi de suite. Quand vous spécifiez plusieurs points de gestion, séparez les valeurs par des points-virgules.

Si le client se connecte à un point de gestion via HTTPS, vous devez en général spécifier le nom de domaine complet, et non le nom de l’ordinateur. La valeur doit correspondre au nom d’objet ou à l’autre nom d’objet du certificat PKI du point de gestion. Même si Configuration Manager permet d’utiliser un nom d’ordinateur dans le certificat pour les connexions intranet, il est recommandé d’utiliser un nom de domaine complet pour plus de sécurité.

Exemple utilisant le nom d’ordinateur : `ccmsetup.exe /mp:SMSMP01`  

Exemple utilisant le nom de domaine complet : `ccmsetup.exe /mp:smsmp01.contoso.com`  

### <a name="retryltminutes"></a>/retry:&lt;Minutes\>

Intervalle entre les tentatives si CCMSetup.exe ne réussit pas à télécharger les fichiers d’installation.  CCMSetup renouvelle les tentatives jusqu’à atteindre la limite indiquée dans la propriété **downloadtimeout**.  

Exemple : `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Empêche l’exécution de CCMSetup comme service (comportement par défaut). Quand CCMSetup est exécuté comme service, il s’exécute dans le contexte du compte système local de l’ordinateur, qui peut ne pas disposer des droits suffisants pour accéder aux ressources réseau nécessaires pour l’installation. Avec **/noservice**, CCMSetup.exe s’exécute dans le contexte du compte d’utilisateur que vous utilisez pour démarrer l’installation. Par ailleurs, si vous utilisez un script pour exécuter CCMSetup.exe avec la propriété **/service**, CCMSetup.exe s’arrête au démarrage du service et risque de ne pas renvoyer correctement les détails de l’installation.   

Exemple : `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Indique que CCMSetup doit s'exécuter comme un service qui utilise le compte système local.  

Exemple : `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Indique que le logiciel client doit être désinstallé. Pour plus d'informations, voir [Comment gérer des clients dans Configuration Manager](../manage/manage-clients.md).  

Exemple : `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Force l’installation du client à s’arrêter si une version du client est déjà installée.  

Exemple : `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 Indique que CCMSetup doit forcer l’ordinateur client à redémarrer si nécessaire pour terminer l’installation. Sinon, CCMSetup se ferme quand un redémarrage est nécessaire et continue après le prochain redémarrage manuel.  

 Exemple : `CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;Priorité\>

 Indique la priorité de téléchargement lorsque les fichiers d'installation du client sont téléchargés via une connexion HTTP. Les valeurs possibles sont les suivantes :  

-   FOREGROUND (avant-plan)  

-   HIGH (élevée)  

-   NORMAL (normale)  

-   LOW (faible)  

 La valeur par défaut est NORMAL.  

 Exemple : `ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;Minutes\>

Durée (en minutes) pendant laquelle CCMSetup essaie de télécharger les fichiers d’installation avant d’arrêter. La valeur par défaut est **1 440** minutes (1 jour).  

Exemple : `ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

 Quand cette propriété est spécifiée, le client utilise un certificat PKI qui inclut l’authentification du client, le cas échéant. Si aucun certificat valide n’est trouvé, le client utilise une connexion HTTP et un certificat auto-signé, ce qui est aussi le comportement quand vous n’utilisez pas cette propriété.

> [!NOTE]  
>  Dans certains cas, il n’est pas nécessaire de spécifier cette propriété quand vous installez un client, tout en utilisant un certificat client. C’est le cas, notamment, de l’installation d’un client via une installation Push et de l’installation d’un client basée sur un point de mise à jour logicielle. Toutefois, vous devez indiquer cette propriété à chaque fois que vous installez un client manuellement et utiliser la propriété **/mp** pour indiquer un point de gestion qui est configuré pour accepter uniquement les connexions client HTTPS. Vous devez également spécifier cette propriété lorsque vous installez un client pour la communication Internet uniquement, en utilisant la propriété CCMALWAYSINF=1 (conjointement avec les propriétés pour le point de gestion basé sur Internet et le code de site). Pour plus d’informations sur la gestion du client basée sur Internet, consultez [Éléments à prendre en considération pour les communications de clients à partir d’Internet ou d’une forêt non approuvée](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) dans [Communications entre points de terminaison dans System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Exemple : `CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 Spécifie qu’un client ne doit pas vérifier la liste de révocation de certificats (CRL) quand il communique via HTTPS avec un certificat PKI.  

 Quand cette propriété n’est pas spécifiée, le client vérifie la liste de révocation de certificats avant d’établir une connexion HTTPS.  

 Pour plus d’informations sur la vérification de la liste de révocation des certificats clients, consultez [Planification de la révocation de certificats PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) dans [Planifier la sécurité dans System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Exemple : `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;fichier_configuration\>

Indique le nom d'un fichier texte contenant les propriétés d'installation du client.

- Si vous ne spécifiez pas la propriété CCMSetup **/noservice**, ce fichier doit se trouver dans le dossier CCMSetup, c’est-à-dire dans %Windir%\\Ccmsetup pour les systèmes d’exploitation 32 bits et 64 bits.
- Si vous spécifiez la propriété **/noservice** , ce fichier doit se trouver dans le dossier à partir duquel vous exécutez CCMSetup.exe.  

Exemple : `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

Utilisez le fichier mobileclienttemplate.tcf dans le dossier &lt;Répertoire_Configuration Manager\>\\bin\\&lt;plateforme\> sur l’ordinateur serveur de site pour fournir le format de fichier approprié. Ce fichier contient également des commentaires sur les sections et leur utilisation. Spécifiez les propriétés d'installation du client dans la section [Client Install], à la suite du texte ci-après : **Install=INSTALL=ALL**.  

Exemple d’entrée de section [Client Install] : `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;nom_fichier\>

 Indique que CCMSetup.exe ne doit pas installer le programme prérequis spécifié pendant l’installation du client Configuration Manager. Cette propriété accepte plusieurs valeurs. Pour séparer chaque valeur, utilisez le point-virgule (;).  


 Exemples : `CCMSetup.exe /skipprereq:silverlight.exe` ou `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe`  

### <a name="forceinstall"></a>/forceinstall

 Force la désinstallation du client existant avant l’installation du nouveau client.  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;fonctionnalité\>

Spécifie que CCMSetup.exe n’installera pas la fonction spécifiée si le client est installé.  

Exemple : `CCMSetup.exe /ExcludeFeatures:ClientUI` n’installera pas le Centre logiciel sur le client.  

> [!NOTE]  
>  Pour cette version, **ClientUI** est la seule valeur prise en charge avec la propriété **/ExcludeFeatures** .  

##  <a name="ccmsetupReturnCodes"></a> Codes de retour de CCMSetup.exe  
 La commande CCMSetup.exe fournit les codes de retour suivants à la fin de son exécution. Pour résoudre les problèmes, examinez le fichier ccmsetup.log sur l’ordinateur client pour déterminer le contexte et obtenir des détails supplémentaires sur les codes de retour.  

|Code de retour|Signification|  
|-----------------|-------------|  
|0|Opération réussie|  
|6|Erreur|  
|7|Redémarrage obligatoire|  
|8|Programme d’installation déjà en cours d’exécution|  
|9|Échec d’évaluation de condition préalable|  
|10|Échec de validation de hachage de manifeste de configuration|  

##  <a name="clientMsiProps"></a> Propriétés de Client.msi  
 Les propriétés suivantes peuvent modifier le comportement d’installation de client.msi. Si vous utilisez la méthode d'installation push du client, vous pouvez également spécifier les propriétés sous l'onglet **Client** de la boîte de dialogue **Propriétés de l'installation push du client** .  

### <a name="ccmadmins"></a>CCMADMINS  

Indique un ou plusieurs groupes ou comptes d'utilisateurs Windows auxquels accorder l'accès aux paramètres et stratégies du client. Cette propriété est utile si l’administrateur de Configuration Manager ne dispose pas d’informations d’identification d’administration locale sur l’ordinateur client. Indiquez une liste de comptes séparés par des points-virgules.  

Exemple : `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Spécifie que l’ordinateur est autorisé à redémarrer après l’installation du client, si nécessaire.  

> [!IMPORTANT]  
>  L’ordinateur redémarre sans avertissement, même si un utilisateur est connecté.  

Exemple : **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 À définir sur 1 pour indiquer que le client sera toujours basé sur Internet et ne se connectera jamais à l'intranet. Le type de connexion du client affiche **Toujours Internet**.  

 Cette propriété doit être utilisée avec CCMHOSTNAME, qui indique le nom de domaine complet du point de gestion basé sur Internet. Elle doit également être utilisée avec la propriété CCMSetup /UsePKICert et avec le code de site.  

 Pour plus d’informations sur la gestion du client basée sur Internet, consultez [Éléments à prendre en considération pour les communications de clients à partir d’Internet ou d’une forêt non approuvée](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) dans [Communications entre points de terminaison dans System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Exemple : `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Spécifie la liste des émetteurs de certificats, qui est une liste de certificats issus d’autorités de certification racines de confiance que le site Configuration Manager a approuvées.  

 Pour plus d’informations sur la liste des émetteurs de certificats et sur la façon dont les clients l’utilisent lors du processus de sélection de certificat, consultez [Planification de la sélection de certificats client PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) dans [Planifier la sécurité dans System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Il s'agit d'une correspondance qui respecte la casse pour les attributs d'objet qui se trouvent dans le certificat d'autorité de certification racine. Les attributs peuvent être séparés par une virgule (,) ou un point-virgule (;). Plusieurs certificats d'autorité de certification racine peuvent être spécifiés à l'aide d'une barre de séparation. Exemple :  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  Faites référence au fichier mobileclient.tcf dans le dossier &lt;répertoire_Configuration_Manager\>\bin\\&lt;plateforme\> sur l’ordinateur de serveur de site pour copier les **CertificateIssuers=&lt;chaîne\>** configurés pour le site.  

### <a name="ccmcertsel"></a>CCMCERTSEL

 Indique les critères de sélection des certificats si le client possède plusieurs certificats pour la communication HTTPS (un certificat valide incluant des fonctions d’authentification du client).  

 Vous pouvez rechercher une correspondance exacte (utilisez **Subject:**) ou une correspondance partielle (utilisez **SubjectStr:)**dans le nom d’objet ou l’autre nom de l’objet. Exemples :  

 `CCMCERTSEL="Subject:computer1.contoso.com"` recherche un certificat avec une correspondance exacte au nom d’ordinateur « computer1,contoso.com » dans le nom d’objet ou l’autre nom de l’objet.  

 `CCMCERTSEL="SubjectStr:contoso.com"` recherche un certificat contenant « contoso.com » dans le nom d’objet ou l’autre nom de l’objet.  

 Vous pouvez également utiliser un identificateur d'objet (OID) ou des attributs de nom unique dans les attributs du nom d'objet ou de l'autre nom de l'objet, par exemple :  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` recherche l’attribut d’unité organisationnelle exprimé comme identificateur d’objet et nommé Computers.  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` recherche l’attribut d’unité organisationnelle exprimé comme nom unique et nommé Computers.  

> [!IMPORTANT]  
>  Si vous utilisez la zone Nom d’objet, **Subject:** respecte la casse, mais **SubjectStr:** ne la respecte pas.  
>   
>  Si vous utilisez la zone Autre nom de l’objet, **Subject:**et **SubjectStr:** respectent la casse tous les deux.  

 La liste complète des attributs que vous pouvez utiliser pour la sélection de certificat figure dans [Valeurs d'attribut prises en charge pour les critères de sélection de certificat PKI](#BKMK_attributevalues).  

 Si plusieurs certificats correspondent à la recherche et si la propriété que CCMFIRSTCERT a été définie sur 1, le certificat dont la période de validité est la plus longue est sélectionné.  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 Indique un autre nom de magasin de certificats si le certificat du client pour HTTPS ne se trouve pas dans le magasin de certificats par défaut de **Personnel** du magasin Ordinateur.  

 Exemple : `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  Active l’enregistrement du débogage dans le journal (journalisation). Les valeurs peuvent être définies sur 0 (désactivée, par défaut) ou sur 1 (activée). Dans ce cas, le client enregistre dans le journal des informations détaillées pour le dépannage. Nous vous recommandons d'éviter d'utiliser cette propriété dans des sites en production, car une journalisation excessive peut alors se produire et compliquer la recherche d'informations pertinentes dans les fichiers journaux. CCMENABLELOGGING doit être également définie sur TRUE pour activer la journalisation du débogage.  

  Exemple : `CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  Par défaut, elle est définie à la valeur TRUE pour activer la journalisation. Les fichiers journaux sont stockés dans le dossier **Logs** du dossier d’installation du client Configuration Manager. Par défaut, ce dossier est %Windir%\CCM\Logs.  

  Exemple : `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 Fréquence d’exécution de l’outil d’évaluation de l’intégrité du client (ccmeval.exe). La valeur peut être comprise entre **1** et **1440** minutes. Par défaut, il est exécuté une fois par jour.  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 Heure d’exécution de l’outil d’évaluation de l’intégrité du client (ccmeval.exe), entre **0** (minuit) et **23** (23 h). S’exécute à minuit par défaut.  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 Si la valeur est définie sur 1, cette propriété spécifie que le client doit sélectionner le certificat PKI dont la période de validité est la plus longue. Ce paramètre peut être requis si vous utilisez un mécanisme d'application de protection d'accès réseau avec la contrainte IPsec.  

 Exemple : `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  

### <a name="ccmhostname"></a>CCMHOSTNAME

 Indique le nom de domaine complet du point de gestion basé sur Internet, si le client est géré sur Internet.  

 N'attribuez pas la propriété d'installation SMSSITECODE=AUTO à cette option. Vous devez directement attribuer les clients Internet à leur site Internet.  

 Exemple : `CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

### <a name="ccmhttpport"></a>CCMHTTPPORT

 Indique le port que le client doit utiliser lors de la communication sur HTTP avec des serveurs de système de site. Le port 80 est le port par défaut.  

 Exemple : `CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Indique le port que le client doit utiliser lors de la communication sur HTTPS avec des serveurs de système de site. Le port 443 est le port par défaut.  

Exemple : `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Indique le dossier dans lequel les fichiers du client Configuration Manager sont installés, *%Windir%*\CCM par défaut. Quel que soit l’emplacement d’installation de ces fichiers, le fichier Ccmcore.dll est toujours installé dans le dossier *%Windir%\System32*. Sur les systèmes d’exploitation 64 bits, une copie du fichier Ccmcore.dll est toujours installée dans le dossier *%Windir%*\SysWOW64 pour prendre en charge les applications 32 bits qui utilisent la version 32 bits des API du client Configuration Manager fournies dans le SDK Configuration Manager.  

 Exemple : `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Indique le niveau de détails à écrire dans les fichiers journaux de Configuration Manager. Spécifiez un entier entre 0 et 3, où 0 représente la journalisation la plus complète et où 3 ne consigne que les erreurs. La valeur par défaut est 1.  

Exemple : `CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Quand la taille d’un fichier journal de Configuration Manager atteint 250 000 octets (ou la valeur indiquée par la propriété CCMLOGMAXSIZE), le fichier est renommé pour sauvegarde et un nouveau fichier journal est créé.  

Cette propriété indique combien conserver de versions précédentes du fichier journal. La valeur par défaut est 1. Si la valeur est définie sur 0, aucun ancien fichier journal n'est conservé.  

Exemple : `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Taille maximale du fichier journal, en octets. Quand un journal atteint la taille spécifiée, il est renommé comme fichier d’historique et un nouveau fichier est créé. Cette propriété doit être définie sur 10 000 octets au moins. La valeur par défaut est 250 000 octets.  

Exemple : `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 Si cette propriété est définie sur TRUE, elle désactive la capacité des utilisateurs finaux disposant d’informations d’identification d’administration sur l’ordinateur client à modifier le site attribué Configuration Manager dans **Configuration Manager** dans le Panneau de configuration du client.  

 Exemple : **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Si cette propriété a la valeur TRUE, elle empêche les utilisateurs finaux disposant d’informations d’identification administratives sur l’ordinateur client de modifier les paramètres du dossier du cache client pour le client Configuration Manager à l’aide de Configuration Manager dans le Panneau de configuration de l’ordinateur client.  

Exemple : `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 Spécifie un domaine DNS pour que les clients localisent les points de gestion qui sont publiés dans DNS. Lorsqu'un point de gestion est localisé, il indique au client d'autres points de gestion dans la hiérarchie. Cela signifie qu'il n'est pas nécessaire que le point de gestion qui est localisé à l'aide de la publication DNS provienne du site du client, et il peut s'agir de n'importe quel point de gestion de la hiérarchie.  

> [!NOTE]  
>  Vous n'êtes pas tenu de spécifier cette propriété si le client se trouve dans le même domaine qu'un point de gestion publié. Dans ce cas, le domaine du client est automatiquement utilisé pour rechercher des points de gestion dans DNS.  

 Pour plus d’informations sur la publication DNS comme méthode d’emplacement du service pour les clients Configuration Manager, consultez [Emplacement du service et façon dont les clients déterminent leur point de gestion attribué](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) dans [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

> [!NOTE]  
>  Par défaut, la publication DNS n’est pas activée dans Configuration Manager.  

 Exemple : `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

Indique le point d’état de secours qui reçoit et traite les messages d’état envoyés par les ordinateurs clients Configuration Manager.  

Pour plus d’informations sur le point d’état de secours, consultez [Déterminer si vous avez besoin d’un point d’état de secours](/sccm/core/clients/deploy/plan#determine-if-you-need-a-fallback-status-point).  

Exemple : `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 Spécifie que la présence de la version minimale requise de Microsoft Application Virtualization (App-V) n’est pas vérifiée avant l’installation du client.  

> [!IMPORTANT]  
>  Si vous installez le client Configuration Manager sans installer App-V, vous ne pouvez pas déployer des applications virtuelles.  

 Exemple : `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

Indique que l’état du client sera signalé, mais que les problèmes détectés au niveau du client ne seront pas corrigés.  

Exemple : `CCMSetup.exe NOTIFYONLY=TRUE`  

Pour plus d’informations, voir [Comment configurer l’état du client dans System Center Configuration Manager](configure-client-status.md).  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Si un client Configuration Manager possède la mauvaise clé racine approuvée de Configuration Manager et ne peut pas contacter de point de gestion approuvé pour recevoir la nouvelle clé racine approuvée, vous devez supprimer manuellement l’ancienne clé racine approuvée à l’aide de cette propriété. Cette situation peut se produire quand vous déplacez un client d’une hiérarchie de site à une autre. Cette propriété s'applique aux clients qui utilisent la communication client HTTP et HTTPS.  

 Exemple : `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Permet la réattribution de site automatique pour les mises à niveau du client si cette propriété est utilisée avec [SMSSITECODE](#smssitecode)=AUTO.

Exemple : `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Spécifie l'emplacement du dossier de cache du client sur l'ordinateur client, qui stocke les fichiers temporaires. Par défaut, l'emplacement est *%Windir\ccmcache*.  

Exemple : `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Cette propriété peut être utilisée avec la propriété SMSCACHEFLAGS pour contrôler l’emplacement du dossier du cache du client.  

Exemple : `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` installe le dossier du cache du client sur le lecteur de disque disponible le plus grand du client.  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Spécifie davantage les détails d'installation pour le dossier mis dans la mémoire cache du client. Vous pouvez utiliser les propriétés de SMSCACHEFLAGS individuellement ou en combinaison, séparées par des points-virgules. Si cette propriété n’est pas spécifiée, le dossier mis dans la mémoire cache du client est installé conformément à la propriété SMSCACHEDIR, il n'est pas compressé et la valeur de SMSCACHESIZE est utilisée pour sa taille en Mo.  

Ce paramètre est ignoré lorsque vous mettez à niveau un client existant.  

Propriétés :  

-   PERCENTDISKSPACE : indique la taille du dossier sous forme de pourcentage de l’espace disque total. Si vous indiquez cette propriété, vous devez également indiquer la propriété SMSCACHESIZE comme valeur de pourcentage à utiliser.  

-   PERCENTFREEDISKSPACE : indique la taille du dossier sous forme de pourcentage de l’espace disque disponible. Si vous indiquez cette propriété, vous devez également indiquer la propriété SMSCACHESIZE comme valeur de pourcentage à utiliser. Par exemple, si le disque dispose de 10 Mo libres et que SMSCACHESIZE indique 50, cela signifie que la taille du dossier est définie sur 5 Mo. Vous ne pouvez pas utiliser cette propriété avec la propriété PERCENTDISKSPACE.  

-   MAXDRIVE : indique que le dossier doit être installé sur le disque le plus volumineux disponible. Cette valeur sera ignorée si un chemin a été spécifié avec la propriété SMSCACHEDIR.  

-   MAXDRIVESPACE : indique que le dossier doit être installé sur le lecteur de disque possédant l’espace disponible le plus important. Cette valeur sera ignorée si un chemin a été spécifié avec la propriété SMSCACHEDIR.  

-   NTFSONLY : indique que le dossier peut être installé uniquement sur des lecteurs de disque NTFS. Cette valeur sera ignorée si un chemin a été spécifié avec la propriété SMSCACHEDIR.  

-   COMPRESS : indique que le dossier doit être conservé sous une forme compressée.  

-   FAILIFNOSPACE : indique que le logiciel client doit être supprimé si l’espace est insuffisant pour installer le dossier.  

Exemple : `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> À partir de Configuration Manager version 1606, de nouveaux paramètres client sont disponibles pour spécifier la taille du dossier du cache du client. L’ajout de ces paramètres du client remplace l’utilisation de SMSCACHESIZE comme propriété client.msi pour spécifier la taille du cache du client. Pour plus d’informations, consultez les [paramètres du client pour la taille du cache](about-client-settings.md#client-cache-settings).  

Pour la version 1602 et antérieure, SMSCACHESIZE indique la taille du dossier mis dans la mémoire cache du client en mégaoctets (Mo) ou sous forme de pourcentage quand elle est utilisée avec la propriété PERCENTDISKSPACE ou PERCENTFREEDISKSPACE. Si cette propriété n’est pas définie, la taille maximale du dossier est par défaut de 5120 Mo. La valeur la plus basse que vous pouvez spécifier est 1 Mo.  

> [!NOTE]  
>  Si un nouveau package qui doit être téléchargé peut provoquer le dépassement de la taille maximale du dossier et que le dossier ne peut pas être purgé pour libérer un espace suffisant, le téléchargement du package échoue et le programme ou l'application ne s'exécute pas.  

Ce paramètre est ignoré lorsque vous mettez à niveau un client existant et lorsque le client télécharge les mises à jour logicielles.  

Exemple : `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  Si vous réinstallez un client, vous ne pouvez pas utiliser les propriétés d'installation SMSCACHESIZE ou SMSCACHEFLAGS pour définir une taille de cache inférieure à la taille de cache précédente. Si vous essayez d’effectuer cette opération, votre valeur est ignorée et la taille du cache est automatiquement définie à la taille précédente.  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Indique l’emplacement et l’ordre dans lesquels le programme d’installation de Configuration Manager vérifie les paramètres de configuration. La propriété est une chaîne contenant un ou plusieurs caractères, chacun définissant une source de configuration spécifique. Utilisez les caractères R, P, M et U seuls ou en combinaison :  

-   R : vérification des paramètres de configuration dans le Registre.  

   Pour en savoir plus, consultez [les informations sur le stockage des propriétés d’installation du client dans le Registre](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision).  

-   P : vérification des paramètres de configuration dans les propriétés d’installation fournies à l’invite de commandes.  

-   M : vérification des paramètres existants à l’occasion de la mise à niveau d’un ancien client avec le logiciel client Configuration Manager.  

-   U : mise à niveau du client installé vers une version plus récente (et utilisation du code de site attribué).  

 Par défaut, l’installation du client utilise `PU` pour vérifier d’abord les propriétés d’installation, puis les paramètres existants.  

 Exemple : `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 Indique si le client peut utiliser les services WINS (Windows Internet Name Service) pour trouver un point de gestion qui accepte les connexions HTTP. Les clients utilisent cette méthode lorsqu'ils ne peuvent pas trouver de point de gestion dans les services de domaine Active Directory ou dans DNS.  

 Cette propriété n’a pas d’impact sur le fait que le client utilise ou non WINS pour la résolution de noms.  

 Vous pouvez configurer deux modes différents pour cette propriété :  

-   NOWINS : il s’agit du paramètre le plus sûr pour cette propriété et il empêche les clients de trouver un point de gestion dans le service WINS.  Lorsque vous utilisez ce paramètre, les clients doivent disposer d'une autre méthode de localisation d'un point de gestion sur l'Intranet, telle que les services de domaine Active Directory ou en utilisant la publication DNS.  

-   WINSSECURE (valeur par défaut) : dans ce mode, un client qui utilise la communication HTTP peut utiliser WINS pour trouver un point de gestion. Toutefois, le client doit disposer d'une copie de la clé racine approuvée avant de pouvoir se connecter correctement au point de gestion. Pour plus d’informations, consultez [Planification de la clé racine approuvée](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) dans [Planifier la sécurité dans System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  


 Exemple : `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Spécifie un point de gestion initial à utiliser par le client Configuration Manager.  

> [!IMPORTANT]  
>  Si le point de gestion accepte uniquement les connexions clientes sur HTTPS, vous devez ajouter le préfixe https:// au nom du point de gestion.  

Exemple : `CCMSetup.exe SMSMP=smsmp01.contoso.com`

Exemple : `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Indique la clé racine approuvée de Configuration Manager lorsque celle-ci ne peut pas être récupérée à partir des services de domaine Active Directory. Cette propriété s'applique aux clients qui utilisent la communication client HTTP et HTTPS. Pour plus d’informations, consultez [Planification de la clé racine approuvée](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) dans [Planifier la sécurité dans System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Exemple : `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Utilisée pour réinstaller la clé racine approuvée de Configuration Manager. Indique le chemin d'accès complet et le nom de fichier d'un fichier contenant la clé racine approuvée. Cette propriété s'applique aux clients qui utilisent la communication client HTTP et HTTPS. Pour plus d’informations, consultez [Planification de la clé racine approuvée](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) dans [Planifier la sécurité dans System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Exemple : 'CCMSetup.exe SMSROOTKEYPATH=&lt;chemin_complet_et_nom_de_fichier\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 Spécifie le chemin d'accès complet et le nom de fichier .cer du certificat auto-signé exporté sur le serveur de site.  

 Ce certificat est stocké dans le magasin de certificats **SMS** et porte le nom d'objet **Serveur de site** et le nom convivial **Certificat de signature du serveur de site**.  

 Exemple : **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;chemin _complet_et_nom_de_fichier\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Indique le site Configuration Manager auquel attribuer le client Configuration Manager. Il peut s’agir d’un code de site à trois caractères ou du mot AUTO. Si AUTO est spécifié ou si cette propriété n’est pas spécifiée, le client tente de déterminer son affectation de site Configuration Manager à partir des services de domaine Active Directory ou d’un point de gestion spécifié. Pour activer AUTO pour les mises à niveau du client, vous devez également affecter à [SITEREASSIGN](#sitereassign) la valeur TRUE.    

> [!NOTE]  
>  N'utilisez pas AUTO si vous spécifiez également le point de gestion basé sur Internet (CCMHOSTNAME). Dans ce cas, vous devez directement attribuer le client à son site.  

 Exemple : `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> Valeurs d'attribut prises en charge pour les critères de sélection de certificat PKI  
 Configuration Manager prend en charge les valeurs d’attribut suivantes pour les critères de sélection de certificat PKI :  

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

