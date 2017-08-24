---
title: "Variables d’action de séquence de tâches | Microsoft Docs"
description: "Les variables d’action de séquence, telles que les variables de paramètres réseau, permettent de spécifier les paramètres de configuration d’une seule étape de séquence de tâches Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2269031-0977-4f01-a274-420e00630575
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 6049ec2369e0a97b21ce6523ba8448335385ab9a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Variables d’action de séquence de tâches dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les variables d’action de séquence de tâches spécifient les paramètres de configuration utilisés par une seule étape de séquence de tâches Configuration Manager. Par défaut, les paramètres utilisés par une étape de séquence de tâches sont initialisés avant l'exécution de l'étape et sont disponibles uniquement lors de l'exécution de l'étape de séquence de tâches associée. En d'autres termes, le paramètre de variable de séquence de tâches est ajouté à l'environnement de la séquence de tâches avant l'exécution de l'étape de séquence de tâches, et la valeur est supprimée de l'environnement de la séquence de tâches après exécution de l'étape de séquence de tâches.  

## <a name="action-variable-example"></a>Exemple de variable d'action  
 Par exemple, vous pouvez spécifier un répertoire de départ pour une action de ligne de commande à l'aide de l'étape de séquence de tâches **Exécuter la ligne de commande** . Cette étape comprend une propriété **Démarrer dans** dont la valeur par défaut est stockée dans le même environnement de la séquence de tâches que la variable **WorkingDirectory** . La variable d'environnement **WorkingDirectory** est initialisée avant l'exécution de l'action de séquence de tâches **Exécuter la ligne de commande** . Lors de l'étape **Exécuter la ligne de commande** , la valeur **WorkingDirectory** est accessible via la propriété **Démarrer dans** . Une fois l'étape de séquence de tâches terminée, la valeur de la variable **WorkingDirectory** est supprimée de l'environnement de la séquence de tâches. Si la séquence contient une autre étape **Exécuter la ligne de commande** , la nouvelle variable **WorkingDirectory** est initialisée et définie d'après la valeur de démarrage de l'étape de séquence de tâches en question.  

 Tandis que la valeur par défaut d'un paramètre d'action de séquence de tâches reste présente lors de l'exécution de l'étape de séquence de tâches, toutes les nouvelles valeurs que vous définissez peuvent être utilisées par plusieurs étapes de la séquence. Si vous faites appel à des méthodes de création de variables de séquence de tâches pour remplacer une valeur de variable intégrée, la nouvelle valeur demeure dans l'environnement et remplace la valeur par défaut des autres étapes de la séquence de tâches. Dans l’exemple précédent, si une étape **Définir une variable de séquence de tâches** est ajoutée comme première étape de la séquence de tâches et qu’elle attribue à la variable d’environnement **WorkingDirectory** la valeur **C:\\**, les deux étapes **Exécuter la ligne de commande** de la séquence de tâches utilisent la nouvelle valeur de répertoire de démarrage.  

## <a name="action-variables-for-task-sequence-actions"></a>Variables d'action pour des actions de séquence de tâches  
 Les variables de séquence de tâches Configuration Manager sont regroupées en fonction de l’action de séquence de tâches à laquelle est elles sont associées. Utilisez les liens suivants pour collecter des informations sur les variables d'action associées à une action spécifique. Les variables de séquence de tâches régissent le fonctionnement de l’action de séquence de tâches. L’action de séquence de tâches lit et utilise les variables que vous marquez en tant que variables d’entrée. Vous pouvez également utiliser l’action Définir la variable de séquence de tâches ou l’objet COM TSEnvironment pour définir les variables lors de l’exécution. Seule l’action de séquence de tâches marque les variables en tant que variables de sortie, qui sont lues par les actions qui se produisent ultérieurement dans la séquence de tâches.  

> [!NOTE]  
>  Toutes les actions de séquence de tâches ne sont pas associées à un ensemble de variables de séquence de tâches. Par exemple, bien qu'il existe des variables associées à l'action Activer BitLocker, il n'existe aucune variable associée à l'action Désactiver BitLocker.  

###  <a name="BKMK_ApplyDataImage"></a> Variables d'action de séquence de tâches Appliquer l'image de données  
 Les variables pour cette action spécifient quelle image d'un fichier WIM est appliquée à l'ordinateur de destination et s'il faut supprimer les fichiers sur la partition de destination. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Étape de séquence de tâches Appliquer l’image de données](task-sequence-steps.md#BKMK_ApplyDataImage).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (entrée)|Spécifie la valeur d'index de l'image qui est appliquée à l'ordinateur de destination.|  
|OSDWipeDestinationPartition<br /><br /> (entrée)|Spécifie s'il faut supprimer les fichiers situés sur la partition de destination.<br /><br /> Valeurs valides :<br /><br /> **« true »** (par défaut)<br /><br /> **« false »**|  

