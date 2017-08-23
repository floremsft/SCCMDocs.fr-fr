---
title: Von Configuration Manager verwendete Konten | Microsoft-Dokumentation
description: Identifizieren und Verwalten der Windows-Gruppen und Konten in System Center Configuration Manager.
ms.custom: na
ms.date: 2/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a776667cc9f24bd4a468afea76e466c34ce66864
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="accounts-used-in-system-center-configuration-manager"></a>In System Center Configuration Manager verwendete Konten

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die folgenden Informationen, um die in System Center Configuration Manager verwendeten Windows-Gruppen und Konten, die Art der Verwendung sowie alle Anforderungen zu identifizieren.  

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a>Windows-Gruppen, die von Configuration Manager erstellt und verwendet werden  
 Die folgenden Windows-Gruppen werden von Configuration Manager automatisch erstellt und in vielen Fällen automatisch verwaltet.  

> [!NOTE]  
>  Wenn von Configuration Manager eine Gruppe auf einem Computer erstellt wird, der ein Domänenmitglied ist, ist die Gruppe eine lokale Sicherheitsgruppe. Wenn der Computer ein Domänencontroller ist, ist die Gruppe eine lokale Gruppe der Domäne, die von allen Domänencontrollern in der Domäne gemeinsam verwendet wird.  


### <a name="configmgrcollectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess  
Diese Gruppe wird von Configuration Manager für den Zugriff auf Dateien verwendet, die von der Softwareinventur gesammelt wurden.  

In der folgenden Tabelle sind zusätzliche Informationen zu dieser Gruppe aufgelistet:  

|Detail|Weitere Informationen|  
|------------|----------------------|  
|Typ und Speicherort|Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf dem primären Standortserver erstellt wurde.<br /><br /> Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Sie muss manuell gelöscht werden.|  
|Membership|Die Gruppenmitgliedschaft wird von Configuration Manager automatisch verwaltet. In die Mitgliedschaft sind auch Administratoren eingeschlossen, denen die Berechtigung **Gesammelte Dateien anzeigen** für das sicherungsfähige Objekt **Sammlung** von einer zugewiesenen Sicherheitsrolle erteilt wurde.|  
|Berechtigungen|Standardmäßig ist dieser Gruppe die Berechtigung **Read** für den folgenden Ordner auf dem Standortserver gewährt: **%path%\Microsoft Configuration Manager\sinv.box\FileCol**.|  

### <a name="configmgrdviewaccess"></a>ConfigMgr_DViewAccess  
 Diese Gruppe ist eine lokale Sicherheitsgruppe, die von Configuration Manager auf dem Standortdatenbankserver oder dem Datenbankreplikatserver erstellt wird. Sie wird derzeit nicht verwendet, ist aber für die zukünftige Verwendung reserviert.  

### <a name="configmgr-remote-control-users"></a>ConfigMgr Remote Control Users  
 Diese Gruppe wird von Configuration Manager-Remotetools verwendet, um die Konten und Gruppen zu speichern, die Sie in der Liste der zugelassenen Viewer für jeden Client einrichten.  

 In der folgenden Tabelle sind zusätzliche Informationen zu dieser Gruppe aufgelistet:  

|Detail|Weitere Informationen|  
|------------|----------------------|  
|Typ und Speicherort|Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf dem Configuration Manager-Client erstellt wird, wenn der Client eine Clientrichtlinie erhält, durch die Remotetools aktiviert werden.<br /><br /> Wenn Sie Remotetools für einen Client deaktivieren, wird diese Gruppe nicht automatisch entfernt. Sie muss von jedem Clientcomputer manuell gelöscht werden.|  
|Membership|Diese Gruppe enthält standardmäßig keine Mitglieder. Wenn Sie der Liste Zugelassene Betrachter Benutzer hinzufügen, werden die Benutzer auch dieser Gruppe automatisch hinzugefügt.<br /><br /> Sie können mit der ‎Liste „Zugelassene Betrachter“ die Mitgliedschaft dieser Gruppe verwalten, anstatt Benutzer oder Gruppen dieser Gruppe direkt hinzuzufügen.<br /><br /> Administratoren müssen der Liste der zugelassenen Betrachter hinzugefügt werden, und sie benötigen die Berechtigung **Remotesteuerung** für das Objekt **Sammlung**. Sie können diese Berechtigung mithilfe der Sicherheitsrolle Remotetoolsverantwortlicher zuweisen.|  
|Berechtigungen|Standardmäßig sind dieser Gruppe keinerlei Berechtigungen für Speicherorte auf dem Computer erteilt. Sie wird ausschließlich zum Speichern der Liste der zugelassenen Betrachter verwendet.|  

### <a name="sms-admins"></a>SMS-Administratoren  
 Configuration Manager verwendet diese Gruppe, um dem SMS-Anbieter den Zugriff über WMI (Windows Management Instrumentation) zu gewähren. Dieser Zugriff auf den SMS-Anbieter ist erforderlich, um Objekte in der Configuration Manager-Konsole anzuzeigen und zu ändern.  

> [!NOTE]  
>  Durch die rollenbasierte Administrationskonfiguration eines Administrators wird bestimmt, welche Objekte der Administrator mithilfe der Configuration Manager-Konsole anzeigen und verwalten kann.  

 In der folgenden Tabelle sind zusätzliche Informationen zu dieser Gruppe aufgelistet:  

