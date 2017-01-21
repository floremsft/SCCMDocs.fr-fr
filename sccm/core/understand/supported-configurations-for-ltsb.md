---
title: Configurations prises en charge pour LTSB | Microsoft Docs
description: "Découvrez les systèmes d’exploitation et produits dépendants qui fonctionnent avec la branche de maintenance Long-Term Servicing Branch de System Center Configuration Manager."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 573115e54d734d492ca776a040bad804a792ada6


---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Configurations prises en charge pour la branche de maintenance Long-Term Servicing Branch de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Long-Term Servicing Branch)*

Utilisez les informations de cette rubrique pour découvrir les systèmes d’exploitation et dépendances de produits pris en charge par la branche de maintenance Long-Term Servicing Branch (LTSB) de Configuration Manager.
Sauf indication contraire dans cette rubrique (ou les rubriques spécifiques à LTSB), les configurations et limitations qui s’appliquent à la branche de maintenance Current Branch version 1606 s’appliquent également à la branche de maintenance LTSB.  En cas de conflits, utilisez les informations qui s’appliquent à l’édition dont vous vous servez. En règle générale, LTSB est plus limité que Current Branch.

## <a name="general-statement-of-support"></a>Déclaration générale sur la prise en charge
Les produits et technologies détaillés dans les sections suivantes sont pris en charge par Configuration Manager. Cependant, leur inclusion dans ce contenu ne signifie pas une extension de prise en charge des produits au-delà de leur cycle de vie individuel. L’utilisation de produits qui ont dépassé leur cycle de vie n’est pas prise en charge avec Configuration Manager. Pour plus d’informations, visitez le site web [Politique de support Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) et lisez la page [Politique de support Microsoft - FAQ](http://go.microsoft.com/fwlink/p/?LinkId=31976).

En outre, les produits et versions de produits non répertoriés dans les rubriques suivantes ne sont pas pris en charge, sauf s’ils ont été annoncés dans le [Blog Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/).

**Limitations de la prise en charge future :** LTSB offre une prise en charge limitée pour les futures versions des systèmes d’exploitation client/serveur et dépendances de produits. La liste des plateformes pour LTSB est fixée pour la durée de vie de la version :

**Windows :**
- Seules les mises à jour de qualité et de sécurité pour Windows sont prises en charge
- Aucune prise en charge ne sera ajoutée pour les branches CB (Current Branch), CBB (Current Branch For Business) ou LTSB de Windows 10
-   Aucune prise en charge pour les nouvelles versions majeures de Windows Server

**SQL Server :**
- Seules les mises à jour de qualité et de sécurité, ou les mises à niveau mineures comme les Service Packs, sont prises en charge pour SQL Server
- Aucune prise en charge pour les nouvelles versions majeures de SQL Server  

## <a name="site-systems-and-servers"></a>Systèmes et serveurs de site
LTSB prend en charge les systèmes d’exploitation Windows suivants comme systèmes de site.  Chaque système d’exploitation a les mêmes exigences et limitations que l’entrée correspondante dans [Systèmes d’exploitation pris en charge pour les serveurs de système de site](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  Par exemple, l’installation minimale de Windows 2012 R2 doit être une version x64, elle n’est prise en charge que pour l’hébergement d’un point de distribution et ne prend pas en charge PXE ou la multidiffusion.

**Systèmes d’exploitation pris en charge :**
- **Windows Server 2016**
- **Windows Server 2012** (x64) - Standard, Datacenter
- **Windows Server 2008 R2 avec SP1** (x64) - Standard, Enterprise, Datacenter
- **Windows Server 2008 avec SP2** (x86, x64) - Standard, Enterprise, Datacenter
- **Windows 10 Entreprise 2015 LTSB** (x86, x64)
- **Windows 10 Entreprise 2016 LTSB** (x86, x64)
- **Windows 8.1** (x86, x64) - Professionnel, Entreprise
- **Windows 7 avec SP1** (x86, x64) - Professionnel, Entreprise, Édition Intégrale
- **Installation minimale de Windows Server 2012**
- **Installation minimale de Windows Server 2012 R2**  

## <a name="client-management"></a>Gestion des clients
Les sections suivantes identifient les systèmes d’exploitation clients que vous pouvez gérer via LTSB. LTSB ne prend pas en charge l’ajout de nouveaux systèmes d’exploitation comme clients pris en charge.

### <a name="windows-computers"></a>Ordinateurs Windows
Vous pouvez utiliser LTSB pour gérer les systèmes d’exploitation Windows suivants avec le logiciel client Configuration Manager inclus dans Configuration Manager. Pour plus d’informations, consultez [Guide pratique pour déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

**Systèmes d’exploitation pris en charge :**
- **Windows Server 2016**
- **Windows Server 2012 R2** (x64) - Standard, Datacenter (Remarque 1)
- **Windows Server 2012** (x64) - Standard, Datacenter (Remarque 1)
- **Windows Storage Server 2012 R2** (x64)
- **Windows Storage Server 2012** (x64)
- **Windows Server 2008 R2 avec SP1** (x64) - Standard, Enterprise, Datacenter (Remarque 1)
- **Windows Storage Server 2008 R2** (x86, x64) - Workgroup, Standard, Enterprise
- **Windows Server 2008 avec SP2** (x86, x64) - Standard, Enterprise, Datacenter (Remarque 1)
- **Windows 10 Entreprise 2015 LTSB** (x86, x64)
- **Windows 10 Entreprise 2016 LTSB** (x86, x64)
- **Windows 8.1** (x86, x64) - Professionnel, Entreprise
- **Windows 7 avec SP1** (x86, x64) - Professionnel, Entreprise, Édition Intégrale
- **Installation minimale de Windows Server 2012 R2** (x64) (Remarque 2)
- **Installation minimale de Windows Server 2012** (x64) (Remarque 2)
- **Installation minimale de Windows Server 2008 R2 SP1** (x64)
- **Installation minimale de Windows Server 2008 SP2** (x86, x64)

**(Remarque 1)** Les versions de Datacenter sont prises en charge mais ne sont pas certifiées pour Configuration Manager.  
**(Remarque 2)** Pour prendre en charge l’installation Push du client, l’ordinateur exécutant cette version du système d’exploitation doit exécuter le service de rôle Serveur de fichiers pour le rôle serveur Services de fichiers et de stockage. Pour plus d’informations sur l’installation des fonctionnalités Windows sur un ordinateur Server Core, consultez Installer des rôles et fonctionnalités de serveur sur un serveur en mode d’installation minimale dans la bibliothèque TechNet de Windows Server 2012.

### <a name="windows-embedded"></a>Windows Embedded :
Vous pouvez utiliser LTSB pour gérer les appareils Windows Embedded suivants en installant le logiciel client sur l’appareil.  Pour plus d’informations, consultez [Planification du déploiement de clients sur des appareils Windows Embedded dans System Center Configuration Manager](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).

**Configuration requise et limitations :**  

-   Toutes les fonctionnalités du client sont prises en charges sur les systèmes Windows Embedded pris en charge qui ne disposent pas de filtres d’écriture activés.  

-   Les clients qui utilisent l’un des éléments suivants sont pris en charge pour toutes les fonctionnalités, à l’exception de la gestion de l’alimentation :  

    -   Filtres d’écriture améliorés (EWF)    

    -   Filtres d’écriture basés sur des fichiers (FBWF) RAM    

    -   Filtres d’écriture unifiés (UWF)  

-   Le catalogue des applications n’est pris en charge pour aucun appareil Windows Embedded.  

-   Avant de pouvoir surveiller les programmes malveillants détectés sur les appareils Windows Embedded basés sur Windows XP, vous devez installer le package de script Microsoft Windows WMI sur les appareils intégrés. Utilisez Windows Embedded Target Designer pour installer ce package. Les fichiers **WBEMDISP.DLL** et **WBEMDISP.TLB** doivent exister et être inscrits dans le dossier **%windir%\System32\WBEM** sur l’appareil intégré pour garantir que les programmes malveillants sont signalés.  

**Systèmes d’exploitation pris en charge :**  
-   **Windows 10 Entreprise 2016 LTSB** (x86, x64)  
-   **Windows 10 Entreprise 2015 LTSB** (x86, x64)  
-   **Windows Embedded 8.1 Industry** (x86, x64)    
-   **Windows Thin PC** (x86, x64)    
-   **Windows Embedded POSReady 7** (x86, x64)    
-   **Windows Embedded Standard 7 avec SP1** (x86, x64)    
-   **Windows Embedded POSReady 2009** (x86)   
-   **Windows Embedded Standard 2009** (x86)  

### <a name="windows-ce"></a>Windows CE  
 Vous pouvez gérer les appareils Windows CE avec le client hérité d’appareil mobile Configuration Manager inclus dans Configuration Manager.  

**Configuration requise et limitations**  

-   L’installation du client d’appareil mobile nécessite 0,78 Mo d’espace de stockage. La journalisation sur l’appareil mobile peut nécessiter jusqu’à 256 Ko d’espace de stockage supplémentaire.    

-   Les fonctionnalités de ces appareils mobiles varient selon la plateforme et le type de client. Pour plus d’informations sur les fonctions de gestion prises en charge par Configuration Manager pour le client hérité d’appareil mobile, consultez [Choisir une solution de gestion d’appareils pour System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Systèmes d’exploitation pris en charge :**  

-   Windows CE 7.0 (processeurs ARM et x86)  

**Langues prises en charge :**  
-   Chinois (simplifié et traditionnel)    
-   Anglais (États-Unis)    
-   Français (France)    
-   Allemand    
-   Italien    
-   Japonais  
-   Coréen  
-   Portugais (Brésil)  
-   Russe  
-   Espagnol (Espagne)  

### <a name="mac-computers"></a>Ordinateurs Mac  
 Vous pouvez utiliser LTSB pour gérer les ordinateurs Mac OS X avec le client Configuration Manager pour Mac.

Le package d’installation de client Mac n’est pas fourni avec le support d’installation de Configuration Manager. Vous pouvez le télécharger en même temps que les clients d’autres systèmes d’exploitation à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

La prise en charge des systèmes d’exploitation Mac se limite à ceux qui sont listés dans cette section. Elle n’inclut pas les systèmes d’exploitation supplémentaires pouvant être pris en charge par une mise à jour future des packages d’installation de client Mac pour Current Branch.

Pour plus d’informations, consultez [Guide pratique pour déployer des clients sur des ordinateurs Mac dans System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs).

**Versions prises en charge :**  
-   **Mac OS X 10.9** (Mavericks)  
-   **Mac OS X 10.10** (Yosemite)  
-   **Mac OS X 10.11** (El Capitan)  

## <a name="linux-and-unix-servers"></a>Serveurs Linux et UNIX
Vous pouvez utiliser LTSB pour gérer les serveurs Linux et UNIX avec le client Configuration Manager pour Linux et UNIX.

Les packages d’installation du client Linux et UNIX ne sont pas fournis avec le média Configuration Manager. Vous pouvez les télécharger en même temps que les clients d’autres systèmes d’exploitation à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). En plus des packages d’installation du client, le client inclut le script d’installation qui gère l’installation du client sur chaque ordinateur.

La prise en charge des systèmes d’exploitation Linux et UNIX se limite à ceux qui sont listés dans cette section. Elle n’inclut pas les systèmes d’exploitation supplémentaires pouvant être pris en charge par une mise à jour future des packages d’installation de clients Linux et UNIX pour Current Branch.

**Configuration requise et limitations :**  

-   Pour vérifier les dépendances des fichiers du système d’exploitation pour le client pour Linux et UNIX, consultez [Conditions préalables pour le déploiement du client pour les serveurs Linux et UNIX](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#bkmk_clientdeployprereqforlnu).  
-   Pour une vue d’ensemble des fonctionnalités de gestion prises en charge pour les ordinateurs exécutant Linux ou UNIX, consultez [Guide pratique pour déployer des clients sur des serveurs UNIX et Linux dans System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  
-   Pour versions prises en charge de Linux et UNIX, la version répertoriée inclut toutes les versions mineures suivantes. Par exemple, quand la prise en charge est indiquée pour CentOS version 6, elle inclut également toute version mineure suivante de CentOS 6, telle CentOS 6.3. De même, quand la prise en charge est indiquée pour un système d’exploitation utilisant des Service Packs, comme SUSE Linux Enterprise Server 11 SP1, elle inclut les Service Packs suivants pour cette version du système d’exploitation.
-   Pour plus d’informations sur les packages d’installation client et l’agent universel, consultez [Guide pratique pour déployer des clients sur des serveurs UNIX et Linux dans System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).


**Versions prises en charge :**   
Les versions suivantes sont prises en charge à l’aide du fichier .tar indiqué.  
### <a name="aix"></a>AIX  

|Version|Fichier|  
|-|-|  
|Version 5.3 (Power)|ccm-Aix53ppc.&lt;version\>.tar|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;version\>.tar|  
|Version 7.1 (Power)|ccm-Aix71ppc.&lt;version\>.tar|  

### <a name="centos"></a>CentOS  

|Version|Fichier|  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;version\>.tar|  

### <a name="debian"></a>Debian  

|Version|Fichier|    
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 7 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 8 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 8 x64|ccm-Universalx64.&lt;version\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|Version|Fichier|  
|-|-|  
|Version 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;version\>.tar|  
|Version 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;version\>.tar|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;version\>.tar|  
|Version 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;version\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Version|Fichier|    
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;version\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Version|Fichier|  
|-|-|  
|Version 4 x86|ccm-RHEL4x86.&lt;version\>.tar|  
|Version 4 x64|ccm-RHEL4x64.&lt;version\>.tar|  
|Version 5 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;version\>.tar|  

### <a name="solaris"></a>Solaris  

|Version|Fichier|   
|-|-|  
|SPARC version 9|ccm-Sol9sparc.&lt;version\>.tar|  
|Version 10 x86|ccm-Sol10x86.&lt;version\>.tar|  
|SPARC version 10|ccm-Sol10sparc.&lt;version\>.tar|  
|Version 11 x86|ccm-Sol11x86.&lt;version\>.tar|  
|SPARC version 11|ccm-Sol11sparc.&lt;version\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Version|Fichier|  
|-|-|  
|Version 9 x86|ccm-SLES9x86.&lt;version\>.tar|  
|Version 10 SP1 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 10 SP1 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 11 SP1 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 11 SP1 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 12 x64|ccm-Universalx64.&lt;version\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|Version|Fichier|    
|-|-|  
|Version 10.04 LTS x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 10.04 LTS x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 12.04 LTS x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 12.04 LTS x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 14.04 LTS x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 14.04 LTS x64|ccm-Universalx64.&lt;version\>.tar|  

### <a name="exchange-server-connector"></a>Connecteur Exchange Server
 LTSB prend en charge une gestion limitée des appareils qui se connectent à votre serveur Exchange Server, sans installation d’un logiciel client. Pour plus d’informations, consultez [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).

 **Configuration requise et limitations :**  

-   Configuration Manager offre une gestion limitée des appareils mobiles durant l’utilisation du connecteur du serveur Exchange Server pour les appareils compatibles Exchange Active Sync (EAS) qui se connectent à un serveur exécutant Exchange Server ou Exchange Online.  

-   Pour plus d’informations sur les fonctions de gestion prises en charge par Configuration Manager pour les appareils mobiles gérés par le connecteur Exchange Server, consultez [Choisir une solution de gestion d’appareils pour System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Versions d’Exchange Server prises en charge :**  
-   **Exchange Server 2010 SP1**  
-   **Exchange Server 2010 SP2**  
-   **Exchange Server 2013**  

> [!NOTE]
> LTSB ne prend pas en charge la gestion des appareils qui se connectent via un service en ligne, par exemple Exchange Online (Office 365).


## <a name="configuration-manager-console"></a>Console Configuration Manager
LTSB prend en charge les systèmes d’exploitation suivants pour l’exécution de la console Configuration Manager. Chaque ordinateur qui héberge la console doit avoir au minimum .NET Framework version 4.5.2, sauf pour Windows 10, qui nécessite au minimum .NET Framework 4.6.

**Systèmes d’exploitation pris en charge :**
- **Windows Server 2016**
- **Windows Server 2012 R2** (x64) - Standard, Datacenter
- **Windows Server 2012** (x64) - Standard, Datacenter
- **Windows Server 2008 R2 avec SP1** (x64) - Standard, Enterprise, Datacenter
- **Windows Server 2008 avec SP2** (x86, x64) - Standard, Enterprise, Datacenter
- **Windows 10 Entreprise 2016 LTSB** (x86, x64)
- **Windows 10 Entreprise 2015 LTSB** (x86, x64)
- **Windows 8.1** (x86, x64) - Professionnel, Entreprise. Windows 7 avec SP1** (x86, x64) - Professionnel, Entreprise, Édition Intégrale

## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Versions de SQL Server prises en charge pour la base de données du site et le point de rapport
LTSB prend en charge les versions suivantes de SQL Server pour héberger la base de données du site et le point de rapport. Pour chaque version prise en charge, les mêmes exigences et limitations de configuration apparaissant dans [Prise en charge des versions de SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions) pour Current Branch s’appliquent à LTSB.  Cela inclut l’utilisation d’un cluster SQL Server ou d’un groupe de disponibilité AlwaysOn SQL Server.  

**Versions prises en charge :**

- **SQL Server 2016** - Standard, Enterprise
- **SQL Server 2014 SP2** - Standard, Enterprise
- **SQL Server 2014 SP1** - Standard, Enterprise
- **SQL Server 2012 SP3** - Standard, Enterprise
- **SQL Server 2012 SP2** - Standard, Enterprise
- **SQL Server 2008 R2 SP3** - Standard, Enterprise, Datacenter
- **SQL Server 2016 Express**
- **SQL Server 2014 Express SP2**
- **SQL Server 2014 Express SP1**
- **SQL Server 2012 Express SP3**
- **SQL Server 2012 Express SP2**

## <a name="support-for-active-directory-domains"></a>Prise en charge des domaines Active Directory
Tous les systèmes de site LTSB doivent être membres d’un domaine Windows Active Directory pris en charge. La prise en charge des domaines Active Directory présente les mêmes exigences et limitations que celles décrites dans [Prise en charge des domaines Active Directory](/sccm/core/plan-design/configs/support-for-active-directory-domains). Toutefois, elle se limite aux niveaux fonctionnels de domaine suivants :

**Niveaux pris en charge :**
- **Windows Server 2008**
- **Windows Server 2008 R2**
- **Windows Server 2012**
- **Windows Server 2012 R2**

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Rubriques de prise en charge supplémentaires qui s’appliquent à Long-Term Servicing Branch
Les informations contenues dans les rubriques Current Branch suivantes s’appliquent à LTSB :
- [Taille et échelle en chiffres](/sccm/core/plan-design/configs/size-and-scale-numbers)
- [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [Options de haute disponibilité](/sccm/protect/understand/high-availability-options)
- [Matériel recommandé](/sccm/core/plan-design/configs/recommended-hardware)
- [Prise en charge des fonctionnalités Windows et des réseaux](/sccm/core/plan-design/configs/support-for-windows-features-and-networks)
- [Prise en charge des environnements de virtualisation](/sccm/core/plan-design/configs/support-for-virtualization-environments)



<!--HONumber=Dec16_HO3-->


