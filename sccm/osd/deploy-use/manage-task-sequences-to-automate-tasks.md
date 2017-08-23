---
title: Verwalten von Tasksequenzen zum Automatisieren von Tasks | Microsoft-Dokumentation
description: "Sie können Tasksequenzen erstellen, bearbeiten, bereitstellen, importieren und exportieren, um sie in Ihrer System Center Configuration Manager-Umgebung zu verwalten."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
caps.latest.revision: "10"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2f3d66362c49d28a52d7f9c535eb0b3b4cc4eaf7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-task-sequences-to-automate-tasks-in-system-center-configuration-manager"></a>Verwalten von Tasksequenzen zum Automatisieren von Aufgaben in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie Tasksequenzen, um Schritte in Ihrer System Center Configuration Manager-Umgebung zu automatisieren. Zu diesen Schritten gehören die Bereitstellung eines Betriebssystemimages für einen Zielcomputer, das Erstellen und Erfassen eines Betriebssystemimages aus einem Satz von Betriebssysteminstallationsdateien sowie das Erfassen und Wiederherstellen von Benutzerzustandsinformationen. Die Tasksequenzen befinden sich in der Configuration Manager-Konsole unter **Softwarebibliothek** > **Betriebssysteme** > **Tasksequenzen**. Der Knoten **Tasksequenz** mit den erstellten Unterordnern wird in der gesamten Configuration Manager-Hierarchie repliziert. Planungsinformationen finden Sie unter [Planungsüberlegungen für das Automatisieren von Tasks](../plan-design/planning-considerations-for-automating-tasks.md).  

 Verwenden Sie die Informationen in den folgenden Abschnitten, um Tasksequenzen zu verwalten.

##  <a name="BKMK_CreateTaskSequence"></a> Erstellen von Tasksequenzen  
 Erstellen Sie Tasksequenzen mithilfe des Tasksequenzerstellungs-Assistenten. Mit diesem Assistenten können Sie die folgenden Typen von Tasksequenzen erstellen:  

|Tasksequenztyp|Weitere Informationen|  
|------------------------|----------------------|  
|[Tasksequenz zum Installieren eines Betriebssystems](create-a-task-sequence-to-install-an-operating-system.md)|Dieser Tasksequenztyp erstellt die Schritte zum Installieren eines Betriebssystems sowie die Option zum Migrieren von Benutzerdaten, Einschließen von Softwareupdates und Installieren von Anwendungen.|  
|[Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem](create-a-task-sequence-to-upgrade-an-operating-system.md)|Dieser Tasksequenztyp erstellt die Schritte zum Ausführen eines Betriebssystemupgrades sowie die Option zum Einschließen von Softwareupdates und Installieren von Anwendungen.|  
|[Tasksequenz zum Erfassen eines Betriebssystems](create-a-task-sequence-to-capture-an-operating-system.md)|Dieser Tasksequenztyp erstellt die Schritte zum Erstellen und Erfassen eines Betriebssystems auf einem Referenzcomputer. Sie können Softwareupdates einschließen und Anwendungen auf dem Referenzcomputer installieren, bevor das Image erfasst wird.|  
|[Tasksequenz zum Erfassen und Wiederherstellen des Benutzerzustands](create-a-task-sequence-to-capture-and-restore-user-state.md)|Diese Tasksequenz stellt die einer vorhandenen Tasksequenz hinzuzufügenden Schritte zum Erfassen und Wiederherstellen von Benutzerzustandsdaten bereit.|  
|[Tasksequenz zum Verwalten virtueller Festplatten](use-a-task-sequence-to-manage-virtual-hard-disks.md)|Dieser Tasksequenztyp enthält die Schritte zum Erstellen einer virtuellen Festplatte, einschließlich der Schritte zum Installieren von Betriebssystem und Anwendungen, die Sie über die Configuration Manager-Konsole in System Center Virtual Machine Manager (VMM) veröffentlichen können.|  
|[Benutzerdefinierte Tasksequenz](create-a-custom-task-sequence.md)|Dieser Tasksequenztyp fügt keine Schritte zur Tasksequenz hinzu. Nach der Erstellung der Tasksequenz müssen Sie sie bearbeiten und ihr Schritte hinzufügen.|  

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Rückkehr zur vorherigen Seite, wenn eine Tasksequenz fehlschlägt
Ab Configuration Manager Version 1702 können Sie zu einer vorherigen Seite zurückkehren, wenn Sie eine Tasksequenz ausführen und ein Fehler auftritt. Bevor es diese Version gab, mussten Sie die Tasksequenz neu starten, wenn ein Fehler aufgetreten ist. In den folgenden Szenarios können Sie zum Beispiel die Schaltfläche **Zurück** verwenden:

- Beim Starten eines Computers in Windows PE wird möglicherweise der Bootstrap-Dialog der Tasksequenz angezeigt, bevor die Tasksequenz verfügbar ist. Wenn Sie in diesem Szenario auf „Weiter“ klicken, wird auf der letzten Seite der Tasksequenz eine Nachricht angezeigt, die darüber informiert, dass es keine verfügbaren Tasksequenzen gibt. Klicken Sie jetzt auf **Zurück**, um erneut nach verfügbaren Tasksequenzen zu suchen. Sie können diesen Vorgang wiederholen, bis die Tasksequenz verfügbar ist.
- Wenn die abhängigen Paketinhalte beim Ausführen einer Tasksequenz an den Verteilungspunkten noch nicht verfügbar sind, kann die Tasksequenz nicht ausgeführt werden. Sie können jetzt fehlenden Inhalt (wenn dieser noch nicht verteilt wurde) verteilen oder warten, bis der Inhalt an den Verteilungspunkten verfügbar ist. Klicken Sie dann auf **Zurück**, damit die Tasksequenz wieder nach dem Inhalt sucht.

##  <a name="BKMK_ModifyTaskSequence"></a> Bearbeiten einer Tasksequenz  
 Sie können eine Tasksequenz ändern, indem Sie der Tasksequenz Schritte oder Tasksequenzgruppen hinzufügen, Schritte oder Tasksequenzgruppen aus ihr entfernen oder die Reihenfolge der Schritte ändern. Gehen Sie wie folgt vor, um eine vorhandene Tasksequenz zu ändern.  

> [!IMPORTANT]  
>  Wenn Sie eine Tasksequenz bearbeiten, die mithilfe des Tasksequenzerstellungs-Assistenten erstellt wurde, kann die Aktion des jeweiligen Schritts oder der Typ des Schritts als Schrittname verwendet werden. Ein Schritt kann z.B. den Namen „Festplatte 0 partitionieren“ haben. Dies ist die Aktion für einen Schritt vom Typ [Datenträger formatieren und partitionieren](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk). Alle Tasksequenzschritte werden nach Ihrem Typ dokumentiert, also nicht unbedingt nach dem im Editor angezeigten Namen des Schritts.  