|Detail|Weitere Informationen|  
|------------|----------------------|  
|Typ und Speicherort|Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf jedem Computer mit SMS-Anbieter erstellt wird.<br /><br /> Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Sie muss manuell gelöscht werden.|  
|Membership|Die Gruppenmitgliedschaft wird von Configuration Manager automatisch verwaltet. Standardmäßig sind alle Administratoren einer Hierarchie sowie das Computerkonto des Standortservers Mitglieder der Gruppe SMS-Administratoren auf allen SMS-Anbietercomputern an einem Standort.|  
|Berechtigungen|Rechte und Berechtigungen von SMS Admins werden im WMI-Steuerungs-MMC-Snap-In festgelegt. Der Gruppe „SMS-Administratoren“ werden standardmäßig die Berechtigungen **Enable Account** und **Remote Enable** im Namespace „Root\SMS“ erteilt. Der Gruppe „Authentifizierte Benutzer“ sind die Berechtigungen **Methoden ausführen**, **Anbieterschreibzugriff** und **Konto aktivieren** erteilt.<br /><br /> Wenn ein Administrator eine Configuration Manager-Remotekonsole verwendet, benötigt er DCOM-Berechtigungen für eine Remoteaktivierung auf dem Standortservercomputer und dem SMS-Anbietercomputer. Eine bewährte Methode zur Vereinfachung der Verwaltung besteht darin, diese Berechtigungen nicht einzelnen Benutzern oder Gruppen, sondern der Gruppe SMS-Administratoren zu erteilen. Weitere Informationen finden Sie im Abschnitt [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) des Themas [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) .|  

### <a name="smssitesystemtositeserverconnectionmpltsitecode"></a>SMS_SiteSystemToSiteServerConnection_MP_&lt;Standortcode\>  
 Diese Gruppe wird von Configuration Manager-Verwaltungspunkten, die sich außerhalb des Standortservers befinden, zum Herstellen einer Verbindung mit der Standortdatenbank verwendet. Mithilfe dieser Gruppe wird den Verwaltungspunkten ein Zugriff auf den Ordner Eingangsbox des Standortservers sowie der Standortdatenbank ermöglicht.  

 In der folgenden Tabelle sind zusätzliche Informationen zu dieser Gruppe aufgelistet:  

|Detail|Weitere Informationen|  
|------------|----------------------|  
|Typ und Speicherort|Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf jedem Computer mit SMS-Anbieter erstellt wird.<br /><br /> Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Sie muss manuell gelöscht werden.|  
|Membership|Die Gruppenmitgliedschaft wird von Configuration Manager automatisch verwaltet. Standardmäßig sind die Computerkonten von Remotecomputern mit einem Verwaltungspunkt für den Standort in die Mitgliedschaft eingeschlossen.|  
|Berechtigungen|Diese Gruppe verfügt standardmäßig im Ordner **%path%\Microsoft Configuration Manager\inboxes** des Standortservers über die Berechtigungen **Lesen**, **Lesen & Ausführen** und **Ordnerinhalt auflisten**. Dieser Gruppe wurde die zusätzliche Berechtigung **Schreiben** für **inboxes**-Unterordner, in die vom Verwaltungspunkt Clientdaten geschrieben werden, erteilt.|  

### <a name="smssitesystemtositeserverconnectionsmsprovltsitecode"></a>SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;Standortcode\>  
 Diese Gruppe wird von Configuration Manager-SMS-Anbietercomputern, die sich außerhalb des Standortservers befinden, zum Herstellen einer Verbindung mit dem Standortserver verwendet.  

 In der folgenden Tabelle sind zusätzliche Informationen zu dieser Gruppe aufgelistet:  

|Detail|Weitere Informationen|  
|------------|----------------------|  
|Typ und Speicherort|Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf dem Standortserver erstellt wurde.<br /><br /> Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Sie muss manuell gelöscht werden.|  
|Membership|Die Gruppenmitgliedschaft wird von Configuration Manager automatisch verwaltet. Standardmäßig ist das Computerkonto oder das Domänenbenutzerkonto, das von Remotecomputern mit installiertem SMS-Anbieter für den Standort zum Herstellen einer Verbindung mit dem Standortserver verwendet wird, in die Mitgliedschaft eingeschlossen.|  
|Berechtigungen|Diese Gruppe verfügt standardmäßig im Ordner **%path%\Microsoft Configuration Manager\inboxes** des Standortservers über die Berechtigungen **Lesen**, **Lesen & Ausführen** und **Ordnerinhalt auflisten**. Dieser Gruppe wurde die zusätzliche Berechtigung **Schreiben** oder die Berechtigungen **Schreiben** und **Ändern** für **inboxes**-Unterordner erteilt, auf die für den SMS-Anbieter Zugriff erforderlich ist.<br /><br /> Diese Gruppe verfügt auch in den Ordnern unterhalb von **%path%\Microsoft Configuration Manager\OSD\boot** über die Berechtigungen **Lesen**, **Lesen & Ausführen**, **Ordnerinhalt auflisten**, **Schreiben** und **Ändern**, sowie für die Ordner unterhalb von **%path%\Microsoft Configuration Manager\OSD\Bin** über die Berechtigung **Lesen**.|  

### <a name="smssitesystemtositeserverconnectionstatltsitecode"></a>SMS_SiteSystemToSiteServerConnection_Stat_&lt;Standortcode\>  
 Diese Gruppe wird vom Datei-Verteilungs-Manager auf Configuration Manager-Remote-Standortsystemcomputern zum Herstellen einer Verbindung mit dem Standortserver verwendet.  

 In der folgenden Tabelle sind zusätzliche Informationen zu dieser Gruppe aufgelistet:  