###  <a name="BKMK_ApplyDriverPackage"></a> Variables de l'action de séquence de tâches Appliquer le package de pilotes  
 Les variables pour cette action spécifient les informations de l'installation des pilotes de stockage de masse et s'il faut installer des pilotes non signés. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Appliquer le package de pilotes](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (entrée)|Spécifie l'ID de contenu du pilote de périphérique de stockage de masse à installer à partir du package de pilotes. Si vous ne spécifiez pas ce paramètre, aucun pilote de stockage de masse n'est installé.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (entrée)|Spécifie le fichier INF du pilote de stockage de masse à installer.<br /><br /> <br /><br /> Cette variable de séquence de tâches est requise si OSDApplyDriverBootCriticalContentUniqueID est défini.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (entrée)|Spécifie si un pilote de périphérique de stockage de masse est installé, qui doit être de type **scsi**.<br /><br /> <br /><br /> Cette variable de séquence de tâches est requise si OSDApplyDriverBootCriticalContentUniqueID est défini.|  
|OSDApplyDriverBootCriticalID<br /><br /> (entrée)|Spécifie l'ID critique de démarrage du pilote de périphérique de stockage de masse à installer. Cet ID apparaît dans la section «**scsi**» du fichier txtsetup.oem du pilote de périphérique.<br /><br /> <br /><br /> Cette variable de séquence de tâches est requise si OSDApplyDriverBootCriticalContentUniqueID est défini.|  
|OSDAllowUnsignedDriver<br /><br /> (entrée)|Spécifie s'il faut configurer Windows pour autoriser l'installation de pilotes de périphérique non signés. Cette variable de séquence de tâches n'est pas utilisée au cours du déploiement du système d'exploitation Windows Vista et version ultérieure.<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  

###  <a name="BKMK_ApplyNetworkSettings"></a> Variables de l'action de séquence de tâches Appliquer les paramètres réseau  
 Les variables pour cette action spécifient les paramètres réseau de l'ordinateur de destination, tels que les paramètres pour les cartes réseau de l'ordinateur, les paramètres de domaine et les paramètres de groupe de travail. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Appliquer l’étape des paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (entrée)|Cette variable de séquence de tâches est une variable de matrice. Chaque élément de la matrice représente les paramètres d'une carte réseau de l'ordinateur. Vous accédez aux paramètres définis pour chaque carte en combinant le nom de la variable de matrice avec le numéro de carte réseau de base zéro et le nom de propriété.<br /><br /> <br /><br /> Si plusieurs cartes réseau sont configurées dans cette action de séquence de tâches, les propriétés de la deuxième carte sont définies en précisant son numéro dans le nom de la variable, par exemple OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList, OSDAdapter1EnableWINS et ainsi de suite.<br /><br /> <br /><br /> Par exemple, vous pouvez utiliser les noms de variables suivants pour définir les propriétés de la première carte réseau configurée dans l'action de séquence de tâches :<br /><br /> <ul><li>**OSDAdapter0EnableDHCP** - true pour activer le protocole DHCP (Dynamic Host Configuration Protocol) de la carte.<br />    Ce paramètre est obligatoire. Les valeurs possibles sont True et False.</li><li>**OSDAdapter0IPAddressList** - Liste délimitée par des virgules des adresses IP de la carte. Cette propriété est ignorée sauf si **EnableDHCP** est réglé sur **false**.<br />    Ce paramètre est obligatoire.</li><li>**OSDAdapter0SubnetMask** - Liste délimitée par des virgules des masques de sous-réseaux. Cette propriété est ignorée sauf si **EnableDHCP** est réglé sur **false**.<br />    Ce paramètre est obligatoire.</li><li>**OSDAdapter0Gateways** - Liste délimitée par des virgules des adresses IP de passerelle. Cette propriété est ignorée sauf si **EnableDHCP** est réglé sur **false**.<br />    Ce paramètre est obligatoire.</li><li>**OSDAdapter0DNSDomain** : domaine DNS (Domain Name System) de la carte.</li><li>**OSDAdapter0DNSServerList** - Liste délimitée par des virgules des serveurs DNS de la carte.<br />    Ce paramètre est obligatoire.</li><li>**OSDAdapter0EnableDNSRegistrationtrue** - **true** pour enregistrer l’adresse IP de la carte dans DNS.</li><li>**OSDAdapter0EnableFullDNSRegistrationtrue** - **true** pour enregistrer l’adresse IP de la carte dans DNS sous le nom DNS complet de l’ordinateur.</li><li>**OSDAdapter0EnableIPProtocolFilteringtrue** - **true** pour activer le filtrage de protocole IP sur la carte.</li><li>**OSDAdapter0IPProtocolFilterList** - Liste délimitée par des virgules des protocoles autorisés à s’exécuter sur IP. Cette propriété est ignorée sauf si **EnableIPProtocolFiltering** est réglé sur **false**.</li><li>**OSDAdapter0EnableTCPFilteringtrue** - **true** pour activer le filtrage de port TCP sur la carte.</li><li>**OSDAdapter0TCPFilterPortList** – Liste délimitée par des virgules des ports auxquels les autorisations d’accès à TCP sont à accorder. Cette propriété est ignorée sauf si **EnableTCPFiltering** est réglé sur **false**.</li><li>**OSDAdapter0TcpipNetbiosOptions** - Options pour NetBIOS sur TCP/IP. Les valeurs possibles sont les suivantes :<br /><br /> <ul><li>0 Utiliser des paramètres NetBIOS du serveur DHCP</li><li>1 Activer NetBIOS avec TCP/IP</li><li>2 Désactiver NetBIOS avec TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINStrue** - **true** pour utiliser WINS pour la résolution de noms.</li><li>**OSDAdapter0WINSServerList** - Liste délimitée par des virgules des adresses IP du serveur WINS. Cette propriété est ignorée sauf si **EnableWINS** est réglé sur **true**.</li><li>**OSDAdapter0MacAddress** - Adresse MAC (Media Access Controller) utilisée pour faire correspondre les paramètres à la carte réseau physique.</li><li>**OSDAdapter0Name** - Nom de la connexion réseau tel qu’il apparaît dans le programme Connexions réseau du Panneau de configuration. La longueur du nom est comprise entre 0 et 255 caractères.</li><li>**OSDAdapter0Index** - Index des paramètres de carte réseau dans le tableau des paramètres.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (entrée)|Spécifie le nombre de cartes réseau installées sur l'ordinateur de destination. Quand la valeur **OSDAdapterCount** est définie, toutes les options de configuration de chaque carte doivent être définies. Par exemple, si vous définissez la valeur **OSDAdapterTCPIPNetbiosOptions** pour une carte spécifique, toutes les valeurs pour cette carte doivent également être configurées.<br /><br /> <br /><br /> Si cette valeur n’est pas spécifiée, toutes les valeurs **OSDAdapter** sont ignorées.|  
|OSDDNSDomain<br /><br /> (entrée)|Spécifie le serveur DNS principal utilisé sur l'ordinateur de destination.|  
|OSDDomainName<br /><br /> (entrée)|Spécifie le nom du domaine Windows auquel l'ordinateur de destination se joint. La valeur spécifiée doit être un nom de domaine de services de domaine Active Directory valide.|  
|OSDDomainOUName<br /><br /> (entrée)|Spécifie le format du nom RFC 1779 de l'unité d'organisation que l'ordinateur de destination joint. S'il est spécifié, la valeur doit contenir le chemin complet.<br /><br /> Exemple :<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (entrée)|Spécifie si le filtrage TCP/IP est activé.<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  
|OSDJoinAccount<br /><br /> (entrée)|Spécifie le compte réseau utilisé pour ajouter l'ordinateur de destination à un domaine Windows.|  
|OSDJoinPassword<br /><br /> (entrée)|Spécifie le mot de passe réseau utilisé pour ajouter l'ordinateur de destination à un domaine Windows.|  
|OSDNetworkJoinType<br /><br /> (entrée)|Spécifie si l'ordinateur de destination se joint à un domaine Windows ou un groupe de travail.<br /><br /> **« 0 »** indique que l'ordinateur de destination se joint à un domaine Windows. **« 1 »** spécifie que l'ordinateur se joint à un groupe de travail.<br /><br /> Valeurs valides :<br /><br /> **« 0 »**<br /><br /> **« 1 »**|  
|OSDDNSSuffixSearchOrder<br /><br /> (entrée)|Spécifie l'ordre de recherche DNS de l'ordinateur de destination.|  
|OSDWorkgroupName<br /><br /> (entrée)|Spécifie le nom du groupe de travail auquel l'ordinateur de destination se joint.<br /><br /> Vous devez spécifier cette valeur ou la valeur **OSDDomainName** . Le nom du groupe de travail est limité à 32 caractères.<br /><br /> Exemple :<br /><br /> **« Comptabilité »**|  

###  <a name="BKMK_ApplyOperatingSystem"></a> Variables de l'action de séquence de tâches Appliquer l'image du système d'exploitation  
 Les variables pour cette action spécifient les paramètres du système d'exploitation que vous souhaitez installer sur l'ordinateur de destination. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Appliquer l’image de système d’exploitation](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (entrée)|Spécifie le nom du fichier de réponse de déploiement du système d'exploitation associé au package de déploiement du système d'exploitation.|  
|OSDImageIndex<br /><br /> (entrée)|Spécifie la valeur d'index de l'image du fichier WIM qui est appliquée à l'ordinateur de destination.|  
|OSDInstallEditionIndex<br /><br /> (entrée)|Spécifie la version du système d'exploitation Windows Vista ou version ultérieure qui est installée. Si aucune version n'est précisée, le programme d'installation de Windows déterminera la version à installer à l'aide de la clé du produit référencé.<br /><br /> Utilisez uniquement une valeur égale à zéro (0) si les conditions suivantes sont vraies :<br /><br /> -   Vous installez un système d’exploitation antérieur à Windows Vista.<br />-   Vous installez une édition de licence en volume de Windows Vista ou version ultérieure, et aucune clé de produit n’est spécifiée.<br /><br /> Valeurs valides :<br /><br /> **« 0 »** (par défaut)|  
|OSDTargetSystemDrive (sortie)|Indique la lettre de lecteur de la partition contenant les fichiers du système d'exploitation.|  

###  <a name="BKMK_ApplyWindowsSettings"></a> Variables d'action de séquence de tâches Appliquer les paramètres Windows  
 Les variables pour cette action spécifient des paramètres Windows pour l'ordinateur de destination, tels que le nom de l'ordinateur, la clé de produit Windows, l'utilisateur et l'organisation inscrits et le mot de passe d'administrateur local. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Appliquer les paramètres Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (entrée)|Spécifie le nom de l'ordinateur de destination.<br /><br /> Exemple :<br /><br /> **« %_SMSTSMachineName% »** (par défaut)|  
|OSDProductKey<br /><br /> (entrée)|Spécifie la clé de produit Windows. La valeur spécifiée doit comprendre entre 1 et 255 caractères.|  
|OSDRegisteredUserName<br /><br /> (entrée)|Spécifie le nom d'utilisateur inscrit par défaut dans le nouveau système d'exploitation. La valeur spécifiée doit comprendre entre 1 et 255 caractères.|  
|OSDRegisteredOrgName<br /><br /> (entrée)|Spécifie le nom d'organisation inscrit par défaut dans le nouveau système d'exploitation. La valeur spécifiée doit comprendre entre 1 et 255 caractères.|  
|OSDTimeZone<br /><br /> (entrée)|Spécifie le paramètre de fuseau horaire par défaut utilisé dans le nouveau système d'exploitation.|  
|OSDServerLicenseMode<br /><br /> (entrée)|Spécifie le mode de licence Windows Server utilisé.<br /><br /> Valeurs valides :<br /><br /> **« PerSeat »**<br /><br /> **« PerServer »**|  
|OSDServerLicenseConnectionLimit<br /><br /> (entrée)|Spécifie le nombre maximal de connexions autorisées. Le nombre spécifié doit comprendre entre 5 et 9 999 connexions.|  
|OSDRandomAdminPassword<br /><br /> (entrée)|Spécifie un mot de passe généré de manière aléatoire pour le compte de l'administrateur dans le nouveau système d'exploitation. Si cette variable est définie sur **true**, le compte d’administrateur local est désactivé sur l’ordinateur cible. Si elle est définie sur **false**, il est activé sur l’ordinateur cible et son mot de passe prend la valeur de la variable **OSDLocalAdminPassword**.<br /><br /> Valeurs valides :<br /><br /> **« true »** (par défaut)<br /><br /> **« false »**|  
|OSDLocalAdminPassword<br /><br /> (entrée)|Spécifie le mot de passe de l'administrateur local. Cette valeur est ignorée si vous sélectionnez l'option **Générer de façon aléatoire le mot de passe de l'administrateur local et désactiver le compte sur toutes les plates-formes prises en charge** . La valeur spécifiée doit comprendre entre 1 et 255 caractères.|  

###  <a name="BKMK_AutoApplyDrivers"></a> Variables de l'action de séquence de tâches Appliquer automatiquement les pilotes  
 Les variables pour cette action spécifient quels pilotes Windows sont installés sur l'ordinateur de destination et si des pilotes non signés sont installés. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Appliquer automatiquement les pilotes](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (entrée)|Liste délimitée par des virgules des ID de catégorie uniques du catalogue de pilotes. Si elle est spécifiée, l'action de séquence de tâches **Appliquer automatiquement les pilotes** ne prend en compte que les pilotes compris dans au moins une de ces catégories lors de l'installation de ceux-ci. Cette valeur est facultative et n'est pas définie par défaut. Les ID de catégorie peuvent être obtenus par énumération de la liste des objets **SMS_CategoryInstance** sur le site.|  
|OSDAllowUnsignedDriver<br /><br /> (entrée)|Spécifie si Windows est configuré pour autoriser l'installation de pilotes de périphérique non signés. Cette variable de séquence de tâches n'est pas utilisée au cours du déploiement de Windows Vista et des systèmes d'exploitation ultérieurs.<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (entrée)|Spécifie ce que fait l'action de la séquence de tâches s'il existe dans le catalogue de pilotes plusieurs pilotes de périphérique compatibles avec un périphérique matériel. Si cette variable est définie sur **true**, seul le meilleur pilote de périphérique est installé.  Si cette variable est définie sur **false**, tous les pilotes de périphériques compatibles sont installés et le système d’exploitation choisit le meilleur pilote à utiliser.<br /><br /> Valeurs valides :<br /><br /> **« true »** (par défaut)<br /><br /> **« false »**|  

###  <a name="BKMK_CaptureNetworkSettings"></a> Variables de l'action de séquence de tâches Capturer les paramètres réseau  
 Les variables pour cette action spécifient si les informations de configuration des paramètres de carte réseau (TCP/IP, DNS et WINS) sont capturées et si les informations d'appartenance à un groupe de travail ou un domaine sont migrées dans le cadre du déploiement du système d'exploitation. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Capturer les paramètres réseau](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (entrée)|Spécifie si les informations de configuration des paramètres de carte réseau (TCP/IP, DNS et WINS) sont capturées.<br /><br /> Exemples :<br /><br /> **« true »** (par défaut)<br /><br /> **« false »**|  
|OSDMigrateNetworkMembership<br /><br /> (entrée)|Spécifie si les informations d'appartenance à un groupe de travail ou un domaine sont migrées dans le cadre du déploiement du système d'exploitation.<br /><br /> Exemples :<br /><br /> **« true »** (par défaut)<br /><br /> **« false »**|  

###  <a name="BKMK_CaptureOperatingSystemImage"></a> Variables de l'action de séquence de tâches Capturer l'image du système d'exploitation  
 Les variables pour cette action spécifient des informations sur l'image du système d'exploitation capturée, telles que l'emplacement de stockage de l'image, le créateur de l'image et une description de l'image. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Capturer l’image du système d’exploitation](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (entrée)|Spécifie un nom de compte Windows qui dispose d'autorisations pour stocker l'image capturée sur un partage réseau.|  
|OSDCaptureAccountPassword<br /><br /> (entrée)|Spécifie le mot de passe du compte Windows employé pour le stockage de l'image capturée sur un partage réseau.|  
|OSDCaptureDestination<br /><br /> (entrée)|Spécifie l'emplacement où l'image capturée du système d'exploitation est enregistrée. Le nom du répertoire est limité à 255 caractères.|  
|OSDImageCreator<br /><br /> (entrée)|Nom facultatif de l'utilisateur qui a créé l'image. Ce nom est stocké dans le fichier WIM. Le nom de l'utilisateur est limité à 255 caractères.|  
|OSDImageDescription<br /><br /> (entrée)|Description facultative de l'image du système d'exploitation capturée définie par l'utilisateur. Cette description est stockée dans le fichier WIM. La description est limitée à 255 caractères.|  
|OSDImageVersion<br /><br /> (entrée)|Numéro de version facultatif défini par l'utilisateur à attribuer à l'image du système d'exploitation capturée. Ce numéro de version est stocké dans le fichier WIM. Cette valeur peut être n'importe quelle combinaison de lettres avec une longueur maximale de 32 caractères.|  
|OSDTargetSystemRoot<br /><br /> (entrée)|Spécifie le chemin du répertoire Windows où a été installé le système d'exploitation sur l'ordinateur de référence. Configuration Manager vérifie que ce système d’exploitation est pris en charge pour la capture.|  

###  <a name="BKMK_CaptureUserState"></a> Variables de l'action de séquence de tâches Capturer l'état utilisateur  
 Les variables pour cette action spécifient des informations utilisées par l’outil de migration de l’état utilisateur (USMT), telles que le dossier où l’état utilisateur est enregistré, des options de ligne de commande pour l’outil USMT et les fichiers de configuration utilisés pour contrôler la capture des profils utilisateur.  Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Capturer l’état utilisateur](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrée)|Le chemin d'accès UNC ou local du dossier sur lequel l'état utilisateur est enregistré. Pas de valeur par défaut.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (entrée)|Spécifie des options de ligne de commande de l’outil de migration utilisateur (USMT) qui sont utilisées pour la capture de l’état utilisateur, mais qui n’apparaissant pas dans l’interface utilisateur de Configuration Manager. Ces options supplémentaires sont spécifiées sous forme d'une chaîne ajoutée à la ligne de commande USMT générée de manière automatique.<br /><br /> <br /><br /> La précision des options USMT spécifiées avec cette variable de séquence de tâches n'est pas validée avant l'exécution de la séquence de tâches.|  
