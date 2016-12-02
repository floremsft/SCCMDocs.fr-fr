---
title: Clients et appareils pris en charge | System Center Configuration Manager
description: "Découvrez les systèmes d’exploitation que System Center Configuration Manager prend en charge pour les clients et les appareils."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
caps.latest.revision: 5
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 862291f52d5a1bb34fb5483806972fcf70f158a8

---
# <a name="supported-operating-systems-for-clients-and-devices-for-system-center-configuration-manager"></a>Systèmes d’exploitation pris en charge pour les clients et les appareils pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*




 System Center Configuration Manager prend en charge l’installation de logiciels clients sur différents ordinateurs Windows, Mac, Linux et UNIX.  

 **Conditions requises et limitations pour tous les clients :**  

-   La modification du type de démarrage ou des paramètres d’ouverture de session n’est pas prise en charge, quel que soit le service Configuration Manager. Cela peut empêcher l’exécution correcte de certains services clés.    

-   L’installation ou l’exécution du client Configuration Manager pour Linux ou UNIX ou du client pour Mac sur des ordinateurs sous un compte autre que root n’est pas prise en charge. Cela peut empêcher l’exécution correcte de certains services clés.  

##  <a name="a-namebkmkwinclientosa-windows-computers"></a><a name="bkmk_WinClientos"></a> Ordinateurs Windows  
 Vous pouvez gérer les ordinateurs Windows avec le client Configuration Manager fourni avec Configuration Manager. Pour plus d’informations, consultez [Guide pratique pour déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

**Systèmes d’exploitation pris en charge :**  

-  **Windows Server 2016** : Standard, Datacenter <sup>1</sup>
  - Windows Server 2016 est pris en charge à compter de Configuration Manager version 1606 assortie du correctif cumulatif KB3186654 (ou la version de référence 1606 publiée en octobre 2016).  


-   **Windows Server 2012 R2** (x64) : Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64) : Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 avec SP1** (x64) : Standard, Entreprise, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64) - Workgroup, Standard, Enterprise    

-   **Windows Server 2008 avec SP2** (x86, x64) : Standard, Entreprise, Datacenter <sup>1</sup>    

-   **Windows 10 Entreprise LTSB** (x86, x64) <sup>3</sup>    

-   **Windows 10** (x86, x64) : Professionnel, Entreprise    

-   **Windows 8.1** (x86, x64) : Professionnel, Entreprise    

-   **Windows 8** (x86, x64) : Professionnel, Entreprise    

-   **Windows 7 avec SP1** (x86, x64) - Professionnel, Entreprise, Édition Intégrale    

-   **Installation minimale de Windows Server 2012 R2** (x64) <sup>2</sup>    

-   **Installation minimale de Windows Server 2012** (x64) <sup>2</sup>    

-   **Installation minimale de Windows Server 2008 R2**  
    **(sans Service Pack ou avec SP1)** (x64)    

