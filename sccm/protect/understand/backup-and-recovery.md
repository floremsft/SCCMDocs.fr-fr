---
title: Sichern von Standorten | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Standorte vor einen Ausfall oder Datenverlust in System Center Configuration Manager sichern.
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: "22"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7deb00d4b67eabf3238907b337a9d0367c3d99cc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="back-up-a-configuration-manager-site"></a>Sichern eines Configuration Manager-Standorts

*Gilt für: System Center Configuration Manager (Current Branch)*

Bereiten Sie Sicherungs- und Wiederherstellungs-Ansätze vor, um Datenverluste zu vermeiden. Für Configuration Manager-Standorte kann ein Ansatz für die Sicherung und Wiederherstellung dazu beitragen, Standorte und Hierarchien schneller und mit geringstem Datenverlust wiederherzustellen.  

Die Abschnitte in diesem Thema können Ihnen beim Sichern Ihrer Standorte helfen. Informationen zur Wiederherstellung eines Standorts finden Sie unter [Wiederherstellung für Configuration Manager](/sccm/protect/understand/recover-sites).  

## <a name="considerations-before-creating-a-backup"></a>Überlegungen vor dem Erstellen einer Sicherung  
-   **Wenn Sie eine SQL Server AlwaysOn-Verfügbarkeitsgruppe zum Hosten der Standortdatenbank verwenden:** Ändern Sie Ihre Sicherungs- und Wiederherstellungspläne gemäß der Anleitung unter [Vorbereiten zur Verwendung von SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup).

-   Configuration Manager kann die Standortdatenbank aus dem Configuration Manager-Sicherungswartungstask oder aus der Standortdatenbanksicherung wiederherstellen, die Sie mit einem anderen Prozess erstellen.   

    Beispielsweise können Sie die Standortdatenbank anhand einer Sicherung wiederherstellen, die im Rahmen des Microsoft SQL Server-Wartungsplans erstellt wurde. Sie können auch eine Sicherung, die mithilfe von Data Protection Manager (DPM) erstellt wurde, zur Sicherung Ihrer Standortdatenbank verwenden.

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Verwenden von Data Protection Manager zur Sicherung der Standortdatenbank
Sie können die Standortdatenbank mit System Center 2012 Data Protection Manager (DPM) sichern.

