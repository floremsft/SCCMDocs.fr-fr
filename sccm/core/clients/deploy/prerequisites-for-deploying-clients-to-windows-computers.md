---
title: "Voraussetzungen für die Bereitstellung des Windows-Clients | Microsoft-Dokumentation"
description: "Hier erhalten Sie Informationen über die Voraussetzungen für die Bereitstellung von Clients auf Windows-Computern in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
caps.latest.revision: "16"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6636ce4d929326fad0210407d7634ea585eb0a2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-system-center-configuration-manager"></a>Voraussetzungen für die Bereitstellung von Clients auf Windows-Computern in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei der Bereitstellung von Configuration Manager-Clients in einer Umgebung sind die folgenden externen und produktinternen Abhängigkeiten zu beachten. Darüber hinaus weist jede Clientbereitstellungsmethode eigene Abhängigkeiten auf, die erfüllt sein müssen, um eine erfolgreiche Clientinstallation auszuführen.  

  Lesen Sie auch den Artikel [Unterstützte Konfigurationen für System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md), um sicherzustellen, dass die Geräte die Mindestanforderungen an Hardware und Betriebssystem für den Configuration Manager-Client erfüllen.  

 Weitere Informationen zu den Anforderungen an den Configuration Manager-Client für Linux und UNIX finden Sie unter [Planen der Clientbereitstellung auf Linux- und UNIX-Computern in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

> [!NOTE]  
>  Bei den in diesem Artikel aufgeführten Softwareversionsnummern handelt es sich um die erforderlichen Mindestversionsnummern.  

##  <a name="BKMK_prereqs_computers"></a> Voraussetzungen für Computerclients  
 Mithilfe der folgenden Informationen können Sie die Voraussetzungen für die Installation des Configuration Manager-Clients auf Computern bestimmen.  

### <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  

|||  
|-|-|  
|Windows Installer Version 3.1.4000.2435|Erforderlich, um die Verwendung der Microsoft Windows Installer-Updatedateien (.msp) für Pakete und Softwareupdates zu unterstützen.|  
|[KB2552033](http://go.microsoft.com/fwlink/p/?LinkId=240048)|Wenn die Clientpushinstallation aktiviert ist, müssen Sie diesen Hotfix auf Standortservern installieren, auf denen Windows Server 2008 R2 ausgeführt wird.|  
|Microsoft Background Intelligent Transfer Service (BITS) Version 2.5|Erforderlich, um Datenübertragungen eingeschränkter Bandbreite zwischen dem Clientcomputer und den Configuration Manager-Standortsystemen zu ermöglichen. BITS wird während der Clientinstallation nicht automatisch heruntergeladen. Wird BITS auf Computern installiert, ist zum Abschließen der Installation in der Regel ein Neustart erforderlich.<br /><br /> Die meisten Betriebssysteme enthalten BITS. Ist dies nicht der Fall (z.B. bei Windows Server 2003 R2 SP2), müssen Sie BITS vor der Installation des Configuration Manager-Clients installieren.|  
|Microsoft-Aufgabenplanung|Aktivieren Sie diesen Dienst auf dem Client, um die Clientinstallation abzuschließen.|  

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a>Externe abhängige Komponenten, die bei der Installation von Configuration Manager automatisch heruntergeladen werden  
 Der Configuration Manager-Client verfügt über einige potenzielle externe Abhängigkeiten. Diese Abhängigkeiten hängen vom Betriebssystem und der installierten Software auf dem Clientcomputer ab.  

 Wenn diese abhängigen Komponenten zum Abschließen der Clientinstallation erforderlich sind, werden sie automatisch mit der Clientsoftware installiert.  

|||  
|-|-|  
|Windows Update Agent Version 7.0.6000.363|Wird von Windows zur Unterstützung der Updateerkennung und -bereitstellung benötigt.|  
|Microsoft Core XML Services (MSXML) Version 6.20.5002 oder höher|Wird unter Windows zur Unterstützung der Verarbeitung von XML-Dokumenten benötigt.|  
|Microsoft Remote Differential Compression (RDC)|Ist erforderlich, um die Datenübertragung über das Netzwerk zu optimieren.|  
|Microsoft Visual C++ 2013 Redistributable Version 12.0.21005.1|Ist zur Unterstützung von Clientoperationen erforderlich. Wenn dieses Update auf den Clientcomputern installiert wird, ist möglicherweise ein Neustart erforderlich, um die Installation abzuschließen.|  
|Microsoft Visual C++ 2005 Redistributable Version 8.0.50727.42|Für die Version 1606 und ältere Versionen ist erforderlich, das Microsoft SQL Server Compact-Operationen unterstützt werden.|  
|Windows Imaging APIs 6.0.6001.18000|Ist erforderlich für die Verwaltung von Windows-Imagedateien (.wim) mit Configuration Manager.|  
|Microsoft-Richtlinienplattform 1.2.3514.0|Ist erforderlich, damit Kompatibilitätseinstellungen von Clients ausgewertet werden können.|  
|Microsoft Silverlight 5.1.41212.0 (beginnend in Configuration Manager-Version 1602)|Ist erforderlich, um die Benutzerfreundlichkeit der Anwendungskatalog-Website zu unterstützen.|  
|Microsoft .NET Framework 4.5.2|Ist zur Unterstützung von Clientoperationen erforderlich. Wird automatisch auf auf dem Clientcomputer installiert, wenn Microsoft .NET Framework 4.5 oder höher nicht installiert ist. Weitere Informationen finden Sie im nächsten Abschnitt unter [Weitere Informationen über Microsoft .NET Framework, Version 4.5.2](#dotNet).|  
|Microsoft SQL Server Compact 3.5 SP2-Komponenten|Ist erforderlich zum Speichern von Informationen zu Clientoperationen.|  
|Microsoft Windows Imaging Components|Ist erforderlich für Microsoft .NET Framework 4.0 auf 64-Bit-Computern unter Windows Server 2003 oder Windows XP SP2.|
|Microsoft Intune PC-Softwareclient|Der Intune PC-Softwareclient und der Configuration Manager-Client können nicht auf dem gleichen PC ausgeführt werden. Stellen Sie sicher, dass der Intune-Client entfernt wurde, bevor Sie den Configuration Manager-Client installieren.|

####  <a name="dotNet"></a> Weitere Informationen über Microsoft .NET Framework, Version 4.5.2  

> [!NOTE]  
>  Die Unterstützung für .NET 4.0, 4.5 und 4.5.1 ist am 12. Januar 2016 abgelaufen. Weitere Informationen finden Sie in den [häufig gestellten Fragen zur Microsoft-Support-Lifecycle-Richtlinie für .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) unter „support.microsoft.com“.  

 Zum Abschluss der Installation von Microsoft .NET Framework 4.5.2 ist möglicherweise ein Neustart des Systems erforderlich. Der Benutzer sieht auf der Taskleiste die Benachrichtigung **Neustart erforderlich** .  Allgemeine Szenarien, die den Neustart von Clientcomputern erfordern:  

-   .NET-Anwendungen oder -Dienste, die auf dem Computer ausgeführt werden.  

-   Es fehlen ein oder mehrere Softwareupdates, die für die .NET-Installation erforderlich sind.  

-   Der Computer wartet auf einen Neustart aufgrund einer vorherigen Installation von Softwareupdates für .NET Framework.  

 Nach der Installation von .NET Framework 4.5.2 müssen möglicherweise weitere Updates installiert werden, was weitere Neustarts erfordern kann.  

### <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  
 Weitere Informationen über diese Standortsystemrollen finden Sie unter [Ermitteln der Standortsystemrollen für System Center Configuration Manager-Clients](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|||  
|-|-|  
|Verwaltungspunkt|Obgleich kein Verwaltungspunkt notwendig ist, um den Configuration Manager-Client bereitzustellen, muss ein Verwaltungspunkt vorhanden sein, um Informationen zwischen Clientcomputern und Configuration Manager-Servern zu übertragen. Ohne Verwaltungspunkt können Sie Clientcomputer nicht verwalten.|  
|Verteilungspunkt|Der Verteilungspunkt ist eine optionale Standortsystemrolle, deren Verwendung für die Clientbereitstellung jedoch empfohlen wird. Die Clientquelldateien werden auf allen Verteilungspunkten gehostet. So können Computer den nächsten Verteilungspunkt ermitteln, von dem die Clientquelldateien während der Clientbereitstellung heruntergeladen werden können. Falls der Standort nicht über einen Verteilungspunkt verfügt, werden die Clientquelldateien von Computern vom jeweiligen Verwaltungspunkt heruntergeladen.|  
|Fallbackstatuspunkt|Der Fallbackstatuspunkt ist eine optionale Standortsystemrolle, deren Verwendung für die Clientbereitstellung jedoch empfohlen wird. Mithilfe des Fallbackstatuspunkts wird die Clientbereitstellung nachverfolgt, und es wird Computern am Configuration Manager-Standort ermöglicht, Zustandsmeldungen zu senden, wenn sie nicht mit einem Verwaltungspunkt kommunizieren können.|  
|Reporting Services-Punkt|Der Reporting Services-Punkt ist eine optionale, aber empfohlene Standortsystemrolle, über die Berichte zur Bereitstellung und Verwaltung von Clients angezeigt werden können. Weitere Informationen finden Sie unter [Berichterstellung in System Center Configuration Manager](../../../core/servers/manage/reporting.md).|  

### <a name="installation-method-dependencies"></a>Installationsmethodenabhängigkeiten  
 Die folgenden Voraussetzungen gelten für die verschiedenen Clientinstallationsmethoden.  

-   Clientpushinstallation  

    -   Clientpushinstallationskonten werden verwendet, um eine Verbindung mit Computern zur Installation des Clients herzustellen. Sie werden im Dialogfeld **Eigenschaften von Clientpushinstallation** auf der Registerkarte **Konten** angegeben. Das Konto muss ein Mitglied der lokalen Gruppe „Administratoren“ auf dem Zielcomputer sein.  

         Wenn Sie kein Clientpushinstallationskonto angeben, wird das Konto des Standortservercomputers verwendet.  

    -   Der Zielcomputer der Clientinstallation muss mit mindestens einer Configuration Manager-Ermittlungsmethode ermittelt worden sein.  

    -   Auf dem Computer ist eine ADMIN$-Freigabe vorhanden.  

    -   Im Dialogfeld **Eigenschaften der Clientpushinstallation** muss die Option **Clientpushinstallation auf zugewiesenen Ressourcen aktivieren** aktiviert sein, wenn Sie den Configuration Manager-Client automatisch mittels Push auf die ermittelten Ressourcen übertragen möchten.  

    -   Vom Clientcomputer muss eine Verbindung mit einem Verteilungspunkt oder einem Verwaltungspunkt hergestellt werden können, um unterstützende Dateien herunterzuladen.  

     Sie müssen über die folgenden Sicherheitsberechtigungen verfügen, um den Configuration Manager-Client mithilfe der Clientpushinstallation installieren zu können:  

    -   Berechtigungen **Ändern** und **Lesen** für das Standortobjekt, um das Clientpushinstallationskonto konfigurieren zu können  

    -   Berechtigungen **Ressource ändern** und **Lesen** für das Sammlungsobjekt, um den Client mithilfe der Clientpushinstallation in Sammlungen installieren zu können  

     Die Sicherheitsrolle **Infrastrukturadministrator** umfasst die für die Verwaltung der Clientpushinstallation erforderlichen Berechtigungen.  

-   Auf einem Softwareupdatepunkt basierende Installation  

    -   Wenn das Active Directory-Schema nicht erweitert wurde oder Sie Clients von einer anderen Gesamtstruktur aus installieren, müssen die Installationseigenschaften für CCMSetup.exe mithilfe von Gruppenrichtlinien in der Registrierung des Computers angegeben werden. Weitere Informationen finden Sie unter  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   Der Configuration Manager-Client muss auf dem Softwareupdatepunkt veröffentlicht werden.  

    -   Vom Clientcomputer muss eine Verbindung mit einem Verteilungspunkt oder einem Verwaltungspunkt hergestellt werden können, um unterstützende Dateien herunterzuladen.  

     Die erforderlichen Sicherheitsberechtigungen zum Verwalten von Configuration Manager-Softwareupdates finden Sie unter [Voraussetzungen für Softwareupdates in System Center Configuration Manager](../../../sum/plan-design/prerequisites-for-software-updates.md).  

-   Auf einer Gruppenrichtlinie basierende Installation  

    -   Wenn das Active Directory-Schema nicht erweitert wurde oder Sie Clients von einer anderen Gesamtstruktur aus installieren, müssen die Installationseigenschaften für CCMSetup.exe mithilfe von Gruppenrichtlinien in der Registrierung des Computers angegeben werden. Weitere Informationen finden Sie unter  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   Der Clientcomputer muss eine Verbindung mit einem Verwaltungspunkt herstellen können, damit er unterstützende Dateien herunterladen kann.  

-   Auf einem Anmeldeskript basierende Installation  

     Vom Clientcomputer muss eine Verbindung mit einem Verteilungspunkt oder einem Verwaltungspunkt hergestellt werden können, um unterstützende Dateien herunterzuladen. Dies ist nicht erforderlich, wenn „CCMSetup.exe“ mit der Befehlszeileneigenschaft **ccmsetup /source**über die Eingabeaufforderung angegeben wurde.  

-   Manuelle Installation  

     Vom Clientcomputer muss eine Verbindung mit einem Verteilungspunkt oder einem Verwaltungspunkt hergestellt werden können, um unterstützende Dateien herunterzuladen. Dies ist nicht erforderlich, wenn „CCMSetup.exe“ mit der Befehlszeileneigenschaft **ccmsetup /source**über die Eingabeaufforderung angegeben wurde.  

-   Installation von Arbeitsgruppencomputern  

     Das Netzwerkzugriffskonto muss für den Standort konfiguriert sein, um auf Ressourcen in der Configuration Manager-Standortserverdomäne zugreifen zu können.  

     Weitere Informationen zum Konfigurieren des Netzwerkzugriffskontos finden Sie unter [Fundamental concepts for content management in System Center Configuration Manager (Grundlegende Konzepte für das Content Management in System Center Configuration Manager)](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Auf einer Softwareverteilung basierende Installation (nur für Upgrades)  

    -   Wenn das Active Directory-Schema nicht erweitert wurde oder Sie Clients von einer anderen Gesamtstruktur aus installieren, müssen die Installationseigenschaften für CCMSetup.exe mithilfe von Gruppenrichtlinien in der Registrierung des Computers angegeben werden. Weitere Informationen finden Sie unter [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   Vom Clientcomputer muss eine Verbindung mit einem Verteilungspunkt oder einem Verwaltungspunkt hergestellt werden können, um unterstützende Dateien herunterzuladen.  

     Die Sicherheitsberechtigungen, die für ein Upgrade des Configuration Manager-Clients über die Anwendungsverwaltung erforderlich sind, finden Sie unter [Sicherheit und Datenschutz für die Anwendungsverwaltung](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   Automatische Clientupgrades  

     Sie müssen ein Mitglied der Sicherheitsrolle **Hauptadministrator** sein, um automatische Clientupgrades konfigurieren zu können.  

### <a name="firewall-requirements"></a>Firewallanforderungen  
 Wenn sich zwischen den Standortsystemservern und den Computern, auf denen der Configuration Manager-Client installiert werden soll, eine Firewall befindet, lesen Sie die Hinweise unter [Windows-Firewall- und -Porteinstellungen für Clients in System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

##  <a name="BKMK_prereqs_mobiledevices"></a> Voraussetzungen für Clients für mobile Geräte  
 Mithilfe der folgenden Informationen können Sie die Voraussetzungen für die Installation des Configuration Manager-Clients auf mobilen Geräten bestimmen und diese mithilfe von Configuration Manager registrieren.  

### <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  

-   Eine Microsoft-Unternehmenszertifizierungsstelle (CA) mit Zertifikatvorlagen, um die Zertifikate bereitzustellen und zu verwalten, die für mobile Geräte erforderlich sind  

     Von der ausstellenden Zertifizierungsstelle müssen im Rahmen der Anmeldung automatisch Zertifikatanforderungen genehmigt werden, die von Benutzern mobiler Geräte übermittelt wurden.  

     Weitere Informationen zu Zertifikatanforderungen finden Sie unter [Sicherheit und Datenschutz für Zertifikatprofile in System Center Configuration Manager](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

-   Eine Sicherheitsgruppe mit Benutzern, die ihre mobilen Geräte anmelden können  

     Mit dieser Sicherheitsgruppe wird die im Rahmen der Anmeldung der mobilen Geräte verwendete Zertifikatvorlage konfiguriert.  

-   Optional, jedoch empfohlen: ein für den Namen des Standortsystemservers, auf dem der Anmeldungsproxypunkt installiert wird, konfigurierter DNS-Alias (CNAME-Eintrag) mit der Bezeichnung **ConfigMgrEnroll**  

     Dieser DNS-Alias ist erforderlich, um die automatische Ermittlung für den Anmeldungsdienst zu unterstützen: Wenn dieser DNS-Datensatz nicht konfiguriert wird, müssen Benutzer im Rahmen des Anmeldungsprozesses den Namen des Standortsystemservers für den Anmeldungsproxypunkt manuell angeben.  

-   Abhängigkeiten der Standortsystemrollen für die Computer, auf denen die Standortsystemrollen „Anmeldungspunkt“ und „Anmeldungsproxypunkt“ ausgeführt werden  

     Informationen hierzu finden Sie unter [Supported operating systems for site system servers](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md) (Unterstützte Betriebssysteme für Standortsystemserver).  

### <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  
 Weitere Informationen über diese Standortsystemrollen finden Sie unter [Ermitteln der Standortsystemrollen für System Center Configuration Manager-Clients](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

-   Verwaltungspunkt, der für HTTPS-Clientverbindungen konfiguriert und für mobile Geräte aktiviert ist  

     Ein Verwaltungspunkt ist immer erforderlich, um den Configuration Manager-Client auf mobilen Geräten installieren zu können. Zusätzlich zu diesen Konfigurationsanforderungen (HTTPS-Unterstützung und aktiviert für mobile Geräte) muss der Verwaltungspunkt mit einem Internet-FQDN konfiguriert sein, und Clientverbindungen über das Internet müssen möglich sein.  

-   Anmeldungspunkt und Anmeldungsproxypunkt  

     Mithilfe eines Anmeldungsproxypunkts werden Anmeldungsanforderungen von mobilen Geräten verwaltet. Der Anmeldungspunkt schließt den Anmeldungsprozess ab. Der Anmeldungspunkt muss sich in der gleichen Active Directory-Gesamtstruktur befinden wie der Standortserver. Der Anmeldungsproxypunkt kann sich dagegen in einer anderen Gesamtstruktur befinden.  

-   Clienteinstellungen für die Anmeldung mobiler Geräte  

     Konfigurieren Sie Clienteinstellungen, damit Benutzer mobile Geräte anmelden können, und konfigurieren Sie mindestens ein Anmeldungsprofil.  

-   Reporting Services-Punkt  

     Der Reporting Services-Punkt ist eine optionale, aber empfohlene Standortsystemrolle, über die Berichte zur Anmeldung mobiler Geräte und zur Clientverwaltung angezeigt werden können.  

     Weitere Informationen finden Sie unter [Berichterstellung in System Center Configuration Manager](../../../core/servers/manage/reporting.md).  

-   Sie müssen über die folgenden Sicherheitsberechtigungen verfügen, um die Anmeldung mobiler Geräte konfigurieren zu können:  

    -   Berechtigung **Ändern** für das Objekt **Standort** , um Anmeldungsstandortsystemrollen hinzufügen, ändern und löschen zu können  

    -   Berechtigung **Ändern** für das Objekt **Standort** , um Clienteinstellungen für die Anmeldung konfigurieren zu können, sowie **Client-Agent**  -Berechtigungen, um benutzerdefinierte Clienteinstellungen konfigurieren zu können  

     Die Sicherheitsrolle **Hauptadministrator** umfasst die für die Konfiguration der Anmeldungsstandortsystemrollen erforderlichen Berechtigungen.  

     Sie müssen über die folgenden Sicherheitsberechtigungen verfügen, um angemeldete mobile Geräte verwalten zu können:  

    -   Berechtigung **Ressource löschen** für das Objekt **Sammlung** , um ein mobiles Gerät zurücksetzen oder außer Kraft setzen zu können  

    -   Berechtigung **Ressource löschen** für das Objekt **Sammlung** , um das Zurücksetzen oder Außerkraftsetzen eines mobilen Geräts abbrechen zu können  

    -   Berechtigung **Ressource ändern** für das Objekt **Sammlung** , um mobile Geräte zulassen und blockieren zu können  

    -   Berechtigung **Ressource ändern** für das Objekt **Sammlung** , um die Kennung auf einem mobilen Gerät remote sperren oder zurücksetzen zu können  

     Die Sicherheitsrolle **Betriebsadministrator** umfasst die für die Verwaltung mobiler Geräte erforderlichen Berechtigungen.  

     Weitere Informationen zum Konfigurieren von Sicherheitsberechtigungen finden Sie unter [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md) und  [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Firewallanforderungen  
 Von beteiligten Netzwerkgeräten wie Routern und Firewalls (einschließlich der Windows-Firewall) muss der Datenverkehr der Anmeldung mobiler Geräte zugelassen werden.  

-   Zwischen mobilen Geräten und Anmeldungsproxypunkt: HTTPS (standardmäßig TCP 443)  

-   Zwischen Anmeldungsproxypunkt und Anmeldungspunkt: HTTPS (standardmäßig TCP 443)  

 Wenn Sie einen Proxywebserver verwenden, muss dieser für SSL-Tunneling konfiguriert sein. SSL-Bridging wird für mobile Geräte nicht unterstützt.  