|Detail|Weitere Informationen|  
|------------|----------------------|  
|Typ und Speicherort|Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf dem Standortserver erstellt wurde.<br /><br /> Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Sie muss manuell gelöscht werden.|  
|Membership|Die Gruppenmitgliedschaft wird von Configuration Manager automatisch verwaltet. Standardmäßig ist das Computerkonto oder das Domänenbenutzerkonto, das von Remote-Standortsystemcomputern mit dem Datei-Verteilungs-Manager zum Herstellen einer Verbindung mit dem Standortserver verwendet wird, in die Mitgliedschaft eingeschlossen.|  
|Berechtigungen|Diese Gruppe verfügt standardmäßig im Ordner **%path%\Microsoft Configuration Manager\inboxes** des Standortservers und Ordnern unterhalb davon über die Berechtigungen **Lesen**, **Lesen & Ausführen** und **Ordnerinhalt auflisten**. Dieser Gruppe wurden die zusätzlichen Berechtigungen **Schreiben** und **Ändern** für den Ordner **%path%\Microsoft Configuration Manager\inboxes\statmgr.box** auf dem Standortserver erteilt.|  

### <a name="smssitetositeconnectionltsitecode"></a>SMS_SiteToSiteConnection_&lt;Standortcode\>  
 Diese Gruppe wird von Configuration Manager verwendet, um die dateibasierte Replikation zwischen Standorten innerhalb einer Hierarchie zu aktivieren. Für jeden Remotestandort, von dem Dateien direkt an diesen Standort übertragen werden, verfügt diese Gruppe über Konten, die als **Dateireplikationskonto** eingerichtet sind.  

 In der folgenden Tabelle sind zusätzliche Informationen zu dieser Gruppe aufgelistet:  

|Detail|Weitere Informationen|  
|------------|----------------------|  
|Typ und Speicherort|Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf dem Standortserver erstellt wurde.|  
|Membership|Wenn Sie einen neuen Standort als untergeordneten Standort eines anderen Standorts installieren, wird das Computerkonto des neuen Standorts von Configuration Manager automatisch der Gruppe auf dem übergeordneten Standortserver hinzugefügt. Außerdem fügt Configuration Manager das Computerkonto des übergeordneten Standorts der Gruppe auf dem neuen Standortserver hinzu. Wenn Sie ein anderes Konto für dateibasierte Übertragungen angeben, fügen Sie dieses Konto der Gruppe auf dem Zielstandortserver hinzu.<br /><br /> Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Sie muss manuell gelöscht werden.|  
|Berechtigungen|Standardmäßig ist dieser Gruppe die Berechtigung **Vollzugriff** für den Ordner **%path%\Microsoft Configuration Manager\inboxes\despoolr.box\receive** erteilt.|  

## <a name="accounts-that-configuration-manager-uses"></a>Konten, die von Configuration Manager verwendet werden  
 Sie können die folgenden Konten für Configuration Manager einrichten.  

### <a name="active-directory-group-discovery-account"></a>Konto für die Active Directory-Sicherheitsgruppenermittlung  
 Das **Konto für die Active Directory-Sicherheitsgruppenermittlung** wird zur Ermittlung der lokalen, globalen und universellen Sicherheitsgruppen, der Mitgliedschaft in diesen Gruppen und der Mitgliedschaft in Verteilergruppen an den Orten, die in den Active Directory-Domänendiensten angegebenen sind, verwendet. Verteilergruppen werden nicht als Gruppenressourcen ermittelt.  

 Bei diesem Konto kann es sich um das Computerkonto des Standortservers, von dem die Ermittlung ausgeführt wird, oder um ein Windows-Benutzerkonto handeln. Sie benötigen die Zugriffsberechtigung **Lesen** für die Active Directory-Speicherorte, die für die Ermittlung angegeben sind.  

### <a name="active-directory-system-discovery-account"></a>Konto für die Active Directory-Systemermittlung  
 Das **Konto für die Active Directory-Systemermittlung** wird verwendet, um Computer ausgehend von den Orten, die in den Active Directory-Domänendiensten angegeben sind, zu ermitteln.  

 Bei diesem Konto kann es sich um das Computerkonto des Standortservers, von dem die Ermittlung ausgeführt wird, oder um ein Windows-Benutzerkonto handeln. Sie benötigen die Zugriffsberechtigung **Lesen** für die Active Directory-Speicherorte, die für die Ermittlung angegeben sind.  

### <a name="active-directory-user-discovery-account"></a>Konto für die Active Directory-Benutzerermittlung  
 Das **Konto für die Active Directory-Benutzerermittlung** wird verwendet, um Benutzerkonten ausgehend von den Orten, die in den Active Directory-Domänendiensten angegeben sind, zu ermitteln.  

 Bei diesem Konto kann es sich um das Computerkonto des Standortservers, von dem die Ermittlung ausgeführt wird, oder um ein Windows-Benutzerkonto handeln. Sie benötigen die Zugriffsberechtigung **Lesen** für die Active Directory-Speicherorte, die für die Ermittlung angegeben sind.  

### <a name="active-directory-forest-account"></a>Konto für die Active Directory-Gesamtstruktur  
 Das **Konto für die Active Directory-Gesamtstruktur** wird verwendet, um die Netzwerkinfrastruktur von Active Directory-Gesamtstrukturen zu ermitteln. Es wird auch von zentralen Verwaltungsstandorten und primären Standorten verwendet, um Standortdaten für Active Directory-Domänendienste für eine Gesamtstruktur zu veröffentlichen.  

