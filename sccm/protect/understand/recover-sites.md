---
title: Standortwiederherstellung | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Ihre Standorte in System Center Configuration Manager wiederherstellen.
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 49eea15ea2888f8f93c33eb771c09147ba21529e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
#  <a name="recover-a-configuration-manager-site"></a>Wiederherstellen eines Configuration Manager-Standorts

*Gilt für: System Center Configuration Manager (Current Branch)*

Führen Sie nach einem Standortausfall oder bei einem Datenverlust in der Standortdatenbank eine Configuration Manager-Standortwiederherstellung aus. Bei der Standortwiederherstellung geht es primär darum, Daten zu reparieren und erneut zu synchronisieren, um eine Unterbrechung von Vorgängen zu vermeiden.

Die Abschnitte in diesem Thema helfen Ihnen bei der Wiederherstellung eines Configuration Manager-Standorts. Informationen zum Erstellen einer Sicherung finden Sie unter [Sichern eines Configuration Manager-Standorts](/sccm/protect/understand/backup-and-recovery).

## <a name="considerations-before-recovering-a-site"></a>Überlegungen vor dem Wiederherstellen eines Standorts
**Sie müssen die gleiche Version und Edition von SQL Server verwenden:** Das Wiederherstellen einer Datenbank, die mit SQL Server 2014 ausgeführt wurde, mit SQL Server 2016 wird beispielsweise nicht unterstützt. Gleichermaßen kann eine Standortdatenbank, die mit einer Standard Edition von SQL Server 2016 ausgeführt wurde, nicht mit einer Enterprise Edition von SQL Server 2016 wiederhergestellt werden.
-   SQL Server darf nicht auf den **Einzelbenutzermodus**festgelegt werden.
-   Stellen Sie sicher, dass die MDF- und. LDF-Dateien gültig sind. Wenn Sie einen Standort wiederherstellen, wird der Status der Dateien, die Sie wiederherstellen möchten, nicht überprüft.

