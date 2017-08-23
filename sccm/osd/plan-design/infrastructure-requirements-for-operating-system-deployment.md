---
title: "Anforderungen an die Infrastruktur für die Betriebssystembereitstellung| Microsoft-Dokumentation"
description: "Stellen Sie sicher, dass Sie externe Abhängigkeiten und Produktabhängigkeiten kennen, bevor Sie System Center 2012 Configuration Manager für die Betriebssystembereitstellung verwenden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
caps.latest.revision: "24"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 167e639cdb9995fd743787cc9fbf364ec70f6ed9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="infrastructure-requirements-for-operating-system-deployment-in-system-center-configuration-manager"></a>Anforderungen an die Infrastruktur für die Betriebssystembereitstellung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Betriebssystembereitstellung in System Center 2012 Configuration Manager weist externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts auf. In den folgenden Themen finden Sie hilfreiche Informationen zur Vorbereitung der Betriebssystembereitstellung.  

##  <a name="BKMK_ExternalDependencies"></a> Externe Abhängigkeiten von Configuration Manager  
 Nachstehend finden Sie Informationen zu externen Tools, Installationskits und Betriebssystemen, die für die Bereitstellung von Betriebssystemen in Configuration Manager erforderlich sind.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK für Windows 10  
 Windows ADK umfasst Tools und Dokumentation zur Unterstützung der Konfiguration und Bereitstellung von Windows-Betriebssystemen. Configuration Manager verwendet Windows ADK zum Automatisieren von Windows-Installationen, Erfassen von Windows-Images, Migrieren von Benutzerprofilen und -daten usw.  

 Die folgenden Funktionen von Windows ADK müssen auf dem Standortserver des obersten Standorts der Hierarchie, auf dem Standortserver jedes primären Standorts der Hierarchie und auf dem Standortsystemserver mit der Rolle SMS-Anbieter installiert sein:  

-   Migrationsprogramm für den Benutzerzustand (USMT) <sup>1</sup>  

-   Windows-Bereitstellungstools  

-   Windows-Vorinstallationsumgebung (Windows Preinstallation Environment, Windows PE)