> [!NOTE]  
>  Die Veröffentlichung in Active Directory durch sekundäre Standorte erfolgt immer über das Computerkonto des sekundären Standortservers.  

> [!NOTE]  
>  Beim Konto für die Active Directory-Gesamtstruktur muss es sich um ein globales Konto handeln, damit Ermittlung und Veröffentlichen in nicht vertrauenswürdigen Gesamtstrukturen möglich sind. Wenn Sie nicht das Computerkonto des Standortservers verwenden, können Sie nur ein globales Konto auswählen.  

 Für dieses Konto ist die Berechtigung **Lesen** für jede Active Directory-Gesamtstruktur, in der die Netzwerkinfrastruktur ermittelt werden soll, erforderlich.  

 Außerdem ist die Berechtigung **Vollzugriff** auf den System Management-Container und all seine untergeordneten Objekte in jeder Active Directory-Gesamtstruktur, in der Standortdaten veröffentlicht werden sollen, erforderlich.  

### <a name="asset-intelligence-synchronization-point-proxy-server-account"></a>Proxyserverkonto für Asset Intelligence-Synchronisierungspunkt  
 Das **Proxyserverkonto für Asset Intelligence-Synchronisierungspunkt** wird vom Asset Intelligence-Synchronisierungspunkt für den Zugriff auf das Internet verwendet. Der Zugriff erfolgt dabei über einen Proxyserver oder eine Firewall, für den bzw. die ein authentifizierter Zugriff erforderlich ist.  

> [!IMPORTANT]  
>  Geben Sie ein Konto mit den geringstmöglichen Berechtigungen für den erforderlichen Proxyserver bzw. für die erforderliche Firewall an.  

### <a name="certificate-registration-point-account"></a>Konto des Zertifikatregistrierungspunkts  
 Über das **Konto des Zertifikatregistrierungspunkts** wird eine Verbindung zwischen dem Zertifizierungsregistrierungspunkt und der Configuration Manager-Datenbank hergestellt. Zwar wird standardmäßig das Computerkonto des Zertifikatregistrierungspunktservers verwendet, aber Sie können stattdessen auch ein Benutzerkonto einrichten. Sie müssen stets ein Benutzerkonto angeben, wenn der Zertifikatregistrierungspunkt sich in einer nicht vertrauenswürdigen Domäne des Standortservers befindet. Für dieses Konto ist nur der **Lesezugriff** auf die Standortdatenbank erforderlich, da Schreibvorgänge vom Zustandsmeldungssystem abgewickelt werden.  

### <a name="capture-operating-system-image-account"></a>Konto für die Erfassung des Betriebssystemabbilds  
 Mit dem **Konto für die Erfassung des Betriebssystemimages** wird von Configuration Manager auf den Ordner zugegriffen, in dem erfasste Images bei der Betriebssystembereitstellung gespeichert werden. Dieses Konto ist erforderlich, wenn Sie den Schritt **Betriebssystemabbild erfassen** zu einer Tasksequenz hinzufügen.  

 Das Konto muss die Berechtigungen **Lesen** und **Schreiben** für die Netzwerkfreigabe aufweisen, in der das erfasste Abbild gespeichert wird.  

 Falls das Kennwort des Kontos in Windows geändert wird, müssen Sie anhand des neuen Kennworts ein Update der Tasksequenz ausführen. Der Configuration Manager-Client erhält das neue Kennwort beim nächsten Download der Clientrichtlinie.  

 Wenn Sie dieses Konto verwenden, können Sie ein Domänenbenutzerkonto mit minimalen Berechtigungen für den Zugriff auf die erforderlichen Netzwerkressourcen erstellen und für alle Tasksequenzkonten verwenden.  

> [!IMPORTANT]  
>  Weisen Sie diesem Konto keine Rechte zur interaktiven Anmeldung zu.  
>   
>  Verwenden Sie für dieses Konto nicht das Netzwerkzugriffskonto.  

### <a name="client-push-installation-account"></a>Clientpushinstallations-Konto  
 Über das **Clientpushinstallationskonto** wird eine Verbindung mit Computern hergestellt und die Configuration Manager-Clientsoftware installiert, wenn Sie Clients mithilfe der Clientpushinstallation bereitstellen. Ist dieses Konto nicht angegeben, wird das Standortserverkonto zum Installieren der Clientsoftware verwendet.  

 Dieses Konto muss ein Mitglied der lokalen Gruppe **Administratoren** auf den Computern sein, auf denen die Configuration Manager-Clientsoftware installiert werden soll. Für dieses Konto sind keine **Domänenadministratorrechte** erforderlich.  

 Sie können mehrere Clientpushinstallationskonten festlegen, die von Configuration Manager nacheinander ausprobiert werden, bis eines erfolgreich ist.  

> [!TIP]  
>  Damit Kontoupdates in umfangreichen Active Directory-Bereitstellungen effektiver koordiniert werden können, erstellen Sie ein neues Konto mit einem anderen Namen, und fügen Sie dieses Konto dann der Liste der Clientpushinstallationskonten in Configuration Manager hinzu. Lassen Sie genügend Zeit zur Replikation des neuen Kontos durch Active Directory Domain Services verstreichen, und entfernen Sie das alte Konto aus Configuration Manager und Active Directory Domain Services.  

