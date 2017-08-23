---
title: Erstellen einer Tasksequenz zum Erfassen und Wiederherstellen eines Benutzerzustands | Microsoft-Dokumentation
description: "Verwenden Sie die Tasksequenzen von System Center Configuration Manager zum Erfassen und Wiederherstellen von Benutzerzustandsdaten in Bereitstellungsszenarios für Betriebssysteme."
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 4b3668094d576b1b8710f08b384aa2f7c5eb0cca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-system-center-configuration-manager"></a>Erstellen einer Tasksequenz zum Erfassen und Wiederherstellen eines Benutzerzustands in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit Tasksequenzen von System Center Configuration Manager können Sie bei der Betriebssystembereitstellung die Benutzerzustandsdaten erfassen und wiederherstellen, wenn Sie den Benutzerzustand des aktuellen Betriebssystems beibehalten möchten. Je nach Art der erstellten Tasksequenz werden die Schritte zum Erfassen und Wiederherstellen möglicherweise automatisch zur Tasksequenz hinzugefügt. In anderen Szenarien müssen Sie die Schritte zum Erfassen und Wiederherstellen möglicherweise manuell zur Tasksequenz hinzufügen. Dieses Thema enthält die Schritte, die Sie zu einer vorhandenen Tasksequenz hinzufügen müssen, um Benutzerzustandsdaten zu erfassen und wiederherzustellen.  

##  <a name="BKMK_CaptureRestoreUserState"></a> Erfassen und Wiederherstellen von Benutzerzustandsdaten  
 Zum Erfassen und Wiederherstellen des Benutzerzustands müssen Sie die folgenden Schritte zur Tasksequenz hinzufügen:  

-   **Zustandsspeicher anfordern**: Dieser Schritt ist nur erforderlich, wenn Sie den Benutzerzustand auf dem Zustandsmigrationspunkt speichern.  

-   **Benutzerzustand erfassen**: Bei diesem Schritt werden die Benutzerzustandsdaten erfasst und entweder auf dem Zustandsmigrationspunkt oder lokal mithilfe von Links gespeichert.  

-   **Benutzerzustand wiederherstellen**: Bei diesem Schritt werden die Benutzerzustandsdaten auf dem Zielcomputer wiederhergestellt. Dabei können die Daten von einem Migrationspunkt für den Benutzerzustand oder vom Zielcomputer abgerufen werden.  

-   **Zustandsspeicher freigeben**: Dieser Schritt ist nur erforderlich, wenn Sie den Benutzerzustand auf dem Zustandsmigrationspunkt speichern. Bei diesem Schritt werden diese Daten aus dem Zustandsmigrationspunkt entfernt.  

 Gehen Sie wie folgt vor, um die zum Erfassen und Wiederherstellen des Benutzerzustands erforderlichen Tasksequenzschritte hinzuzufügen. Weitere Informationen zum Erstellen von Tasksequenzen finden Sie unter [Verwaltung von Tasksequenzen zum Automatisieren von Tasks](manage-task-sequences-to-automate-tasks.md).  

#### <a name="to-add-task-sequence-steps-to-capture-the-user-state"></a>So fügen Sie Tasksequenzschritte zum Erfassen des Benutzerzustands hinzu  

1.  Wählen Sie in der Liste **Tasksequenz** eine Tasksequenz aus, und klicken Sie dann auf **Bearbeiten**.  