-   **Installation minimale de Windows Server 2008 SP2** (x86, x64)  

 <sup>1</sup> Les versions Datacenter sont prises en charge, mais ne sont pas certifiées pour Configuration Manager. Les correctifs ne sont pas pris en charge pour résoudre les problèmes spécifiques de l'édition Windows Server Datacenter.  

 <sup>2</sup> Pour prendre en charge l’installation Push du client, l’ordinateur exécutant cette version du système d’exploitation doit exécuter le service de rôle Serveur de fichiers pour le rôle serveur Services de fichiers et de stockage. Pour plus d’informations sur l’installation des fonctionnalités Windows sur un ordinateur Server Core, consultez [Installer des rôles et fonctionnalités de serveur sur un serveur en mode d’installation minimale](http://go.microsoft.com/fwlink/p/?LinkId=299359) dans la bibliothèque TechNet de Windows Server 2012.  

 <sup>3</sup> L’utilisation de ce système d’exploitation nécessite la version 1602 ou ultérieure.  

##  <a name="a-namebkmkembeddedosa-windows-embedded"></a><a name="bkmk_EmbeddedOS"></a> Windows Embedded  
 Vous pouvez gérer les appareils Windows Embedded en installant le logiciel client Configuration Manager sur ceux-ci.  Pour plus d’informations, consultez [Planification du déploiement de clients sur des appareils Windows Embedded dans System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

**Configuration requise et limitations :**  

-   Toutes les fonctionnalités du client sont prises en charges sur les systèmes Windows Embedded pris en charge qui ne disposent pas de filtres d’écriture activés.  

-   Les clients qui utilisent l’un des éléments suivants sont pris en charge pour toutes les fonctionnalités, à l’exception de la gestion de l’alimentation :  

    -   Filtres d’écriture améliorés (EWF)    

    -   Filtres d’écriture basés sur des fichiers (FBWF) RAM    

    -   Filtres d’écriture unifiés (UWF)  

-   Le catalogue des applications n’est pris en charge pour aucun appareil Windows Embedded.  

-   Avant de pouvoir surveiller les programmes malveillants détectés sur les appareils Windows Embedded basés sur Windows XP, vous devez installer le package de script Microsoft Windows WMI sur les appareils intégrés. Utilisez Windows Embedded Target Designer pour installer ce package. Les fichiers **WBEMDISP.DLL** et **WBEMDISP.TLB** doivent exister et être inscrits dans le dossier **%windir%\System32\WBEM** sur l’appareil intégré pour garantir que les programmes malveillants sont signalés.  

**Systèmes d’exploitation pris en charge** :  

-   **Windows 10 Entreprise** (x86, x64)  

-   **Windows 10 IoT Entreprise** (x86, x64)  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

-   **Windows Embedded 8 Industry** (x86, x64)    

-   **Windows Embedded 8 Standard** (x86, x64)    

-   **Windows Embedded 8 Pro** (x86, x64)    

-   **Windows Thin PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 avec SP1** (x86, x64)    

-   **WEPOS 1.1 avec SP3** (x86)    

-   **Windows Embedded POSReady 2009** (x86, x64)    

-   **Windows Fundamentals for Legacy PCs (WinFLP)** (x86)    

-   **Windows XP Embedded SP3** (x86)    

-   **Windows Embedded Standard 2009** (x86)  

## <a name="windows-ce"></a>Windows CE  
 Vous pouvez gérer les appareils Windows CE avec le client hérité d’appareil mobile Configuration Manager inclus dans Configuration Manager.  

**Configuration requise et limitations**  

-   L’installation du client d’appareil mobile nécessite 0,78 Mo d’espace de stockage. La journalisation sur l’appareil mobile peut nécessiter jusqu’à 256 Ko d’espace de stockage supplémentaire.    

-   Les fonctionnalités de ces appareils mobiles varient selon la plateforme et le type de client. Pour plus d’informations sur les fonctions de gestion prises en charge par Configuration Manager pour le client hérité d’appareil mobile, consultez [Choisir une solution de gestion d’appareils pour System Center Configuration Manager](../../../core/plan-design/choose-a-device-management-solution.md).  

**Systèmes d’exploitation pris en charge :**  

-   Windows CE 7.0 (processeurs ARM et x86)  

**Langues prises en charge :**  

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

## <a name="mac-computers"></a>Ordinateurs Mac  
 Vous pouvez gérer les ordinateurs Mac OS X à l’aide du client Configuration Manager pour Mac.  

 Le package d’installation de client Mac n’est pas fourni avec le support d’installation de Configuration Manager. Vous pouvez le télécharger en même temps que les clients pour les autres systèmes d’exploitation à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

**Configuration requise et limitations :**  

 Vous devez utiliser le client Configuration Manager pour Mac (version 5.0.8333.1 ou ultérieure), qui doit être téléchargé séparément. Contrairement au client Windows, le client Mac n’est pas inclus dans le logiciel Configuration Manager au moment où vous l’installez. Pour télécharger le client Mac, accédez à [Microsoft System Center Configuration Manager - Clients pour d’autres systèmes d’exploitation](http://go.microsoft.com/fwlink/?LinkID=525184).  

 Pour plus d’informations, consultez [Guide pratique pour déployer des clients sur des ordinateurs Mac dans System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-macs.md).  

**Versions prises en charge :**  

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

##  <a name="a-namebkmklinuxosa-linux-and-unix-servers"></a><a name="bkmk_LinuxOS"></a> Serveurs Linux et UNIX  
 Vous pouvez gérer les serveurs Linux et UNIX avec le client Configuration Manager pour Linux et UNIX.  

 Les packages d’installation du client Linux et UNIX ne sont pas fournis avec le support d’installation de Configuration Manager. Vous pouvez les télécharger en même temps que les clients pour les autres systèmes d’exploitation à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). En plus des packages d’installation du client, le client inclut le script d’installation qui gère l’installation du client sur chaque ordinateur.  

**Configuration requise et limitations :**  

-   Pour vérifier les dépendances des fichiers du système d’exploitation pour le client pour Linux et UNIX, consultez [Conditions préalables pour le déploiement du client pour les serveurs Linux et UNIX](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

-   Pour une vue d’ensemble des fonctionnalités de gestion prises en charge pour les ordinateurs exécutant Linux ou UNIX, consultez [Guide pratique pour déployer des clients sur des serveurs UNIX et Linux dans System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

-   Pour versions prises en charge de Linux et UNIX, la version répertoriée inclut toutes les versions mineures suivantes. Par exemple, quand la prise en charge est indiquée pour CentOS version 6, elle inclut également toute version mineure suivante de CentOS 6, telle CentOS 6.3. De même, quand la prise en charge est indiquée pour un système d’exploitation utilisant des Service Packs, comme SUSE Linux Enterprise Server 11 SP1, elle inclut les Service Packs suivants pour cette version du système d’exploitation.  

-   Pour plus d’informations sur les packages d’installation du client et sur l’Agent universel, consultez [Guide pratique pour déployer des clients sur des serveurs UNIX et Linux dans System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

**Versions prises en charge** : les versions suivantes sont prises en charge en utilisant le fichier .tar indiqué.  

### <a name="aix"></a>AIX  

|||  
|-|-|  
|Version 5.3 (Power)|ccm-Aix53ppc.&lt;version\>.tar|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;version\>.tar|  
|Version 7.1 (Power)|ccm-Aix71ppc.&lt;version\>.tar|  

### <a name="centos"></a>CentOS  

|||  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;version\>.tar|  

### <a name="debian"></a>Debian  

|||  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 7 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 8 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 8 x64|ccm-Universalx64.&lt;version\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|||  
|-|-|  
|Version 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;version\>.tar|  
|Version 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;version\>.tar|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;version\>.tar|  
|Version 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;version\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|||  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;version\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|||  
|-|-|  
|Version 4 x86|ccm-RHEL4x86.&lt;version\>.tar|  
|Version 4 x64|ccm-RHEL4x64.&lt;version\>.tar|  
|Version 5 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;version\>.tar|  

### <a name="solaris"></a>Solaris  

|||  
|-|-|  
|SPARC version 9|ccm-Sol9sparc.&lt;version\>.tar|  
|Version 10 x86|ccm-Sol10x86.&lt;version\>.tar|  
|SPARC version 10|ccm-Sol10sparc.&lt;version\>.tar|  
|Version 11 x86|ccm-Sol11x86.&lt;version\>.tar|  
|SPARC version 11|ccm-Sol11sparc.&lt;version\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|||  
|-|-|  
|Version 9 x86|ccm-SLES9x86.&lt;version\>.tar|  
|Version 10 SP1 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 10 SP1 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 11 SP1 x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 11 SP1 x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 12 x64|ccm-Universalx64.&lt;version\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|||  
|-|-|  
|Version 10.04 LTS x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 10.04 LTS x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 12.04 LTS x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 12.04 LTS x64|ccm-Universalx64.&lt;version\>.tar|  
|Version 14.04 LTS x86|ccm-Universalx86.&lt;version\>.tar|  
|Version 14.04 LTS x64|ccm-Universalx64.&lt;version\>.tar|  

##  <a name="a-namebkmkintuneosa-mobile-devices-enrolled-by-microsoft-intune"></a><a name="bkmk_IntuneOS"></a> Appareils mobiles inscrits par Microsoft Intune  
 Pour plus d’informations sur les ordinateurs et les appareils que vous pouvez gérer quand vous intégrez Microsoft Intune à Configuration Manager, consultez les deux rubriques ci-dessous dans la bibliothèque de la documentation Microsoft Intune :  

-   [Fonctionnalités de gestion des appareils mobiles dans Microsoft Intune](https://docs.microsoft.com/intune/get-started/choose-how-to-manage-devices)  
-   [Fonctionnalités de gestion des PC Windows dans Microsoft Intune](https://docs.microsoft.com/intune/get-started/windows-pc-management-capabilities-in-microsoft-intune)  

##  <a name="a-namebkmkonpremosa-on-premises-mobile-device-management"></a><a name="bkmk_OnpremOS"></a> Gestion des appareils mobiles locale  
 Configuration Manager offre des fonctionnalités intégrées permettant de gérer des appareils locaux sans devoir installer de logiciel client.  Pour plus d’informations, consultez [Gérer des appareils mobiles avec une infrastructure locale dans System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Configuration requise et limitations :**  

-   Vous devez configurer le **point de connexion de service** sur le site de niveau supérieur de votre hiérarchie.  

 **Systèmes d’exploitation pris en charge** :  

-   **Windows 10 Professionnel** (x86, x64)  

-   **Windows 10 Entreprise** (x86, x64)  

-   **Windows 10 IoT Entreprise** (x86, x64)

-   **Windows 10 Mobile**  

-   **Windows 10 Mobile Entreprise**  

-  **Windows 10 IoT Mobile Entreprise**

##  <a name="a-namebkmkexsrvconosa-exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Connecteur Exchange Server  
 Configuration Manager prend en charge une gestion limitée des appareils qui se connectent à Exchange Server, sans installation de logiciel client.  Pour plus d’informations, consultez [Gérer les appareils mobiles avec System Center Configuration Manager et Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

 **Configuration requise et limitations :**  

-   Configuration Manager assure une gestion limitée des appareils mobiles quand vous utilisez le connecteur Exchange Server pour les appareils compatibles Exchange Active Sync (EAS) qui se connectent à un serveur exécutant Exchange Server ou Exchange Online.  

-   Pour plus d’informations sur les fonctions de gestion prises en charge par Configuration Manager pour les appareils mobiles gérés par le connecteur Exchange Server, consultez Déterminer comment gérer des appareils mobiles dans Configuration Manager.  

**Versions d’Exchange Server prises en charge** :  

-   **Exchange Server 2010 SP1**  

-   **Exchange Server 2010 SP2**  

-   **Exchange Server 2013**  

-   **Exchange Online (Office 365)** : inclut Business Productivity Online Standard Suite  



<!--HONumber=Nov16_HO1-->