#### <a name="to-edit-a-task-sequence"></a>So bearbeiten Sie eine Tasksequenz  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Wählen Sie in der Liste **Tasksequenz** die Tasksequenz aus, die Sie bearbeiten möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Tasksequenz** auf **Bearbeiten**, und führen Sie dann eine der folgenden Vorgänge aus:  

    -   Wenn Sie einen Tasksequenzschritt hinzufügen möchten, klicken Sie auf **Hinzufügen**, wählen Sie den Typ des Schritts aus, und klicken Sie dann auf den hinzuzufügenden Tasksequenzschritt. Beispiel: Wenn Sie den Schritt "Befehlszeile ausführen" hinzufügen möchten, klicken Sie auf **Hinzufügen**, wählen Sie **Allgemein**aus, und klicken Sie dann auf **Befehlszeile ausführen**.  

         Eine Liste aller Tasksequenzschritte und des jeweils dazugehörenden Typs finden Sie in der nachfolgenden Tabelle.  

    -   Wenn Sie der Tasksequenz eine Gruppe hinzufügen möchten, klicken Sie zuerst auf **Hinzufügen**und dann auf **Neue Gruppe**. Nachdem Sie der Tasksequenz eine Gruppe hinzugefügt haben, können Sie der Gruppe Schritte hinzufügen.  

    -   Wenn Sie die Reihenfolge der Schritte und Gruppen in der Tasksequenz ändern möchten, wählen Sie den neu anzuordnenden Schritt bzw. die Gruppe aus, und verschieben Sie den Schritt dann mithilfe des Symbols **Element nach oben verschieben** oder **Element nach unten verschieben** . Sie können nicht mehrere Schritte oder Gruppen gleichzeitig verschieben.  

    -   Wenn Sie einen Schritt oder eine Gruppe entfernen möchten, wählen Sie den Schritt oder die Gruppe aus, und klicken Sie dann auf **Entfernen**.  

5.  Klicken Sie zum Speichern der Änderungen auf **OK** .  

 Eine Liste verfügbarer Tasksequenzschritte finden Sie unter [Tasksequenzschritte](../understand/task-sequence-steps.md).  

## <a name="configure-software-center-properties"></a>Konfigurieren der Eigenschaften des Softwarecenters
Gehen Sie wie folgt vor, um die Angaben für die Tasksequenz, die im Softwarecenter angezeigt werden, zu konfigurieren. Diese Angaben dienen nur zu Informationszwecken.  
1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Betriebssysteme** > **Tasksequenzen**.
2. Wählen Sie die zu bearbeitende Tasksequenz aus, und klicken Sie anschließend auf **Eigenschaften**.
3. Auf der Registerkarte **Allgemein** stehen folgende neuen Einstellungen für das Softwarecenter zur Verfügung:
  - **Neustart erforderlich**: Informiert den Benutzer, ob während der Installation ein Neustart erforderlich ist.
  - **Downloadgröße (in MB)**: Gibt an, wie viele Megabytes für die Tasksequenz im Softwarecenter angezeigt werden.  
  - **Geschätzte Laufzeit (in Minuten)**: Gibt die geschätzte Laufzeit in Minuten für die Tasksequenz an; wird im Softwarecenter angezeigt.

## <a name="configure-advanced-task-sequence-settings"></a>Konfigurieren von erweiterten Einstellungen für eine Tasksequenz
Gehen Sie wie folgt vor, um die Angaben für die Tasksequenz, die im Softwarecenter angezeigt werden, zu konfigurieren. Diese Angaben dienen nur zu Informationszwecken.  
1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Betriebssysteme** > **Tasksequenzen**.
2. Wählen Sie die zu bearbeitende Tasksequenz aus, und klicken Sie anschließend auf **Eigenschaften**.
3. Auf der Registerkarte **Erweitert** sind die folgenden Einstellungen verfügbar:

    - **Ein anderes Programm zuerst ausführen**    
    Aktivieren Sie dieses Kontrollkästchen, um ein anderes Programm (in einem anderen Paket) auszuführen, bevor die Tasksequenz ausgeführt wird. Standardmäßig ist dieses Kontrollkästchen deaktiviert. Das zuerst auszuführende Programm muss nicht gesondert angekündigt werden.

        > [!IMPORTANT]     
        Diese Einstellung gilt nur für Tasksequenzen, die in der Vollversion des Betriebssystems ausgeführt werden. Diese Einstellung wird von Configuration Manager ignoriert, wenn die Tasksequenz mithilfe von PXE- oder Startmedien gestartet wird.

    - **Paket**     
        Wenn Sie **Ein anderes Programm zuerst ausführen** auswählen, geben Sie das Paket mit dem vor dieser Tasksequenz auszuführenden Programm ein, oder suchen Sie danach.

    - **Programm**     
    Wenn Sie **Ein anderes Programm zuerst ausführen** auswählen, wählen Sie in der Dropdownliste **Programm** das vor dieser Tasksequenz auszuführende Programm aus.

        > [!NOTE]    
        > Kann das ausgewählte Programm nicht auf einem Client ausgeführt werden, wird die Tasksequenz nicht ausgeführt. Bei erfolgreicher Ausführung des ausgewählten Programms wird dieses auch bei erneuter Ausführung der Tasksequenz auf dem gleichen Client nicht erneut ausgeführt.
 
    - **Diese Tasksequenz auf Computern, auf denen sie bereitgestellt ist, deaktivieren**    
    Wenn Sie diese Option auswählen, werden alle Bereitstellungen, die diese Tasksequenz enthalten, vorübergehend deaktiviert. Die Tasksequenz wird aus der Liste der zum Ausführen verfügbaren Ankündigungen entfernt und erst wieder ausgeführt, nachdem sie erneut aktiviert wurde. Die Option ist standardmäßig deaktiviert.

    - **Maximal zulässige Laufzeit**    
    Gibt die maximale Zeit (in Minuten) an, die für die Ausführung der Tasksequenz auf dem Zielcomputer erwartet wird. Sie müssen eine ganze Zahl verwenden, die gleich oder größer als null ist. Standardmäßig ist dieser Wert auf 120 Minuten festgelegt.

        > [!IMPORTANT]    
        > Wenn Sie bei der Sammlung, für die diese Tasksequenz ausgeführt wird, Wartungsfenster verwenden, kann ein Konflikt auftreten, wenn die **Maximal zulässige Laufzeit** länger ist als das geplante Wartungsfenster. Wenn für die maximal zulässige Laufzeit der Wert **0** festgelegt ist, wird die Tasksequenz während des Wartungsfensters gestartet, und die Ausführung wird am Ende des Wartungsfensters nicht unterbrochen, sondern solange fortgesetzt, bis das Programm abgeschlossen ist oder ein Fehler auftritt. Entsprechend werden Tasksequenzen, bei denen für die maximal zulässige Laufzeit der Wert **0** festgelegt ist, möglicherweise über das Ende ihrer Wartungsfenster hinaus ausgeführt. Wenn Sie für die maximal zulässige Laufzeit einen bestimmten Zeitraum (also nicht **0**) festlegen, der die Dauer aller verfügbaren Wartungsfenster überschreitet, wird diese Tasksequenz nicht ausgeführt. Weitere Informationen finden Sie unter [Verwenden von Wartungsfenstern](/sccm/core/clients/manage/collections/use-maintenance-windows).
 
        Wenn der Wert **0** festgelegt ist, verwendet Configuration Manager für die maximal zulässige Laufzeit **12** Stunden (720 Minuten) für die Überwachung des Fortschritts. Allerdings wird die Tasksequenz gestartet, solange die Dauer des Countdowns den Wert für das Wartungsfenster nicht überschreitet.

    > [!NOTE]    
    > Wenn die maximal zulässige Laufzeit erreicht wird, beendet Configuration Manager die Tasksequenz, sofern für die Tasksequenz die Einstellung „Mit Administratorrechten ausführen“ festgelegt und die Einstellung „Benutzerinteraktion mit dem Programm zulassen“ deaktiviert ist. Wenn die Tasksequenz selbst nicht beendet wird, beendet Configuration Manager die Überwachung der Tasksequenz, sobald die maximal zulässige Laufzeit erreicht wurde. 

    - **Ein Startimage verwenden**   
        Aktivieren Sie diese Option, um bei der Ausführung der Tasksequenz das ausgewählte Startimage zu verwenden. 

        Klicken Sie auf **Durchsuchen**, um ein anderes Startimage auszuwählen. Deaktivieren Sie diese Option, um bei der Ausführung der Tasksequenz die Verwendung des ausgewählten Startimages zu deaktivieren.

    - **Diese Tasksequenz kann auf jeder Plattform ausgeführt werden**     
        Wenn Sie diese Option auswählen, überprüft Configuration Manager den Plattformtyp des Zielcomputers nicht, wenn die Tasksequenz bereitgestellt wird. Diese Option ist standardmäßig ausgewählt.

    - **Diese Tasksequenz kann nur auf den angegebenen Clientplattformen ausgeführt werden**    
        Mit dieser Option werden die Prozessoren, Betriebssysteme und Service Packs angegeben, unter denen diese Tasksequenz ausgeführt werden kann. Wenn Sie diese Option auswählen, muss auch mindestens eine Plattform aus der Liste ausgewählt werden. Standardmäßig ist keine Plattform ausgewählt. Configuration Manager bewertet mithilfe dieser Informationen, welche Zielcomputer in einer Sammlung die bereitgestellte Tasksequenz erhalten sollen.

        > [!NOTE]    
        > Wenn eine Tasksequenz von Startmedien oder mittels PXE-Start ausgeführt wird, wird diese Option ignoriert. Die Tasksequenz wird dann so ausgeführt, als ob **Dieses Programm kann auf jeder Plattform ausgeführt werden** aktiviert ist.

