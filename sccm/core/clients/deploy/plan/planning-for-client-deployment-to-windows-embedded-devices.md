---
title: "Planung der Clientbereitstellung auf Windows Embedded-Geräten | Microsoft-Dokumentation"
description: "Planen Sie die Clientbereitstellung für Windows Embedded-Geräte in System Center Configuration Manager"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f7ef476a2ebcf0161ebb70d8a3d95f77806aa05e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-system-center-configuration-manager"></a>Planen der Clientbereitstellung für Windows Embedded-Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

<a name="BKMK_DeployClientEmbedded"></a> Wenn der Configuration Manager-Client auf einem Windows Embedded-Gerät nicht vorhanden ist und die erforderlichen Abhängigkeiten von diesem Gerät erfüllt werden, können Sie jede der Clientinstallationsmethoden verwenden. Wenn vom eingebetteten Gerät Schreibfilter unterstützt werden, müssen Sie diese Filter vor der Clientinstallation deaktivieren. Nachdem der Client installiert und einem Standort zugewiesen wurde, können Sie die Schreibfilter erneut aktivieren.  

 Beachten Sie, dass Sie beim Deaktivieren der Filter nicht die Filtertreiber deaktivieren sollten. Diese Treiber werden in der Regel automatisch gestartet, wenn der Computer gestartet wird. Das Deaktivieren der Treiber verhindert die Installation des Clients oder es kommt bei der Schreibfilterorchestrierung zu Konflikten, wodurch bei Clientvorgängen Fehler auftreten. Dies sind die Dienste, die den einzelnen Schreibfiltertypen zugeordnet sind, die weiterhin ausgeführt werden müssen:  

|Schreibfiltertyp|Treiber|Typ|Beschreibung|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|Kernel|Implementiert die E/A-Umleitung auf Sektorebene auf geschützten Volumes.|  
|FBWF|FBWF|Dateisystem|Implementiert die E/A-Umleitung auf Dateiebene auf geschützten Volumes.|  
|UWF|uwfreg|Kernel|UWF-Registrierungsredirector|  
|UWF|uwfs|Dateisystem|UWF-Dateiredirector|  
|UWF|uwfvol|Kernel|UWF-Volume-Manager|  

 Mit Schreibfiltern wird gesteuert, wie das Betriebssystem auf dem eingebetteten Gerät aktualisiert wird, wenn Sie Änderungen vornehmen, beispielsweise bei der Installation von Software. Wenn Schreibfilter aktiviert sind, werden die Änderungen nicht direkt am Betriebssystem vorgenommen, sondern in ein temporäres Overlay umgeleitet. Wenn die Änderungen nur in das Overlay geschrieben werden, gehen sie beim Ausschalten des eingebetteten Geräts verloren. Sind die Schreibfilter vorübergehend deaktiviert, können die Änderungen jedoch permanent gemacht werden, damit Sie sie nicht bei jedem Neustart des eingebetteten Geräts erneut ausführen (bzw. Software neu installieren) müssen. Allerdings ist bei der temporären Deaktivierung und erneuten Aktivierung der Schreibfilter mindestens ein Neustart erforderlich. Durch Konfigurieren von Wartungsfenstern können Sie sicherstellen, dass diese Neustarts außerhalb der Geschäftszeiten stattfinden.  

 Sie können Optionen so konfigurieren, dass die Schreibfilter beim Bereitstellen von Software (z. B. Anwendungen, Tasksequenzen, Softwareupdates und Endpoint Protection-Client) automatisch deaktiviert und erneut aktiviert werden. Die Ausnahme bilden Konfigurationsbasislinien mit Konfigurationselementen, von denen die automatische Wiederherstellung verwendet wird. In diesem Fall findet die Wiederherstellung immer im Overlay statt, d. h., sie ist nur bis zum Neustart des Geräts verfügbar. Die Wiederherstellung wird beim nächsten Auswertungszyklus erneut angewendet, aber nur auf das Overlay, das beim Neustart gelöscht wird. Durch Bereitstellen der Konfigurationsbaseline und einer weiteren Softwarebereitstellung, von der die möglichst baldige Ausführung der Änderung unterstützt wird, können Sie die Ausführung der Wiederherstellungsänderungen durch Configuration Manager erzwingen.  

 Sind die Schreibfilter deaktiviert, können Sie auf Windows Embedded-Geräten mithilfe des Softwarecenters Software installieren. Wenn die Schreibfilter jedoch aktiviert sind, ist die Installation nicht möglich. In Configuration Manager wird daraufhin eine Fehlermeldung angezeigt, aus der hervorgeht, dass Sie über unzureichende Berechtigungen für die Installation der Anwendung verfügen.  