|OSDMigrateMode<br /><br /> (entrée)|Permet de personnaliser les fichiers capturés par l'outil de migration de l'état utilisateur (USMT). Si cette variable est définie sur « Simple », seuls les fichiers de configuration USMT standard sont utilisés. Si elle est définie sur « Avancé », la variable de séquence de tâches OSDMigrateConfigFiles spécifie les fichiers de configuration utilisés par USTM.<br /><br /> Valeurs valides :<br /><br /> **« Simple »**<br /><br /> **« Avancé »**|  
|OSDMigrateConfigFiles<br /><br /> (entrée)|Spécifie les fichiers de configuration employés pour contrôler la capture des profils utilisateur. Cette variable est utilisée uniquement si OSDMigrateMode est défini sur « Avancé ». Cette valeur de liste délimitée par des virgules est définie pour effectuer une migration du profil utilisateur personnalisée.<br /><br /> Exemple : miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (entrée)|Permet de poursuivre la capture de l'état utilisateur si certains fichiers ne peuvent pas être capturés.<br /><br /> Valeurs valides :<br /><br /> **« true »** (par défaut)<br /><br /> **« false »**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrée)|Active la journalisation documentée pour l'outil de migration de l'état utilisateur (USMT).<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (entrée)|Spécifie si les fichiers cryptés sont capturés.<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  
|_OSDMigrateUsmtPackageID<br /><br /> (entrée)|Spécifie l’ID du package Configuration Manager qui contiendra les fichiers USMT. Cette variable est requise.|  