> [!IMPORTANT]  
>  Erteilen Sie diesem Konto nicht das Recht, sich lokal anzumelden.  

### <a name="enrollment-point-connection-account"></a>Verbindungskonto des Anmeldungspunkts  
 Über das **Verbindungskonto des Anmeldungspunkts** wird dieser mit der Configuration Manager-Standortdatenbank verbunden. Zwar wird standardmäßig das Computerkonto des Anmeldungspunkts verwendet, aber Sie können stattdessen auch ein Benutzerkonto einrichten. Sie müssen stets ein Benutzerkonto angeben, wenn der Anmeldungspunkt sich in einer nicht vertrauenswürdigen Domäne des Standortservers befindet. Für dieses Konto sind **Lese**- und **Schreibzugriff** auf die Standortdatenbank erforderlich.  

### <a name="exchange-server-connection-account"></a>Verbindungskonto für Exchange Server  
 Mithilfe des **Verbindungskontos für Exchange Server** wird eine Verbindung zwischen dem Standortserver und dem angegebenen Exchange Server-Computer hergestellt, über die mit Exchange Server verbundene mobile Geräte gesucht werden. Die gefundenen Geräte können über diese Verbindung auch verwaltet werden. Für dieses Konto sind Exchange PowerShell-Cmdlets erforderlich, mit deren Hilfe dem Exchange Server-Computer die erforderlichen Berechtigungen bereitgestellt werden. Weitere Informationen zu diesen Cmdlets finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="exchange-server-connector-proxy-server-account"></a>Konto für den Exchange Server-Connector-Proxyserver  
 Das **Konto für den Exchange Server-Connector-Proxyserver** wird vom Exchange Server-Connector für den Zugriff auf das Internet verwendet. Der Zugriff erfolgt dabei über einen Proxyserver oder eine Firewall, für den bzw. die ein authentifizierter Zugriff erforderlich ist.  

> [!IMPORTANT]  
>  Geben Sie ein Konto mit den geringstmöglichen Berechtigungen für den erforderlichen Proxyserver bzw. für die erforderliche Firewall an.  

### <a name="management-point-connection-account"></a>Verbindungskonto des Verwaltungspunkts  
 Über das **Verbindungskonto des Verwaltungspunkts** wird der Verwaltungspunkt mit der Configuration Manager-Standortdatenbank verbunden, damit Informationen für Clients gesendet und abgerufen werden können. Zwar wird standardmäßig das Computerkonto des Verwaltungspunkts verwendet, aber Sie können stattdessen auch ein Benutzerkonto einrichten. Sie müssen stets ein Benutzerkonto angeben, wenn der Verwaltungspunkt sich in einer nicht vertrauenswürdigen Domäne des Standortservers befindet.  

 Erstellen Sie das Konto als lokales Konto auf dem Computer, auf dem Microsoft SQL Server ausgeführt wird, und statten Sie es nur mit geringen Rechten aus.  

> [!IMPORTANT]  
>  Erteilen Sie diesem Konto keine Rechte zur interaktiven Anmeldung.  

### <a name="multicast-connection-account"></a>Multicastverbindungskonto  
 Über das **Multicastverbindungskonto** können von den Verteilungspunkten, die für Multicast eingerichtet sind, Informationen aus der Standortdatenbank gelesen werden. Zwar wird standardmäßig das Computerkonto des Verteilungspunkts verwendet, aber Sie können stattdessen auch ein Benutzerkonto einrichten. Sie müssen stets ein Benutzerkonto angeben, wenn die Standortdatenbank sich in einer nicht vertrauenswürdigen Gesamtstruktur befindet. Wenn Ihr Rechenzentrum beispielsweise über ein Umkreisnetzwerk in einer anderen Gesamtstruktur als der des Standortservers und der Standortdatenbank verfügt, können Sie mit diesem Konto die Multicast-Informationen aus der Standortdatenbank lesen.  

 Erstellen Sie dieses Konto ggf. als lokales Konto mit geringen Rechten auf dem Computer, auf dem Microsoft SQL Server ausgeführt wird.  

> [!IMPORTANT]  
>  Erteilen Sie diesem Konto keine Rechte zur interaktiven Anmeldung.  

### <a name="network-access-account"></a>Netzwerkzugriffskonto  
 Clientcomputer verwenden das **Netzwerkzugriffskonto**, wenn über ihr lokales Computerkonto kein Zugriff auf Inhalte auf Verteilungspunkten möglich ist. Beispielsweise gilt dies für Arbeitsgruppenclients und Computer aus nicht vertrauenswürdigen Domänen. Dieses Konto wird möglicherweise auch bei der Betriebssystembereitstellung verwendet, falls der Computer, von dem das Betriebssystem installiert wird, noch kein Computerkonto in der Domäne hat.  

> [!NOTE]  
>  Das Netzwerkzugriffskonto wird nie als Sicherheitskontext zum Ausführen von Programmen, Installieren von Softwareupdates oder Ausführen von Tasksequenzen verwendet. Es wird nur für den Zugriff auf Ressourcen im Netzwerk verwendet.  

 Weisen Sie diesem Konto die minimal erforderlichen Berechtigungen für den Inhalt zu, der vom Client für den Zugriff auf die Software benötigt wird. Das Konto muss über die Berechtigung **Auf diesen Computer vom Netzwerk aus zugreifen** für den Verteilungspunkt oder einen anderen Server verfügen, auf dem der Paketinhalt gespeichert ist. Sie können bis zu 10 Netzwerkzugriffskonten pro Standort konfigurieren.  