> [!WARNING]  
>  Selbst wenn Sie die Configuration Manager-Optionen zum Committen der Änderungen nicht auswählen, werden die Änderungen möglicherweise dennoch committet, beispielsweise bei einer anderen Softwareinstallation oder Änderung, bei der Änderungen committet werden. In diesem Fall werden die ursprünglichen Änderungen zusätzlich zu den neuen Änderungen ausgeführt.  

 Wenn die Schreibfilter von Configuration Manager deaktiviert werden, um Änderungen permanent zu machen, ist es nur Benutzern mit lokalen Administratorrechten möglich, sich beim eingebetteten Gerät anzumelden und dieses Gerät zu verwenden. Während dieses Zeitraums werden Benutzer mit geringen Rechten gesperrt. Ferner wird die Meldung angezeigt, dass der Computer nicht verfügbar ist, weil er gewartet wird. Hierdurch wird das Gerät geschützt, solange es sich in einem Zustand befindet, in dem Änderungen permanent angewendet werden können. Dieses Sperrverhalten im Wartungsmodus ist ein weiterer Grund dafür, ein Wartungsfenster für einen Zeitraum zu konfigurieren, in dem Benutzer sich nicht bei diesen Geräten anmelden.  

 Die Verwaltung der folgenden Schreibfilter wird von Configuration Manager unterstützt:  

-   Dateibasierter Schreibfilter (File-Based Write Filter, FBWF) – Weitere Informationen finden Sie unter [File-Based Write Filter (Dateibasierter Schreibfilter)](http://go.microsoft.com/fwlink/?LinkID=204717).  

-   Erweiterter Schreibfilter RAM (Enhanced Write Filter, EWF) – Weitere Informationen finden Sie unter [Enhanced Write Filter (Erweiterter Schreibfilter)](http://go.microsoft.com/fwlink/?LinkId=204718).  

-   Vereinheitlichter Schreibfilter (Unified Write Filter, UWF) – Weitere Informationen finden Sie unter [Vereinheitlichter Schreibfilter (Unified Write Filter, UWF)](http://go.microsoft.com/fwlink/?LinkId=309236).  

 Schreibfiltervorgänge werden von Configuration Manager nicht unterstützt, wenn das Windows Embedded-Gerät sich im Modus „Erweiterter Schreibfilter – Registrierungsoverlay“ befindet.  

> [!IMPORTANT]  
>  Falls Sie die Wahl haben, verwenden Sie dateibasierte Schreibfilter (File-Based Write Filters, FBWF) mit Configuration Manager, um Effizienz und Skalierbarkeit zu steigern.
>
> **Bei Geräten, die nur FBWF verwenden:** Legen Sie die folgenden Ausnahmen fest, um den Clientzustand und die Inventurdaten zwischen Geräteneustarts beizubehalten:  
>   
>  -   CCMINSTALLDIR\\*.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
>  Geräte, die Windows Embedded 8.0 und höher ausführen, unterstützen keine Ausschlüsse, die Platzhalterzeichen enthalten. Auf diesen Geräten müssen Sie die folgenden Ausschlüsse einzeln konfigurieren:  
>   
>  -   Alle Dateien in CMINSTALLDIR mit der Erweiterung „.sdf“. Dies sind in der Regel:  
>   
>     -   UserAffinityStore.sdf  
>     -   InventoryStore.sdf  
>     -   CcmStore.sdf  
>     -   StateMessageStore.sdf  
>     -   CertEnrollmentStore.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
> **Bei Geräten, die nur FBWF und UWF verwenden:** Wenn Clients in einer Arbeitsgruppe Zertifikate zur Authentifizierung bei Verwaltungspunkten verwenden, müssen Sie auch den privaten Schlüssel ausschließen, um sicherzustellen, dass der Client weiterhin mit dem Verwaltungspunkt kommuniziert. Konfigurieren Sie auf diesen Geräten die folgenden Ausnahmen:  
>   
>  -   c:\Windows\System32\Microsoft\Protect  
> -   c:\ProgramData\Microsoft\Crypto  
> -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

 Ein Beispielszenario für die Bereitstellung und Verwaltung von Windows Embedded-Geräten mit aktiviertem Schreibfilter finden Sie unter [Beispielszenario für die Bereitstellung und Verwaltung von System Center Configuration Manager-Clients auf Windows Embedded-Geräten](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md).  

 Weitere Informationen zum Erstellen von Abbildern für Windows Embedded-Geräte und zum Konfigurieren von Schreibfiltern enthält die Windows Embedded-Dokumentation. Auskünfte hierzu erteilt auch der zuständige OEM.  

> [!NOTE]  
>  Wenn Sie die entsprechenden Plattformen für Softwarebereitstellungen und Konfigurationselemente auswählen, werden hierfür keine bestimmten Versionen, sondern die Windows Embedded-Familien angezeigt. Anhand der folgenden Liste können Sie den Optionen im Listenfeld eine bestimmte Windows Embedded-Version zuordnen:  
>   
>  -   **Eingebettete Betriebssysteme auf Basis von Windows XP (32-Bit)** umfasst Folgendes:  
>   
>      -   Windows XP Embedded  
>     -   Windows Embedded for Point of Service  
>     -   Windows Embedded Standard 2009  
>     -   Windows Embedded POSReady 2009  
> -   **Eingebettete Betriebssysteme auf Basis von Windows 7 (32-Bit)** umfasst Folgendes:  
>   
>      -   Windows Embedded Standard 7 (32-Bit)  
>     -   Windows Embedded POSReady 7 (32-Bit)  
>     -   Windows ThinPC  
> -   **Eingebettete Betriebssysteme auf Basis von Windows 7 (64-Bit)** umfasst Folgendes:  
>   
>      -   Windows Embedded Standard 7 (64-Bit)  
>     -   Windows Embedded POSReady 7 (64-Bit)