###  <a name="BKMK_CaptureWindowsSettings"></a> Variables de l'action de séquence de tâches Capturer les paramètres Windows  
 Les variables pour cette action spécifient si des paramètres Windows spécifiques sont migrés vers l'ordinateur de destination, tels que le nom de l'ordinateur, le nom d'organisation inscrit et les informations sur les fuseaux horaires. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Capturer les paramètres Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (entrée)|Spécifie si le nom de l'ordinateur est migré.<br /><br /> Valeurs valides :<br /><br /> **« true »** (par défaut)<br /><br /> **« false »**<br /><br /> Si la valeur est « true », la variable OSDComputerName prend le nom NetBIOS de l’ordinateur.|  
|OSDComputerName<br /><br /> (sortie)|Défini sur le nom NetBIOS de l'ordinateur. La valeur est définie uniquement si la variable OSDMigrateComputerName a la valeur « true ».|  
|OSDMigrateRegistrationInfo<br /><br /> (entrée)|Spécifie si les informations d'utilisateur et d'organisation de l'ordinateur sont migrées.<br /><br /> Valeurs valides :<br /><br /> **« true »** (par défaut)<br /><br /> **« false »**<br /><br /> Si la valeur est « true », la variable OSDRegisteredOrgName prend le nom d’organisation inscrit de l’ordinateur.|  
|OSDRegisteredOrgName<br /><br /> (sortie)|Défini sur le nom d'organisation inscrit de l'ordinateur. La valeur est définie uniquement si la variable OSDMigrateRegistrationInfo a la valeur « true ».|  
|OSDMigrateTimeZone<br /><br /> (entrée)|Spécifie si le fuseau horaire de l'ordinateur est migré.<br /><br /> Valeurs valides :<br /><br /> **« true »** (par défaut)<br /><br /> **« false »**<br /><br /> Si la valeur est « true », la variable OSDTimeZone est définie sur le fuseau horaire de l’ordinateur.|  
|OSDTimeZone<br /><br /> (sortie)|Défini sur le fuseau horaire de l'ordinateur. La valeur est définie uniquement si la variable OSDMigrateTimeZone a la valeur « true ».|  

