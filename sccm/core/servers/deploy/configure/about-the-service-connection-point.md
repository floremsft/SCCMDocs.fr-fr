---
title: Dienstverbindungspunkt | Microsoft-Dokumentation
description: "Erfahren Sie mehr über diese Standortsystemrolle von Configuration Manager, und verstehen und planen Sie den Verwendungsbereich."
ms.custom: na
ms.date: 6/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: "18"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e3d41dc1bb732e887d722f39ee86deaf0aae3240
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>Informationen zum Dienstverbindungspunkt in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Der System Center Configuration Manager-Dienstverbindungspunkt ist eine Standortsystemrolle, die mehrere wichtige Funktionen für die Hierarchie übernimmt. Bevor Sie den Dienstverbindungspunkt einrichten, sollten Sie seinen Verwendungsbereich kennen und planen, da dies Auswirkungen auf die Einrichtung dieser Standortsystemrolle haben kann:  

-   **Verwalten mobiler Geräte mit Microsoft Intune**: Diese Rolle ersetzt den Windows Intune-Connector, der von früheren Configuration Manager-Versionen verwendet wurde, und kann mit Ihren Intune-Abonnementdetails konfiguriert werden. Informationen hierzu finden Sie unter [Hybride Verwaltung mobiler Geräte (MDM) mit System Center Configuration Manager und Microsoft Intune](../../../../mdm/understand/hybrid-mobile-device-management.md).  