Eine Liste der Versionen des Windows 10 ADK, die Sie mit verschiedenen Versionen von Configuration Manager verwenden können, finden Sie unter [Support For Windows 10 as a client (Unterstützung für Windows 10 als ein Client)](https://docs.microsoft.com/en-us/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

 <sup>1</sup> USMT ist auf dem Standortsystemserver mit der Rolle „SMS-Anbieter“ nicht erforderlich.  

> [!NOTE]  
>  Sie müssen Windows ADK manuell auf allen Computern installieren, auf denen ein Standort der zentralen Verwaltung oder ein primärer Standortserver gehostet wird, bevor Sie den Configuration Manager-Standort installieren.  

 Weitere Informationen finden Sie in folgenden Quellen:  

-   [Windows ADK für Windows 10-Szenarien für IT-Experten](https://technet.microsoft.com/library/mt280162\(v=vs.85\).aspx)  

-   [Windows ADK für Windows 10 herunterladen](https://msdn.microsoft.com/windows/hardware/dn913721.aspx#adkwin10)  

-   [Unterstützung für Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>Migrationsprogramm für den Benutzerzustand (USMT)  
 Configuration Manager verwendet ein USMT-Paket, das die USMT 10-Quelldateien enthält, zum Erfassen und Wiederherstellen des Benutzerzustands als Teil Ihrer Betriebssystembereitstellung. Configuration Manager am Standort der obersten Ebene erstellt das USMT-Paket automatisch. USMT 10 kann den Benutzerzustand von Windows 7, Windows 8, Windows 8.1 und Windows 10 erfassen. USMT 10 wird im Windows ADK (Windows Assessment and Deployment Kit) für Windows 10 verteilt.  

 Weitere Informationen finden Sie in folgenden Quellen:  

-   [Allgemeine Migrationsszenarien für USMT 10](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)  

-   [Verwalten des Benutzerzustands](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 Windows PE wird für Startabbilder verwendet, um einen Computer zu starten. Es handelt sich um ein Windows-Betriebssystem mit eingeschränkten Diensten, das vor der Installation und während der Bereitstellung von Windows-Betriebssystemen verwendet wird. Im Folgenden finden Sie die Version von Configuration Manager und die jeweils unterstützte Version des Windows ADK, die Windows PE-Version, auf der das Startimage basiert, das über die Configuration Manager-Konsole angepasst werden kann, und die Windows PE-Versionen, auf denen das Startimage basiert, das Sie mithilfe von DISM anpassen und anschließend der angegebenen Version von Configuration Manager hinzufügen können.  

#### <a name="configuration-manager-version-1511"></a>Configuration Manager, Version 1511  
 Im Folgenden finden Sie die jeweils unterstützte Version des Windows ADK, die Windows PE-Version, auf der das Startimage basiert, das über die Configuration Manager-Konsole angepasst werden kann, und die Windows PE-Versionen, auf denen das Startimage basiert, das Sie mithilfe von DISM anpassen und anschließend Configuration Manager hinzufügen können.  

-   **Windows ADK-Version**  

     Windows ADK für Windows 10  

-   **Windows PE-Versionen für Startimages, die über die Configuration Manager-Konsole angepasst werden können**  

     Windows PE 10  

-   **Unterstützte Windows PE-Versionen für Startimages, die nicht über die Configuration Manager-Konsole angepasst werden können**  

     Windows PE 3.1<sup>1</sup> und Windows PE 5  

     <sup>1</sup> Sie können zu Configuration Manager nur dann ein Startimage hinzufügen, wenn es auf Windows PE 3.1 basiert. Installieren Sie die Ergänzung zu Windows AIK für Windows 7 SP1, um ein Upgrade von Windows AIK für Windows 7 (basierend auf Windows PE 3) mit der Ergänzung zu Windows AIK für Windows 7 SP1 (basierend auf Windows PE 3.1) durchzuführen. Sie können die Ergänzung zu Windows AIK für Windows 7 SP1 aus dem [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=5188)herunterladen.  

     Im Fall von Configuration Manager etwa können Sie Startimages aus Windows ADK für Windows 10 (das auf Windows PE 10 basiert) über die Configuration Manager-Konsole anpassen. Zwar werden auf Windows PE 5 basierende Startabbilder unterstützt, doch müssen Sie sie von einem anderen Computer aus anpassen und die mit dem Windows ADK für Windows 8 installierte DISM-Version verwenden. Danach können Sie das Startimage der Configuration Manager-Konsole hinzufügen. Weitere Informationen und Vorgehensweisen zum Anpassen eines Startimages (Hinzufügen von optionalen Komponenten und Treibern), zum Aktivieren der Befehlsunterstützung für das Startimage, zum Hinzufügen des Startimages zur Configuration Manager-Konsole und zum Aktualisieren der Verteilungspunkte mit dem Startimage finden Sie unter[Anpassen von Startimages](../get-started/customize-boot-images.md). Weitere Informationen zu Startabbildern finden Sie im Thema [Verwalten von Startabbildern (Startimages)](../get-started/manage-boot-images.md).  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
Sie müssen die folgenden WSUS 4.0-Hotfixes installieren:
  - [Hotfix 3095113](https://support.microsoft.com/kb/3095113) ist für die Wartung von Windows 10 erforderlich, für die die Infrastruktur für Softwareupdates verwendet wird, um Upgrades für Windows 10-Features abzurufen. Wenn Sie über WSUS 3.2 verfügen, müssen Sie für Windows 10-Upgrades Tasksequenzen verwenden. Weitere Informationen finden Sie unter [Verwalten von Windows als Dienst](../deploy-use/manage-windows-as-a-service.md).  
  - [Hotfix 3159706](https://support.microsoft.com/kb/3159706) ist erforderlich, um über die Windows 10-Wartung ein Upgrade von Computern auf Windows 10 Anniversary Update sowie Unterversionen durchzuführen. Im Support-Artikel werden manuelle Schritte beschrieben, die Sie ausführen müssen, um diesen Hotfix zu installieren. Weitere Informationen finden Sie unter [Verwalten von Windows als Dienst](../deploy-use/manage-windows-as-a-service.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Internetinformationsdienste (IIS) auf den Standortsystemservern  
 IIS ist für den Verteilungspunkt, Zustandsmigrationspunkt und Verwaltungspunkt erforderlich. Weitere Informationen zu dieser Anforderung finden Sie unter [Voraussetzungen für Standorte und Standortsysteme](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-deployment-services-wds"></a>Windows-Bereitstellungsdienste (Windows Deployment Services, WDS)  
 Für PXE-Bereitstellungen sind Windows-Bereitstellungsdienste (WDS) bei Verwendung von Multicast zur Bandbreitenoptimierung in Ihren Bereitstellungen und zur Offlinewartung von Abbildern erforderlich. Wenn der Anbieter auf einem Remoteserver installiert ist, müssen Sie WDS auf dem Standortserver und dem Remoteanbieter installieren. Weitere Informationen finden Sie unter [Windows-Bereitstellungsdienste](#BKMK_WDS) in diesem Thema.  

### <a name="dynamic-host-configuration-protocol-dhcp"></a>Dynamic Host Configuration-Protokoll (DHCP)  
 DHCP ist für PXE-Bereitstellungen erforderlich. Sie müssen über einen betriebsbereiten DHCP-Server mit einem aktiven Host verfügen, um Betriebssysteme per PXE bereitstellen zu können. Weitere Informationen zu PXE-Bereitstellungen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Unterstützte Betriebssysteme und Festplattenkonfigurationen  
 Weitere Informationen zu den Betriebssystemversionen und Festplattenkonfigurationen, die Configuration Manager bei der Betriebssystembereitstellung unterstützt, finden Sie unter [Unterstützte Betriebssysteme](#BKMK_SupportedOS) und [Unterstützte Festplattenkonfigurationen](#BKMK_SupportedDiskConfig).  

### <a name="windows-device-drivers"></a>Windows-Gerätetreiber  
 Sie können Windows-Gerätetreiber verwenden, wenn Sie das Betriebssystem auf dem Zielcomputer installieren und Windows PE mithilfe eines Startabbilds ausführen. Weitere Informationen zu Gerätetreibern finden Sie unter [Verwalten von Treibern](../get-started/manage-drivers.md).  

##  <a name="BKMK_InternalDependencies"></a> Abhängigkeiten in Configuration Manager  
 Nachstehend finden Sie Informationen zu den Voraussetzungen für die Configuration Manager-Betriebssystembereitstellung.  

### <a name="operating-system-image"></a>Betriebssystemabbild  
 Betriebssystemabbilder in Configuration Manager werden im WIM-Dateiformat (Windows Imaging) gespeichert. Sie stellen eine komprimierte Sammlung von Verweisdateien und -ordnern dar, die für die erfolgreiche Installation und Konfiguration eines Betriebssystems auf einem Computer erforderlich sind. Weitere Informationen finden Sie unter [Verwalten von Betriebssystemimages](../get-started/manage-operating-system-images.md).  

### <a name="driver-catalog"></a>Treiberkatalog  
 Zur Bereitstellung eines Gerätetreibers müssen Sie den Gerätetreiber importieren, aktivieren und auf einem Verteilungspunkt verfügbar machen, auf den der Configuration Manager-Client zugreifen kann. Weitere Informationen finden Sie unter [Verwalten von Treibern](../get-started/manage-drivers.md).  

### <a name="management-point"></a>Verwaltungspunkt  
 Informationen zwischen Clientcomputern und dem Configuration Manager-Standort werden über Verwaltungspunkte übertragen. Verwaltungspunkte werden von Clients zur Ausführung aller Tasksequenzen verwendet, die für den Abschluss der Betriebssystembereitstellung erforderlich sind.  

 Weitere Informationen zu Tasksequenzen finden Sie unter [Planungsüberlegungen für das Automatisieren von Tasks](planning-considerations-for-automating-tasks.md).  

### <a name="distribution-point"></a>Verteilungspunkt  
 Verteilungspunkte werden in den meisten Bereitstellungen verwendet, um die Daten für die Betriebssystembereitstellung zu speichern, beispielsweise das Betriebssystemabbild oder Gerätetreiberpakete. In Tasksequenzen werden Daten normalerweise von einem Verteilungspunkt abgerufen, um das Betriebssystem bereitzustellen.  

 Weitere Informationen zum Installieren von Verteilungspunkten und Verwalten von Inhalt finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="pxe-enabled-distribution-point"></a>PXE-fähiger Verteilungspunkt  
 Für PXE-initiierte Bereitstellungen müssen Sie einen Verteilungspunkt so konfigurieren, dass die von Clients gestellten PXE-Anforderungen vom Verteilungspunkt akzeptiert werden. Weitere Informationen zum Konfigurieren des Verteilungspunkts finden Sie unter [Konfigurieren eines Verteilungspunkts](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).  

### <a name="multicast-enabled-distribution-point"></a>Multicast-fähiger Verteilungspunkt  
 Wenn Sie Ihre Betriebssystembereitstellungen mithilfe von Multicast optimieren möchten, müssen Sie einen Verteilungspunkt für die Unterstützung von Multicast konfigurieren. Weitere Informationen zum Konfigurieren des Verteilungspunkts finden Sie unter [Konfigurieren eines Verteilungspunkts](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).   

### <a name="state-migration-point"></a>Zustandsmigrationspunkt  
 Wenn Sie Benutzerzustandsdaten für parallele oder aktualisierte Bereitstellungen erfassen und wiederherstellen möchten, müssen Sie einen Zustandsmigrationspunkt zum Speichern der Benutzerzustandsdaten auf einem anderen Computer konfigurieren.  

 Weitere Informationen zum Konfigurieren des Zustandsmigrationspunkts finden Sie unter [Zustandsmigrationspunkt](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

 Informationen zum Erfassen und Wiederherstellen des Benutzerzustands finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

### <a name="service-connection-point"></a>Dienstverbindungspunkt  
 Wenn Sie Windows als Dienst (WaaS) zum Bereitstellen des aktuellen Branch von Windows 10 verwenden, muss der Dienstverbindungspunkt installiert sein. Weitere Informationen finden Sie unter [Verwalten von Windows als Dienst](../deploy-use/manage-windows-as-a-service.md).  

### <a name="reporting-services-point"></a>Reporting Services-Punkt  
 Zur Verwendung von Configuration Manager-Berichten für Betriebssystembereitstellungen müssen Sie einen Reporting Services-Punkt installieren und konfigurieren. Weitere Informationen finden Sie unter [Berichterstattung](../../core/servers/manage/reporting.md).  

### <a name="security-permissions-for-operating-system-deployments"></a>Sicherheitsberechtigungen für Betriebssystembereitstellungen  
 Die Sicherheitsrolle **Betriebssystembereitstellungs-Manager** ist eine integrierte Rolle und kann nicht geändert werden. Sie können jedoch eine Kopie dieser Sicherheitsrolle erstellen, ändern und als neue benutzerdefinierte Sicherheitsrolle speichern. Zu den Berechtigungen, die direkt für Betriebssystembereitstellungen gelten, gehören die folgenden:  

-   **Startabbildpaket**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

-   **Gerätetreiber**: Erstellen, Löschen, Ändern, Ordner ändern, Bericht ändern, Objekt verschieben, Lesen, Bericht ausführen  

-   **Treiberpaket**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

-   **Betriebssystemabbild**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

-   **Installationspakete für Betriebssystem**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

-   **Tasksequenzpaket**: Erstellen, Tasksequenzmedien erstellen, Löschen, Ändern, Ordner ändern, Bericht ändern, Objekt verschieben, Lesen, Bericht ausführen, Sicherheitsbereich festlegen  

 Weitere Informationen zu benutzerdefinierten Sicherheitsrollen finden Sie unter [Erstellen von benutzerdefinierten Sicherheitsrollen](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  

### <a name="security-scopes-for-operating-system-deployments"></a>Sicherheitsbereiche für Betriebssystembereitstellungen  
 Verwenden Sie Sicherheitsbereiche, um Administratoren Zugriff auf in Betriebssystembereitstellungen verwendete sicherungsfähige Objekte zu gewähren, beispielsweise auf Betriebssystemabbilder, Startabbilder, Treiberpakete und Tasksequenzpakete. Weitere Informationen finden Sie unter [Sicherheitsbereiche](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  

##  <a name="BKMK_WDS"></a> Windows-Bereitstellungsdienste  
 Die Windows-Bereitstellungsdienste (Windows Deployment Services, WDS) müssen auf dem gleichen Server installiert sein wie die Verteilungspunkte, die Sie für die Unterstützung von PXE oder Multicast konfigurieren. Der Windows-Bereitstellungsdienst ist im Betriebssystem des Servers enthalten. Bei PXE-Bereitstellungen wird der PXE-Start von den Windows-Bereitstellungsdiensten ausgeführt. Wenn der Verteilungspunkt installiert und PXE-fähig ist, erstellt Configuration Manager einen Anbieter in WDS, von dem die PXE-Startfunktionen der Windows-Bereitstellungsdienste verwendet werden.  

> [!NOTE]  
>  Wenn der Server einen Neustart fordert, kann die Installation der WDS fehlschlagen. 

 Ferner sind die folgenden anderen WDS-Konfigurationen zu berücksichtigen:  

-   Für die WDS-Installation auf dem Server muss der Administrator Mitglied der lokalen Administratorgruppe sein.  

-   Der WDS-Server muss entweder Mitglied einer Active Directory-Domäne oder ein Domänencontroller für eine Active Directory-Domäne sein. Alle Windows-Domänen- und Gesamtstrukturkonfigurationen unterstützen WDS.  

-   Wenn der Anbieter auf einem Remoteserver installiert ist, müssen Sie WDS auf dem Standortserver und dem Remoteanbieter installieren.  

###  <a name="BKMK_WDSandDHCP"></a> Aspekte, wenn sich Windows-Bereitstellungsdienst und DHCP auf demselben Server befinden  
 Wenn Sie planen, einen PXE-Verteilungspunkt auf dem gleichen Server zu hosten, auf dem DHCP ausgeführt wird, sollten Sie die folgenden Konfigurationsoptionen in Erwägung ziehen.  

-   Sie benötigen einen funktionsfähigen DHCP-Server mit einem aktiven Bereich. Von den Windows-Bereitstellungsdiensten wird PXE verwendet, sodass ein DHCP-Server erforderlich ist.  

-   Für DHCP und Windows-Bereitstellungsdienste ist jeweils der Port mit der Nummer 67 erforderlich. Wenn Sie die Windows-Bereitstellungsdienste und DHCP auf dem gleichen Server hosten, können Sie DHCP oder den für PXE konfigurierten Verteilungspunkt auf einen separaten Server verschieben. Außerdem können Sie das folgende Verfahren verwenden, um den Server mit den Windows-Bereitstellungsdiensten so zu konfigurieren, dass ein anderer Port überwacht wird.  

    #### <a name="to-configure-the-windows-deployment-services-server-to-listen-on-a-different-port"></a>So konfigurieren Sie den Windows-Bereitstellungsdiensteserver für die Überwachung eines anderen Ports  

    1.  Ändern Sie den folgenden Registrierungsschlüssel:  

         **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE**  

    2.  Legen Sie für den Registrierungswert Folgendes fest: **UseDHCPPorts = 0**  

    3.  Damit die neue Konfiguration wirksam wird, führen Sie den folgenden Befehl auf dem Server aus:  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   Ein DNS-Server wird benötigt, um die Windows-Bereitstellungsdienste auszuführen.  

-   Die folgenden UDP-Ports müssen auf dem Windows-Bereitstellungsdiensteserver geöffnet sein.  

    -   Port 67 (DHCP)  

    -   Port 69 (TFTP)  

    -   Port 4011 (PXE)  

    > [!NOTE]  
    >  Falls die DHCP-Autorisierung auf dem Server erforderlich ist, muss auf dem Server außerdem DHCP-Clientport 68 geöffnet sein.  

##  <a name="BKMK_SupportedOS"></a> Unterstützte Betriebssysteme  
 Alle Betriebssysteme, die als unterstützte Clientbetriebssysteme unter [Unterstützte Betriebssysteme für Clients und Geräte](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) aufgeführt werden, werden für Betriebssystembereitstellungen unterstützt.  

##  <a name="BKMK_SupportedDiskConfig"></a> Unterstützte Festplattenkonfigurationen  
 In der folgenden Tabelle sind die für die Configuration Manager-Betriebssystembereitstellung unterstützten Kombinationen der Festplattenkonfiguration auf dem Referenzcomputer und dem Zielcomputer aufgelistet.  

|Festplattenkonfiguration auf Referenzcomputer|Festplattenkonfiguration auf Zielcomputer|  
|------------------------------------------------|--------------------------------------------------|  
|Basisfestplatte|Basisfestplatte|  
|Einfaches Volume auf einer dynamischen Festplatte|Einfaches Volume auf einer dynamischen Festplatte|  

 Configuration Manager unterstützt das Erfassen eines Betriebssystemimages nur über Computer, die mit einfachen Volumes konfiguriert sind. Die folgenden Festplattenkonfigurationen werden nicht unterstützt:  

-   Übergreifende Volumes  

-   Stripesetvolumes (RAID 0)  

-   Gespiegelte Volumes (RAID 1)  

-   Paritätsvolumes (RAID 5)  

 Die in der folgenden Tabelle angegebene Festplattenkonfiguration auf dem Referenzcomputer und dem Zielcomputer wird in Configuration Manager nicht unterstützt.  

|Festplattenkonfiguration auf Referenzcomputer|Festplattenkonfiguration auf Zielcomputer|  
|------------------------------------------------|--------------------------------------------------|  
|Basisfestplatte|Dynamische Festplatte|  

## <a name="next-steps"></a>Nächste Schritte
[Vorbereiten auf die Betriebssystembereitstellung](../get-started/prepare-for-operating-system-deployment.md)