###  <a name="BKMK_ConnecttoNetworkFolder"></a> Variables d'action de séquence de tâches Connexion à un dossier réseau  
 Les variables pour cette action spécifient des informations sur un dossier sur un réseau, telles que le compte utilisé et le mot de passe pour se connecter au dossier réseau, la lettre de lecteur du dossier et le chemin d'accès au dossier. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Se connecter à un dossier réseau](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (entrée)|Spécifie le compte d'administrateur utilisé pour se connecter au partage réseau.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (entrée)|Spécifie la lettre de lecteur réseau à laquelle se connecter. Cette valeur est facultative. Si vous ne la spécifiez pas, la connexion réseau doit alors être mappée à une lettre de lecteur. À l’inverse, si vous la spécifiez, cette valeur doit être comprise entre D: et Z:.  En outre, n’utilisez pas X: car il s’agit de la lettre de lecteur utilisée par Windows PE au cours de la phase Windows PE.<br /><br /> Exemples :<br /><br /> **« D: »**<br /><br /> **« E: »**|  
|SMSConnectNetworkFolderPassword<br /><br /> (entrée)|Spécifie le mot de passe réseau utilisé pour se connecter au partage réseau.|  
|SMSConnectNetworkFolderPath<br /><br /> (entrée)|Spécifie le chemin d'accès réseau pour la connexion.<br /><br /> Exemple :<br /><br /> **« \\\nom_serveur\nom_partage »**|  

###  <a name="BKMK_ConvertDisk"></a> Variables de l'action de séquence de tâches Convertir en disque dynamique  
 La variable pour cette action indique le numéro du disque physique à convertir d'un disque standard en disque dynamique. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Convertir en disque dynamique](task-sequence-steps.md#BKMK_ConvertDisktoDynamic).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDConvertDiskIndex<br /><br /> (entrée)|Spécifie le numéro du disque physique converti.|  

###  <a name="BKMK_EnableBitLocker"></a> Variables de l'action de séquence de tâches Activer BitLocker  
 Les variables pour cette action spécifient les options de mot de passe de récupération et de clé de démarrage utilisées pour activer BitLocker sur l'ordinateur de destination. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Activer BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (entrée)|Au lieu de créer un mot de passe de récupération aléatoire, l'action de la séquence de tâches **Activer BitLocker** utilise la valeur spécifiée comme mot de passe de récupération. La valeur doit être un mot de passe de récupération numérique BitLocker valide.|  
|OSDBitLockerStartupKey<br /><br /> (entrée)|Au lieu de générer une clé de démarrage aléatoire pour l’option de gestion de clé **Clé de démarrage sur USB uniquement**, l’action de séquence de tâches **Activer BitLocker** utilise le module de plateforme sécurisée (TPM) comme clé de démarrage. La valeur doit être une clé de démarrage BitLocker valide 256 bits codée en Base64.|  