-   **Verwalten mobiler Geräte mit lokaler Verwaltung mobiler Geräte**: Diese Rolle bietet Unterstützung für lokale Geräte, die von Ihnen verwaltet werden und die keine Verbindung mit dem Internet herstellen. Informationen hierzu finden Sie unter [Verwalten mobiler Geräte mit lokaler Infrastruktur in System Center Configuration Manager](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

-   **Hochladen von Nutzungsdaten aus Ihrer Configuration Manager-Infrastruktur**: Sie können die Ebene oder die Menge der hochgeladenen Details steuern. Hochgeladene Daten geben uns folgende Möglichkeiten:  

    -   Proaktives Erkennen und Beheben von Problemen  

    -   Verbesserung unserer Produkte und Dienste  

    -   Ermitteln von Updates für Configuration Manager, die für die von Ihnen verwendete Configuration Manager-Version gelten  

  Informationen zu den auf den einzelnen Ebenen gesammelten Daten und zum Ändern der Sammlungsebene nach der Installation der Rolle finden Sie unter [Diagnose- und Nutzungsdaten](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data). Klicken Sie anschließend auf den Link der verwendeten Configuration Manager-Version.  

  Weitere Informationen finden Sie unter [Ebenen und Einstellungen für Nutzungsdaten](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

-   **Herunterladen von Updates, die auf Ihre Configuration Manager-Infrastruktur zutreffen**: Auf Grundlage der von Ihnen hochgeladenen Nutzungsdaten werden nur Updates verfügbar gemacht, die für Ihre Infrastruktur relevant sind.  

- **Jede Hierarchie unterstützt eine einzelne Instanz dieser Rolle:**  

 -   Die Standortsystemrolle kann nur am Standort der obersten Ebene Ihrer Hierarchie installiert werden. Dabei handelt es sich um einen Standort der zentralen Verwaltung oder einen eigenständigen primären Standort.  

  -   Wenn Sie einen eigenständigen primären Standort auf eine größere Hierarchie erweitern, müssen Sie diese Rolle am primären Standort deinstallieren und können sie dann am Standort der zentralen Verwaltung installieren.  


##  <a name="bkmk_modes"></a> Betriebsmodi  
 Der Dienstverbindungspunkt unterstützt zwei Betriebsmodi:  

-   Im **Onlinemodus** sucht der Dienstverbindungspunkt automatisch alle 24 Stunden nach Updates und lädt dann neue Updates herunter, die für Ihre aktuelle Infrastruktur und Produktversion verfügbar sind. Diese werden dann in der Configuration Manager-Konsole bereitgestellt.  

-   Im **Offlinemodus** stellt der Dienstverbindungspunkt keine Verbindung mit dem Microsoft-Clouddienst her, und Sie müssen das [Dienstverbindungstool für System Center Configuration Manager](../../../../core/servers/manage/use-the-service-connection-tool.md) manuell ausführen, um verfügbare Updates zu importieren.  

Wenn Sie nach der Installation des Dienstverbindungspunkts zwischen dem Online- und Offline-Modus wechseln möchten, müssen Sie anschließend den SMS_DMP_DOWNLOADER-Thread des SMS_Executive-Diensts von Configuration Manager neu starten, damit diese Änderung wirksam wird. Verwenden Sie hierzu den Dienst-Manager von Configuration Manager, um nur den SMS_DMP_DOWNLOADER-Thread des SMS_Executive-Diensts neu zu starten. Sie können auch den SMS_Executive-Dienst für Configuration Manager neu starten (wodurch die meisten Standortkomponenten neu gestartet werden) oder auf einen Zeitplantask wie z.B. eine Standortsicherung warten, der den SMS_Executive-Dienst für Sie beendet und später neu startet.  

Wechseln Sie zum Verwenden des Dienst-Managers von Configuration Manager in der Konsole zu **Überwachung** > **Systemstatus** > **Komponentenstatus**, wählen Sie **Starten**, und wählen Sie anschließend **Dienst-Manager für Configuration Manager**. Gehen Sie im Dienst-Manager folgendermaßen vor:  

-   Erweitern Sie im Navigationsbereich den Standort und dann **Komponenten**, und wählen Sie anschließend die Komponente aus, die neu gestartet werden soll.  

-   Klicken Sie im Detailbereich mit der rechten Maustaste auf die Komponente, und wählen Sie dann **Abfrage**.  

-   Wenn der Status der Komponente bestätigt wurde, klicken Sie erneut mit der rechten Maustaste auf die Komponente, und wählen Sie **Beenden**.  

-   Führen Sie die **Abfrage** für die Komponente erneut aus, um sicherzustellen, dass sie beendet wurde. Klicken Sie mit der rechten Maustaste noch einmal auf die Komponente, und wählen Sie **Starten**.  

> [!IMPORTANT]  
>  Der Prozess, der dem Dienstverbindungspunkt ein Microsoft Intune-Abonnement hinzufügt, legt die Standortsystemrolle automatisch auf „Online“ fest. Der Dienstverbindungspunkt unterstützt den Offlinemodus nicht, wenn er mit einem Intune-Abonnement eingerichtet wird.  

**Wenn die Rolle auf einem Computer installiert wird, der sich an einem vom Standortserver entfernten Ort befindet:**  

-   Das Computerkonto des Standortservers muss ein lokaler Administrator auf dem Computer sein, der eine Remotedienstverbindung hostet.

-   Sie müssen den Standortsystemserver, der die Rolle hostet, mit einem Standortsystem-Installationskonto einrichten.  

-   Der Verteilungs-Manager auf dem Standortserver verwendet das Standortsystem-Installationskonto zum Übertragen von Updates vom Dienstverbindungspunkt.

##  <a name="bkmk_urls"></a> Erforderliche Berechtigungen für den Internetzugriff  
Der Computer, der den Dienstverbindungspunkt und alle Firewalls zwischen dem Computer und dem Internet hostet, muss die Kommunikation über den **TCP-Port 443** und den **TCP-Port 443** an die folgenden Internet-URLs übergeben, um den Vorgang zu aktivieren. Der Dienstverbindungspunkt unterstützt auch Webproxys (mit oder ohne Authentifizierung) für die Verwendung dieser URLs.  Informationen zur Konfiguration eines Web Proxy Accounts finden Sie unter [Unterstützung von Proxyservern in System Center Configuration Manager](/sccm/core/plan-design/network/proxy-server-support).

**Updates und Wartung**  

-   *.akamaiedge.net  

-   *.akamaitechnologies.com 

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   download.windowsupdate.com

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *manage.microsoft.com  
-   https://bspmts.mp.microsoft.com/V
-   https://login.microsoftonline.com/{TenantID}


**Windows 10-Wartung**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  

## <a name="install-the-service-connection-point"></a>Installieren des Dienstverbindungspunkts
Beim Ausführen von **Setup** zum Installieren des Standorts der obersten Ebene einer Hierarchie haben Sie die Möglichkeit, den Dienstverbindungspunkt zu installieren.

Nachdem Sie Setup ausgeführt haben oder wenn Sie die Standortsystemrolle neu installieren, verwenden Sie den **Assistenten zum Hinzufügen von Standortsystemrollen** oder den **Assistenten zum Erstellen von Standortsystemservern**, um das Standortsystem auf einem Server am Standort der obersten Ebene der Hierarchie (dem Standort der zentralen Verwaltung oder einem eigenständigen primären Standort) zu installieren. Beide Assistenten befinden sich auf der Registerkarte **Startseite** in der Konsole unter **Verwaltung** > **Standortkonfiguration** > **Server und Standortsystemrollen**.

## <a name="log-files-used-by-the-service-connection-point"></a>Vom Dienstverbindungspunkt verwendete Protokolldateien
Zeigen Sie **Dmpuploader.log** auf dem Computer an, auf dem der Dienstverbindungspunkt ausgeführt wird, um Informationen zu Uploads in Microsoft anzuzeigen.  Sehen Sie sich **Dmpdownloader.log** an für Informationen zu Downloads und dem Downloadfortschritt von Updates. Die vollständige Liste der mit dem Dienstverbindungspunkt verknüpften Protokolle finden Sie unter [Service Connection Point (Dienstverbindungspunkt)](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) im Thema „log files“ (Protokolldateien) von Configuration Manager.

Die folgendes Flussdiagramme veranschaulichen den Prozessfluss und Protokolleinträge für die Downloads von Updates und die Replikation von Updates an anderen Standorten:
 - [Flussdiagramm: Herunterladen von Updates](/sccm/core/servers/manage/download-updates-flowchart)
 - [Flussdiagramm: Aktualisieren von Replikationen](/sccm/core/servers/manage/update-replication-flowchart)
