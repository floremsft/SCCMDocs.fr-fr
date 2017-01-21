---
title: "Gérer les clients Linux et UNIX | Microsoft Docs"
description: "Découvrez comment gérer les clients sur des serveurs Linux et UNIX dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: d3a44d516bb1e2766a7a10b62d52405eecef31fc


---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Guide pratique pour gérer les clients pour des serveurs Linux et UNIX dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous gérez des serveurs Linux et UNIX avec System Center Configuration Manager, vous pouvez configurer des regroupements, des fenêtres de maintenance et des paramètres client pour mieux gérer les serveurs. En outre, bien que le client Configuration Manager pour Linux et UNIX n’a pas d’interface utilisateur, vous pouvez forcer le client à interroger manuellement la stratégie du client.

##  <a name="a-namebkmkcollectionsforlnua-collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 Les regroupements vous permettent de gérer des groupes de serveurs Linux et UNIX de la même façon que d’autres types de clients. Les regroupements peuvent être des regroupements avec adhésion directe ou des regroupements basés sur une requête qui identifient les systèmes d’exploitation clients, les configurations matérielles ou d’autres détails sur le client, qui sont stockés dans la base de données du site. Par exemple, vous pouvez utiliser des regroupements qui incluent des serveurs Linux et UNIX pour gérer les éléments suivants :  

-   Paramètres du client  

-   Déploiements de logiciels  