###  <a name="BKMK_FormatPartitionDisk"></a> Variables de l'action de séquence de tâches Formater et partitionner le disque  
 Les variables pour cette action spécifient des informations pour le formatage et le partitionnement d'un disque physique, telles que le numéro du disque et un tableau de paramètres de partition. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Formater et partitionner le disque](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (entrée)|Spécifie le nombre de disques physiques à partitionner.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (entrée)|Spécifie si les optimisations d'alignement du cache sont désactivées lors du partitionnement du disque dur pour des raisons de compatibilité avec certains types de BIOS. Cette option peut être nécessaire lors du déploiement des systèmes d'exploitation Windows XP ou Windows Server 2003. Pour plus d'informations, consultez [l'article 931760](http://go.microsoft.com/fwlink/?LinkId=134081) et [l'article 931761](http://go.microsoft.com/fwlink/?LinkId=134082) de la Base de connaissances Microsoft.<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  
|OSDGPTBootDisk<br /><br /> (entrée)|Spécifie la nécessité de créer une partition EFI sur un disque dur GPT afin de pouvoir l'utiliser en tant que disque de démarrage sur des ordinateurs EFI.<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  
|OSDPartitions<br /><br /> (entrée)|Spécifie un tableau de paramètres de partition. Consultez la rubrique liée au kit de développement logiciel (SDK) pour accéder aux variables de matrice dans l'environnement de la séquence de tâches.<br /><br /> Cette variable de séquence de tâches est une variable de matrice. Chaque élément de la matrice représente les paramètres d'une partition simple sur le disque dur. Vous pouvez accéder aux paramètres définis pour chaque partition en combinant le nom de la variable de matrice avec le numéro de partition de disque de base zéro et le nom de propriété.<br /><br /> Par exemple, vous pouvez utiliser les noms de variables suivants pour définir les propriétés de la première partition créée sur le disque dur par cette séquence de tâches :<br /><br /> - **OSDPartitions0Type** : spécifie le type de partition. Cette propriété est obligatoire. Les valeurs valides sont : «**Principal**», «**Étendu**», «**Logique**» et «**Caché**».<br />-   **OSDPartitions0FileSystem** : spécifie le type de système de fichier à utiliser lors du formatage de la partition. Cette propriété est facultative. La partition n'est pas formatée si aucun système de fichier n'est spécifié. Les valeurs valides sont «**FAT32**» et «**NTFS**».<br />-   **OSDPartitions0Bootable** : indique si la partition est amorçable. Cette propriété est obligatoire. Si les disques MBR ont la valeur «**TRUE**», la partition sélectionnée est configurée comme active.<br />-   **OSDPartitions0QuickFormat** : spécifie le type de format utilisé. Cette propriété est obligatoire. Si la valeur est définie sur «**TRUE**», un formatage rapide est effectué. Autrement, le formatage complet est effectué.<br />-   **OSDPartitions0VolumeName** : spécifie le nom attribué au volume après formatage. Cette propriété est facultative.<br />-   **OSDPartitions0Size** : spécifie la taille de la partition. Les unités sont spécifiées par la variable **OSDPartitions0SizeUnits** . Cette propriété est facultative. Si cette propriété n'est pas spécifiée, la partition est créée en utilisant la totalité de l'espace disque disponible.<br />-   **OSDPartitions0SizeUnits** : spécifie les unités utilisées lors de l'interprétation de la variable de séquence de tâches **OSDPartitions0Size** . Cette propriété est facultative. Les valeurs valides sont «**Mo**» (par défaut), «**Go**» et «**Pourcent**».<br />-   **OSDPartitions0VolumeLetterVariable** : une fois créées, les partitions utilisent toujours la lettre de lecteur disponible suivante dans Windows PE. Utilisez cette propriété facultative pour spécifier le nom d'une autre variable de séquence de tâches qui enregistrera la nouvelle lettre de lecteur pour un usage ultérieur.<br /><br /> <br /><br /> Si plusieurs partitions sont définies dans la séquence de tâches, les propriétés de la deuxième partition peuvent être définies en utilisant leur index dans le nom de variable, par exemple : **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**, **OSDPartitions1VolumeName** , et ainsi de suite.|  
|OSDPartitionStyle<br /><br /> (entrée)|Spécifie le style de partition à utiliser lors du partitionnement du disque. «**MBR**» indique le style de partition à enregistrement de démarrage principal, et «**GPT**» indique le style Table de partition GUID.<br /><br /> Valeurs valides :<br /><br /> **« GPT »**<br /><br /> **« MBR »**|  

###  <a name="BKMK_InstallSoftwareUpdates"></a> Variables d'action de séquence de tâches Installer les mises à jour logicielles  
 La variable pour cette action spécifie s'il faut installer toutes les mises à jour ou uniquement les mises à jour obligatoires. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Installer les mises à jour logicielles](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action<br /><br /> (entrée)|Description|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (entrée)|Spécifie s'il faut installer toutes les mises à jour ou uniquement les mises à jour obligatoires.<br /><br /> Valeurs valides :<br /><br /> **« Tout »**<br /><br /> **« Obligatoire »**|  

###  <a name="BKMK_JoinDomainWorkgroup"></a> Variables de l'action de séquence de tâches Joindre le domaine ou le groupe de travail  
 Les variables pour cette action spécifient les informations nécessaires pour joindre l'ordinateur de destination à un domaine Windows ou à un groupe de travail. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Joindre le domaine ou le groupe de travail](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (entrée)|Spécifie le compte utilisé par l'ordinateur de destination pour se joindre au domaine Windows. Cette variable est requise lors de la jonction à un domaine.|  
|OSDJoinDomainName<br /><br /> (entrée)|Spécifie le nom d'un domaine Windows auquel l'ordinateur de destination se joint. Le nom de domaine Windows doit comprendre entre 1 et 255 caractères.|  
|OSDJoinDomainOUName<br /><br /> (entrée)|Spécifie le format du nom RFC 1779 de l'unité d'organisation que l'ordinateur de destination joint. S'il est spécifié, la valeur doit contenir le chemin complet. Le nom de l'unité d'organisation de domaine Windows doit comprendre entre 0 et 32 767 caractères. Ne définissez pas cette valeur si la variable **OSDJoinType** est définie sur « 1 » (joindre le groupe de travail).<br /><br /> Exemple :<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (entrée)|Spécifie le mot de passe réseau utilisé par l'ordinateur de destination pour se joindre au domaine Windows. Si la variable n'est pas spécifiée, l'ordinateur tente d'utiliser un mot de passe vide. Cette valeur est obligatoire si la variable **OSDJoinType** est définie sur «**0**» (joindre le domaine).|  
|OSDJoinSkipReboot<br /><br /> (entrée)|Spécifie s'il faut ignorer le redémarrage après que l'ordinateur de destination joint le domaine ou le groupe de travail.<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »**|  
|OSDJoinType<br /><br /> (entrée)|Spécifie si l'ordinateur de destination se joint à un domaine Windows ou un groupe de travail. Pour joindre l'ordinateur de destination à un domaine Windows, spécifiez «**0**». Pour joindre l'ordinateur de destination à un groupe de travail, spécifiez «**1**».<br /><br /> Valeurs valides :<br /><br /> **« 0 »**<br /><br /> **« 1 »**|  
|OSDJoinWorkgroupName<br /><br /> (entrée)|Spécifie le nom d'un groupe de travail auquel l'ordinateur de destination se joint. Le nom de groupe de travail doit comprendre entre 1 et 32 caractères.<br /><br /> Exemple :<br /><br /> **« Comptabilité »**|  

###  <a name="BKMK_PrepareWindowsCapture"></a> Variables de l'action de séquence de tâches Préparer Windows pour capture  
 Les variables pour cette action spécifient les informations utilisées pour capturer le système d'exploitation Windows à partir de l'ordinateur cible. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Préparer le client ConfigMgr pour capture](task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (entrée)|Spécifie si sysprep crée une liste de pilotes de périphérique de stockage de masse. Ce paramètre s’applique uniquement à Windows XP et à Windows Server 2003. Il remplit la section [SysprepMassStorage] de sysprep.inf avec les informations de tous les pilotes de stockage de masse qui sont pris en charge par l’image à capturer.<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  
|OSDKeepActivation<br /><br /> (entrée)|Spécifie si sysprep réinitialise l'indicateur d'activation du produit.<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  
|OSDTargetSystemRoot<br /><br /> (sortie)|Spécifie le chemin du répertoire Windows où a été installé le système d'exploitation sur l'ordinateur de référence. Configuration Manager vérifie que ce système d’exploitation est pris en charge pour la capture.|  

###  <a name="BKMK_ReleaseStateStore"></a> Variables de l'action de séquence de tâches Libérer le magasin d'état  
 Les variables pour cette action spécifient les informations utilisées pour libérer l'état utilisateur enregistré. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Libérer le magasin d’état](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrée)|Le chemin d'accès UNC ou local de l'emplacement à partir duquel l'état utilisateur est restauré. Cette valeur est utilisée par les actions de séquence de tâches **Capturer l'état utilisateur** et **Restaurer l'état utilisateur** .|  

###  <a name="BKMK_RequestState"></a> Variables de l'action de séquence de tâches Demander le magasin d'état  
 Les variables pour cette action spécifient les informations utilisées pour demander l'état d'utilisateur enregistré, telles que le dossier sur le point de migration d'état où sont stockées les données utilisateur. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Libérer le magasin d’état](../../osd/understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (entrée)|Indique si le compte d'accès réseau est utilisé comme un secours lorsque le compte d'ordinateur ne parvient pas à se connecter au point de migration d'état.<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  
|OSDStateSMPRetryCount<br /><br /> (entrée)|Spécifie le nombre de tentatives de recherche d'un point de migration d'état par l'étape de la séquence de tâches avant d'abandonner. Le nombre spécifié doit être compris entre 0 et 600.|  
|OSDStateSMPRetryTime<br /><br /> (entrée)|Indique la durée en secondes pendant laquelle l'étape de la séquence de tâches attend entre chaque tentative. Le nombre de secondes est limité à 30 caractères.|  
|OSDStateStorePath<br /><br /> (sortie)|Le chemin d'accès UNC au dossier sur le point de migration d'état où est stocké l'état d'utilisateur.|  

###  <a name="BKMK_RestartComputer"></a> Variables d'action de séquence de tâches Redémarrer l'ordinateur  
 Les variables pour cette action spécifient les informations utilisées pour redémarrer l'ordinateur de destination. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Redémarrer l’ordinateur](task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (entrée)|Indique le message à afficher aux utilisateurs avant le redémarrage de l'ordinateur de destination. Si vous ne définissez pas cette variable, le texte par défaut est affiché. Le message spécifié ne doit pas dépasser 512 caractères.<br /><br /> Exemple :<br /><br /> -   « Cet ordinateur va redémarrer. Enregistrez votre travail. »|  
|SMSRebootTimeout<br /><br /> (entrée)|Spécifie le nombre de secondes pendant lesquelles l'avertissement est affiché à l'attention de l'utilisateur avant le redémarrage de l'ordinateur. Précisez zéro seconde pour indiquer qu'aucun message de redémarrage n'apparaît.<br /><br /> Exemples :<br /><br /> **« 0 »** (par défaut)<br /><br /> **"5"**<br /><br /> **"10"**|  

###  <a name="BKMK_RestoreUserState"></a> Variables de l'action de séquence de tâches Restaurer l'état utilisateur  
 Les variables pour cette action spécifient les informations utilisées pour restaurer l'état d'utilisateur de l'ordinateur de destination, notamment le nom du chemin d'accès du dossier à partir duquel l'état utilisateur est restauré et la restauration effective ou non du compte d'ordinateur local. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Restaurer l’état utilisateur](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrée)|Le chemin d'accès UNC ou local du dossier à partir duquel l'état utilisateur est restauré.|  
