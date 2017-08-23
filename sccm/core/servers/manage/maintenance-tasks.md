---
title: Wartungstasks | Microsoft-Dokumentation
description: "Hier finden Sie Informationen dazu, welche Wartungstasks für Configuration Manager-Standorte und -Hierarchien zu welchem Zeitpunkt durchgeführt werden müssen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 90b6e4434abc5573a364c769bd835e08e5dff16d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>Wartungstasks für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager-Standorte und -Hierarchien müssen regelmäßig gewartet und überwacht werden, damit Dienste effektiv und ohne Unterbrechungen bereitgestellt werden können. Durch regelmäßige Wartung wird die ordnungsgemäße, effiziente Funktionsfähigkeit von Hardware, Software und der Configuration Manager-Standortdatenbank dauerhaft sichergestellt. Durch optimale Leistung wird das Risiko eines Ausfalls erheblich reduziert.  

 Informationen zum Konfigurieren von Benachrichtigungen sowie zum Überwachen der Integrität von Configuration Manager mit dem Statussystem finden Sie unter [Use alerts and the status system for System Center Configuration Manager (Verwenden von Benachrichtigungen und Statussystem für System Center Configuration Manager)](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   [Wartungstasks](#bkmk_MTs)  

##  <a name="bkmk_MTs"></a> Wartungstasks  
 Eine regelmäßige Wartung ist wichtig, um den ordnungsgemäßen Standortbetrieb zu gewährleisten. Führen Sie ein tägliches Wartungsprotokoll, um zu dokumentieren, wann die Wartung von wem vorgenommen wurde, und um alle wartungsrelevanten Kommentare de den ausgeführten Tasks aufzuzeichnen.  

### <a name="when-to-do-common-maintenance-tasks"></a>Wahl des Zeitpunkts für die Ausführung allgemeiner Wartungstasks  
 Für die Wartung Ihres Standorts sollten Sie eine tägliche oder zumindest wöchentliche Wartung in Erwägung ziehen. Für einige Aufgaben wird ein anderer Zeitplan vonnöten sein. Zur allgemeinen Wartung können sowohl die integrierten Wartungstasks gezählt werden als auch andere Tasks wie die Kontowartung, die Sie zur Einhaltung Ihrer Unternehmensrichtlinien verwenden.  

 Orientieren Sie sich an den folgenden Informationen, wenn Sie den Ausführungszeitpunkt verschiedener Wartungstasks planen. Verwenden Sie diese Listen als Ausgangspunkt, und fügen Sie gegebenenfalls Tasks hinzu, die Sie benötigen.  

**Tägliche Aufgaben**   
Sie sollten erwägen, die folgenden Wartungstasks täglich durchzuführen:  

-   Überprüfen, ob die vordefinierten Wartungstasks, die für die tägliche Durchführung geplant sind, erfolgreich ausgeführt werden.  

-   Überprüfen des Configuration Manager-Datenbankstatus.  

-   Überprüfen Sie den Status des Standortservers.  

-   Überprüfen der Posteingänge des Configuration Manager-Standortsystems auf Dateirückstände.  

-   Überprüfen Sie den Status der Standortsysteme.  

-   Überprüfen Sie die Betriebssystemereignisprotokolle auf den Standortsystemen.  

-   Überprüfen Sie das SQL Server-Fehlerprotokoll auf dem Standortdatenbankcomputer.  

-   Überprüfen Sie die Systemleistung.  

-   Überprüfen von Configuration Manager-Warnmeldungen.  

**Wöchentliche Aufgaben**   
Sie sollten erwägen, die folgenden Wartungstasks wöchentlich durchzuführen:  

-   Überprüfen, ob die vordefinierten Wartungstasks, die für die wöchentliche Durchführung geplant sind, erfolgreich ausgeführt werden  

-   Löschen Sie nicht erforderliche Dateien von Standortsystemen.  

-   Erstellen und verteilen Sie ggf. Endbenutzerberichte.  

-   Sichern Sie Anwendungs-, Sicherheits- und Systemereignisprotokolle und setzen Sie sie zurück.  

-   Überprüfen der Größe der Standortdatenbank und Sicherstellen, dass ausreichend Speicherplatz auf dem Standortdatenbankserver verfügbar ist, um dem Wachstum der Standortdatenbank gerecht zu werden  

-   Durchführen einer SQL Server-Datenbankwartung für die Standortdatenbank entsprechend Ihrem SQL Server-Wartungsplan.  

-   Überprüfen Sie den verfügbaren Speicherplatz auf allen Standortsystemen.  

-   Führen Sie auf allen Standortsystemen Festplattendefragmentierungstools aus.  

**Regelmäßige Tasks**   
Einige Tasks, die jedoch nicht während der täglichen oder wöchentlichen Wartung durchgeführt werden müssen, sind dennoch wichtig, um die Integrität Ihres Standorts zu gewährleisten. Diese Tasks stellen zudem sicher, dass die Sicherheit sowie die Wiederherstellungspläne auf dem neuesten Stand sind. Bei den folgenden Wartungstasks empfiehlt sich unter Umständen eine häufigere Ausführung als täglich oder wöchentlich:  

-   Ggf. Ändern von Konten und Kennwörtern gemäß Ihrem Sicherheitsplan.  

-   Überprüfen des Wartungsplans um sicherzustellen, dass geplante Wartungstasks in Abhängigkeit von den konfigurierten Standorteinstellungen ordnungsgemäß und effektiv geplant sind.  

-   Überprüfen des Configuration Manager-Hierarchieentwurfs auf erforderliche Änderungen.  

-   Prüfen der Netzwerkleistung zur Sicherstellung, dass keine Änderungen vorgenommen wurden, die Standortvorgänge beeinträchtigen.  

-   Prüfen, dass Active Directory-Einstellungen, die sich auf Standortvorgänge auswirken, nicht geändert wurden. Stellen Sie beispielsweise sicher, dass Subnetze, die als Grenzen für einen Configuration Manager-Standort verwendeten Active Directory-Standorten zugewiesen sind, nicht geändert wurden.  

-   Überprüfen des Wiederherstellungsplans auf erforderliche Änderungen  

-   Durchführen einer Standortwiederherstellung gemäß dem Wiederherstellungsplan in einem Testlabor mithilfe einer Sicherungskopie der aktuellen Sicherung, die über den Wartungstask „Standortserver sichern“ erstellt wurde

-   Überprüfen der Hardware auf Fehler oder verfügbare Hardwareupdates  

-   Überprüfen der Gesamtintegrität des Standorts  

###  <a name="BKMK_UseMTs"></a> Aufrechterhalten der funktionalen Integrität Ihrer Standortdatenbank  
 Während die von Ihnen geplanten und eingerichteten Tasks von Configuration Manager-Standort und -Hierarchie ausgeführt werden, werden der Configuration Manager-Datenbank durch Standortkomponenten ständig neue Daten hinzugefügt. Durch zunehmende Datenmengen werden die Datenbankleistung und der Datenbankspeicherplatz zunehmend beansprucht. Sie können Standortwartungstasks so einrichten, dass veraltete Daten, die Sie nicht mehr benötigen, entfernt werden.  

 In Configuration Manager sind vordefinierte Wartungstasks verfügbar, die Sie zur Aufrechterhaltung der Integrität der Configuration Manager-Datenbank verwenden können. Standardmäßig stehen nicht alle Wartungstasks für jeden Standort zur Verfügung. Einige Tasks sind aktiviert, andere nicht, und sie unterstützen alle einen Zeitplan, den Sie einrichten können.  

 Von den meisten Wartungstasks werden veraltete Daten in regelmäßigen Abständen aus der Configuration Manager-Datenbank entfernt. Durch das Entfernen nicht erforderlicher Daten wird die Größe der Datenbank reduziert. Hierdurch werden Leistung und Integrität der Datenbank sowie in der Folge die Effizienz von Standort und Hierarchie erhöht. Andere Tasks, wie etwa **Indizes neu erstellen**, helfen dabei, die Datenbankeffizienz zu gewährleisten. Andere Tasks, wie etwa **Standortserver sichern**, helfen Ihnen bei der Vorbereitung auf Notfallwiederherstellungen.  

> [!IMPORTANT]  
>  Wenn Sie die Ausführung von Tasks planen, von denen Daten gelöscht werden, berücksichtigen Sie die hierarchieweite Verwendung dieser Daten. Wenn von einem Task, durch den Daten gelöscht werden, an einem Standort ausgeführt wird, werden die Informationen aus der Configuration Manager-Datenbank gelöscht, und diese Änderung wird an alle Standorte in der Hierarchie repliziert. Durch diesen Löschvorgang können andere Tasks, die von diesen Daten abhängig sind, beeinträchtigt werden. So können Sie z.B. am Standort der zentralen Verwaltung einen Ermittlungstask einrichten, der monatlich ausgeführt wird, um Nicht-Clientcomputer zu ermitteln. Sie können die Installation des Configuration Manager Client auf diesen Computern innerhalb zwei Wochen vor ihrer Ermittlung planen. An einem Standort in der Hierarchie richtet jedoch ein Administrator den Task „Veraltete Ermittlungsdaten löschen“ ein, sodass dieser wöchentlich ausgeführt wird. Dies führt dazu, dass sieben Tage nach der Ermittlung von Nicht-Clientcomputern diese aus der Configuration Manager-Datenbank gelöscht werden. Sie wiederum bereiten am Standort der zentralen Verwaltung eine Pushinstallation des Configuration Manager-Clients auf den neuen Computern für Tag 10 vor. Doch da der Task „Veraltete Ermittlungsdaten löschen“ kürzlich ausgeführt wurde und dadurch Daten, die älter als 7 Tage waren, gelöscht wurden, sind die kürzlich ermittelten Computer in der Datenbank nicht mehr verfügbar.  

Überprüfen Sie nach der Installation eines Configuration Manager-Standorts die verfügbaren Wartungstasks, und aktivieren Sie diejenigen, die für Ihre Vorgänge erforderlich sind. Überprüfen Sie den Standardzeitplan jedes Tasks, und richten Sie die Zeitpläne nach Bedarf ein, um eine Feinabstimmung des Tasks auf Ihre Hierarchie und Umgebung auszuführen. Der Standardzeitplan jedes Tasks ist für die meisten Umgebungen passend. Überwachen Sie dennoch die Leistung Ihrer Standorte und der Datenbank, und gehen Sie davon aus, dass eine Feinabstimmung der Tasks erforderlich ist, um die Effizienz Ihrer Bereitstellung zu steigern. Planen Sie regelmäßige Überprüfungen der Leistung von Standort und Datenbank ein, und konfigurieren Sie Wartungstasks sowie deren Zeitpläne neu, um die Effizienz zu gewährleisten.  

#### <a name="set-up-maintenance-tasks"></a>Benutzerdefinierte Wartungstasks einrichten  
 Von jedem Configuration Manager-Standort werden Wartungstasks unterstützt, mit denen die Betriebseffizienz der Standortdatenbank aufrechterhalten werden kann. Standardmäßig sind an jedem Standort mehrere Wartungstasks aktiviert. Von allen Tasks werden unabhängige Zeitpläne unterstützt. Wartungstasks werden einzeln für jeden Standort eingerichtet und gelten für die Datenbank an diesem Standort. Einige Tasks, wie etwa **Veraltete Ermittlungsdaten löschen** wirken sich auf Informationen aus, die an allen Standorten in der Hierarchie verfügbar sind.  

 In der Configuration Manager-Konsole werden nur die Wartungstasks angezeigt, die Sie an einem Standort einrichten können. Eine umfassende Liste mit Wartungstasks nach Standorttyp finden Sie unter [Referenz für Wartungstasks für System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Anhand des folgenden Verfahrens können Sie die allgemeinen Einstellungen von Wartungstasks einrichten.  

###### <a name="to-set-up-maintenance-tasks-for-configuration-manager"></a>Einrichten von Wartungstasks für Configuration Manager  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** >**Standorte**.  

2.  Wählen Sie den Standort mit dem einzurichtenden Wartungstask aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** **Standortwartung** aus, und wählen Sie dann den Wartungstask aus, den Sie einrichten möchten.  

    > [!TIP]  
    >  Es werden nur die Tasks angezeigt, die am ausgewählten Standort verfügbar sind.  

4.  Wählen Sie zum Einrichten des Tasks **Bearbeiten** aus, vergewissern Sie sich, dass das Kontrollkästchen **Diese Aufgabe aktivieren** aktiviert ist, und richten Sie einen Zeitplan zum Ausführen des Tasks ein. Wenn mithilfe des Tasks auch veraltete Daten gelöscht werden, legen Sie fest, in welchem Alter Daten bei der Taskausführung aus der Datenbank gelöscht werden sollen. Klicken Sie auf **OK**, um die **Eigenschaften** des Tasks zu schließen.  

    > [!NOTE]  
    >  Legen Sie für **Veraltete Statusmeldungen löschen** fest, in welchem Alter Daten beim Einrichten von Statusfilterregeln gelöscht werden sollen.  

5.  Klicken Sie auf die Schaltflächen **Aktivieren** oder **Deaktivieren**, um den Task zu aktivieren bzw. zu deaktivieren, ohne die Taskeigenschaften zu ändern. Die Bezeichnung der Schaltfläche ändert sich je nach aktueller Konfiguration des Tasks.  

6.  Wenn Sie die Wartungstasks konfiguriert haben, klicken Sie auf **OK**, um den Vorgang abzuschließen.
