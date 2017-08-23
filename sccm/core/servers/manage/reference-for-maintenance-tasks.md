---
title: "Referenz für Wartungstasks | Microsoft-Dokumentation"
description: "Hier finden Sie ausführliche Informationen zu den einzelnen Wartungstasks für System Center Configuration Manager-Standorte sowie dazu, ob diese Tasks standardmäßig aktiviert sind."
ms.custom: na
ms.date: 3/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
caps.latest.revision: "16"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a2d4420c2274a9b1ceb47ffd267849fdb5a55a61
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="reference-for-maintenance-tasks-for-system-center-configuration-manager"></a>Referenz für Wartungstasks für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält eine Liste der Details zu jedem Wartungstask für System Center Configuration Manager-Standorte und gibt die Standorttypen an, für die der Task verfügbar ist. Jeder Eintrag gibt auch an, ob der Task aktiviert ist oder nicht. Informationen zum Planen und Konfigurieren von Standorten zur Ausführung von Wartungstasks finden Sie unter [Wartungstasks für System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md).  

**Standortserver sichern**: Verwenden Sie diesen Task, um die Wiederherstellung wichtiger Daten vorzubereiten. Sie können eine Sicherung Ihrer wichtigen Informationen erstellen, um einen Standort und die Configuration Manager-Datenbank wiederherzustellen. Weitere Informationen finden Sie unter [Sicherung und Wiederherstellung für System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Nicht aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Anwendungstitel mit Inventurinformationen prüfen**: Verwenden Sie diesen Task, um die Konsistenz zwischen Softwaretiteln in der Softwareinventur und Softwaretiteln im Asset Intelligence-Katalog zu gewährleisten. Weitere Informationen finden Sie unter [Einführung in Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Installationsflag löschen**: Verwenden Sie diesen Task, um das Installationsflag für Clients zu entfernen, die während des **Clientneuermittlungs-Zeitraums** keinen von der Frequenzermittlung erstellten Datensatz übermitteln. Durch das Installationsflag wird die automatische Clientpushinstallation auf einen Computer verhindert, auf dem ein aktiver Configuration Manager-Client vorhanden ist.  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Nicht aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Anwendungsanforderungsdaten löschen**: Verwenden Sie diesen Task, um veraltete Anwendungsanforderungen aus der Datenbank zu löschen. Weitere Informationen über Anwendungsanforderungen finden Sie unter [Create and deploy an application with System Center Configuration Manager (Erstellen und Bereitstellen einer Anwendung mit System Center Configuration Manager)](/sccm/apps/get-started/create-and-deploy-an-application).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veralteten Client-Downloadverlauf löschen**: Verwenden Sie diesen Task, um Verlaufsdaten über die von Clients verwendete Downloadquelle zu löschen. Das Herunterladen von Quellinformationen wird zum Auffüllen des [Dashboards „Clientdatenquellen“](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) verwendet.  
-  Standortserver der zentralen Verwaltung: Nicht verfügbar
-    **Primärer Standort** – Aktiviert
-  Sekundärer Standort: Nicht verfügbar

**Veraltete Clientvorgänge löschen**: Verwenden Sie diesen Task, um alle veralteten Daten für Clientvorgänge aus der Standortdatenbank zu löschen. Dies umfasst beispielsweise Daten für veraltete oder abgelaufene Clientbenachrichtigungen (z.B. Downloadanforderungen für Computer- oder Benutzerrichtlinien) und für Endpoint Protection (z.B. Anforderungen eines administrativen Benutzers, dass auf den Clients eine Überprüfung ausgeführt werden soll oder aktualisierte Definitionen heruntergeladen werden sollen).

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veralteten Anwesenheitsverlauf für Clients löschen**: Verwenden Sie diesen Task zum Löschen von Verlaufsdaten über den (von der Clientbenachrichtigung erfassten) Onlinestatus von Clients, wenn sie seit dem angegebenen Zeitpunkt nicht aktualisiert wurden. Weitere Informationen zur Clientbenachrichtigung finden Sie unter [How to monitor clients in System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md) (So überwachen Sie Clients in System Center Configuration Manager).  

-   **Standort der zentralen Verwaltung**: Aktiviert   
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Daten zum Cloudverwaltungsgateway-Datenverkehr löschen**: Verwenden Sie diesen Task, um alle veraltete Daten über den Datenverkehr zu löschen, die die [Cloudverwaltungsgateway](/sccm/core/clients/manage/plan-cloud-management-gateway) aus der Standortdatenbank durchlaufen. Dies enthält z.B. Daten zur Anzahl von Anforderungen, gesamten Anforderungsbytes, gesamten Antwortbytes, die Anzahl von fehlerhaften Anforderungen und die maximale Anzahl gleichzeitiger Anforderungen.  
- **Standort der zentralen Verwaltung** – Aktiviert
- **Primärer Standort** – Aktiviert
- Sekundärer Standort: Nicht verfügbar


**Veraltete gesammelte Dateien löschen**: Verwenden Sie diesen Task, um veraltete Informationen zu gesammelten Dateien aus der Datenbank zu löschen. Mit diesem Task werden darüber hinaus die gesammelten Dateien aus der Ordnerstruktur des Standortservers auf dem ausgewählten Standort gelöscht. Standardmäßig werden die fünf neuesten Kopien der gesammelten Dateien auf dem Standortserver im Verzeichnis **Inboxes\sinv.box\FileCol** gespeichert. Weitere Informationen finden Sie unter [Introduction to software inventory in System Center Configuration Manager (Einführung in die Softwareinventur in System Center Configuration Manager)](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Computerzuordnungsdaten löschen**: Verwenden Sie diesen Task, um veraltete Computerzuordnungsdaten für die Bereitstellung von Betriebssystemen aus der Datenbank zu löschen. Diese Informationen werden beim Wiederherstellen des Benutzerzustands verwendet. Weitere Informationen zu Computerzuordnungen finden Sie unter [Verwalten des Benutzerzustands in System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Erkennungsdaten von Löschvorgängen löschen**: Verwenden Sie diesen Task, um veraltete Daten aus der Datenbank zu löschen, die mithilfe von Extraktionsansichten erstellt wurden. Standardmäßig sind Extraktionsansichten deaktiviert. Sie werden nur über das Configuration Manager SDK aktiviert. Wenn Extraktionsansichten deaktiviert sind, sind für diesen Task keine zu löschenden Daten vorhanden.  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veralteten Datensatz für Zurücksetzen von Geräten löschen**: Verwenden Sie diesen Task, um veraltete Daten zu Zurücksetzungsaktionen für mobile Geräte aus der Datenbank zu löschen. Weitere Informationen zum Zurücksetzen mobiler Geräte finden Sie unter [Schützen von Daten mit Remotezurücksetzung, Remotesperre oder Kennungsrücksetzung mithilfe von System Center Configuration Manager](/sccm/mdm/deploy-use/wipe-lock-reset-devices).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete, mithilfe von Exchange Server Connector verwaltete Geräte löschen**: Verwenden Sie diesen Task, um veraltete Daten zu mobilen Geräten zu löschen, die mithilfe des Exchange Server-Connectors verwaltet werden. Diese Daten werden auf der Basis des Intervalls gelöscht, das für die Option **Anzahl der Tage der Inaktivität, nach der mobile Geräte ignoriert werden** auf der Registerkarte **Ermittlung** der Eigenschaften für den Exchange Server-Connector festgelegt wurde. Weitere Informationen finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Microsoft Intune](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar   
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Ermittlungsdaten löschen**: Verwenden Sie diesen Task, um veraltete Ermittlungsdaten aus der Datenbank zu löschen. Dabei kann es sich um Daten aus der Frequenzermittlung, aus der Netzwerkermittlung und aus Ermittlungsmethoden von Active Directory Domain Services (System, Benutzer und Gruppe) handeln. Bei Ausführung dieses Tasks an einem Standort werden mit diesem Standort verknüpfte Daten gelöscht. Die Änderungen werden anschließend an andere Standort repliziert. Informationen zur Ermittlung finden Sie unter [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Nutzungsdaten für Verteilungspunkte löschen**: Verwenden Sie diesen Task, um veraltete Daten für Verteilungspunkte aus der Datenbank zu löschen, deren Aufbewahrungsdauer überschritten ist.  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Verlaufsdaten zum Endpoint Protection-Integritätsstatus löschen**: Verwenden Sie diesen Task, um veraltete Statusinformationen für Endpoint Protection aus der Datenbank zu löschen. Weitere Informationen zu Endpoint Protection-Statusinformationen finden Sie unter [Überwachen von Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete angemeldete Geräte löschen**: Seit dem Update für 1602 ist dieser Task standardmäßig deaktiviert. Mit diesem Task können Sie veraltete Daten zu mobilen Geräten aus der Datenbank löschen, die über einen bestimmten Zeitraum keine Informationen an den Standort übermittelt haben.

Dieser Task gilt für Geräte, die über Microsoft Intune (hybrid) oder über die lokale Configuration Manager-Verwaltung mobiler Geräte registriert wurden. Informationen über die Betriebssysteme von Geräten, die über Configuration Manager oder Intune registriert werden, finden Sie unter [Unterstützte Betriebssysteme für Clients und Geräte für System Center Configuration Manager](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) im Abschnitt [Durch Microsoft Intune registrierte mobile Geräte](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mobile-devices-enrolled-by-microsoft-intune).

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Nicht aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veralteten Inventurverlauf löschen**: Verwenden Sie diesen Task, um Inventurdaten aus der Datenbank zu löschen, deren Aufbewahrungsdauer überschritten ist. Informationen zum Inventurverlauf finden Sie unter [Anzeigen des Hardwareinventars mit dem Ressourcen-Explorer in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Protokolldaten löschen**: Verwenden Sie diesen Task, um veraltete, für die Problembehandlung verwendete Protokolldaten aus der Datenbank zu löschen. Diese Daten stehen nicht im Zusammenhang mit Configuration Manager-Komponentenvorgängen.  

> [!IMPORTANT]  
> Standardmäßig wird dieser Task an jedem Standort täglich ausgeführt. An einem Standort der zentralen Verwaltung und primären Standorten werden mit dem Task Daten gelöscht, die älter als 30 Tage sind. Stellen Sie beim Verwenden von SQL Server Express an einem sekundären Standort sicher, dass dieser Task täglich ausgeführt wird und Daten gelöscht werden, die seit sieben Tagen inaktiv sind.  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   **Sekundärer Standort**: Aktiviert  

**Veralteten Benachrichtigungstaskverlauf löschen**: Verwenden Sie diesen Task zum Löschen von Informationen über Clientbenachrichtigungstasks aus der Standortdatenbank, wenn die Daten innerhalb eines angegebenen Zeitraums nicht aktualisiert wurden. Weitere Informationen zur Clientbenachrichtigung finden Sie unter [Clientbereitstellungstasks für System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Zusammenfassungsdatenreplikation löschen**: Verwenden Sie diesen Task zum Löschen von Informationen über veraltete Zusammenfassungsdaten für die Replikation aus der Standortdatenbank, wenn die Daten innerhalb eines angegebenen Zeitraums nicht aktualisiert wurden. Weitere Informationen finden Sie im Abschnitt [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) des Themas [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) .  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   **Sekundärer Standort**: Aktiviert  

**Veraltete Kennungsdatensätze löschen**: Verwenden Sie diesen Task am Standort auf oberster Ebene der Hierarchie, um veraltete Daten zu Kennungszurücksetzungen für Android- und Windows Phone-Geräte zu löschen. Daten zum Zurücksetzen der Kennung sind verschlüsselt, enthalten allerdings die PIN für Geräte. Standardmäßig ist dieser Task aktiviert und löscht Daten, die älter als 1 Tag sind.  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Replikationsüberwachungsdaten löschen**: Verwenden Sie diesen Task, um veraltete Daten zur Datenbankreplikation zwischen Configuration Manager-Standorten aus der Datenbank zu löschen. Wenn Sie die Konfiguration dieses Wartungstasks ändern, wirkt sich die Konfiguration auf jeden entsprechenden Standort in der Hierarchie aus. Weitere Informationen finden Sie im Abschnitt [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) des Themas [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) .  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   **Sekundärer Standort**: Aktiviert  

**Veraltete Softwaremessungsdaten löschen**: Verwenden Sie diesen Task, um veraltete Softwaremessungsdaten, deren Aufbewahrungsdauer überschritten ist, aus der Datenbank zu löschen. Weitere Informationen finden Sie unter [Softwaremessung in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Softwaremessungs-Zusammenfassungsdaten löschen**: Verwenden Sie diesen Task, um veraltete Softwaremessungs-Zusammenfassungsdaten, deren Aufbewahrungsdauer überschritten ist, aus der Datenbank zu löschen. Weitere Informationen finden Sie unter [Softwaremessung in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Statusmeldungen löschen**: Verwenden Sie diesen Task, um veraltete, über Statusfilterregeln konfigurierte Statusmeldungsdaten aus der Datenbank zu löschen. Informationen finden Sie im Abschnitt „Überwachen des Statussystems für Configuration Manager“ unter [Verwenden von Benachrichtigungen und des Statussystems für System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Bedrohungsdaten löschen**: Verwenden Sie diesen Task, um veraltete Endpoint Protection-Bedrohungsdaten, deren Aufbewahrungsdauer überschritten ist, aus der Datenbank zu löschen. Weitere Informationen zu Endpoint Protection finden Sie unter [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md) (Endpoint Protection in System Center Configuration Manager).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete unbekannte Computer löschen**: Verwenden Sie den Task zum Löschen von Daten über unbekannte Computer aus der Standortdatenbank, wenn diese im Verlauf eines festgelegten Zeitraums nicht aktualisiert wurden. Weitere Informationen finden Sie unter [Vorbereiten auf Bereitstellungen für unbekannte Computer in System Center Configuration Manager](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Daten zur Affinität zwischen Benutzer und Gerät löschen**: Verwenden Sie diesen Task, um veraltete Daten zur Affinität zwischen Benutzer und Gerät aus der Datenbank zu löschen. Weitere Informationen finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Löschen von abgelaufenen MDM-Massenregistrierungspaket-Datensätzen**: Verwenden Sie diesen Task, um alte Massenregistrierungszertifikate und dazugehörige Profile zu löschen, nachdem das Registrierungszertifikat abgelaufen ist. Weitere Informationen finden Sie unter [Erstellen von Zertifikatprofilen](/sccm/protect/deploy-use/create-certificate-profiles).
-   **Standort der zentralen Verwaltung**: Aktiviert
-   **Primärer Standort**: Aktiviert
-   Sekundärer Standort: Nicht verfügbar

**Inaktive Clientermittlungsdaten löschen**: Verwenden Sie diesen Task, um Ermittlungsdaten für inaktive Clients aus der Datenbank zu löschen. Clients werden als inaktiv gekennzeichnet, wenn der Client als veraltet markiert wird, sowie durch für den Clientstatus vorgenommene Konfigurationen.

Dieser Task kann nur für Ressourcen ausgeführt werden, bei denen es sich um Configuration Manager-Clients handelt. Er unterscheidet sich vom Task **Veraltete Ermittlungsdaten löschen**, über den alle veralteten Ermittlungsdatensätze gelöscht werden. Wenn dieser Task an einem Standort ausgeführt wird, werden Daten auf allen Standorten in der Hierarchie aus der Datenbank gelöscht. Weitere Informationen finden Sie unter [Konfigurieren des Clientstatus in System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).  

> [!IMPORTANT]  
> Wenn Sie diesen Task aktivieren, legen Sie als Ausführungsintervall einen höheren Wert fest als beim Zeitplan für die **Frequenzermittlung**. Dadurch können aktive Clients einen Frequenzermittlungsdatensatz senden, um Ihre Clientdatensätze als aktiv zu kennzeichnen, sodass sie von diesem Task nicht gelöscht werden.  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Nicht aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Warnungen löschen**: Verwenden Sie diesen Task, um abgelaufene Warnungen aus der Datenbank zu löschen, deren Aufbewahrungsdauer überschritten ist. Weitere Informationen finden Sie unter [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Clientermittlungsdaten löschen**: Mithilfe dieses Tasks können Sie veraltete Clientdatensätze aus der Datenbank löschen. Ein als veraltet markierter Datensatz wurde normalerweise durch einen neueren Datensatz für den gleichen Client ersetzt. Der neue Datensatz wird als aktiver Datensatz des Clients übernommen. Informationen zur Ermittlung finden Sie unter [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

> [!IMPORTANT]  
> Wenn Sie diesen Task aktivieren, legen Sie als Ausführungsintervall einen höheren Wert fest als beim Zeitplan für die Frequenzermittlung. Dadurch kann der Client einen Frequenzermittlungsdatensatz senden, um den Status „Veraltet“ ordnungsgemäß festzulegen.  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Nicht aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Veraltete Standorte und Subnetze der Gesamtstrukturermittlung löschen**: Verwenden Sie diesen Task, um Daten zu Active Directory-Standorten, -Subnetzen und -Domänen zu löschen, die innerhalb der letzten 30 Tage nicht mithilfe der Active Directory-Gesamtstrukturermittlung ermittelt wurden. Dadurch werden zwar die Ermittlungsdaten gelöscht, jedoch werden mithilfe dieser Ermittlungsdaten erstellte Grenzen nicht beeinträchtigt. Weitere Informationen finden Sie unter [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Statusdatensätze zur verwaisten Clientbereitstellung löschen**: Verwenden Sie diesen Task, um in regelmäßigen Abständen die Tabelle zu löschen, die Statusinformationen zur Clientbereitstellung enthält. Dieser Task bereinigt Datensätze, die veralteten oder außer Betrieb genommenen Geräten zugeordnet sind.  
-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar

**Nicht verwendete Anwendungsrevisionen löschen**: Verwenden Sie diesen Task, um Anwendungsrevisionen zu löschen, die nicht mehr referenziert werden. Weitere Informationen finden Sie unter [Überarbeiten und Ablösen von Anwendungen in System Center Configuration Manager](../../../apps/deploy-use/revise-and-supersede-applications.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Sammlungsmitglieder auswerten**: Sie konfigurieren die Auswertung der Sammlungsmitgliedschaft als Standortkomponente. Informationen zu Standortkomponenten finden Sie unter [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Schlüssel überwachen**: Verwenden Sie diesen Task, um die Integrität der primären Schlüssel der Configuration Manager-Datenbank zu überwachen. Ein primärer Schlüssel ist eine Spalte (oder eine Spaltenkombination), mit der eine Zeile eindeutig identifiziert und von allen übrigen Zeilen in einer Microsoft SQL Server-Datenbanktabelle unterschieden wird.  

-   **Standort der zentralen Verwaltung**: Aktiviert    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Indizes neu erstellen**: Verwenden Sie diesen Task, um die Configuration Manager-Datenbankindizes neu zu erstellen. Ein Index ist eine Datenbankstruktur, die für eine Datenbanktabelle erstellt wird, um das Abrufen von Daten zu beschleunigen. So führt das Suchen in einer indizierten Spalte häufig wesentlich schneller zum Ziel als das Suchen in einer nicht indizierten Spalte.

Zu Verbesserung der Leistung werden die Configuration Manager-Datenbankindizes häufig aktualisiert, damit sie mit den sich ständig verändernden Daten in der Datenbank synchronisiert bleiben. Dieser Task erstellt Indizes für Datenbankspalten, die zu mindestens 50 % eindeutig sind, löscht Indizes für Spalten, die zu weniger als 50 % eindeutig sind, und erstellt alle vorhandenen Indizes neu, die die Kriterien der Eindeutigkeit der Daten erfüllen.  

-   **Standort der zentralen Verwaltung**: Nicht aktiviert    
-   **Primärer Standort**: Nicht aktiviert    
-   **Sekundärer Standort**: Nicht aktiviert  

**Daten installierter Software zusammenfassen**: Verwenden Sie diesen Task, um die Daten für installierte Software aus mehreren Datensätzen in einem allgemeinen Datensatz zusammenzufassen. Mithilfe der Datenzusammenfassung kann die Datenmenge in der Configuration Manager-Datenbank komprimiert werden. Weitere Informationen finden Sie unter [Introduction to software inventory in System Center Configuration Manager (Einführung in die Softwareinventur in System Center Configuration Manager)](../../clients/manage/inventory\introduction-to-software-inventory.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Softwaremessungsdaten der Dateinutzung zusammenfassen**: Mit diesem Task werden die Softwaremessungsdaten der Dateinutzung aus verschiedenen Datensätzen in einem allgemeinen Datensatz zusammengefasst. Mithilfe der Datenzusammenfassung kann die Datenmenge in der Configuration Manager-Datenbank komprimiert werden.

Sie können diesen Task in Kombination mit dem Task **Softwaremessungsdaten der monatlichen Nutzung zusammenfassen** verwenden, um Softwaremessungsdaten zusammenzufassen und die Speicherplatznutzung in der Configuration Manager-Datenbank zu verringern. Weitere Informationen finden Sie unter [Softwaremessung in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Softwaremessungsdaten der monatlichen Nutzung zusammenfassen**: Verwenden Sie diesen Task, um die Softwaremessungsdaten für die monatliche Nutzung aus mehreren Datensätzen in einem allgemeinen Datensatz zusammenzufassen. Mithilfe der Datenzusammenfassung kann die Datenmenge in der Configuration Manager-Datenbank komprimiert werden.

Sie können diesen Task in Kombination mit dem Task **Softwaremessungsdaten der Dateinutzung zusammenfassen** verwenden, um Softwaremessungsdaten zusammenzufassen und die Speicherplatznutzung in der Configuration Manager-Datenbank zu verringern. Weitere Informationen finden Sie unter [Softwaremessung in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**In der Anwendung verfügbare Ziele aktualisieren**: Verwenden Sie diesen Task, um Configuration Manager die Zuordnung von Richtlinien und Anwendungsbereitstellungen zu Ressourcen in Sammlungen neu berechnen zu lassen. Beim Bereitstellen von Richtlinien oder Anwendungen in einer Sammlung erstellt Configuration Manager eine anfängliche Zuordnung zwischen den Objekten, die Sie bereitstellen, und den Mitgliedern der Sammlung.

Diese Zuordnungen werden zur schnellen Bezugnahme in einer Tabelle gespeichert. Wenn sich die Mitgliedschaft von Sammlungen ändern, werden diese gespeicherten Zuordnungen entsprechend diesen Änderungen aktualisiert. Es ist jedoch möglich, dass diese Zuordnungen ihre Synchronität verlieren. Wenn z. B. der Standort eine Benachrichtigungsdatei nicht ordnungsgemäß verarbeiten kann, wird diese Änderung ggf. nicht als Änderung an den Zuordnungen wiedergegeben. Dieser Task aktualisiert diese Zuordnung basierend auf der aktuellen Mitgliedschaft in der Sammlung.  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  

**Tabellen für Anwendungskatalog-Updates**: Verwenden Sie diesen Task, um den Datenbankcache der Anwendungskatalog-Website mit den aktuellen Anwendungsinformationen zu synchronisieren. Wenn Sie die Konfiguration dieses Wartungstasks ändern, wirkt sich die Konfiguration auf alle primären Standorte der Hierarchie aus.  

-   Standortserver der zentralen Verwaltung: Nicht verfügbar    
-   **Primärer Standort**: Aktiviert    
-   Sekundärer Standort: Nicht verfügbar  