## <a name="configure-high-impact-task-sequence-settings"></a>Konfigurieren von Einstellungen für eine Tasksequenz mit schwerwiegenden Auswirkungen
Ab Configuration Manager Version 1702 können Sie eine Tasksequenz als Tasksequenz mit schwerwiegenden Auswirkungen festlegen und die Meldungen anpassen, die Benutzer erhalten, wenn sie die Tasksequenz ausführen.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Festlegen einer Tasksequenz als Tasksequenz mit schwerwiegenden Auswirkungen
Gehen Sie wie folgt vor, um eine Tasksequenz als Tasksequenz mit schwerwiegenden Auswirkungen festzulegen:
> [!NOTE]    
> Jede Tasksequenz, die bestimmte Bedingungen erfüllt, wird automatisch als „high-impact“ (mit schwerwiegenden Auswirkungen) definiert. Weitere Informationen finden Sie unter [Verwalten risikoreicher Bereitstellungen](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Betriebssysteme** > **Tasksequenzen**.
2. Wählen Sie die zu bearbeitende Tasksequenz aus, und klicken Sie anschließend auf **Eigenschaften**.
3. Wählen Sie in der Registerkarte **Benutzerbenachrichtigung** **Dies ist eine Tasksequenz mit schwerwiegenden Auswirkungen** aus.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Erstellen einer benutzerdefinierten Benachrichtigung für risikoreiche Bereitstellungen
Verwenden Sie die folgende Prozedur, um eine benutzerdefinierte Benachrichtigung zu Bereitstellungen mit schwerwiegenden Auswirkungen zu erstellen.
1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Betriebssysteme** > **Tasksequenzen**.
2. Wählen Sie die zu bearbeitende Tasksequenz aus, und klicken Sie anschließend auf **Eigenschaften**.
3. Wählen Sie in der Registerkarte **Benutzerbenachrichtigung** **Benutzerdefinierten Text verwenden** aus.
>  [!NOTE]    
>  Sie können den Text von Benutzerbenachrichtigungen nur festlegen, wenn **Dies ist eine Tasksequenz mit schwerwiegenden Auswirkungen** ausgewählt ist.

4. Konfigurieren Sie folgende Einstellungen (maximal 255 Zeichen pro Text):

  **Überschriftentext der Benutzerbenachrichtigung**: Gibt den blauen Text an, der in der Benutzerbenachrichtigung vom Softwarecenter angezeigt wird. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt beispielsweise folgenden Text: „Bestätigen Sie, dass Sie das Betriebssystem auf diesem Computer aktualisieren möchten“ o.Ä.

  **Nachrichtenrest der Benutzerbenachrichtigung**: Es gibt drei Textfelder, die den Text der benutzerdefinierten Benachrichtigungen enthalten. Sie müssen in jedes Textfeld Text eingeben.
  - Erstes Textfeld: Gibt den Hauptteil des Texts an, der üblicherweise Anweisungen an den Benutzer enthält. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt beispielsweise folgenden Text: „Das Upgrade des Betriebssystems kann einige Zeit dauern und mehrere Neustarts des Computers erfordern“ o.Ä.
  - Zweites Textfeld: Gibt den fetten Text unterhalb des Hauptteils an. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt beispielsweise folgenden Text: „Dieses direkte Upgrade installiert das neue Betriebssystem und führt eine automatische Migration Ihrer Apps, Daten und Einstellungen durch“ o.Ä.
  - Drittes Textfeld: Gibt die letzte Textzeile unterhalb des fetten Texts an. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt beispielsweise folgenden Text: „Klicken Sie auf Installieren, um den Vorgang zu starten. Klicken Sie andernfalls auf Abbrechen.“   
    
Angenommen, Sie konfigurieren folgende benutzerdefinierte Benachrichtigung in den Eigenschaften.

![Benutzerdefinierte Benachrichtigung für eine Tasksequenz](..\media\user-notification.png)

Folgende Benachrichtigung wird angezeigt, wenn der Endbenutzer die Installation aus dem Softwarecenter öffnet.

![Benutzerdefinierte Benachrichtigung für eine Tasksequenz](..\media\user-notification-enduser.png)


##  <a name="BKMK_DistributeTS"></a> Verteilen von Inhalt, auf den von einer Tasksequenz verwiesen wird  
 Sie müssen Inhalt, auf den von einer Tasksequenz verwiesen wird, an Verteilungspunkte verteilen, bevor diese Tasksequenz von Clients ausgeführt wird. Sie können die Tasksequenz jederzeit auswählen und ihren Inhalt verteilen, um eine neue Liste von Referenzpaketen für die Verteilung zu erstellen. Wenn Sie die Tasksequenz mit aktualisiertem Inhalt ändern, müssen Sie den Inhalt erneut verteilen, bevor er für Clients verfügbar ist. Gehen Sie wie folgt vor, um den Inhalt, auf den von einer Tasksequenz verwiesen wird, zu verteilen.  

#### <a name="to-distribute-referenced-content-to-distribution-points"></a>So verteilen Sie referenzierten Inhalt an Verteilungspunkte  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Wählen Sie in der Liste **Tasksequenz** die Tasksequenz aus, die Sie verteilen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Inhalt verteilen** , um den Assistenten für die Verteilung von Inhalt zu starten.  

5.  Vergewissern Sie sich auf der Seite **Allgemein** , dass die richtige Tasksequenz für die Verteilung ausgewählt ist, und klicken Sie dann auf **Weiter**.  

6.  Überprüfen Sie auf der Seite **Inhalt** den zu verteilenden Inhalt, z. B. das Startabbild, auf das von der Tasksequenz verwiesen wird, und klicken Sie dann auf **Weiter**.  

7.  Geben Sie auf der Seite **Inhaltsziel** die Sammlungen, den Verteilungspunkt oder die Verteilungspunktgruppe an, an die der Inhalt der Tasksequenz verteilt werden soll, und klicken Sie dann auf **Weiter**.  

    > [!IMPORTANT]  
    >  Wenn von der ausgewählten Tasksequenz auf Inhalt verwiesen wird, der bereits an einen bestimmten Verteilungspunkt verteilt wurde, wird der betreffende Verteilungspunkt nicht im Assistenten aufgeführt.  

8.  Schließen Sie den Assistenten ab.  

 Sie können den Inhalt, auf den in der Tasksequenz verwiesen wird, vorab bereitstellen. Configuration Manager erstellt eine komprimierte, vorab bereitgestellte Inhaltsdatei, die die Dateien, zugeordnete Abhängigkeiten und zugeordnete Metadaten für den von Ihnen ausgewählten Inhalt umfasst. Sie können den Inhalt dann manuell in einen Standortserver, sekundären Standort oder Verteilungspunkt importieren. Weitere Informationen zum Vorabbereitstellen von Inhaltsdateien finden Sie unter [Vorabbereitstellen von Inhalt](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).  

##  <a name="BKMK_DeployTS"></a> Bereitstellen einer Tasksequenz  
 Mithilfe der folgenden Vorgehensweise können Sie eine Tasksequenz auf Computern in einer Sammlung bereitstellen.  

> [!WARNING]  
>  Sie können das Verhalten für Tasksequenzbereitstellungen mit hohem Risiko verwalten. Bei einer Bereitstellung mit hohem Risiko handelt es sich um eine Bereitstellung, die automatisch installiert wird und zu unerwünschten Ergebnissen führen kann. Beispielsweise wird eine Tasksequenz, die als Zweck **Erforderlich** aufweist und ein Betriebssystem bereitstellt, als eine Bereitstellung mit hohem Risiko betrachtet. Weitere Informationen finden Sie unter [Einstellungen für die Verwaltung hochriskanter Bereitstellungen](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

> [!NOTE]  
>  Die Statusmeldungen für die Tasksequenzbereitstellung werden in einem Meldungsfenster an einem primären Standort, nicht jedoch an einem Standort der zentralen Verwaltung angezeigt.  

#### <a name="to-deploy-a-task-sequence"></a>So stellen Sie eine Tasksequenz bereit  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Wählen Sie in der Liste **Tasksequenz** die Tasksequenz aus, die Sie bereitstellen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

    > [!NOTE]  
    >  Wenn **Bereitstellen** nicht verfügbar ist, hat die Tasksequenz eine ungültige Referenz.  Korrigieren Sie die Referenz, und versuchen Sie dann erneut, die Tasksequenz bereitzustellen.  

5.  Geben Sie auf der Seite **Allgemein** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   **Tasksequenz**: Geben Sie die Tasksequenz an, die Sie bereitstellen möchten. In diesem Feld wird standardmäßig die von Ihnen ausgewählte Tasksequenz angezeigt.  

    -   **Sammlung**: Geben Sie die Sammlung an, die die Computer enthält, von denen die Tasksequenz ausgeführt werden soll.  

         Stellen Sie keine Tasksequenzen bereit, mit denen Betriebssysteme in ungeeigneten Sammlungen wie beispielsweise **Alle Systeme** installiert werden. Achten Sie darauf, dass die von Ihnen ausgewählte Sammlung nur die Computer enthält, von denen die Tasksequenz ausgeführt werden soll.  

        > [!NOTE]  
        >  Bei einer Bereitstellung mit hohem Risiko, wie z.B. einem Betriebssystem, werden im Fenster **Sammlung auswählen** nur die benutzerdefinierten Sammlungen angezeigt, die den in den Eigenschaften des Standorts konfigurierten Einstellungen zur Bereitstellungsüberprüfung entsprechen. Bereitstellungen mit hohem Risiko sind immer auf benutzerdefinierte Sammlungen, von Ihnen erstellte Sammlungen und die integrierte Sammlung **Unbekannte Computer** beschränkt. Beim Erstellen einer Bereitstellung mit hohem Risiko können Sie keine integrierte Sammlung auswählen, wie z. B. **Alle Systeme**. Deaktivieren Sie die Einstellung **Hide collections with a member count greater than the site's minimum size configuration** (Sammlungen mit einer Anzahl der Mitglieder ausblenden, die größer als die minimale Größenkonfiguration des Standorts ist), um alle benutzerdefinierten Sammlungen anzuzeigen, die weniger Clients als die konfigurierte maximale Größe enthalten. Weitere Informationen finden Sie unter [Einstellungen für die Verwaltung hochriskanter Bereitstellungen](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
        >   
        >  Die Einstellungen zur Bereitstellungsüberprüfung basieren auf der aktuellen Mitgliedschaft der Sammlung. Nach der Bereitstellung der Tasksequenz wird die Sammlungsmitgliedschaft für die Einstellungen für eine Bereitstellung mit hohem Risiko nicht erneut bewertet.  
        >   
        >  Angenommen, Sie legen **Standardgröße** auf 100 und **Maximale Größe** auf 1000 fest. Wenn Sie eine Bereitstellung mit hohem Risiko erstellen, werden im Fenster **Sammlung auswählen** nur die Sammlungen angezeigt, die weniger als 100 Clients enthalten. Wenn Sie die Einstellung **Hide collections with a member count greater than the site's minimum size configuration** (Sammlungen mit einer Anzahl der Mitglieder ausblenden, die größer als die minimale Größenkonfiguration des Standorts ist) deaktivieren, werden im Fenster Sammlungen angezeigt, die weniger als 1.000 Clients enthalten.  
        >   
        >  Wenn Sie eine Sammlung auswählen, die eine Standortrolle enthält, gilt Folgendes:  
        >   
        >  -   Wenn die Sammlung einen Standortsystemserver enthält und Sie die Einstellungen zur Bereitstellungsüberprüfung so konfigurieren, dass Sammlungen mit Standortsystemservern blockiert werden, tritt ein Fehler auf, und Sie können nicht fortfahren.  
        > -   Wenn die Sammlung einen Standortsystemserver enthält und Sie die Einstellungen zur Bereitstellungsüberprüfung so konfigurieren, dass Sie im Fall von Sammlungen mit Standortsystemservern gewarnt werden, wird im Assistenten zum Bereitstellen von Software eine Warnung über ein hohes Risiko angezeigt, falls die Sammlung den Standardwert für die Größe überschreitet oder falls die Sammlung einen Server enthält. Sie müssen der Erstellung einer Bereitstellung mit hohem Risiko zustimmen, und eine Überwachungsstatusmeldung wird erstellt.  

    -   **Kommentare (optional)**: Geben Sie zusätzliche Informationen zur Beschreibung dieser Tasksequenzbereitstellung an.  

6.  Geben Sie auf der Seite **Bereitstellungseinstellungen** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   **Zweck**: Wählen Sie in der Dropdownliste eine der folgenden Optionen aus:  

        -   **Verfügbar**: Wenn die Tasksequenz für einen Benutzer bereitgestellt wird, wird die veröffentlichte Tasksequenz dem Benutzer im Anwendungskatalog angezeigt, und der Benutzer kann sie bei Bedarf anfordern. Wenn die Tasksequenz auf einem Gerät bereitgestellt wird, wird sie dem Benutzer im Softwarecenter angezeigt, und der Benutzer kann sie bei Bedarf installieren.  

        -   **Erforderlich**: Die Tasksequenz wird gemäß dem konfigurierten Zeitplan automatisch bereitgestellt. Allerdings kann ein Benutzer den Bereitstellungsstatus der Tasksequenz (sofern dieser nicht ausgeblendet ist) nachverfolgen und die Tasksequenz vor Ablauf der Frist über das Softwarecenter installieren.  

    -   **Automatische Bereitstellung nach Zeitplan unabhängig von Benutzeranmeldung**: Diese Option ist nicht verfügbar, wenn Sie eine Tasksequenz bereitstellen.  

    -   **Aktivierungspakete senden**: Wenn der Bereitstellungszweck auf **Erforderlich** festgelegt und diese Option ausgewählt ist, wird vor der Installation der Bereitstellung ein Aktivierungspaket an den Computer gesendet, um ihn zum Zeitpunkt der Installation aus dem Standbymodus zu aktivieren. Sie können diese Option nur verwenden, wenn Computer und Netzwerke für Wake-On-LAN konfiguriert sind.  

    -   **Clients mit einer getakteten Internetverbindung dürfen den Inhalt nach dem Installationsstichtag herunterladen (Zusatzkosten können anfallen)**: Bei einer Tasksequenz, mit der eine Anwendung installiert, aber kein Betriebssystem bereitgestellt wird, können Sie angeben, ob Clients mit einer getakteten Internetverbindung Inhalt nach einem Installationsstichtag herunterladen dürfen. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.  

        > [!NOTE]  
        >  Die Verwendung einer getakteten Internetverbindung funktioniert zwar möglicherweise für Tasksequenzen, bei denen kein Betriebssystem bereitgestellt wird, aber dies wird nicht unterstützt.  

    -   **Genehmigung durch Administrator erforderlich, wenn Benutzer diese Anwendung anfordern**: Diese Option ist nicht verfügbar, wenn Sie eine Tasksequenz bereitstellen.  

    -   **Verfügbar machen für**: Geben Sie an, ob die Tasksequenz für Configuration Manager-Clients, Medien oder die PXE verfügbar sein soll.  

        > [!IMPORTANT]  
        >  Verwenden Sie die Einstellung **Nur Medien und PXE (ausgeblendet)** für automatisierte Bereitstellungen von Tasksequenzen. Aktivieren Sie die Option **Unbeaufsichtigte Betriebssystembereitstellung zulassen** , und legen Sie die Variable "SMSTSPreferredAdvertID" als Teil des Mediums fest, damit der Computer bei der Bereitstellung ohne Benutzerinteraktion automatisch gestartet wird. Weitere Informationen zu Tasksequenzvariablen finden Sie unter [Integrierte Tasksequenzvariablen](../understand/task-sequence-built-in-variables.md)  

7.  Geben Sie auf der Seite **Zeitplanung** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    > [!IMPORTANT]  
    >  Bei ein Windows PE-Client von PXE oder von Startmedien gestartet wird, wertet der Client keine Bereitstellungspläne (Start-, Ablauf- oder Stichtagzeiten) aus. Konfigurieren Sie Zeitpläne nur in Bereitstellungen auf Clients, die vom vollständigen Windows-Betriebssystem gestartet werden. Ziehen Sie die Verwendung anderer Methoden in Betracht, z. B. Wartungsfenster, um aktive Tasksequenzen für Clients zu steuern, die von Windows PE gestartet werden.  

    -   **Verfügbarkeitsdatum der Bereitstellung festlegen**: Geben Sie den Zeitpunkt (Datum und Uhrzeit) an, zu dem die Tasksequenz zur Ausführung auf dem Zielcomputer verfügbar ist. Wenn Sie das Kontrollkästchen **UTC** aktivieren, ist die Tasksequenz zum gleichen Zeitpunkt für mehrere Zielcomputer verfügbar, anstatt der lokalen Zeit auf den Zielcomputern entsprechend zu unterschiedlichen Zeitpunkten.  

         Wenn die Startzeit vor der erforderlichen Zeit liegt, wird die Tasksequenz vom Client zu der von Ihnen angegebenen Startzeit heruntergeladen.  

    -   **Ablaufdatum der Bereitstellung festlegen**: Geben Sie den Zeitpunkt (Datum und Uhrzeit) an, zu dem die Tasksequenz auf dem Zielcomputer abläuft. Wenn Sie das Kontrollkästchen **UTC** aktivieren, endet die Gültigkeit der Tasksequenz auf mehreren Zielcomputern zum gleichen Zeitpunkt, anstatt der lokalen Zeit auf den Zielcomputern entsprechend zu unterschiedlichen Zeitpunkten.  

    -   **Zuweisungszeitplan**: Geben Sie an, wann die erforderliche Tasksequenz auf dem Zielcomputer ausgeführt wird. Sie können mehrere Zeitpläne hinzufügen.  

         Sie können angeben, zu welchem Zeitpunkt der Zeitplan gestartet wird, in welchem Intervall die Ausführung der Tasksequenz erfolgt (wöchentlich, monatlich oder benutzerdefiniert) und ob die Tasksequenz nach einem Ereignis wie dem Anmelden oder Abmelden beim Computer ausgeführt wird.  

        > [!NOTE]  
        >  Wenn Sie für eine erforderliche Tasksequenz eine Startzeit planen, die vor dem Zeitpunkt liegt, zu dem die Tasksequenz verfügbar ist, wird die Tasksequenz vom Configuration Manager-Client zur geplanten Startzeit heruntergeladen, auch wenn sie bereits früher verfügbar ist.  

    -   **Verhalten beim erneuten Ausführen**: Geben Sie an, wann die Tasksequenz erneut ausgeführt wird. Sie können eine der folgenden Optionen angeben.  

        -   **Bereitgestelltes Programm nie erneut ausführen**: Die Tasksequenz wird auf dem Client nicht erneut ausgeführt, wenn sie bereits auf dem Client ausgeführt wurde. Die Tasksequenz wird selbst dann nicht erneut ausgeführt, wenn bei der ursprünglichen Ausführung ein Fehler aufgetreten ist oder die Tasksequenzdateien geändert wurden.  

        -   **Programm immer erneut ausführen**: Die Tasksequenz wird auf dem Client immer erneut ausgeführt, wenn die Bereitstellung geplant ist, auch dann, wenn die Tasksequenz bereits erfolgreich ausgeführt wurde. Diese Einstellung ist insbesondere nützlich, wenn Sie wiederholte Bereitstellungen verwenden, bei denen routinemäßig ein Update der Tasksequenz ausgeführt wird.  

            > [!IMPORTANT]  
            >  Diese Option wird zwar standardmäßig festgelegt, aber sie hat keine Auswirkungen, bis Sie eine erforderliche Bereitstellung zuweisen. Verfügbare Bereitstellungen können stets von einem Benutzer erneut ausgeführt werden.  

        -   **Bei fehlgeschlagenem vorherigem Versuch erneut ausführen**: Die Tasksequenz wird bei geplanter Bereitstellung nur dann erneut ausgeführt, wenn bei der vorherigen Ausführung ein Fehler aufgetreten ist. Diese Einstellung ist insbesondere bei erforderlichen Bereitstellungen nützlich. Die Ausführung dieser Bereitstellungen wird dem Zuweisungszeitplan entsprechend automatisch erneut versucht, wenn der letzte Ausführungsversuch nicht erfolgreich war.  

        -   Bei erfolgreichem vorherigen Versuch erneut ausführen: Die Tasksequenz wird nur dann erneut ausgeführt, wenn sie auf dem Client bereits erfolgreich ausgeführt wurde. Diese Einstellung ist nützlich, wenn Sie wiederholte Bereitstellungen verwenden, bei denen routinemäßig ein Update der Tasksequenz ausgeführt wird, und jedes dieser Updates nur möglich ist, wenn das vorherige Update erfolgreich installiert wurde.  

        > [!NOTE]  
        >  Da ein Benutzer eine verfügbare Tasksequenzbereitstellung erneut ausführen kann, prüfen und testen Sie eingehend, welche Auswirkungen die mehrmalige erneute Ausführung der Tasksequenz durch einen Benutzer hat, bevor Sie eine verfügbare Tasksequenz in einer Produktionsumgebung bereitstellen.  

8.  Geben Sie auf der Seite **Benutzerfreundlichkeit** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   **Benutzern zuweisungsunabhängige Programmausführung erlauben**: Geben Sie an, ob der Benutzer eine erforderliche Tasksequenz unabhängig von den Bereitstellungszuweisungen ausführen darf.  

    -   **Tasksequenzstatus anzeigen**: Geben Sie an, ob der Status der Tasksequenz vom Configuration Manager-Client angezeigt wird.  

    -   **Softwareinstallation**: Geben Sie an, ob der Benutzer außerhalb eines konfigurierten Wartungsfensters nach dem geplanten Zeitpunkt Software installieren darf.  

    -   **Systemneustart (falls dieser zum Abschluss der Installation erforderlich ist)**: Geben Sie an, ob der Benutzer den Computer im Anschluss an eine Softwareinstallation außerhalb eines konfigurierten Wartungsfensters nach der Zuweisungszeit neu starten darf.  

    -   **Ausführung der Tasksequenz für internetbasierten Client zulassen**: Geben Sie an, ob die Tasksequenz auf einem internetbasierten Client ausgeführt werden darf, der von Configuration Manager im Internet erkannt wird. Vorgänge, mit denen Software wie ein Betriebssystem installiert wird, werden von dieser Einstellung nicht unterstützt. Verwenden Sie diese Option nur für generische skriptbasierte Tasksequenzen, mit denen Vorgänge im Standardbetriebssystem ausgeführt werden.  

9. Geben Sie auf der Seite **Warnungen** die für diese Tasksequenzbereitstellung gewünschten Warnungseinstellungen an, und klicken Sie dann auf **Weiter**.  

10. Geben Sie auf der Seite **Verteilungspunkte** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   **Bereitstellungsoptionen:**: Geben Sie eine der folgenden Optionen an:  

        > [!NOTE]  
        >  Wenn Sie zum Bereitstellen eines Betriebssystems einen Multicast verwenden, muss der Inhalt entweder je nach Bedarf oder vor Ausführung der Tasksequenz auf die Zielcomputer heruntergeladen werden.  

        -   Geben Sie an, dass Clients den Inhalt vom Verteilungspunkt auf den Zielcomputer herunterladen, wenn dieser von der Tasksequenz benötigt wird.  

        -   Geben Sie an, dass Clients den gesamten Inhalt vom Verteilungspunkt auf den Zielcomputer herunterladen, bevor die Tasksequenz ausgeführt wird. Diese Option wird nicht angezeigt, wenn Sie angegeben haben, dass die Tasksequenz für die Bereitstellung per PXE und Startmedien verfügbar ist (siehe Seite **Bereitstellungseinstellungen** ).  

        -   Geben Sie an, dass Clients den Inhalt vom Verteilungspunkt ausführen. Diese Option ist nur verfügbar, wenn alle der Tasksequenz zugeordneten Pakete für die Verwendung einer Paketfreigabe auf dem Verteilungspunkt aktiviert sind. Verwenden Sie für ein Paket unter **Eigenschaften** jeweils die Registerkarte **Datenzugriff** , um für Inhalte die Nutzung einer Paketfreigabe zu aktivieren.  

    -   **Remoteverteilungspunkt verwenden, wenn kein lokaler Verteilungspunkt verfügbar ist**: Geben Sie an, ob Verteilungspunkte in langsamen und unzuverlässigen Netzwerken von Clients zum Herunterladen des Inhalts verwendet werden können, der für die Tasksequenz erforderlich ist.  

11. Schließen Sie den Assistenten ab.  

##  <a name="BKMK_ExportImport"></a> Exportieren und Importieren von Tasksequenzen  
 Sie können Tasksequenzen exportieren und importieren und dabei nach Wunsch die zugehörigen Objekte einschließen, beispielsweise ein Betriebssystemabbild, ein Startabbild, ein Client-Agent-Paket, ein Treiberpaket sowie Anwendungen mit Abhängigkeiten.  

 Beachten Sie beim Exportieren und Importieren von Tasksequenzen die folgenden Punkte.  

-   Kennwörter, die in der Tasksequenz gespeichert sind, werden nicht exportiert. Wenn Sie eine Tasksequenz exportieren und importieren, die Kennwörter enthält, müssen Sie die importierte Tasksequenz bearbeiten und sämtliche Kennwörter erneut angeben. Achten Sie darauf, Kennwörter für die Aktionen [Einer Domäne oder Arbeitsgruppe beitreten](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup), [Verbindung mit Netzwerkordner herstellen](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) und [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine) anzugeben.  

- Wenn Sie eine Tasksequenz mit dem Schritt **Set Dynamic Variables** (Dynamische Variablen festlegen) exportieren, werden keine Werte für Variablen exportiert, die die Einstellung **Secret value** (Geheimer Wert) haben. Sie müssen die Werte für diese Variablen erneut eingeben, nachdem Sie die Tasksequenz importiert haben.

-   Wenn mehrere primäre Standorte vorliegen, wird empfohlen, Tasksequenzen am Standort der zentralen Verwaltung zu importieren.  

 Gehen Sie wie folgt vor, um eine Tasksequenz zu exportieren und zu importieren.  

#### <a name="to-export-task-sequences"></a>So exportieren Sie Tasksequenzen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Wählen Sie in der Liste **Tasksequenz** die Tasksequenzen aus, die Sie exportieren möchten. Wenn Sie mehrere Tasksequenzen auswählen, werden diese in einer Exportdatei gespeichert.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Tasksequenz** auf **Exportieren** , um den Assistenten zum Exportieren von Tasksequenzen zu starten.  

5.  Geben Sie auf der Seite **Allgemein** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   Geben Sie im Feld **Datei** den Speicherort und den Namen der Exportdatei an. Wenn Sie den Dateinamen direkt eingeben, achten Sie darauf, an den Dateinamen die Erweiterung ZIP anzuhängen. Wenn Sie nach der Exportdatei suchen, wird diese Dateinamenerweiterung vom Assistenten automatisch hinzugefügt.  

    -   Deaktivieren Sie das Kontrollkästchen **Alle Tasksequenzabhängigkeiten exportieren** , wenn Sie keine Tasksequenzabhängigkeiten exportieren möchten. Standardmäßig werden alle zugehörigen Objekte vom Assistenten gesucht und zusammen mit der Tasksequenz exportiert. Dazu gehören alle Abhängigkeiten für Anwendungen.  

    -   Deaktivieren Sie das Kontrollkästchen **Alle Inhalte für die ausgewählten Anwendungen und Abhängigkeiten exportieren** , wenn Sie den Inhalt nicht von der Paketquelle in den Exportpfad kopieren möchten. Wenn dieses Kontrollkästchen aktiviert ist, wird der Importpfad vom Assistenten zum Importieren von Tasksequenzen als neuer Paketquellpfad verwendet.  

    -   Geben Sie im Feld **Administratorkommentare** eine Beschreibung der zu exportierenden Tasksequenzen ein.  

6.  Schließen Sie den Assistenten ab.  

 Die folgenden Ausgabedateien werden vom Assistenten erstellt:  

-   Wenn Sie keinen Inhalt exportieren, wird eine ZIP-Datei erstellt.  

-   Wenn Sie Inhalt exportieren, werden eine ZIP-Datei und ein Ordner namens *Export*_files erstellt. Dabei ist *Export* der Name der ZIP-Datei mit dem exportierten Inhalt.  

 Wenn Sie beim Exportieren einer Tasksequenz auch den Inhalt einschließen, müssen Sie die ZIP-Datei und den Ordner *Export*_files kopieren. Andernfalls tritt beim Import ein Fehler auf.  

#### <a name="to-import-task-sequences"></a>So importieren Sie Tasksequenzen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenz importieren** , um den Assistenten zum Importieren von Tasksequenzen zu starten.  

4.  Geben Sie auf der Seite **Allgemein** die exportierte ZIP-Datei an, und klicken Sie dann auf **Weiter**.  

5.  Wählen Sie auf der Seite **Dateiinhalt** für jedes importierte Objekt die gewünschte Aktion aus. Auf dieser Seite werden alle Objekte angezeigt, die Configuration Manager importiert.  

    -   Wenn ein Objekt noch nie importiert wurde, wählen Sie **Neu erstellen**aus.  

    -   Wenn ein Objekt bereits importiert wurde, wählen Sie eine der folgenden Aktionen aus:  

        -   **Duplikat ignorieren** (Standard): Bei dieser Aktion wird das Objekt nicht importiert. Stattdessen wird das vorhandene Objekt vom Assistenten mit der Tasksequenz verknüpft.  

        -   **Überschreiben**: Bei dieser Aktion wird das vorhandene Objekt vom importierten Objekt überschrieben. Sie können Anwendungen eine Revision hinzufügen, um ein Update der vorhandenen Anwendung auszuführen oder eine neue Anwendung zu erstellen.  

6.  Schließen Sie den Assistenten ab.  

 Bearbeiten Sie die Tasksequenz nach dem Import, um Kennwörter anzugeben, die bei der ursprünglichen Tasksequenz verwendet wurden. Kennwörter werden aus Sicherheitsgründen nicht exportiert.  

##  <a name="BKMK_CreateTSVariables"></a> Erstellen von Tasksequenzvariablen für Computer und Sammlungen  
Sie können benutzerdefinierte Tasksequenzvariablen für Computer und Sammlungen definieren. Für einen Computer definierte Variablen werden als computerspezifische Tasksequenzvariablen bezeichnet. Für eine Sammlung definierte Variablen werden als sammlungsspezifische Tasksequenzvariablen bezeichnet. Bei einem Konflikt haben computerspezifische Variablen Vorrang vor den sammlungsspezifischen Variablen. Die einem bestimmten Computer zugewiesenen Tasksequenzvariablen haben also automatisch eine höhere Priorität als Variablen, die der Sammlung zugewiesen wurden, in der der Computer sich befindet.  

Angenommen, der Sammlung ABC und dem Computer XYZ, der Mitglied der Sammlung ABC ist, wurde jeweils eine gleichnamige Variable zugewiesen. In diesem Fall hat die Variable, die dem Computer XYZ zugewiesen wurde, eine höhere Priorität als die der Sammlung ABC zugewiesene Variable.  

Sie können computerspezifische und sammlungsspezifische Variablen ausblenden, damit sie in der Configuration Manager-Konsole nicht sichtbar sind. Wenn Sie wünschen, dass diese Variablen nicht mehr ausgeblendet werden, müssen Sie sie löschen und anschließend erneut definieren, ohne die Option zum Ausblenden der Variablen auszuwählen. Bei Verwendung der Option **Diesen Wert nicht in der Configuration Manager-Konsole anzeigen** wird der Wert der Variablen in der Konsole nicht angezeigt, kann aber immer noch von der Tasksequenz verwendet werden, wenn diese ausgeführt wird.  

> [!WARNING]    
> Die Einstellung **Diesen Wert nicht in der Configuration Manager-Konsole anzeigen** gilt für die Configuration Manager-Konsole, aber die Werte für die Variablen werden weiterhin in der Protokolldatei der Tasksequenz (SMSTS.LOG) angezeigt. 

Sie können computerspezifische Variablen an einem primären Standort oder an einem Standort der zentralen Verwaltung verwalten. Configuration Manager unterstützt je Computer maximal 1000 zugewiesene Variablen.  

> [!IMPORTANT]  
>  Bei der Verwendung sammlungsspezifischer Variablen für Tasksequenzen ist Folgendes zu beachten:  
>   
> - Änderungen an Sammlungen werden immer in der gesamten Hierarchie repliziert. Daher gelten alle Änderungen, die Sie an Sammlungsvariablen vornehmen, nicht nur für die Mitglieder des aktuellen Standorts, sondern für alle Mitglieder der Sammlung in der gesamten Hierarchie.  
> - Wenn Sie eine Sammlung löschen, werden auch die Tasksequenzvariablen gelöscht, die für die Sammlung konfiguriert sind.  

 Gehen Sie wie folgt vor, um Tasksequenzvariablen für einen Computer oder eine Sammlung zu erstellen.  

#### <a name="to-create-task-sequence-variables-for-a-computer"></a>So erstellen Sie Tasksequenzvariablen für einen Computer  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die Sammlung, die den Computer enthält, dem Sie die Variable hinzufügen möchten.  

3.  Wählen Sie den Computer aus, und klicken Sie auf **Eigenschaften**.  

4.  Klicken Sie im Dialogfeld **Eigenschaften** auf die Registerkarte **Variablen** .  

5.  Klicken Sie im Dialogfeld **<Neue\> Variable** für jede Variable, die Sie erstellen möchten, auf das Symbol **Neu**. Geben Sie dann den Namen und den Wert der Tasksequenzvariablen an. Deaktivieren Sie das Kontrollkästchen **Diesen Wert nicht in der Configuration Manager-Konsole anzeigen**, wenn Sie die Variablen ausblenden möchten, damit sie in der Configuration Manager-Konsole nicht sichtbar sind.  

6.  Klicken Sie auf **OK**, nachdem Sie dem Computer alle Variablen hinzugefügt haben.  

#### <a name="to-create-task-sequence-variables-for-a-collection"></a>So erstellen Sie Tasksequenzvariablen für eine Sammlung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Wählen Sie im Arbeitsbereich **Bestand und Kompatibilität** die Sammlung aus, der Sie die Variable hinzufügen möchten, und klicken Sie auf **Eigenschaften**.  

3.  Klicken Sie im Dialogfeld **Eigenschaften** auf die Registerkarte **Sammlungsvariablen** .  

4.  Klicken Sie im Dialogfeld **<Neue\> Variable** für jede Variable, die Sie erstellen möchten, auf das Symbol **Neu**. Geben Sie dann den Namen und den Wert der Tasksequenzvariablen an. Deaktivieren Sie das Kontrollkästchen **Diesen Wert nicht in der Configuration Manager-Konsole anzeigen**, wenn Sie die Variablen ausblenden möchten, damit sie in der Configuration Manager-Konsole nicht sichtbar sind.  

5.  Geben Sie optional die Priorität an, die bei der Auswertung der Tasksequenzvariablen durch Configuration Manager gelten soll.  

6.  Klicken Sie auf **OK**, nachdem Sie der Sammlung alle Variablen hinzugefügt haben.  

##  <a name="BKMK_AdditionalActionsTS"></a> Zusätzliche Aktionen zum Verwalten von Tasksequenzen  
 Für die Verwaltung von Tasksequenzen können Sie zusätzliche Aktionen verwenden, wenn Sie die Tasksequenz auswählen.  

#### <a name="to-select-a-task-sequence-to-manage"></a>So wählen Sie eine Tasksequenz zur Verwaltung aus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme** , und klicken Sie dann auf **Tasksequenzen**.  

3.  Wählen Sie in der Liste **Tasksequenz** die Tasksequenz aus, die Sie verwalten möchten. Wählen Sie dann eine der verfügbaren Optionen aus.  

 Die folgende Tabelle enthält weitere Informationen zu einigen der zusätzlichen Aktionen zur Verwaltung von Tasksequenzen.  

|Aktion|Beschreibung|  
|------------|-----------------|  
|**Kopieren**|Hiermit wird eine Kopie der ausgewählten Tasksequenz erstellt. Diese Aktion kann sich als nützlich erweisen, wenn Sie eine neue Tasksequenz erstellen möchten, die auf einer vorhandenen Tasksequenz basiert.<br /><br /> Wenn Sie in einem Ordner eine Kopie einer Tasksequenz erstellen, wird die Kopie in diesem Ordner aufgeführt, bis Sie den Tasksequenzknoten aktualisieren.  Nach der Aktualisierung wird die Kopie im Stammordner angezeigt.|  
|**Deaktivieren**|Hiermit wird die Tasksequenz deaktiviert, damit sie nicht auf Computern ausgeführt werden kann. Deaktivierte Tasksequenzen können zwar an Computer bereitgestellt werden, aber sie werden von den Computern erst ausgeführt, nachdem sie aktiviert wurden.|  
|**Aktivieren**|Hiermit wird die Tasksequenz aktiviert, damit sie ausgeführt werden kann. Es ist nicht notwendig, eine bereitgestellte Tasksequenz nach der Aktivierung erneut bereitzustellen.|  
|**Datei für vorab bereitgestellten Inhalt erstellen**|Hiermit wird der Assistenten zum Erstellen von vorab bereitgestellten Inhaltsdateien gestartet, mit dem der Inhalt der Tasksequenz vorab bereitgestellt wird. Informationen zum Erstellen einer vorab bereitgestellten Inhaltsdatei finden Sie unter [Vorabbereitstellen von Inhalt](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).|  
|**Verschieben**|Hiermit wird die ausgewählte Tasksequenz in einen anderen Ordner verschoben.|  

## <a name="next-steps"></a>Nächste Schritte
[Szenarien für die Bereitstellung von Unternehmensbetriebssystemen](scenarios-to-deploy-enterprise-operating-systems.md)