Sie müssen in DPM eine neue Schutzgruppe für den Standortdatenbankcomputer erstellen. Auf der Seite **Gruppenmitglieder auswählen** des Assistenten zum Erstellen einer neuen Schutzgruppe wählen Sie den SMS-Writer-Dienst aus der Datenquellenliste und anschließend die Standortdatenbank als geeignetes Mitglied aus. Weitere Informationen zur Verwendung DPM zur Sicherung Ihrer Standortdatenbank finden Sie in der [Data Protection Manager-Dokumentationsbibliothek](http://go.microsoft.com/fwlink/?LinkId=272772) auf der TechNet-Webseite.  

> [!IMPORTANT]  
>  Configuration Manager unterstützt die DPM-Sicherung für einen SQL Server-Cluster nicht, der eine benannte Instanz verwendet, wohl aber eine DPM-Sicherung auf einem SQL Server-Cluster, der die Standardinstanz von SQL Server verwendet.  

 Nachdem Sie die Standortdatenbank wiederhergestellt haben, befolgen Sie die Schritte im Setup, um den Standort wiederherzustellen. Wählen Sie die Wiederherstellungsoption **Manuell wiederhergestellte Standortdatenbank verwenden** aus, um die Standortdatenbank zu verwenden, die Sie mithilfe von Data Protection Manager wiederhergestellt haben.  

## <a name="backup-maintenance-task"></a>Sicherungswartungstask
Durch Planen des vordefinierten Wartungstasks „Standortserver sichern“ können Sie die Sicherung von Configuration Manager-Standorten automatisieren. Dieser Task:

-   Wird nach einem Zeitplan ausgeführt
-   Sichert die Standortdatenbank
-   Sichert bestimmte Registrierungsschlüssel
-   Sichert bestimmte Ordner und Dateien
-   Sichert den Ordner [CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder)   

Planen Sie die Ausführung des Standardtasks für die Standortsicherung mindestens alle 5 Tage. Der Grund dafür ist, dass Configuration Manager einen Zeitraum für die *Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server* von fünf Tagen verwendet.  (Siehe [Beibehaltungsdauer der SQL Server-Änderungsnachverfolgung](/sccm/protect/understand/recover-sites#bkmk_SQLretention) im Thema zum Wiederherstellen von Standorten.)

Zur Vereinfachung des Sicherungsprozesses können Sie eine Datei **AfterBackup.bat** erstellen, um nach der erfolgreichen Ausführung des Sicherungswartungstasks weitere Aktionen automatisch auszuführen. Die Datei „AfterBackup.bat“ wird normalerweise zur Archivierung der Sicherungsmomentaufnahme an einem sicheren Speicherort verwendet. Sie können mit der Datei „AfterBackup.bat“ auch Dateien in den Sicherungsordner kopieren und andere zusätzliche Sicherungstasks starten.  

Sie können einen Standort der zentralen Verwaltung und einen primären Standort sichern. Bei sekundären Standorten oder Standortsystemservern hingegen wird eine Sicherung nicht unterstützt.

Wenn der Configuration Manager-Sicherungsdienst ausgeführt wird, läuft dieser Vorgang den in der Sicherungssteuerungsdatei (**&lt;Configuration Manager-Installationsordner\>\Inboxes\Smsbkup.box\Smsbkup.ctl**) definierten Anweisungen entsprechend ab. Sie können die Sicherungssteuerungsdatei ändern, um das Verhalten des Sicherungsdienstes zu ändern.  

Informationen zum Status der Standortsicherung werden in die Datei **Smsbkup.log** geschrieben. Diese Datei wird in dem Zielordner erstellt, den Sie in den Eigenschaften des Wartungstasks „Standortserver sichern“ angeben.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>So aktivieren Sie den Wartungstask zur Standortsicherung  

1.  Öffnen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** > **Standorte**.  

2.  Wählen Sie den Standort aus, an dem Sie den Wartungstask zur Standortsicherung aktivieren möchten.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** die **Standortwartungstasks**.  

4.  Wählen Sie **Standortserver sichern**  >  **Bearbeiten** aus.  

5.  Wählen Sie **Diese Aufgabe aktivieren** > **Pfade festlegen** aus, um das Sicherungsziel anzugeben. Hierzu stehen Ihnen folgende Optionen zur Verfügung:  

    > [!IMPORTANT]  
    >  Speichern Sie die Dateien an einem sicheren Ort, um einer Manipulation der Sicherungsdateien vorzubeugen. Der sicherste Pfad für eine Sicherung ist ein lokales Laufwerk, sodass Sie NTFS-Dateisystemberechtigungen für den Ordner einrichten können. Configuration Manager verschlüsselt nicht die Sicherungsdaten, die im den Sicherungspfad gespeichert sind.  

    -   **Lokales Laufwerk auf Standortserver für Standortdaten und -datenbank**: Bei Auswahl dieser Option werden die Sicherungsdateien für den Standort und die Standortdatenbank im angegebenen Pfad auf dem lokalen Laufwerk des Standortservers gespeichert. Sie müssen den lokalen Ordner erstellen, bevor der Sicherungstask ausgeführt wird. Das lokale Systemkonto auf dem Standortserver muss über die NTFS-Dateisystemberechtigung **Schreiben** für den lokalen Ordner verfügen, der für die Sicherung des Standorts vorgesehen ist. Das lokale Systemkonto auf dem Computer, auf dem SQL Server ausgeführt wird, muss über die NTFS-Berechtigung **Schreiben** für den Ordner verfügen, der für die Sicherung der Standortdatenbank vorgesehen ist.  

    -   **Netzwerkpfad (UNC-Name) für Standortdaten und -datenbank**: Bei Auswahl dieser Option werden die Sicherungsdateien für den Standort und die Standortdatenbank im angegebenen UNC-Pfad gespeichert. Sie müssen die Freigabe erstellen, bevor der Sicherungstask ausgeführt wird. Das Computerkonto des Standortservers sowie das Computerkonto von SQL Server, so SQL Server auf einem anderen Computer installiert ist, müssen die NTFS-Berechtigung **Schreiben** sowie Freigabeberechtigungen für den freigegebenen Netzwerkordner aufweisen.  

    -   **Lokale Laufwerke auf dem Standortserver und SQL Server**: Bei Auswahl dieser Option werden die Sicherungsdateien für den Standort im angegebenen Pfad auf dem lokalen Laufwerk des Standortservers gespeichert, und die Sicherungsdateien für die Standortdatenbank werden im angegebenen Pfad auf dem lokalen Laufwerk des Standortdatenbankservers gespeichert. Sie müssen die lokalen Ordner erstellen, bevor der Sicherungstask ausgeführt wird. Für das Computerkonto des Standortservers müssen die NTFS-Berechtigungen **Schreiben** für den Ordner vorliegen, den Sie auf dem Standortserver erstellen. Für das Computerkonto des SQL Servers müssen die NTFS-Berechtigungen **Schreiben** für den Ordner vorliegen, den Sie auf dem Standortdatenbankserver erstellen. Diese Option ist nur verfügbar, wenn die Standortdatenbank nicht auf dem Standortserver installiert ist.  

    > [!NOTE]  
    >   Die Option zum Durchsuchen des Sicherungsziels ist nur verfügbar, wenn Sie den UNC-Pfad des Sicherungsziels angeben.

    > Der Ordner- oder Freigabename, der für das Sicherungsziel verwendet wird, darf keine Unicode-Zeichen enthalten.  

6.  Konfigurieren Sie einen Zeitplan für den Standortsicherungstask. Empfehlenswert ist ein Sicherungszeitplan, der außerhalb der Arbeitszeit liegt. Falls Sie über eine Hierarchie verfügen, empfiehlt sich ein Zeitplan, der mindestens zweimal pro Woche ausgeführt wird. Auf diese Weise bleibt bei einem Standortausfall ein Maximum an Daten erhalten.  

    Wenn Sie die Configuration Manager-Konsole auf dem gleichen Standortserver ausführen, den Sie für die Sicherung konfigurieren, wird vom Wartungstask „Standortserver sichern“ die lokale Zeit für den Zeitplan verwendet. Wenn Sie die Configuration Manager-Konsole auf einem Computer außerhalb des Standorts ausführen, den Sie für die Sicherung konfigurieren, wird vom Wartungstask „Standortserver sichern“ UTC (Coordinated Universal Time, koordinierte Weltzeit) für den Zeitplan verwendet.  

7.  Geben Sie an, ob eine Warnung generiert werden soll, wenn beim Standortsicherungstask ein Fehler auftritt, und klicken Sie auf **OK**. Klicken Sie anschließend auf **OK**. Wenn diese Option ausgewählt ist, wird von Configuration Manager bei einem Sicherungsfehler eine kritische Warnung generiert. Details zu dieser Warnung können Sie im Arbeitsbereich **Überwachung** im Knoten **Warnungen** einsehen.  

 Überprüfen Sie als nächstes, ob der Wartungstask „Standortserver sichern“ ausgeführt wird, um sicherzustellen, dass die Sicherungen erstellt werden.  

#### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>So überprüfen Sie, ob der Wartungstask „Standortserver sichern“ ausgeführt wird  
Überprüfen Sie wie folgt, ob der Wartungstask zur Standortsicherung ausgeführt wird:  

-   Überprüfen Sie den Zeitstempel auf den Dateien im Sicherungszielordner, die vom Task erstellt wurden. Überprüfen Sie, ob der Zeitstempel aktualisiert wurde und die Zeitangabe mit der Zeit übereinstimmt, zu der die Ausführung des Tasks laut Zeitplan zuletzt vorgesehen war.  

-   Prüfen Sie im Arbeitsbereich **Überwachung** im Knoten **Komponentenstatus** die Statusmeldungen für SMS_SITE_BACKUP. Wenn die Standortsicherung erfolgreich abgeschlossen ist, wird die Meldungs-ID 5035 angezeigt. Dies bedeutet, dass die Standortsicherung ohne Fehler abgeschlossen wurde.  

-   Wenn vom Wartungstask „Standortserver sichern“ bei einem Sicherungsfehler konfigurationsgemäß eine Warnung generiert wird, können Sie die Systemfehler im Arbeitsbereich **Überwachung** im Knoten **Warnungen** überprüfen.  

-   Prüfen Sie die Datei „Smsbkup.log“ unter „&lt;*Configuration Manager-Installationsordner*>\Logs“ auf Warnungen und Fehler. Wenn die Standortsicherung erfolgreich abgeschlossen ist, wird `Backup completed` zusammen mit einem Zeitstempel und der Meldungs-ID `STATMSG: ID=5035`angezeigt.  

    > [!TIP]  
    >  Wenn beim Sicherungswartungstask ein Fehler auftritt, können Sie den Task durch Anhalten und Neustarten des Dienstes SMS_SITE_BACKUP neu starten.  

## <a name="archive-the-backup-snapshot"></a>Archivieren der Sicherungsmomentaufnahme  
Bei der ersten Ausführung des Wartungstasks „Standortserver sichern“ wird eine Sicherungsmomentaufnahme erstellt, mit der Sie Ihren Standortserver nach einem Fehler wiederherstellen können. Wenn der Sicherungstask im Verlauf späterer Zyklen erneut ausgeführt wird, erstellt er jeweils einen neuen Sicherungssnapshot, mit dem der vorherige Snapshot überschrieben wird. Für einen Standort gibt es daher immer nur eine Sicherungsmomentaufnahme, und es ist nicht möglich, eine frühere Sicherungsmomentaufnahme abzurufen.  

Aus den folgenden Gründen wird empfohlen, mehrere Archive der Sicherungsmomentaufnahme aufzubewahren:  

-   Es kommt häufig vor, dass Sicherungsmedien ausfallen, verlegt werden oder nur eine unvollständige Sicherung enthalten. Das Wiederherstellen eines ausgefallenen eigenständigen primären Standorts anhand einer älteren Sicherung ist besser als das Wiederherstellen ohne Sicherung. Bei einem Standortserver in einer Hierarchie muss die Sicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server liegen. Andernfalls ist die Sicherung nicht erforderlich.  

-   Eine Beschädigung im Standort kann über mehrere Sicherungszyklen hinweg unentdeckt bleiben. Sie müssen möglicherweise eine Sicherungsmomentaufnahme verwenden, die vor der Beschädigung des Standorts erstellt wurde. Dies gilt für einen eigenständigen primären Standort und Standorte in einer Hierarchie, bei denen die Sicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server liegt.  

-   Für den Standort gibt es möglicherweise keine Sicherungsmomentaufnahme, beispielsweise weil beim Wartungstask „Standortserver sichern“ ein Fehler aufgetreten ist. Da der Sicherungstask den vorherigen Sicherungssnapshot entfernt, bevor er mit dem Sichern der aktuellen Daten beginnt, gibt es zeitweise keinen gültigen Sicherungssnapshot.  

## <a name="using-the-afterbackupbat-file"></a>Verwenden der Datei „AfterBackup.bat“  
Nach der erfolgreichen Sicherung des Standorts wird vom Task „Standortserver sichern“ automatisch versucht, eine Datei namens AfterBackup.bat auszuführen. Sie müssen die Datei „AfterBackup.bat“ manuell in „&lt;*Configuration Manager-Installationsordner*>\Inboxes\Smsbkup“ erstellen. Wenn eine Datei „AfterBackup.bat“ vorhanden ist und sich im richtigen Ordner befindet, wird sie nach Abschluss des Sicherungstasks automatisch ausgeführt.

Mit der Datei AfterBackup.bat können Sie die Sicherungsmomentaufnahme am Ende jedes Sicherungsvorgangs archivieren und automatisch andere nach der Sicherung erforderliche Tasks ausführen, die nicht zum Wartungstask „Standortserver sichern“ gehören. Mit der Datei AfterBackup.bat werden die Archivierungs- und Sicherungsvorgänge integriert. Dadurch wird sichergestellt, dass jede neue Sicherungsmomentaufnahme archiviert wird.

Wenn die Datei AfterBackup.bat nicht vorhanden ist, wird sie vom Sicherungstask übersprungen. Dies hat keine Auswirkungen auf den Sicherungsvorgang. Prüfen Sie im Arbeitsbereich **Überwachung** im Knoten **Komponentenstatus** die Statusmeldungen für SMS_SITE_BACKUP. Daran erkennen Sie, ob die Datei "AfterBackup.bat" vom Standortsicherungstask erfolgreich ausgeführt wurde. Wenn die Befehlsdatei „AfterBackup.bat“ erfolgreich gestartet wurde, wird die Meldungs-ID 5040 angezeigt.  

> [!TIP]  
>  Sie müssen ein Kopierbefehlstool wie [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408) in der Batchdatei verwenden, um die Datei „AfterBackup.bat“ zum Archivieren der Sicherungsdateien für den Standortserver zu erstellen. Beispielsweise können Sie die Datei „AfterBackup.bat“ erstellen und der ersten Zeile Folgendes hinzufügen: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

 Die Datei AfterBackup.bat ist zwar zum Archivieren von Sicherungsmomentaufnahmen vorgesehen, Sie aber können auch eine Datei AfterBackup.bat erstellen, um am Ende jedes Sicherungsvorgangs zusätzliche Tasks auszuführen.  

##  <a name="supplemental-backup-tasks"></a>Zusätzliche Sicherungstasks  
Mit dem Wartungstask „Standortserver sichern“ wird eine Sicherungsmomentaufnahme für die Standortserverdateien und die Standortdatenbank erstellt. Beim Erstellen einer Sicherungsstrategie müssen Sie aber noch andere Elemente berücksichtigen, die nicht gesichert werden. In den folgenden Abschnitten erfahren Sie, wie Sie eine Configuration Manager-Sicherungsstrategie vervollständigen.  

### <a name="back-up-custom-reporting-services-reports"></a>Sichern benutzerdefinierter Reporting Services-Berichte  
Wenn Sie vordefinierte Reporting Services-Berichte geändert oder benutzerdefinierte Reporting Services-Berichte erstellt haben, stellt die Sicherung der Berichtsserver-Datenbankdateien eine wichtige Komponente Ihrer Sicherungsstrategie dar. Die Berichtsserver-Sicherung muss eine Sicherung der Quelldateien für Berichte und Modelle, Verschlüsselungsschlüssel, benutzerdefinierte Assemblys oder Erweiterungen, Konfigurationsdateien, in benutzerdefinierten Berichten verwendete benutzerdefinierte SQL Server-Ansichten, benutzerdefinierte gespeicherte Prozeduren usw. umfassen.  

> [!IMPORTANT]  
>  Wenn Configuration Manager auf eine neuere Version aktualisiert wird, werden die vordefinierten Berichte möglicherweise von neuen Berichten überschrieben. Wenn Sie einen vordefinierten Bericht ändern, sichern Sie ihn, und stellen Sie den Bericht dann in Reporting Services wieder her.  

 Weitere Informationen zum Sichern benutzerdefinierter Berichte in Reporting Services finden Sie unter [Sicherungs- und Wiederherstellungsvorgänge für eine Reporting Services-Installation](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) in der Onlinedokumentation zu SQL Server 2014.  

### <a name="back-up-content-files"></a>Sichern von Inhaltsdateien  
Die Inhaltsbibliothek in Configuration Manager ist der Ort, an dem alle Inhaltsdateien für Softwareupdates, Anwendungen, Betriebssystembereitstellungen usw. gespeichert werden. Sie befindet sich auf dem Standortserver und an jedem Verteilungspunkt. Vom Wartungstask „Standortserver sichern“ wird keine Sicherung der Inhaltsbibliothek oder der Paketquelldateien ausgeführt. Beim Ausfall eines Standortservers werden die Informationen zu den Dateien der Inhaltsbibliothek in der Standortdatenbank wiederhergestellt. Sie müssen jedoch die Inhaltsbibliothek sowie die Paketquelldateien auf dem Standortserver wiederherstellen.  

-   **Inhaltsbibliothek**: Die Inhaltsbibliothek muss wiederhergestellt werden, damit Sie Inhalt erneut an Verteilungspunkte verteilen können. Wenn Sie die Neuverteilung des Inhalts starten, werden die Dateien von Configuration Manager aus der Inhaltsbibliothek auf dem Standortserver auf die Verteilungspunkte kopiert. Die Inhaltsbibliothek für den Standortserver befindet sich im Ordner „SCCMContentLib“. Dieser Ordner wiederum befindet sich in der Regel auf dem Laufwerk, auf dem zum Zeitpunkt der Standortinstallation am meisten freier Speicher verfügbar war.  

-   **Paketquelldateien**: Die Paketquelldateien müssen wiederhergestellt werden, damit Sie ein Update des Inhalts an Verteilungspunkten ausführen können. Wenn Sie ein Inhaltsupdate starten, werden neue oder geänderte Dateien von Configuration Manager aus der Paketquelle in die Inhaltsbibliothek kopiert. Von dort werden die Dateien auf die zugeordneten Verteilungspunkte kopiert. Sie können die folgende Abfrage in SQL Server ausführen, um den Quellspeicherort für alle Pakete und Anwendungen zu ermitteln: `SELECT * FROM v_Package`. Sie können den Paketquellstandort anhand der ersten drei Zeichen der Paket-ID identifizieren. Wenn beispielsweise die Paket-ID „CEN00001“ lautet, ist „CEN“ der Standortcode für den Quellstandort. Paketquelldateien müssen an den gleichen Speicherort wiederhergestellt werden wie vor dem Fehler.  

 Achten Sie darauf, bei der Dateisystemsicherung für den Standortserver sowohl die Inhaltsbibliothek als auch die Paketquellspeicherorte einzuschließen.  

### <a name="back-up-custom-software-updates"></a>Sichern benutzerdefinierter Softwareupdates  
 System Center Updates Publisher 2011 ist ein eigenständiges Tool, mit dem Sie benutzerdefinierte Softwareupdates in Windows Server Update Services (WSUS) veröffentlichen, die Softwareupdates mit Configuration Manager synchronisieren, die Konformität der Softwareupdates bewerten sowie die benutzerdefinierten Softwareupdates für Clients bereitstellen können. Updates Publisher verwendet eine lokale Datenbank für das Softwareupdaterepository. Wenn Sie den Updates Publisher zur Verwaltung benutzerdefinierter Softwareupdates verwenden, legen Sie fest, ob die Updates Publisher-Datenbank in Ihrem Sicherungsplan enthalten sein muss. Weitere Informationen zu Updates Publisher finden Sie unter [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) in der System Center TechNet-Bibliothek.  

 Gehen Sie wie folgt vor, um die Updates Publisher-Datenbank zu sichern.  

#### <a name="to-back-up-the-updates-publisher-2011-database"></a>So sichern Sie die Updates Publisher 2011-Datenbank  

1.  Suchen Sie auf dem Computer, auf dem Updates Publisher ausgeführt wird, die Updates Publisher-Datenbankdatei („Scupdb.sdf“) in „%*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\“. Für jeden Benutzer, der Updates Publisher ausführt, gibt es eine eigene Datenbankdatei.  

2.  Kopieren Sie die Datenbankdatei in das Sicherungsziel. Wenn das Sicherungsziel beispielsweise „E:\ConfigMgr_Backup“ lautet, können Sie die Updates Publisher-Datenbankdatei nach „E:\ConfigMgr_Backup\SCUP2011“ kopieren.  

    > [!TIP]  
    >  Wenn es auf einem Computer mehrere Datenbankdateien gibt, empfiehlt es sich, die Datei in einem Unterordner zu speichern, der den Namen des mit der Datenbankdatei verbundenen Benutzerprofils trägt. Beispielsweise kann sich eine Datenbankdatei in E:\ConfigMgr_Backup\SCUP2011\User1 befinden und eine andere Datenbankdatei in E:\ConfigMgr_Backup\SCUP2011\User2.  

## <a name="user-state-migration-data"></a>Daten zur Benutzerzustandsmigration  
Mit Configuration Manager-Tasksequenzen können Sie bei der Betriebssystembereitstellung die Benutzerstatusdaten erfassen und wiederherstellen, wenn Sie den Benutzerstatus des aktuellen Betriebssystems beibehalten möchten. Die Ordner, in denen die Benutzerzustandsdaten gespeichert werden, werden in den Eigenschaften des Zustandsmigrationspunkts aufgeführt. Diese Daten zur Benutzerzustandsmigration werden vom Wartungstask „Standortserver sichern“ nicht gesichert. Im Rahmen Ihres Sicherungsplans müssen Sie die Ordner, in denen die Daten zur Benutzerzustandsmigration gespeichert werden, manuell sichern.   

### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>So bestimmen Sie die Ordner, in denen die Daten zur Benutzerzustandsmigration gespeichert werden  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Standortkonfiguration**, und wählen Sie anschließend **Server und Standortsystemrollen**.  

3.  Wählen Sie das Standortsystem aus, auf dem die Rolle „Zustandsmigration“ gehostet wird. Wählen Sie anschließend in **Standortsystemrollen** die Option **Zustandsmigrationspunkt**aus.  


4.  Klicken Sie auf der Registerkarte **Standortrolle** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  
5.  Die Ordner, in denen die Daten zur Benutzerzustandsmigration gespeichert werden, werden auf der Registerkarte **Allgemein** im Abschnitt **Ordnerdetails** aufgeführt.  



## <a name="about-the-sms-writer-service"></a>Informationen zum SMS-Writer-Dienst  
Während des Sicherungsprozesses findet zwischen dem SMS-Writer-Dienst und dem Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) eine Interaktion statt. Der SMS-Writer-Dienst muss ausgeführt werden, damit die Configuration Manager-Standortsicherung erfolgreich abgeschlossen werden kann.  

### <a name="purpose"></a>Zweck  
SMS-Writer wird beim VSS registriert und an dessen Schnittstellen und Ereignissse gebunden. Wenn vom VSS Ereignisse übertragen oder bestimmte Benachrichtigungen an SMS-Writer gesendet werden, wird von SMS-Writer daraufhin eine entsprechende Aktion ausgeführt. Zunächst wird die Sicherungssteuerungsdatei „smsbkup.ctl“, die sich unter „&lt;*Configuration Manager-Installationspfad*>\inboxes\smsbkup.box“ befindet, von SMS-Writer gelesen, und dann werden die zu sichernden Dateien und Daten ermittelt. Anschließend werden von SMS-Writer Metadaten erstellt, die sich aus verschiedenen Komponenten zusammensetzen. Dabei dienen die ermittelten Informationen sowie bestimmte Daten aus den SMS-Registrierungsschlüsseln und Unterschlüsseln als Grundlage. Die Metadaten werden an den VSS gesendet, wenn sie angefordert werden. Vom VSS werden die Metadaten wiederum an die anfordernde Anwendung gesendet (Configuration Manager-Sicherungs-Manager). Vom Sicherungs-Manager werden die zu sichernden Daten ausgewählt und über den VSS an SMS-Writer gesendet. Von SMS-Writer werden geeignete Maßnahmen zur Vorbereitung der Sicherung ergriffen. Vom VSS wird ein Ereignis gesendet, wenn er für die Momentaufnahme bereit ist. Daraufhin werden von SMS-Write sämtliche Configuration Manager-Dienste angehalten, und es wird sichergestellt, dass die Configuration Manager-Aktivitäten während der Erstellung der Momentaufnahme gesperrt sind. Nachdem die Momentaufnahme erstellt wurde, werden die Dienste und Aktivitäten von SMS-Writer neu gestartet.  

Der SMS-Writer-Dienst wird automatisch installiert. Dieser Dienst muss ausgeführt werden, wenn eine Sicherungs- oder Wiederherstellungsanforderung von der VSS-Anwendung eingeht.  

### <a name="writer-id"></a>Writer-ID  
Die Writer-ID für SMS-Writer lautet: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Berechtigungen  
Der SMS-Writer-Dienst muss unter dem lokalen Systemkonto ausgeführt werden.  

### <a name="volume-shadow-copy-service"></a>Volumeschattenkopie-Dienst  
Der Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) ist ein Satz COM APIs, mit denen ein Framework implementiert wird. Dank dieses Frameworks können Volumesicherungen ausgeführt werden, während von Anwendungen auf einem System weiterhin auf die Volumes geschrieben wird. Mit dem VSS wird eine konsistente Schnittstelle bereitgestellt, mit der Benutzeranwendungen, die zum Ausführen eines Updates für Daten auf einem Datenträger dienen (SMS-Writer-Dienst), und Benutzeranwendungen, die zur Anwendungssicherung verwendet werden (Sicherungs-Manager-Dienst), koordiniert werden können. Weitere Informationen finden Sie im Thema [Volume Shadow Copy Service](http://go.microsoft.com/fwlink/p/?LinkId=241968) (Volumeschattenkopie-Dienst) im Windows Server TechCenter.  

## <a name="next-steps"></a>Nächste Schritte
Üben Sie nach der Erstellung einer Sicherung die [Standortwiederherstellung](/sccm/protect/understand/recover-sites) mit dieser Sicherung. Dadurch können Sie sich mit dem Wiederherstellungsprozess vertraut machen, bevor Sie ihn verwenden müssen, und können so überprüfen, ob die Sicherung für den beabsichtigten Zweck erfolgreich ausgeführt wurde.  
