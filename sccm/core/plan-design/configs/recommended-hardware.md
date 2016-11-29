---
title: "Matériel recommandé | System Center Configuration Manager"
description: "Consultez les recommandations de matériel pour mieux assurer la scalabilité de votre environnement System Center Configuration Manager après son déploiement de base."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
caps.latest.revision: 26
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d5aa39a9551cc872631895bb1664de5a35531854


---
# <a name="recommended-hardware-for-system-center-configuration-manager"></a>Matériel recommandé pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les recommandations suivantes sont des indications destinées à vous aider à adapter votre environnement System Center Configuration Manager pour qu’il prenne en charge un déploiement plus complexe de sites, de systèmes de site et de clients. Elles ne sont pas prévues pour couvrir toutes les configurations possibles de site et de hiérarchie.  

 Les informations des sections suivantes sont destinées à vous aider à prévoir le matériel capable de répondre aux charges de traitement des clients et des sites qui utilisent les fonctionnalités de Configuration Manager disponibles avec les configurations par défaut.  


##  <a name="a-namebkmkscalesiesystemsa-site-systems"></a><a name="bkmk_ScaleSieSystems"></a> Systèmes de site  
 Cette section identifie les configurations matérielles recommandées pour les systèmes de site Configuration Manager pour les déploiements prenant en charge le nombre maximal de clients et utilisant toutes ou la plupart des fonctionnalités de Configuration Manager. Les déploiements qui prennent en charge moins que le nombre maximal de clients et n’utilisent pas toutes les fonctionnalités disponibles peuvent nécessiter moins de ressources informatiques. En règle générale, les facteurs clés qui limitent les performances de l'ensemble du système sont les suivants, par ordre d'importance :  

1.  Performances d'E/S du disque  

2.  Mémoire disponible  

3.  Processeur  

Pour des performances optimales, utilisez des configurations RAID 10 pour tous les lecteurs de données et une connectivité réseau Ethernet 1 Gbit/s.  

###  <a name="a-namebkmkscalesiteservera-site-servers"></a><a name="bkmk_ScaleSiteServer"></a> Serveurs de site  

|Site principal autonome|Cœurs de processeurs|Mémoire en Go|% d’allocation de mémoire pour SQL Server|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Serveur de site principal autonome avec rôle de base de données de site sur le même serveur<sup>1</sup>|16|96|80|  
|Serveur de site principal autonome avec une base de données de site distante|8|16|-|  
|Serveur de bases de données distant pour un site principal autonome|16|64|90|  
|Serveur de site d’administration centrale avec rôle de base de données de site sur le même serveur<sup>1</sup>|16|96|80|  
|Serveur de site d’administration centrale avec une base de données de site distante|8|16|-|  
|Serveur de bases de données distant pour un site d’administration centrale|16|96|90|  
|Site principal enfant avec rôle de base de données de site sur le même serveur|16|96|80|  
|Serveur de site principal enfant avec une base de données de site distante|8|16|-|  
|Serveur de bases de données distant pour un site principal enfant|16|64|90|  
|Serveur de site secondaire|8|16|-|  

 <sup>1</sup> Quand le serveur de site et SQL Server sont installés sur le même ordinateur, le déploiement prend en charge les [tailles et échelles](/sccm/core/plan-design/configs/size-and-scale-numbers) maximales pour les sites et les clients. Toutefois, cette configuration peut limiter les [Options de haute disponibilité pour System Center Configuration Manager](/sccm/protect/understand/high-availability-options), comme l’utilisation d’un cluster SQL Server.  De plus, en raison des besoins d’E/S plus élevés pour prendre en charge à la fois SQL Server et le serveur de site Configuration Manager lors de leur exécution sur le même ordinateur, nous recommandons aux clients ayant des déploiements plus importants d’utiliser une configuration avec un ordinateur SQL Server distant.  

###  <a name="a-namebkmkremotesitesystema-remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a> Serveurs de système de site distants  
 Les indications ci-dessous concernent les ordinateurs qui comportent un seul rôle de système de site. Ajustez les valeurs indiquées si vous installez plusieurs rôles de système de site sur le même ordinateur.  