|OSDMigrateContinueOnRestore<br /><br /> (entrée)|Indique que la restauration de l'état utilisateur se poursuit, même si certains fichiers ne peuvent pas être restaurés.<br /><br /> Valeurs valides :<br /><br /> **« true »** (par défaut)<br /><br /> **« false »**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrée)|Active la journalisation documentée pour l'outil USMT. Cette valeur est requise par l'action ; elle doit être définie sur « true » ou « false ».<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  
|OSDMigrateLocalAccounts<br /><br /> (entrée)|Indique si le compte d'ordinateur local est restauré.<br /><br /> Valeurs valides :<br /><br /> **« true »**<br /><br /> **« false »** (par défaut)|  
|OSDMigrateLocalAccountPassword<br /><br /> (entrée)|Si la variable **OSDMigrateLocalAccounts** est définie sur « true », cette variable doit contenir le mot de passe qui est affecté à tous les comptes locaux qui sont migrés. Comme le même mot de passe est attribué à tous les comptes locaux migrés, il est considéré comme un mot de passe temporaire qui sera modifié ultérieurement par une autre méthode que le déploiement de système d’exploitation Configuration Manager.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (entrée)|Indique les options de ligne de commande supplémentaires de l'outil de migration de l'état utilisateur (USMT) qui sont utilisées lors de la restauration de l'état utilisateur. Ces options supplémentaires sont spécifiées sous forme d'une chaîne ajoutée à la ligne de commande USMT générée de manière automatique. La précision des options USMT spécifiées avec cette variable de séquence de tâches n'est pas validée avant l'exécution de la séquence de tâches.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (entrée)|Spécifie l’ID du package Configuration Manager qui contient les fichiers USMT. Cette variable est requise.|  