> [!WARNING]  
>  Falls beim Versuch, den Inhalt über das Computername$-Konto herunterzuladen, ein Fehler auftritt, wird von Configuration Manager automatisch das Netzwerkzugriffskonto verwendet. Dies geschieht selbst dann, wenn bei früheren Versuchen mit diesem Konto Fehler aufgetreten sind.  

 Erstellen Sie das Konto in einer Domäne, die den erforderlichen Zugriff auf Ressourcen ermöglicht. Das Netzwerkzugriffskonto muss immer einen Domänennamen enthalten. Pass-Through-Sicherheit wird für dieses Konto nicht unterstützt. Wenn es Verteilungspunkte in mehreren Domänen gibt, erstellen Sie das Konto in einer vertrauenswürdigen Domäne.  

> [!TIP]  
>  Zur Vermeidung von Kontosperrungen sollten Sie das Kennwort für ein vorhandenes Netzwerkzugriffskonto nicht ändern. Erstellen Sie stattdessen ein neues Konto, und richten Sie das neue Konto in Configuration Manager ein. Wenn genügend Zeit verstrichen ist, sodass alle Clients die neuen Kontodetails empfangen haben, entfernen Sie das alte Konto aus den freigegebenen Netzwerkordnern, und löschen Sie es.  

> [!IMPORTANT]  
>  Erteilen Sie diesem Konto keine Rechte zur interaktiven Anmeldung.
>   
>  Gewähren Sie diesem Konto nicht das Recht, der Domäne Computer hinzuzufügen. Wenn während einer Tasksequenz Computer der Domäne beitreten müssen, verwenden Sie dafür das Tasksequenz-Editor-Domänenbeitrittskonto.  

### <a name="package-access-account"></a>Paketzugriffskonto  
 Mit einem **Paketzugriffskonto** können Sie durch Festlegen von NTFS-Berechtigungen angeben, welche Benutzer und Benutzergruppen auf einen Paketordner auf Verteilungspunkten zugreifen können. Standardmäßig wird in Configuration Manager Zugriff nur auf die allgemeinen Zugriffskonten **Benutzer** und **Administratoren** gewährt. Sie können den Zugriff für Clientcomputer über zusätzliche Windows-Konten oder -Gruppen steuern. Mobile Geräte rufen Paketinhalte immer anonym ab, daher verwenden sie die Paketzugriffskonten nicht.  

 Standardmäßig erteilt Configuration Manager beim Erstellen der Paketfreigabe auf einem Verteilungspunkt der lokalen Gruppe **Benutzer** die Berechtigung **Lesen** und der Gruppe **Administratoren** die Berechtigung **Vollzugriff**. Die tatsächlich erforderlichen Berechtigungen hängen vom jeweiligen Paket ab. Von Clients in Arbeitsgruppen oder nicht vertrauenswürdigen Gesamtstrukturen wird das Netzwerkzugriffskonto zum Zugriff auf den Paketinhalt verwendet. Stellen Sie anhand der definierten Paketzugriffskonten sicher, dass das Netzwerkzugriffskonto über Berechtigungen für das Paket verfügt.  

 Verwenden Sie Konten in einer Domäne mit Zugriff auf die Verteilungspunkte. Wenn Sie das Konto nach der Paketerstellung erstellen oder ändern, müssen Sie das Paket erneut verteilen. Beim Aktualisieren des Pakets werden die NTFS-Berechtigungen für das Paket nicht geändert.  

 Das Netzwerkzugriffskonto braucht nicht als Paketzugriffskonto hinzugefügt werden, da es Mitglied der Gruppe Benutzer ist und somit standardmäßig hinzugefügt wird. Der Zugriff von Clients auf das Paket kann nicht dadurch verhindert werden, dass das Paketzugriffskonto auf das Netzwerkzugriffskonto beschränkt wird.  

### <a name="reporting-services-point-account"></a>Konto des Reporting Services-Punkts  
 Das **Konto des Reporting Services-Punkts** wird von SQL Server Reporting Services zum Abrufen der Daten für Configuration Manager-Berichte aus der Standortdatenbank verwendet. Das von Ihnen angegebene Windows-Benutzerkonto und das dazugehörende Kennwort werden verschlüsselt und in der SQL Server Reporting Services-Datenbank gespeichert.  

### <a name="remote-tools-permitted-viewer-accounts"></a>Informationen zu Konten für zugelassene Viewer für Remotetools  
 Bei den Konten, die Sie als **Zugelassene Betrachter** für die Remotesteuerung festlegen, handelt es sich um eine Liste der Benutzer, die die Remotetoolsfunktion auf Clients verwenden dürfen.  

### <a name="site-system-installation-account"></a>Standortsystem-Installationskonto  
 Die **Standortsystem-Installationskonten** werden vom Standortserver zur Installation, erneuten Installation, Deinstallation und Einrichtung von Standortsystemen verwendet. Wenn Sie das Standortsystem so einrichten, dass Verbindungen mit diesem Standortsystem vom Standortserver initiiert werden müssen, wird dieses Konto von Configuration Manager auch dazu verwendet, Daten nach der Installation des Standortsystems und der Standortsystemrollen vom Standortsystemcomputer abzurufen. Jedes Standortsystem kann ein anderes Standortsystem-Installationskonto aufweisen. Sie können aber nur ein Standortsystem-Installationskonto für die Verwaltung aller Standortsystemrollen in diesem Standortsystem einrichten.  

 Für dieses Konto sind lokale Administratorberechtigungen auf den Standortsystemen erforderlich, die von Administratoren installiert und eingerichtet werden sollen. Darüber hinaus muss dieses Konto die Berechtigung **Auf diesen Computer vom Netzwerk aus zugreifen** in der Sicherheitsrichtlinie auf den Standortsystemen aufweisen, die von den Administratoren installiert und eingerichtet werden sollen.  