|Rôle de système de site|Cœurs de processeurs|Mémoire en Go|Espace disque : Go|  
|----------------------|---------------|---------------|--------------------|  
|Point de gestion|4|8|50|  
|Point de distribution|2|8|En fonction des besoins du système d’exploitation et pour stocker le contenu que vous déployez|  
|Catalogue d'applications, avec le service Web et le site Web sur l'ordinateur du système de site|4|16|50|  
|Point de mise à jour logicielle<sup>1</sup>|8|16|En fonction des besoins du système d’exploitation et pour stocker les mises à jour que vous déployez|  
|Tous les autres rôles de système de site|4|8|50|  

 <sup>1</sup> L’ordinateur qui héberge un point de mise à jour logicielle nécessite les configurations suivantes pour les pools d’applications IIS :  

-   Augmenter la **longueur de file d’attente WsusPool** à **2000**  

-   Multiplier par quatre la **limite de mémoire privée WsusPool** , ou lui affecter la valeur **0** (illimitée)  

###  <a name="a-namebkmkdiskspacea-disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a> Espace disque pour les systèmes de site  
 L’allocation et la configuration de disque contribuent aux performances de Configuration Manager. Comme chaque environnement Configuration Manager est différent, ajustez les valeurs indiquées ci-dessous en fonction de vos besoins.  

 Pour des performances optimales, placez chaque objet sur un volume RAID séparé et dédié. Pour tous les volumes de données (Configuration Manager et ses fichiers de base de données), utilisez RAID 10 pour des performances optimales.  

|Utilisation des données|Espace disque minimum|25 000 clients|50 000 clients|100 000 clients|150 000 clients|700 000 clients (site d’administration centrale)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Système d'exploitation|Consultez les conseils pour le système d'exploitation.|Consultez les conseils pour le système d'exploitation.|Consultez les conseils pour le système d'exploitation.|Consultez les conseils pour le système d'exploitation.|Consultez les conseils pour le système d'exploitation.|Consultez les conseils pour le système d'exploitation.|  
|Fichiers journaux et d’application de Configuration Manager|25 Go|50 Go|100 Go|200 Go|300 Go|200 Go|  
|Fichier .mdf de base de données du site|75 Go par tranche de 25 000 clients|75 Go|150 Go|300 Go|500 Go|2 To|  
|Fichier .ldf de base de données du site|25 Go par tranche de 25 000 clients|25 Go|50 Go|100 Go|150 Go|100 Go|  
|Fichiers de base de données temporaires (.mdf et .ldf)|En fonction des besoins|En fonction des besoins|En fonction des besoins|En fonction des besoins|En fonction des besoins|En fonction des besoins|  
|Contenu (partages de point de distribution)|En fonction des besoins<sup>1</sup>|En fonction des besoins<sup>1</sup>|En fonction des besoins<sup>1</sup>|En fonction des besoins<sup>1</sup>|En fonction des besoins<sup>1</sup>|En fonction des besoins<sup>1</sup>|  

 <sup>1</sup> Les instructions relatives à l'espace disque n'incluent pas l'espace requis pour le contenu situé dans la bibliothèque de contenu sur le serveur de site ou les points de distribution. Pour plus d’informations sur la planification de la bibliothèque de contenu, consultez [Bibliothèque de contenu](../../../core/plan-design/hierarchy/the-content-library.md).  

 En plus des indications précédentes, prenez en compte les recommandations suivantes pour prévoir l’espace disque nécessaire :  

-   Chaque client nécessite environ 5 Mo d’espace.  

-   Lorsque vous planifiez la taille de la base de données temporaire pour un site principal, prévoyez une taille combinée de 25 à 30 % du fichier .mdf de base de données du site. La taille effective peut être beaucoup plus petite, ou plus grande, et dépend des performances du serveur de site et du volume de données entrantes, sur de courtes et longues périodes.  

    > [!NOTE]  
    >  Lorsque vous avez plus de 50 000 clients sur un site, prévoyez d'utiliser au moins quatre fichiers .mdf de base de données temporaire.  

-   La taille de la base de données temporaire pour un site deadministration centrale est généralement beaucoup plus petite que celle d'un site principal.  

-   La base de données d'un site secondaire est limitée en taille pour les éléments suivants :  

    -   SQL Server 2012 Express : 10 Go  

    -   SQL Server 2014 Express : 10 Go  

##  <a name="a-namebkmkscaleclienta-clients"></a><a name="bkmk_ScaleClient"></a> Clients  
 Cette section identifie les configurations matérielles recommandées pour les ordinateurs gérés en installant le logiciel client Configuration Manager.  

### <a name="client-for-windows-computers"></a>Client pour les ordinateurs Windows  
 Le tableau suivant indique la configuration minimale requise pour les ordinateurs Windows gérés avec Configuration Manager, y compris les systèmes d’exploitation incorporés :  