2.  Wenn Sie einen Zustandsmigrationspunkt zum Speichern des Benutzerzustands verwenden, fügen Sie der Tasksequenz den Schritt **Zustandsspeicher anfordern** hinzu. Klicken Sie im Dialogfeld **Tasksequenz-Editor** auf **Hinzufügen**, zeigen Sie auf **Benutzerzustand**, und klicken Sie dann auf **Zustandsspeicher anfordern**. Geben Sie für den Schritt **Zustandsspeicher anfordern** die folgenden Eigenschaften und Optionen an, und klicken Sie dann auf **Anwenden**.  

     Geben Sie auf der Registerkarte **Eigenschaften** die folgenden Optionen an:  

    -   Geben Sie einen Namen und eine Beschreibung für den Schritt ein.  

    -   Klicken Sie auf **Zustand des Computers erfassen**.  

    -   Geben Sie im Feld **Anzahl von Wiederholungen** an, wie oft von der Tasksequenz im Falle eines Fehlers versucht wird, die Benutzerzustandsdaten zu erfassen.  

    -   Geben Sie im Feld **Wiederholungsverzögerung (in Sekunden)** an, wie viele Sekunden von der Tasksequenz bis zum nächsten Datenerfassungsversuch gewartet werden soll.  

    -   Aktivieren Sie das Kontrollkästchen **Das Netzwerkzugriffskonto verwenden, wenn vom Computerkonto keine Verbindung mit dem Zustandsspeicher hergestellt werden kann**, um anzugeben, ob das [Netzwerkzugriffskonto](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#a-namebkmknaaa-network-access-account) von Configuration Manager zum Verbinden mit dem Zustandsspeicher verwendet werden soll.  

     Geben Sie auf der Registerkarte **Optionen** die folgenden Optionen an:  

    -   Aktivieren Sie das Kontrollkästchen **Bei Fehler fortsetzen** , wenn die Tasksequenz im Falle eines Fehlers bei diesem Schritt mit dem nächsten Schritt fortgesetzt werden soll.  

    -   Geben Sie alle Bedingungen an, die erfüllt sein müssen, damit die Tasksequenz bei einem Fehler fortgesetzt werden kann.  

3.  Fügen Sie der Tasksequenz den Schritt **Benutzerzustand erfassen** hinzu. Klicken Sie im Dialogfeld **Tasksequenz-Editor** auf **Hinzufügen**, zeigen Sie auf **Benutzerzustand**, und klicken Sie dann auf **Benutzerzustand erfassen**. Geben Sie für den Schritt **Benutzerzustand erfassen** die folgenden Eigenschaften und Optionen an, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Legen Sie beim Hinzufügen dieses Schritts der Tasksequenz auch die Tasksequenzvariable **OSDStateStorePath** fest, um anzugeben, wo die Benutzerzustandsdaten gespeichert werden sollen. Wenn Sie den Benutzerstatus lokal speichern, sollten Sie keinen Stammordner angeben, da dies dazu führen kann, dass für die Tasksequenz ein Fehler auftritt. Verwenden Sie immer einen Ordner oder Unterordner, wenn Sie die Benutzerdaten lokal speichern. Informationen zu dieser Variablen finden Sie unter [Erfassen von Tasksequenz-Aktionsvariablen des Benutzerzustands](../understand/task-sequence-action-variables.md#BKMK_CaptureUserState).  

     Geben Sie auf der Registerkarte **Eigenschaften** die folgenden Optionen an:  

    -   Geben Sie einen Namen und eine Beschreibung für den Schritt ein.  

    -   Geben Sie das Paket an, das die USMT-Quelldatei (Windows-EasyTransfer) zum Erfassen der Benutzerzustandsdaten enthält.  

    -   Geben Sie die zu erfassenden Benutzerprofile an:  

        -   Klicken Sie auf **Alle Benutzerprofile mithilfe von Standardoptionen erfassen** , um alle Benutzerprofile zu erfassen.  

        -   Klicken Sie auf **Erfassung der Benutzerprofile anpassen** , um einzelne Benutzerprofile anzugeben, die erfasst werden sollen. Wählen Sie die Konfigurationsdatei („miguser.xml“, „migsys.xml“ oder „migapp.xml“) aus, die die Benutzerprofilinformationen enthält. Sie können die Konfigurationsdatei „config.xml“ hier nicht verwenden. Allerdings können Sie diese manuell mit den Variablen „OSDMigrageAdditionalCaptureOptions“ und „OSDMigrateAdditionalRestoreOptions“ der USMT-Befehlszeile hinzufügen.

    -   Aktivieren Sie das Kontrollkästchen **Ausführliche Protokollierung aktivieren** , um den Umfang der Informationen anzugeben, die bei einem Fehler in Protokolldateien geschrieben werden.  

    -   Aktivieren Sie das Kontrollkästchen **Dateien mit EFS (Encrypted File System) überspringen**.  

    -   Wählen Sie **Mithilfe des normalen Dateisystemzugriffs kopieren** aus, um die folgenden Einstellungen anzugeben:  

        -   **Fortsetzen, wenn einige Dateien nicht erfasst werden können**: Bei dieser Einstellung kann der Migrationsprozess auch dann von dem Tasksequenzschritt fortgesetzt werden, wenn einige Dateien nicht erfasst werden können. Wenn Sie diese Option deaktivieren und eine Datei nicht erfasst werden kann, kann der Tasksequenzschritt nicht ausgeführt werden. Diese Option ist standardmäßig aktiviert.  

        -   **Lokal erfassen mithilfe von Links statt durch Kopieren von Dateien**: Bei dieser Einstellung können Sie die in USMT 4.0 verfügbare, auf festen Links basierende Migrationsfunktion verwenden. Diese Einstellung wird ignoriert, wenn Sie USMT-Versionen vor USMT 4.0 verwenden.  

        -   **Im Offlinemodus erfassen (nur Windows PE)**: Bei dieser Einstellung können Sie den Benutzerzustand von Windows PE erfassen, ohne das vorhandene Betriebssystem zu starten. Diese Einstellung wird ignoriert, wenn Sie USMT-Versionen vor USMT 4.0 verwenden.  

    -   Wählen Sie **Mithilfe des Volumeschattenkopie-Diensts (VSS) erfassen**aus. Diese Einstellung wird ignoriert, wenn Sie USMT-Versionen vor USMT 4.0 verwenden.  

     Geben Sie auf der Registerkarte **Optionen** die folgenden Optionen an:  

    -   Aktivieren Sie das Kontrollkästchen **Bei Fehler fortsetzen** , wenn die Tasksequenz im Falle eines Fehlers bei diesem Schritt mit dem nächsten Schritt fortgesetzt werden soll.  

    -   Geben Sie alle Bedingungen an, die erfüllt sein müssen, damit die Tasksequenz bei einem Fehler fortgesetzt werden kann.  

4.  Fügen Sie den Schritt [Zustandsspeicher freigeben](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) zur Tasksequenz hinzu, wenn Sie einen Zustandsmigrationspunkt zum Speichern des Benutzerzustands verwenden. Klicken Sie im Dialogfeld **Tasksequenz-Editor** auf **Hinzufügen**, zeigen Sie auf **Benutzerzustand**, und klicken Sie dann auf **Zustandsspeicher freigeben**. Geben Sie für den Schritt **Zustandsspeicher freigeben** die folgenden Eigenschaften und Optionen an, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Die Tasksequenzaktion, die vor dem Schritt **Zustandsspeicher freigeben** ausgeführt wird, muss erfolgreich sein, bevor der Schritt **Zustandsspeicher freigeben** gestartet wird.  

     Geben Sie auf der Registerkarte **Eigenschaften** einen Namen und eine Beschreibung für den Schritt ein.  

     Geben Sie auf der Registerkarte **Optionen** die folgenden Optionen an.  

    -   Aktivieren Sie das Kontrollkästchen **Bei Fehler fortsetzen** , wenn die Tasksequenz im Falle eines Fehlers bei diesem Schritt mit dem nächsten Schritt fortgesetzt werden soll.  

    -   Geben Sie alle Bedingungen an, die erfüllt sein müssen, damit die Tasksequenz bei einem Fehler fortgesetzt werden kann.  

 Stellen Sie diese Tasksequenz bereit, um den Benutzerzustand auf einem Zielcomputer zu erfassen. Informationen zum Bereitstellen von Tasksequenzen finden Sie unter [Tasksequenz bereitstellen](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

#### <a name="to-add-task-sequence-steps-to-restore-the-user-state"></a>So fügen Sie Tasksequenzschritte zum Wiederherstellen des Benutzerzustands hinzu  

1.  Wählen Sie in der Liste **Tasksequenz** eine Tasksequenz aus, und klicken Sie dann auf **Bearbeiten**.  

2.  Fügen Sie den Schritt [Benutzerzustand wiederherstellen](../understand/task-sequence-steps.md#BKMK_RestoreUserState) zur Tasksequenz hinzu. Klicken Sie im Dialogfeld **Tasksequenz-Editor** auf **Hinzufügen**, zeigen Sie auf **Benutzerzustand**, und klicken Sie dann auf **Benutzerzustand wiederherstellen**. Durch diesen Schritt wird eine Verbindung mit dem Zustandsmigrationspunkt hergestellt. Geben Sie für den Schritt **Benutzerzustand wiederherstellen** die folgenden Eigenschaften und Optionen an, und klicken Sie dann auf **OK**.  

     Geben Sie auf der Registerkarte **Eigenschaften** die folgenden Eigenschaften an:  

    -   Geben Sie einen Namen und eine Beschreibung für den Schritt ein.  

    -   Geben Sie das Paket an, das das Windows-EasyTransfer bzw. USMT zum Wiederherstellen der Benutzerzustandsdaten enthält.  

    -   Geben Sie die wiederherzustellenden Benutzerprofile an:  

        -   Klicken Sie auf **Alle erfassten Benutzerprofile mit Standardoptionen wiederherstellen** , um alle Benutzerprofile wiederherzustellen.  

        -   Klicken Sie auf **Wiederherstellung von Benutzerprofilen anpassen**, um einzelne Benutzerprofile wiederherzustellen. Wählen Sie die Konfigurationsdatei („miguser.xml“, „migsys.xml“ oder „migapp.xml“) aus, die die Benutzerprofilinformationen enthält. Sie können die Konfigurationsdatei „config.xml“ hier nicht verwenden. Allerdings können Sie diese manuell mit den Variablen „OSDMigrageAdditionalCaptureOptions“ und „OSDMigrateAdditionalRestoreOptions“ der USMT-Befehlszeile hinzufügen.

    -   Wählen Sie **Lokale Computerbenutzerprofile wiederherstellen** aus, um ein neues Kennwort für die wiederhergestellten Profile bereitzustellen. Sie können keine Kennwörter für lokale Profile migrieren.  

        > [!NOTE]  
        >  Wenn Sie lokale Benutzerkonten verwenden und im Schritt [Benutzerzustand erfassen](../understand/task-sequence-steps.md#BKMK_CaptureUserState) die Option **Alle Benutzerprofile mit Standardoptionen erfassen** auswählen, müssen Sie im Schritt [Benutzerzustand wiederherstellen](../understand/task-sequence-steps.md#BKMK_RestoreUserState) die Einstellung **Lokale Computerbenutzerprofile wiederherstellen** auswählen. Andernfalls tritt für die Tasksequenz ein Fehler auf.  

    -   Wählen Sie **Fortsetzen, wenn einige Dateien nicht wiederhergestellt werden können** aus, wenn der Schritt **Benutzerzustand wiederherstellen** auch fortgesetzt werden soll, falls eine Datei nicht wiederhergestellt werden kann.  

         Wenn Sie den Benutzerzustand mithilfe von lokalen Links speichern und die Wiederherstellung nicht erfolgreich ist, kann der Administrator die zum Speichern der Daten erstellen festen Links manuell löschen. Alternativ kann das Tool USMTUtils von der Tasksequenz ausgeführt werden. Wenn Sie die festen Links mithilfe von USMTUtils löschen, fügen Sie nach dem Ausführen von USMTUtils den Schritt [Computer neu starten](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer) hinzu.  

    -   Aktivieren Sie das Kontrollkästchen **Ausführliche Protokollierung aktivieren** , um den Umfang der Informationen anzugeben, die bei einem Fehler in Protokolldateien geschrieben werden.  

     Geben Sie auf der Registerkarte **Optionen** die folgenden Optionen an:  

    -   Aktivieren Sie das Kontrollkästchen **Bei Fehler fortsetzen** , wenn die Tasksequenz im Falle eines Fehlers bei diesem Schritt mit dem nächsten Schritt fortgesetzt werden soll.  

    -   Geben Sie alle Bedingungen an, die erfüllt sein müssen, damit die Tasksequenz bei einem Fehler fortgesetzt werden kann.  

3.  Fügen Sie den Schritt [Zustandsspeicher freigeben](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) zur Tasksequenz hinzu, wenn Sie einen Zustandsmigrationspunkt zum Speichern des Benutzerzustands verwenden. Klicken Sie im Dialogfeld **Tasksequenz-Editor** auf **Hinzufügen**, zeigen Sie auf **Benutzerzustand**, und klicken Sie dann auf **Zustandsspeicher freigeben**. Geben Sie für den Schritt **Zustandsspeicher freigeben** die folgenden Eigenschaften und Optionen an, und klicken Sie dann auf **OK**.  

    > [!IMPORTANT]  
    >  Die Tasksequenzaktion, die vor dem Schritt **Zustandsspeicher freigeben** ausgeführt wird, muss erfolgreich sein, bevor der Schritt **Zustandsspeicher freigeben** gestartet wird.  

     Geben Sie auf der Registerkarte **Eigenschaften** einen Namen und eine Beschreibung für den Schritt ein.  

     Geben Sie auf der Registerkarte **Optionen** die folgenden Optionen an.  

    -   Aktivieren Sie das Kontrollkästchen **Bei Fehler fortsetzen** , wenn die Tasksequenz im Falle eines Fehlers bei diesem Schritt mit dem nächsten Schritt fortgesetzt werden soll.  

    -   Geben Sie alle Bedingungen an, die erfüllt sein müssen, damit die Tasksequenz bei einem Fehler fortgesetzt werden kann.  

 Stellen Sie diese Tasksequenz bereit, um den Benutzerzustand auf einem Zielcomputer wiederherzustellen. Informationen zum Bereitstellen von Tasksequenzen finden Sie unter [Bereitstellen einer Tasksequenz](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

## <a name="next-steps"></a>Nächste Schritte
[Überwachen der Tasksequenzbereitstellung](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