-   Fenêtres de maintenance appliquées  

 Avant de pouvoir identifier un client Linux ou UNIX par son système d’exploitation ou sa distribution, vous devez collecter l’inventaire matériel du client. Pour plus d’informations sur la collecte de l’inventaire matériel, consultez [Inventaire matériel pour Linux et UNIX dans System Center Configuration Manager](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

 Les paramètres client par défaut pour l’inventaire matériel incluent des informations sur le système d’exploitation de l’ordinateur client. Vous pouvez utiliser la propriété **Légende** de la classe **Système d’exploitation** pour identifier le système d’exploitation d’un serveur Linux ou UNIX.  

 Vous pouvez afficher des informations détaillées sur les ordinateurs qui exécutent le client Configuration Manager pour Linux et UNIX dans le nœud Appareils de l’espace de travail Ressources et Conformité, dans la console Configuration Manager. Dans l’espace de travail Ressources et Conformité de la console Configuration Manager, la colonne **Système d’exploitation** affiche le nom du système d’exploitation de chaque ordinateur.  

 Par défaut, les serveurs Linux et UNIX sont membres du regroupement **Tous les systèmes** . Il est recommandé de créer des regroupements personnalisés qui incluent uniquement les serveurs Linux et UNIX, ou un sous-ensemble de ces serveurs. Cela vous permet de gérer des opérations telles que le déploiement de logiciels ou l’attribution de paramètres client à des groupes d’ordinateurs appropriés. Par exemple, si vous déployez un logiciel pour des ordinateurs x64 RHEL6 vers un regroupement qui contient des ordinateurs Windows et Linux, l’état du déploiement affiche un succès partiel. Au lieu de cela, quand vous déployez le logiciel vers un regroupement qui contient uniquement des ordinateurs x64 RHEL6, vous pouvez utiliser des messages d’état et des rapports pour identifier précisément la réussite du déploiement.  

 Quand vous créez un regroupement personnalisé pour des serveurs Linux et UNIX, insérez des requêtes de règle d’appartenance qui incluent l’attribut Légende pour l’attribut Système d’exploitation. Pour plus d’informations sur la création de regroupements, consultez [Guide pratique pour créer des regroupements dans System Center Configuration Manage](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="a-namebkmkmaintenancewindowsforlnua-maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 Le client Configuration Manager pour les serveurs Linux et UNIX prend en charge l’utilisation des fenêtres de maintenance. Cette prise en charge est inchangée par rapport à celle des clients basés sur Windows.  

 Pour plus d’informations sur l’utilisation des fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance dans System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="a-namebkmkclientsettingsforlnua-client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 Vous pouvez configurer les paramètres client qui s’appliquent à des serveurs Linux et UNIX de la même façon que vous configurez des paramètres pour d’autres clients.  

 Par défaut, les **paramètres d’agent client par défaut** s’appliquent aux serveurs Linux et UNIX. Vous pouvez également créer des paramètres client personnalisés et les déployer sur des regroupements qui contiennent des systèmes d’exploitation clients spécifiques ou différents systèmes d’exploitation clients.  

 Il n’existe pas d’autres paramètres client qui s’appliquent uniquement aux clients Linux et UNIX. Toutefois, il existe des paramètres client par défaut qui ne s’appliquent pas aux clients Linux et UNIX. Le client pour Linux et UNIX applique uniquement les paramètres relatifs aux fonctionnalités qu’il prend en charge, et toutes les configurations pour les fonctionnalités non prises en charge sont ignorées.  

 Par exemple, vous créez un paramètre de périphérique client personnalisé qui spécifie un calendrier d’inventaire matériel, puis vous l’affectez à un regroupement qui inclut des ordinateurs Linux. Par conséquent, le calendrier de l’inventaire matériel est appliqué aux serveurs Linux et UNIX. Ensuite, vous créez un paramètre de périphérique client personnalisé qui active et configure les paramètres de contrôle à distance et vous l’affectez au même regroupement. Il en résulte que les paramètres de contrôle à distance sont ignorés par les serveurs Linux et UNIX. Cela tient au fait que le client pour Linux et UNIX ne prend pas en charge le contrôle à distance dans Configuration Manager.  

 Pour obtenir des informations sur la configuration des paramètres client, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

##  <a name="a-namebkmkpolicyforlnua-computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a> Computer policy for Linux and UNIX servers  
 Le client Configuration Manager des serveurs Linux et UNIX interroge régulièrement son site au sujet de la stratégie d’ordinateur pour en savoir plus sur les configurations demandées et pour rechercher les déploiements.  

 Vous pouvez également forcer le client sur un serveur Linux ou UNIX à interroger immédiatement la stratégie d’ordinateur. Pour interroger immédiatement, utilisez les informations d’identification **racine** sur le serveur pour exécuter la commande suivante : **/opt/microsoft/configmgr/bin/ccmexec -rs policy**  

 Des détails sur l’interrogation de la stratégie d’ordinateur sont entrés dans le fichier journal du client partagé **scxcm.log**.  

> [!NOTE]  
>  Le client Configuration Manager pour Linux et UNIX ne demande et ne traite jamais de stratégie utilisateur.  

##  <a name="a-namebkmkmanagelinuxcertsa-how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a> How to manage certificates on the client for Linux and UNIX  
 Après avoir installé le client pour Linux et UNIX, vous pouvez utiliser l’outil **certutil** pour mettre à jour le client avec un nouveau certificat PKI et importer une nouvelle liste de révocation de certificats (CRL). Quand vous installez le client pour Linux et UNIX, cet outil est placé dans l’emplacement suivant : **/opt/microsoft/configmgr/bin/certutil**  

 Pour gérer les certificats, sur chaque client, exécutez certutil avec l’une des options suivantes :  

|Option|Plus d'informations|  
|------------|----------------------|  
|importPFX|Utilisez cette option pour spécifier un certificat pour remplacer le certificat actuellement utilisé par un client.<br /><br /> Quand vous utilisez **-importPFX**, vous devez également utiliser le paramètre de ligne de commande **-password** pour fournir le mot de passe associé au fichier PKCS#12.<br /><br /> Utilisez **-rootcerts** pour spécifier des exigences de certificat racine supplémentaires.<br /><br /> Exemple : **certutil -importPFX &lt;chemin du certificat PKCS#12> -mot de passe &lt;mot de passe de certificat\> [-rootcerts &lt;liste de certificats séparés par des virgules>]**|  
|-importsitecert|Utilisez cette option pour mettre à jour le certificat de signature du serveur de site qui se trouve sur le serveur d’administration.<br /><br /> Exemple : **certutil -importsitecert &lt;chemin du certificat DER\>**|  
|-importcrl|Utilisez cette option pour mettre à jour la liste de révocation de certificats sur le client avec un ou plusieurs chemins d’accès de fichiers CRL.<br /><br /> Exemple : **certutil -importcrl &lt;liste de chemins de fichier CRL séparés par des virgules\>**|  



<!--HONumber=Dec16_HO3-->