> [!TIP]  
>  Falls Sie mit vielen Domänencontrollern arbeiten und diese Konten domänenübergreifend verwendet werden, vergewissern Sie sich vor der Einrichtung des Standortsystems, dass die Konten repliziert wurden.  
>   
>  Die Festlegung eines lokalen Kontos auf jedem der zu verwaltenden Standortsysteme bietet ein höheres Maß an Sicherheit als der Einsatz von Domänenkonten. Dies liegt daran, dass Angreifer bei einer Gefährdung des Kontos nur in beschränktem Umfang Schaden anrichten können. Allerdings sind Domänenkonten einfacher zu verwalten. Berücksichtigen Sie den Kompromiss zwischen Sicherheit und effektiver Verwaltung.  

### <a name="smtp-server-connection-account"></a>Verbindungskonto für SMTP-Server  
 Über das **Verbindungskonto für SMTP-Server** werden vom Standortserver per E-Mail Warnungen an den SMTP-Server gesendet, wenn für den SMTP-Server ein authentifizierter Zugriff erforderlich ist.  

> [!IMPORTANT]  
>  Geben Sie ein Konto mit den geringstmöglichen Berechtigungen zum Senden von E-Mails an.  

### <a name="software-update-point-connection-account"></a>Verbindungskonto des Softwareupdatepunkts  
 Das **Verbindungskonto des Softwareupdatepunkts** wird vom Standortserver für die beiden folgenden Softwareupdatedienste verwendet:  

-   Der WSUS-Configuration Manager (Windows Server Update Services), der Einstellungen wie Produktdefinitionen, Klassifizierungen und Upstreameinstellungen einrichtet  

-   WSUS-Synchronisierungs-Manager, von dem bei einem WSUS-Upstreamserver oder Microsoft Update eine Synchronisierung angefordert wird  

Mit dem Standortsystem-Installationskonto können zwar Komponenten für Softwareupdates installiert, aber keine softwareupdatespezifischen Funktionen auf dem Softwareupdatepunkt ausgeführt werden. Falls Sie das Computerkonto des Standortservers für diese Funktion nicht verwenden können, weil sich der Softwareupdatepunkt in einer nicht vertrauenswürdigen Gesamtstruktur befindet, müssen Sie dieses Konto zusätzlich zum Standortsystem-Installationskonto angeben.  

Dieses Konto muss ein lokaler Administrator auf dem Computer sein, auf dem WSUS installiert ist. Zudem muss es Teil der lokalen WSUS-Administratorengruppe sein.  

### <a name="software-update-point-proxy-server-account"></a>Proxyserverkonto für Softwareupdatepunkt  
 Das **Proxyserverkonto für Softwareupdatepunkt** wird vom Softwareupdatepunkt für den Zugriff auf das Internet verwendet. Der Zugriff erfolgt dabei über einen Proxyserver oder eine Firewall, für den bzw. die ein authentifizierter Zugriff erforderlich ist.  

> [!IMPORTANT]  
>  Geben Sie ein Konto mit den geringstmöglichen Berechtigungen für den erforderlichen Proxyserver bzw. für die erforderliche Firewall an.  

### <a name="source-site-account"></a>Konto des Quellstandorts  
 Über das **Konto des Quellstandorts** wird vom Migrationsprozess auf den SMS-Anbieter des Quellstandorts zugegriffen. Für dieses Konto ist die Berechtigung **Lesen** für Standortobjekte am Quellstandort erforderlich, damit Daten für Migrationsaufträge gesammelt werden können.  

 Wenn Sie ein Upgrade von Configuration Manager 2007-Verteilungspunkten oder sekundären Standorten mit Verteilungspunkten auf System Center Configuration Manager-Verteilungspunkte planen, muss dieses Konto auch die Berechtigung **Löschen** für die Klasse **Standort** aufweisen, damit der Verteilungspunkt beim Upgrade erfolgreich vom Configuration Manager 2007-Standort entfernt werden kann.  

> [!NOTE]  
>  Sowohl das Konto für Quellstandort als auch das Konto der Datenbank des Quellstandorts werden in der Configuration Manager-Konsole im Knoten **Konten** des Arbeitsbereichs **Verwaltung** als **Migrations-Manager** bezeichnet.  

### <a name="source-site-database-account"></a>Konto der Datenbank des Quellstandorts  
 Über das **Konto der Datenbank des Quellstandorts** greift der Migrationsprozess auf die SQL Server-Datenbank für den Quellstandort zu. Damit von der SQL Server-Datenbank des Quellstandorts Daten gesammelt werden können, muss das Konto der Datenbank des Quellstandorts über die Berechtigungen **Lesen** und **Ausführen** für die SQL Server-Datenbank des Quellstandorts verfügen.  