-   **Processeur et mémoire :** reportez-vous à la configuration de processeur et mémoire RAM requise pour les systèmes d’exploitation des ordinateurs.  

-   **Espace disque :** 500 Mo d’espace disque disponible, avec 5 Go recommandés pour le cache du client Configuration Manager. L’espace disque requis est moindre si vous utilisez des paramètres personnalisés pour installer le client Configuration Manager :  

    -   Utilisez la propriété /skipprereq de la ligne de commande de CCMSetup pour éviter d’installer des fichiers dont le client n’a pas besoin. Par exemple, **CCMSetup.exe /skipprereq:silverlight.exe** si le client ne doit pas utiliser le catalogue d’applications.  

    -   Utilisez la propriété SMSCACHESIZE de Client.msi pour définir un fichier de cache d'une taille inférieure à la taille par défaut de 5 120 Mo. La taille minimale est de 1 Mo. Par exemple, **CCMSetup.exe SMSCachesize=2** crée un cache d’une taille de 2 Mo.  

    Pour plus d’informations sur les paramètres d’installation du client, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    >  L'installation du client avec un minimum d'espace disque est utile pour les appareils Windows Embedded qui ont généralement des tailles de disque plus petites que les ordinateurs Windows standard.  

 Voici des configurations matérielles minimales supplémentaires pour les fonctionnalités facultatives dans Configuration Manager.  

-   **Déploiement de système d’exploitation :** 384 Mo de RAM  

-   **Centre logiciel :** processeur 500 MHz  

-   **Contrôle à distance :** Pentium 4 Hyper-Threaded 3 GHz (simple cœur) ou processeur comparable, avec au moins 1 Go de RAM pour une expérience optimale  

### <a name="client-for-linux-and-unix"></a>Client pour Linux et UNIX  
 Le tableau suivant indique la configuration minimale requise pour les ordinateurs Linux et UNIX que vous gérez avec Configuration Manager.  

|Exigence|Détails|  
|-----------------|-------------|  
|Processeur et mémoire|Reportez-vous à la configuration de processeur et mémoire RAM requise pour le système d'exploitation de l'ordinateur.|  
|Espace disque|500 Mo d’espace disque disponible, avec 5 Go recommandés pour le cache du client Configuration Manager.|  
|Connectivité réseau|Les ordinateurs clients Configuration Manager doivent disposer d’une connexion réseau aux systèmes de site Configuration Manager pour en permettre la gestion.|  

##  <a name="a-namebkmkscaleconsolea-configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a> Console Configuration Manager  
 La configuration requise indiquée dans le tableau ci-dessous s’applique à chaque ordinateur qui exécute la console Configuration Manager.  

 **Configuration matérielle minimale :**  

-   Intel i3 ou processeur comparable  

-   2 Go de RAM  

-   2 Go d'espace disque.  

|Paramètre PPP|Résolution minimale|  
|-----------------|------------------------|  
|96 / 100 %|1024 x 768|  
|120 /125 %|1280 x 960|  
|144 / 150 %|1600 x 1200|  
|196 / 200 %|2500 x 1600|  

 **Prise en charge de PowerShell :**  

 Quand vous installez la prise en charge de PowerShell sur un ordinateur qui exécute la console Configuration Manager, vous pouvez exécuter des applets de commande PowerShell sur cet ordinateur pour gérer Configuration Manager. Les versions minimales suivantes sont prises en charge :  

-   PowerShell 3.0  

-   PowerShell 4.0  

En plus de PowerShell, les versions 3.0 et 4.0 de Windows Management Framework (WMF) sont prises en charge.   
Vous pouvez installer PowerShell avant ou après l’installation de la console Configuration Manager.  

##  <a name="a-namebkmkscalelaba-lab-deployments"></a><a name="bkmk_ScaleLab"></a> Déploiements de laboratoire  
 Utilisez les recommandations de configuration matérielle suivantes pour les déploiements de laboratoire et de test de Configuration Manager. Ces recommandations s’appliquent à tous les types de sites et pour une utilisation avec 100 clients maximum :  

|Rôle|Cœurs de processeurs|Mémoire (Go)|Espace disque (Go)|  
|----------|---------------|-------------------|-----------------------|  
|Serveur de site et de bases de données|2 - 4|7 - 12|100|  
|Serveur de système de site|1 - 4|2 - 4|50|  
|Client|1 - 2|1 - 3|30|  



<!--HONumber=Nov16_HO1-->