###  <a name="BKMK_RunCommand"></a> Variables de l'action de séquence de tâches Exécuter la ligne de commande  
 Les variables pour cette action spécifient les informations utilisées pour exécuter une commande à partir de la ligne de commande, telles que le répertoire de travail où la commande est exécutée. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Exécuter la ligne de commande](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (entrée)|Par défaut, sous un système d'exploitation 64 bits, le programme situé dans la ligne de commande est localisé et exécuté au moyen d'un redirecteur de système de fichiers WOW64 afin de localiser les versions 32 bits des programmes et des DLL du système d'exploitation. La définition de cette variable sur « true » désactive l’utilisation du redirecteur de système de fichiers WOW64 pour permettre la localisation des versions 64 bits natives des programmes et des DLL du système d’exploitation. Cette variable est sans effet sous un système d'exploitation 32 bits.|  
|WorkingDirectory<br /><br /> (entrée)|Spécifie un répertoire de démarrage pour une action de ligne de commande. Le répertoire spécifié ne doit pas dépasser 255 caractères.<br /><br /> Exemples :<br /><br /> -   **« C:\\ »**<br />-   **« %SystemRoot% »**|  
|SMSTSRunCommandLineUserName<br /><br /> (entrée)|Indique le compte par lequel la ligne de commande est exécutée. La valeur est une chaîne au format nomutilisateur ou domaine\nomutilisateur.|  
|SMSTSRunCommandLinePassword<br /><br /> (entrée)|Indique le mot de passe pour le compte spécifié par la variable SMSTSRunCommandLineUserName.|  

### <a name="set-dynamic-variables"></a>Définir des variables dynamiques  
 Les variables pour cette action sont définies automatiquement quand vous ajoutez l’étape de séquence de tâches Définir des variables dynamiques. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Définir des variables dynamiques](task-sequence-steps.md#BKMK_SetDynamicVariables).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action<br /><br /> (entrée)|Description|  
|----------------------------------------|-----------------|  
|_SMSTSMake|Spécifie la marque de l’ordinateur.|  
|_SMSTSModel|Spécifie le modèle de l’ordinateur.|  
|_SMSTSMacAddresses|Spécifie les adresses MAC utilisées par l’ordinateur.|  
|_SMSTSIPAddresses|Spécifie les adresses IP utilisées par l’ordinateur.|  
|_SMSTSSerialNumber|Spécifie le numéro de série de l’ordinateur.|  
|_SMSTSAssetTag|Spécifie la balise de ressource de l’ordinateur.|  
|_SMSTSUUID|Spécifie l’UUID de l’ordinateur.|  
|_SMSTSDefaultGateways|Spécifie les passerelles par défaut utilisées par l’ordinateur.|  

###  <a name="BKMK_SetupWindows"></a> Variables d'action de séquence de tâches Configurer Windows et ConfigMgr  
 La variable pour cette action spécifie les propriétés d’installation de client qui sont utilisées pendant l’installation du client Configuration Manager. Pour plus d’informations sur l’étape de séquence de tâches associée à ces variables, consultez [Configurer Windows et ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action<br /><br /> (entrée)|Description|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (entrée)|Spécifie les propriétés d’installation de client qui sont utilisées pendant l’installation du client Configuration Manager.|  

### <a name="upgrade-operating-system"></a>Mettre à niveau le système d’exploitation  
 La variable utilisée pour cette action spécifie des options de ligne de commande supplémentaires qui ne sont pas disponibles dans la console Configuration Manager, mais qui sont ajoutées au programme d’installation pour une mise à niveau Windows 10. Pour plus d’informations sur l’étape de séquence de tâches associée à cette variable, consultez [Mettre à niveau le système d’exploitation](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action<br /><br /> (entrée)|Description|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (entrée)|Spécifie les options de ligne de commande supplémentaires qui sont ajoutées au programme d’installation au cours d’une mise à niveau Windows 10. Ces options de ligne de commande ne sont pas vérifiées. Par conséquent, vérifiez que l’option que vous entrez est exacte.<br /><br /> Pour plus d’informations, consultez [Options de ligne de commande du programme d’installation de Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).|  