> [!NOTE]  
>  Falls Sie das System Center Configuration Manager-Computerkonto verwenden, vergewissern Sie sich, dass Folgendes auf dieses Konto zutrifft:  
>   
> -   Es gehört der Sicherheitsgruppe **Distributed COM-Benutzer** in der Domäne an, in der sich der Configuration Manager 2007-Standort befindet.  
> -   Es gehört der Sicherheitsgruppe **SMS-Administratoren** an.  
> -   Es hat **Leseberechtigung** auf alle Configuration Manager 2007-Objekte.  

> [!NOTE]  
>  Sowohl das Konto für Quellstandort als auch das Konto der Datenbank des Quellstandorts werden in der Configuration Manager-Konsole im Knoten **Konten** des Arbeitsbereichs **Verwaltung** als **Migrations-Manager** bezeichnet.  

### <a name="task-sequence-editor-domain-joining-account"></a>Tasksequenz-Editor-Domänenbeitrittskonto  
 Das **Tasksequenz-Editor-Domänenbeitrittskonto** wird in Tasksequenzen für den Beitritt eines neu mit einem Abbild versehenen Computers zu einer Domäne verwendet. Das Konto wird benötigt, wenn Sie einer Tasksequenz den Schritt **Einer Domäne oder Arbeitsgruppe beitreten** hinzufügen und anschließend **Einer Domäne beitreten**auswählen. Sie können dieses Konto auch einrichten, wenn Sie einer Tasksequenz den Schritt **Netzwerkeinstellungen anwenden** hinzufügen, es ist jedoch für diesen Schritt nicht zwingend erforderlich.  

 Das Konto muss über die Berechtigung **Domäne beitreten** für die Domäne verfügen, der der Computer beitritt.  

> [!TIP]  
>  Wenn Sie dieses Konto für Ihre Tasksequenzen benötigen, können Sie ein Domänenbenutzerkonto mit minimalen Berechtigungen für den Zugriff auf die erforderlichen Netzwerkressourcen erstellen und für alle Tasksequenzkonten verwenden.  

> [!IMPORTANT]  
>  Weisen Sie diesem Konto keine Rechte zur interaktiven Anmeldung zu.  
>   
>  Verwenden Sie für dieses Konto nicht das Netzwerkzugriffskonto.  

### <a name="task-sequence-editor-network-folder-connection-account"></a>Netzwerkordner-Verbindungskonto des Tasksequenz-Editors  
 Mit dem **Netzwerkordner-Verbindungskonto des Tasksequenz-Editors** wird in einer Tasksequenz eine Verbindung mit einem freigegebenen Ordner im Netzwerk hergestellt. Dieses Konto ist erforderlich, wenn Sie den Schritt **Verbindung mit Netzwerkordner herstellen** zu einer Tasksequenz hinzufügen.  

 Dieses Konto erfordert Berechtigungen für den Zugriff auf den angegebenen freigegebenen Ordner. Es muss ein Benutzerdomänenkonto sein.  

> [!TIP]  
>  Wenn Sie dieses Konto für Ihre Tasksequenzen benötigen, können Sie ein Domänenbenutzerkonto mit minimalen Berechtigungen für den Zugriff auf die erforderlichen Netzwerkressourcen erstellen und für alle Tasksequenzkonten verwenden.  

> [!IMPORTANT]  
>  Weisen Sie diesem Konto keine Rechte zur interaktiven Anmeldung zu.  
>   
>  Verwenden Sie für dieses Konto nicht das Netzwerkzugriffskonto.  

### <a name="task-sequence-run-as-account"></a>Tasksequenzkonto „Ausführen als“  
 Das **Tasksequenzkonto „Ausführen als“** wird zum Ausführen von Befehlszeilen in Tasksequenzen verwendet, deren Anmeldeinformationen von denen des lokalen Systemkontos abweichen. Dieses Konto ist erforderlich, wenn Sie einer Tasksequenz den Schritt **Befehlszeile ausführen** hinzufügen, die Tasksequenz aber nicht mit den Kontoberechtigungen für das lokale System auf dem verwalteten Computer ausgeführt werden soll.  

 Das Konto muss mit den Mindestberechtigungen zum Ausführen der in der Tasksequenz angegebenen Befehlszeile eingerichtet sein. Für das Konto sind interaktive Anmelderechte erforderlich sowie in der Regel die Möglichkeit, Software zu installieren und auf Netzwerkressourcen zuzugreifen.  

> [!IMPORTANT]  
>  Verwenden Sie für dieses Konto nicht das Netzwerkzugriffskonto.  
>   
>  Versehen Sie das Konto niemals mit Domänenadministratorrechten.  
>   
>  Richten Sie niemals servergespeicherte Profile für dieses Konto ein. Wenn die Tasksequenz ausgeführt wird, wird das servergespeicherte Profil für das Konto heruntergeladen. Dadurch wird das Profil für den Zugriff auf dem lokalen Computer anfällig.  
>   
>  Beschränken Sie den Kontoumfang. Erstellen Sie beispielsweise für jede Tasksequenz ein unterschiedliches Tasksequenzkonto für „Ausführen als“, sodass bei Gefährdung eines Kontos nur der Clientcomputer betroffen ist, auf den dieses Konto Zugriff hat.  
>   
>  Wenn für die Befehlszeile Administratorrechte auf dem Computer erforderlich sind, erwägen Sie die Erstellung eines lokalen Administratorkontos lediglich für das Tasksequenzkonto „Ausführen als“ auf allen Computern, um die Tasksequenz auszuführen. Wenn das Konto nicht mehr benötigt wird, kann es gelöscht werden.  