**Wenn Sie eine SQL Server AlwaysOn-Verfügbarkeitsgruppe zum Hosten der Standortdatenbank verwenden:** Ändern Sie Ihre Wiederherstellungspläne gemäß der Anleitung unter [Vorbereiten zur Verwendung von SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

**Wenn Sie Datenbankreplikate verwenden:** Nachdem Sie eine Standortdatenbank wiederhergestellt haben, die für Datenbankreplikate konfiguriert war, müssen Sie vor der Verwendung der Datenbankreplikate jedes Datenbankreplikat neu konfigurieren, indem Sie die Veröffentlichungen und die Abonnements neu erstellen.

## <a name="determine-your-recovery-options"></a>Bestimmen der Wiederherstellungsoptionen
Bei der Wiederherstellung des primären Standortservers und des Standorts der zentralen Verwaltung von Configuration Manager müssen Sie zwei Hauptbereiche berücksichtigen: den **Standortserver** und die **Standortdatenbank**.
Die folgenden Abschnitte helfen Ihnen bei der Auswahl der besten Optionen für Ihr Wiederherstellungsszenario.

> [!NOTE]   
> Wenn beim Setup ein vorhandener Configuration Manager-Standort auf dem Server erkannt wird, können Sie eine Standortwiederherstellung starten. Allerdings sind die Wiederherstellungsoptionen für den Standortserver beschränkt. Wenn Sie Setup beispielsweise auf einem vorhandenen Standortserver ausführen und die Wiederherstellung auswählen, können Sie zwar den Standortdatenbankserver wiederherstellen, aber die Option zum Wiederherstellen des Standortservers ist deaktiviert.

### <a name="site-server-recovery-options"></a>Wiederherstellungsoptionen für den Standortserver
Starten Sie das Setup über eine Kopie des Ordners **CD.Latest**, die Sie außerhalb des Configuration Manager-Installationsordners erstellen.
-   Wenn Sie das Configuration Manager-Setup auf dem Standortserver über das Menü **Start** ausführen, ist die Option **Standort wiederherstellen** nicht verfügbar.
-   Wenn Sie vor der Sicherung Updates mithilfe der Configuration Manager-Konsole installiert haben, können Sie den Standort nicht erfolgreich neu installieren, indem Sie das Setup vom Installationsmedium oder aus dem Installationspfad für Configuration Manager verwenden.

Wählen Sie dann die Option **Standort wiederherstellen** aus. Für den ausgefallenen Standortserver stehen die folgenden Wiederherstellungsoptionen zur Verfügung:

-   **Den Standortserver mit einem vorhandenen Sicherungssatz wiederherstellen**: Verwenden Sie diese Option, wenn Sie über eine Sicherung des Configuration Manager-Standortservers verfügen, die vor dem Standortausfall im Rahmen des Wartungstasks **Standortserver sichern** auf dem Standortserver erstellt wurde. Der Standort wird erneut installiert, und die Standardeinstellungen werden anhand des gesicherten Standorts konfiguriert.
-   **Diesen Standortserver erneut installieren**: Verwenden Sie diese Option, wenn Sie über keine Sicherung des Standortservers verfügen. Der Standortserver wird erneut installiert, und Sie müssen die Standorteinstellungen genau wie bei einer Erstinstallation angeben.
  -   Sie müssen den gleichen Standortcode und den gleichen Namen der Standortdatenbank verwenden, die Sie bei der Erstinstallation des ausgefallenen Standorts angegeben hatten.
  -   Sie können den Standort auf einem neuen Computer neu installieren, auf dem ein neues Betriebssystem ausgeführt wird.
  -   Der Computer muss den gleichen Namen und FQDN des ursprünglichen Standortservers verwenden.   

### <a name="site-database-recovery-options"></a>Wiederherstellungsoptionen für die Standortdatenbank
Beim Ausführen von Setup stehen für die Standortdatenbank die folgenden Wiederherstellungsoptionen zur Verfügung:
-   **Die Standortdatenbank mit dem Sicherungssatz wiederherstellen**: Verwenden Sie diese Option, wenn Sie über eine Sicherung der Configuration Manager-Standortdatenbank verfügen, die vor dem Standortdatenbankfehler bei der Ausführung des Wartungstasks **Standortserver sichern** auf dem Standort erstellt wurde. Wenn Sie über eine Hierarchie verfügen, werden die Änderungen, die Sie seit der letzten Sicherung der Standortdatenbank an der Standortdatenbank vorgenommen haben, für einen primären Standort vom Standort der zentralen Verwaltung abgerufen bzw. für einen Standort der zentralen Verwaltung von einem primären Referenzstandort. Wenn Sie die Standortdatenbank für einen eigenständigen primären Standort wiederherstellen, gehen die Standortänderungen seit der letzten Sicherung verloren.

   Wenn Sie die Standortdatenbank für einen Standort in einer Hierarchie wiederherstellen, hängt das Wiederherstellungsverhalten vom Standorttyp (Standort der zentralen Verwaltung oder primärer Standort) sowie davon ob, ob die letzte Sicherung innerhalb oder außerhalb der Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server liegt. Weitere Informationen finden Sie im Abschnitt [Wiederherstellungsszenarien für die Standortdatenbank](##site-database-recovery-scenarios) in diesem Thema.
  > [!NOTE]   
  > Die Wiederherstellung ist nicht möglich, wenn Sie angeben, dass die Standortdatenbank anhand eines Sicherungssatzes wiederhergestellt werden soll, die Standortdatenbank aber bereits vorhanden ist.  

-   **Eine neue Datenbank für diesen Standort erstellen**: Verwenden Sie diese Option, wenn Sie über keine Sicherung der Configuration Manager-Standortdatenbank verfügen. Wenn Sie über eine Hierarchie verfügen, wird eine neue Standortdatenbank erstellt. Die Daten werden anhand replizierter Daten wiederhergestellt, die bei einem primären Standort vom Standort der zentralen Verwaltung stammen bzw. bei einem Standort der zentralen Verwaltung von einem primären Referenzstandort. Diese Option ist beim Wiederherstellen eines eigenständigen primären Standorts oder eines Standorts der zentralen Verwaltung, der keine primären Standorte hat, nicht verfügbar.

-   **Manuell wiederhergestellte Standortdatenbank verwenden**: Verwenden Sie diese Option, wenn Sie die Configuration Manager-Standortdatenbank bereits wiederhergestellt haben, aber den Wiederherstellungsprozess noch abschließen müssen.
    -   Configuration Manager kann die Standortdatenbank aus dem Configuration Manager-Sicherungswartungstask oder aus der Standortdatenbanksicherung wiederherstellen, die Sie mit DPM oder einem anderen Prozess ausgeführt haben. Nachdem Sie die Standortdatenbank mithilfe einer Methode außerhalb von Configuration Manager wiederhergestellt haben, müssen Sie das Setup ausführen und diese Option auswählen, um die Wiederherstellung der Standortdatenbank abzuschließen.

    > [!NOTE]   
    > Wenn Sie DPM verwenden, um die Standortdatenbank zu sichern, dann verwenden Sie DPM-Prozeduren, um die Standortdatenbank an einem angegebenen Ort wiederherzustellen, bevor Sie den Wiederherstellungsprozess in Configuration Manager fortsetzen. Weitere Informationen zu DPM finden Sie in der [Data Protection Manager-Dokumentationsbibliothek]() auf der TechNet-Webseite.    

    -   Wenn Sie über eine Hierarchie verfügen, werden die Änderungen, die Sie seit der letzten Sicherung der Standortdatenbank an der Standortdatenbank vorgenommen haben, für einen primären Standort vom Standort der zentralen Verwaltung abgerufen bzw. für einen Standort der zentralen Verwaltung von einem primären Referenzstandort. Wenn Sie die Standortdatenbank für einen eigenständigen primären Standort wiederherstellen, gehen die Standortänderungen seit der letzten Sicherung verloren.     


-   **Datenbankwiederherstellung überspringen**: Verwenden Sie diese Option, wenn es auf dem Configuration Manager-Standortdatenbankserver keine Datenverluste gab. Diese Option gilt nur, wenn die Standortdatenbank sich auf einem anderen Computer als der Standortserver, den Sie wiederherstellen, befindet.

### <a name="sql-server-change-tracking-retention-period"></a>Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server
Die Änderungsnachverfolgung ist für die Standortdatenbank in SQL Server aktiviert. Bei der Änderungsnachverfolgung können von Configuration Manager Informationen über die Änderungen abgefragt werden, die seit einem früheren Zeitpunkt an den Datenbanktabellen vorgenommen wurden. Mit der Beibehaltungsdauer wird angegeben, wie lange Informationen zur Änderungsnachverfolgung beibehalten werden. Für die Standortdatenbank ist standardmäßig eine Beibehaltungsdauer von 5 Tagen konfiguriert. Beim Wiederherstellen einer Standortdatenbank richtet sich der Wiederherstellungsprozess danach, ob die Sicherung innerhalb oder außerhalb der Beibehaltungsdauer liegt. Wenn beispielsweise ein Standortdatenbankserver ausfällt und die letzte Sicherung vor 7 Tagen erstellt wurde, liegt die Sicherung außerhalb der Beibehaltungsdauer.

Weitere Informationen zur SQL Server-Änderungsnachverfolgung finden Sie in den folgenden Blogs des SQL Server-Teams: [Change Tracking Cleanup - part 1 (Cleanup für die Änderungsnachverfolgung - Teil 1)](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) und [Change Tracking Cleanup - part 2 (Cleanup für die Änderungsnachverfolgung - Teil 2)](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).

### <a name="reinitialization-of-site-or-global-data"></a>Erneute Initialisierung von Standortdaten oder globalen Daten
Beim erneuten Initialisieren der Standortdaten oder der globalen Daten werden in der Standortdatenbank vorhandene Daten durch Daten aus einer anderen Standortdatenbank ersetzt. Wenn beispielsweise an Standort ABC Daten von Standort XYZ erneut initialisiert werden, werden die folgenden Schritte ausgeführt:
-   Die Daten werden von Standort XYZ zu Standort ABC kopiert.
-   Die für Standort XYZ vorhandenen Daten werden aus der Standortdatenbank an Standort ABC entfernt.
-   Die von Standort XYZ kopierten Daten werden in die Standortdatenbank an Standort ABC eingefügt.

#### <a name="example-scenario-1"></a>Beispielszenario 1
**Die globalen Daten vom Standort der zentralen Verwaltung werden am primären Standort erneut initialisiert**: Bei der Wiederherstellung werden die vorhandenen globalen Daten für den primären Standort aus der Datenbank des primären Standorts entfernt und durch die am Standort der zentralen Verwaltung kopierten globalen Daten ersetzt.

#### <a name="example-scenario-2"></a>Beispielszenario 2
**Die Standortdaten von einem primären Standort werden am Standort der zentralen Verwaltung erneut initialisiert**: Bei der Wiederherstellung werden die vorhandenen Standortdaten für diesen primären Standort aus der Datenbank des Standorts der zentralen Verwaltung entfernt und durch die am primären Standort kopierten Standortdaten ersetzt. Die Standortdaten für andere primäre Standorte bleiben unverändert.

### <a name="site-database-recovery-scenarios"></a>Wiederherstellungsszenarien für die Standortdatenbank
Nach der Wiederherstellung einer Standortdatenbank anhand einer Sicherung wird von Configuration Manager versucht, die seit der letzten Datenbanksicherung an den Standortdaten und globalen Daten vorgenommenen Änderungen wiederherzustellen. Im Folgenden sind die Aktionen aufgeführt, die nach der Wiederherstellung einer Standortdatenbank anhand einer Sicherung von Configuration Manager gestartet werden.

**Der wiederhergestellte Standort ist ein Standort der zentralen Verwaltung:**
-   **Datenbanksicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung**
    -   **Globale Daten:** Die Änderungen in globalen Daten nach der Sicherung werden von allen primären Standorten repliziert.
    -   **Standortdaten:** Die Änderungen in Standortdaten nach der Sicherung werden von allen primären Standorten repliziert.


-   **Datenbanksicherung, die älter ist als die Beibehaltungsdauer der Änderungsnachverfolgung**
    -   **Globale Daten:** Am Standort der zentralen Verwaltung werden die globalen Daten vom primären Referenzstandort, sofern angegeben, neu initialisiert. Anschließend werden die globalen Daten vom Standort der zentralen Verwaltung auf allen anderen primären Standorten neu initialisiert. Wenn kein Referenzstandort angegeben wurde, werden die globalen Daten vom Standort der zentralen Verwaltung (die aus der Sicherung wiederhergestellten Daten) auf allen primären Standorten neu initialisiert.
    -   **Standortdaten:** Am Standort der zentralen Verwaltung werden die Standortdaten von jedem primären Standort neu initialisiert.


**Der wiederhergestellte Standort ist ein primärer Standort:**
-   **Datenbanksicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung**
    -   **Globale Daten:** Die nach der Sicherung an globalen Daten vorgenommenen Änderungen werden vom Standort der zentralen Verwaltung repliziert.
    -   **Standortdaten:** Am Standort der zentralen Verwaltung werden die Standortdaten vom primären Standort erneut initialisiert. Die nach der Sicherung ausgeführten Änderungen gehen verloren. Die meisten Daten werden jedoch von Clients erneut generiert, von denen Informationen an den primären Standort gesendet werden.


-   **Datenbanksicherung, die älter ist als die Beibehaltungsdauer der Änderungsnachverfolgung**
    -   **Globale Daten:** Am primären Standort werden die globalen Daten vom Standort der zentralen Verwaltung erneut initialisiert.
    -   **Standortdaten:** Am Standort der zentralen Verwaltung werden die Standortdaten vom primären Standort erneut initialisiert. Die nach der Sicherung ausgeführten Änderungen gehen verloren. Die meisten Daten werden jedoch von Clients erneut generiert, von denen Informationen an den primären Standort gesendet werden.

## <a name="site-recovery-procedures"></a>Verfahren zur Standortwiederherstellung
Wenden Sie eines der folgenden Verfahren an, um Standortserver und Standortdatenbank wiederherzustellen.

### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>So starten Sie eine Standortwiederherstellung im Setup-Assistenten
1.  Kopieren Sie den Ordner [CD.Latest](/sccm/core/servers/manage/the-cd.latest-folde) an einen Speicherort außerhalb des Configuration Manager-Installationsordners.
Führen Sie von der Kopie des Ordners „CD.Latest“ aus den Configuration Manager-Setup-Assistenten aus.

2.  Wählen Sie auf der Seite **Erste Schritte** die Option **Standort wiederherstellen**aus, und klicken Sie dann auf **Weiter**.

3.  Wählen Sie die Optionen aus, die für die Standortwiederherstellung geeignet sind, und schließen Sie den Assistenten ab.

  -   Während der Wiederherstellung wird der Port des SQL Server-Service Brokers (SSB), der von SQL Server verwendet wird, von Setup identifiziert. Ändern Sie die Einstellung für diesen Port während der Wiederherstellung nicht, da andernfalls die Datenreplikation nach Abschluss der Wiederherstellung nicht ordnungsgemäß ausgeführt werden kann.

  -   Sie können den ursprünglichen oder einen neuen Pfad für die Configuration Manager-Installation im Setup-Assistenten angeben.

### <a name="to-start-an-unattended-site-recovery"></a>So starten Sie eine unbeaufsichtigte Standortwiederherstellung
  1.    Bereiten Sie das Skript für eine unbeaufsichtigte Installation mit den für die Standortwiederherstellung erforderlichen Optionen vor.  Siehe [Skriptdateischlüssel für unbeaufsichtigte Standortwiederherstellung](/sccm/protect/understand/unattended-site-recovery-script-file-keys).

  2.    Führen Sie das Configuration Manager-Setup mit der Befehlszeilenoption **/script** aus. Wenn der Name der Setupinitialisierungsdatei zum Beispiel „ConfigMgrUnattend.ini“ lautet und die Datei im Verzeichnis „C:\Temp“ des Computers gespeichert ist, auf dem Sie das Setup ausführen, lautet der Befehl wie folgt: **Setup /script C:\temp\ConfigMgrUnattend.ini**

  > [!NOTE]   
  >  Nach dem Wiederherstellen eines zentralen Verwaltungsstandorts kann es bei der Replikation bestimmter Standortdaten von untergeordneten Standorten zu Fehlern kommen. Dies kann Hardwareinventur, Softwareinventur und Statusmeldungen umfassen.
  >
  >  In diesem Fall müssen Sie **ConfigMgrDRSSiteQueue** für die Datenbankreplikation erneut initialisieren.  Verwenden Sie hierzu **SQL Server Manager** zum Ausführen der folgenden Abfrage über die Configuration Manager-Standortdatenbank am Standort der zentralen Verwaltung:
  >
  >  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**
  >
  >  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**


## <a name="post-recovery-tasks"></a>Aufgaben nach der Wiederherstellung
Nach der Wiederherstellung Ihres Standorts müssen Sie ggf. einige zusätzliche Tasks ausführen, bevor die Standortwiederherstellung abgeschlossen ist. In den folgenden Abschnitten erfahren Sie, wie Sie Ihre Standortwiederherstellung abschließen.

### <a name="re-enter-user-account-passwords"></a>Erneutes Eingeben der Kennwörter von Benutzerkonten
Nach der Wiederherstellung eines Standortservers müssen die Kennwörter der für den Standort angegebenen Benutzerkonten erneut eingegeben werden, da sie im Rahmen der Standortwiederherstellung zurückgesetzt werden. Die Konten werden nach Abschluss der Standortwiederherstellung im Setup-Assistenten auf der Seite **Fertig gestellt** aufgelistet und auf dem wiederhergestellten Standortserver unter "C:\ConfigMgrPostRecoveryActions.html" gespeichert.

#### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>So geben Sie Kennwörter für Benutzerkonten nach der Standortwiederherstellung erneut ein

1.  Öffnen Sie die Configuration Manager-Konsole, und stellen Sie eine Verbindung mit dem wiederhergestellten Standort her.

2.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.

3.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Sicherheit**, und klicken Sie dann auf **Konten**.

4.  Gehen Sie für jedes Konto, für das Sie das Kennwort erneut eingeben, wie folgt vor:

    1.  Wählen Sie das Konto aus der nach der Standortwiederherstellung angezeigten Liste von Konten aus. Sie finden diese Liste auf dem wiederhergestellten Standortserver unter C:\ConfigMgrPostRecoveryActions.html.

    2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften** , um die Kontoeigenschaften zu öffnen.

    3.  Klicken Sie auf der Registerkarte **Allgemein** auf **Festlegen**, und geben Sie dann die Kennwörter für das Konto erneut ein.

    4.  Klicken Sie auf **Überprüfen**, wählen Sie die entsprechende Datenquelle für das ausgewählte Benutzerkonto aus, und klicken Sie dann auf **Testverbindung** , um zu überprüfen, ob eine Verbindung des Benutzerkontos mit der Datenquelle möglich ist.

    5.  Klicken Sie auf **OK** , um die Kennwortänderungen zu speichern, und klicken Sie dann auf **OK**.

### <a name="re-enter-sideloading-keys"></a>Sideload-Schlüssel neu eingeben
Nach der Wiederherstellung eines Standortservers müssen Sie die Windows-Sideload-Schlüssel für den Standort erneut eingeben, weil diese im Rahmen der Standortwiederherstellung zurückgesetzt werden. Nach dem erneuten Eingeben der Sideload-Schlüssel wird der Zähler in der Spalte **Verwendete Aktivierungen** für Windows-Sideload-Schlüssel in der Configuration Manager-Konsole zurückgesetzt. Angenommen, vor dem Standortausfall hätte der Zähler **Aktivierungen insgesamt** den Wert **100** und **Verwendete Aktivierungen** den Wert **90** für die Anzahl der von Geräten verwendeten Schlüssel gehabt. Nach der Standortwiederherstellung zeigt die Spalte **Aktivierungen insgesamt** weiterhin **100**an, der Wert in **Verwendete Aktivierungen** wurde jedoch fälschlich auf **0**zurückgesetzt. Wenn nun jedoch Sideload-Schlüssel von zehn weiteren Geräten verwendet werden, sind nachfolgend keine Sideload-Schlüssel mehr übrig, und für das nächste Gerät wird kein Sideload-Schlüssel mehr zur Anwendung verfügbar sein.

### <a name="recreate-the-microsoft-intune-subscription"></a>Neuerstellen des Microsoft Intune-Abonnements
 Wenn Sie einen Configuration Manager-Standortserver wiederherstellen, nachdem ein neues Image auf den Standortservercomputer aufgespielt wurde, wird das Microsoft Intune-Abonnement nicht wiederhergestellt. Sie müssen Ihr Abonnement nach dem Wiederherstellen des Standorts erneut verbinden.  Erstellen Sie keine neue APN-Anforderung, sondern laden Sie stattdessen die aktuell gültige PEM-Datei hoch, die bei der letzten Konfiguration oder Erneuerung der iOS-Verwaltung hochgeladen wurde. Weitere Informationen finden Sie unter [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Konfigurieren von SSL für Standortsystemrollen, die IIS verwenden
Wenn Sie Standortserver wiederherstellen, auf denen IIS ausgeführt wird und die vor dem Auftreten des Fehlers für HTTPS konfiguriert wurden, müssen Sie IIS für die Verwendung des Webserverzertifikats umkonfigurieren.

### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Erneutes Installieren von Hotfixes auf dem wiederhergestellten Standortserver
Nach der Wiederherstellung eines Standorts müssen Sie alle Hotfixes neu installieren, die auf den Standortserver angewendet worden waren. Zeigen Sie die Liste der zuvor installierten Hotfixes nach Abschluss der Standortwiederherstellung im Setup-Assistenten auf der Seite **Fertig gestellt** an. Diese Liste wird auch auf dem wiederhergestellten Standortserver unter **C:\ConfigMgrPostRecoveryActions.html** gespeichert.

### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Wiederherstellen von benutzerdefinierten Berichten auf dem Computer, auf dem Reporting Services ausgeführt wird
Wenn Sie benutzerdefinierte Reporting Services-Berichte erstellt haben und ein Fehler in Reporting Services auftritt, können Sie die Berichte wiederherstellen, sofern der Berichtsserver gesichert wurde. Weitere Informationen zum Wiederherstellen benutzerdefinierter Berichte in Reporting Services finden Sie unter [Sicherungs- und Wiederherstellungsvorgänge für eine Reporting Services-Installation](http://go.microsoft.com/fwlink/p/?LinkId=228724) in der Onlinedokumentation zu SQL Server 2008.

### <a name="recover-content-files"></a>Wiederherstellen von Inhaltsdateien
 Die Standortdatenbank enthält Informationen zum Speicherort der Inhaltsdateien auf dem Standortserver, jedoch werden die Inhaltsdateien beim normalen Sicherungs- und Wiederherstellungsverfahren nicht berücksichtigt. Zum vollständigen Wiederherstellen von Inhaltsdateien müssen Sie die Inhaltsbibliothek und die Paketquelldateien am Originalspeicherort wiederherstellen. Es gibt verschiedene Methoden zum Wiederherstellen von Inhaltsdateien. Am einfachsten ist die Wiederherstellung der Dateien aus einer Sicherung des Dateisystems des Standortservers.

 Wenn eine Sicherung des Dateisystems für die Paketquelldateien nicht verfügbar ist, müssen Sie diese Dateien wie beim ursprünglichen Erstellen des Pakets manuell kopieren bzw. herunterladen. Sie können die folgende Abfrage in SQL Server ausführen, um den Quellspeicherort für alle Pakete und Anwendungen zu ermitteln: `SELECT * FROM v_Package`. Sie können den Paketquellstandort anhand der ersten drei Zeichen der Paket-ID identifizieren. Wenn beispielsweise die Paket-ID „CEN00001“ lautet, ist „CEN“ der Standortcode für den Quellstandort. Paketquelldateien müssen an den gleichen Speicherort wiederhergestellt werden wie vor dem Fehler.

 Wenn eine Sicherung des Dateisystems mit der Inhaltsbibliothek nicht verfügbar ist, gibt es folgende Möglichkeiten zur Wiederherstellung:

-   **Importieren einer vorab bereitgestellten Inhaltsdatei**: Wenn Sie über eine Configuration Manager-Hierarchie verfügen, können Sie eine vorab bereitgestellte Inhaltsdatei mit allen Paketen und Anwendungen von einem anderen Speicherort erstellen und anschließend die vorab bereitgestellte Inhaltsdatei importieren, um die Inhaltsbibliothek auf dem Standortserver wiederherzustellen.

-   **Aktualisieren des Inhalts**: Wenn Sie die Aktion zum Aktualisieren des Inhalts für den Bereitstellungstyp eines Pakets oder einer Anwendung starten, wird der Inhalt aus der Paketquelle in die Inhaltsbibliothek kopiert. Die Paketquelldateien müssen im ursprünglichen Speicherort verfügbar sein, damit diese Aktion erfolgreich ausgeführt werden kann. Sie müssen diese Aktion für jedes Paket und jede Anwendung ausführen.

### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Wiederherstellen von benutzerdefinierten Softwareupdates auf dem Computer, auf dem Updates Publisher ausgeführt wird
Wenn Sie Updates Publisher-Datenbankdateien in Ihren Sicherungsplan einbezogen haben, können Sie die Datenbanken wiederherstellen, falls auf dem Computer, auf dem Updates Publisher ausgeführt wird, ein Fehler auftritt. Weitere Informationen zu Updates Publisher finden Sie unter [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) in der System Center TechNet-Bibliothek.

Gehen Sie wie folgt vor, um die Updates Publisher-Datenbank wiederherzustellen.

#### <a name="to-restore-the-updates-publisher-2011-database"></a>So stellen Sie die Updates Publisher 2011-Datenbank wieder her
1.  Installieren Sie Updates Publisher auf dem wiederhergestellten Computer neu.

2.  Kopieren Sie die Datenbankdatei (Scupdb.sdf) von Ihrem Sicherungsziel nach „%*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\“ auf dem Computer, auf dem Updates Publisher ausgeführt wird.

3.  Wenn Updates Publisher auf dem Computer von mehreren Benutzern ausgeführt wird, müssen Sie jede Datenbankdatei in den Speicherort für das entsprechende Benutzerprofil kopieren.

### <a name="user-state-migration-data"></a>Daten zur Benutzerzustandsmigration
In den Standortsystemeigenschaften für den Zustandsmigrationspunkt geben Sie die Ordner an, in denen die Daten zur Benutzerzustandsmigration gespeichert werden. Nach der Wiederherstellung eines Servers mit einem Ordner, in dem Daten zur Benutzerzustandsmigration gespeichert sind, müssen Sie die Daten zur Benutzerzustandsmigration auf dem Server manuell in den gleichen Ordner wiederherstellen, in dem sie vor dem Auftreten des Fehlers gespeichert waren.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Generieren der Zertifikate für Verteilungspunkte
Nach der Wiederherstellung eines Standorts kann die Datei „distmgr.log“ den folgenden Eintrag für einen oder mehrere Verteilungspunkte enthalten: **Fehler beim Entschlüsseln der Zertifikat-PFX-Daten**. Dieser Eintrag gibt an, dass die Verteilungspunktzertifikat-Daten nicht vom Standort entschlüsselt werden können. Zum Beheben dieses Problems müssen Sie das Zertifikat für die betroffenen Verteilungspunkte erneut generieren oder erneut importieren. Dies kann mithilfe des PowerShell-Cmdlets [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) erfolgen.

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Aktualisieren von Zertifikaten für cloudbasierte Verteilungspunkte
 Für Configuration Manager ist ein Verwaltungszertifikat erforderlich, das für die Kommunikation zwischen Standortserver und cloudbasiertem Verteilungspunkt verwendet wird. Nach einer Standortwiederherstellung müssen Sie die Zertifikate für cloudbasierte Verteilungspunkte aktualisieren.

## <a name="recover-a-secondary-site"></a>Wiederherstellen eines sekundären Standorts
 Die Sicherung der Datenbank an einem sekundären Standort wird von Configuration Manager nicht unterstützt, während die Wiederherstellung durch Neuinstallation des sekundären Standorts unterstützt wird. Bei einem Fehler auf einem sekundären Standort von Configuration Manager ist eine Wiederherstellung des sekundären Standorts erforderlich.

### <a name="requirements-for-reinstalling-a-secondary-site"></a>Anforderungen für die Neuinstallation eines sekundären Standorts
-   Der Computer muss alle Voraussetzungen für einen sekundären Standort erfüllen, und es müssen die entsprechenden Sicherheitsrechte konfiguriert sein.
-   Sie müssen den gleichen Installationspfad verwenden, der für den fehlerhaften Standort verwendet wurde.
-   Sie müssen einen Computer mit derselben Konfiguration wie der des fehlerhaften Computers verwenden, wie etwa dessen FQDN, um den sekundären Standort erfolgreich wiederherzustellen.
-   Der Computer muss die gleiche SQL Server-Konfiguration wie der ausgefallene Standort aufweisen.
  -   Während der Wiederherstellung eines sekundären Standorts wird SQL Server Express nicht von Configuration Manager installiert, wenn diese Software noch nicht auf dem Computer installiert ist.
  -   Sie müssen dieselbe Version und Instanz von SQL Server verwenden, die Sie vor Auftreten des Fehlers für die sekundäre Standortdatenbank verwendet haben.

### <a name="to-recover-a-secondary-site"></a>So stellen Sie einen sekundären Standort wieder her
Verwenden Sie zum Wiederherstellen eines sekundären Standorts in der Configuration Manager-Konsole unter dem Knoten **Standorte** die Aktion **Sekundären Standort wiederherstellen**. Im Gegensatz zur Wiederherstellung für einen Standort der zentralen Verwaltung oder einen primären Standort verwendet die Wiederherstellung für einen sekundären Standort keine Sicherungsdatei und installiert stattdessen die sekundären Standortdateien auf dem fehlerhaften Computer des sekundären Standorts neu. Nach der Neuinstallation des Standorts werden die Daten des sekundären Standorts mit Daten vom übergeordneten primären Standort neu initialisiert.

Während des Wiederherstellungsprozesses wird von Configuration Manager überprüft, ob die Inhaltsbibliothek auf dem Computer des sekundären Standorts vorhanden und der entsprechende Inhalt verfügbar ist. Der sekundäre Standort verwendet die vorhandene Inhaltsbibliothek, wenn sie den entsprechenden Inhalt enthält. Andernfalls muss zum Wiederherstellen der Inhaltsbibliothek eines wiederhergestellten sekundären Standorts der Inhalt für diesen wiederhergestellten Standort verteilt oder vorab bereitgestellt werden.

Bei einem Verteilungspunkt, der sich nicht am sekundären Standort befindet, müssen Sie während der Wiederherstellung des sekundären Standorts den Verteilungspunkt nicht neu installieren. Nach der Wiederherstellung des sekundären Standorts wird der Standort automatisch mit dem Verteilungspunkt synchronisiert.

Sie können den Status der Wiederherstellung des sekundären Standorts überprüfen, indem Sie in der Configuration Manager-Konsole unter dem Knoten **Standorte** die Aktion **Installationsstatus anzeigen** verwenden.
