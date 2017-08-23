---
title: Verwalten der Softwareupdatesynchronisierung | Microsoft-Dokumentation
description: "So planen Sie die Softwareupdatesynchronisierung, starten die Softwareupdatesynchronisierung manuell, und überwachen die Softwareupdatesynchronisierung."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
ms.openlocfilehash: e68170a16a6a908e035247ed9c0f3cc6cdbe1983
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_SUMSync"></a> Synchronisieren von Softwareupdates

*Gilt für: System Center Configuration Manager (Current Branch)*

 Bei der Softwareupdatesynchronisierung in Configuration Manager werden die Metadaten für Softwareupdates abgerufen, die die von Ihnen festgelegten Kriterien erfüllen. Dies umschließt bestimmte Produkte, Klassifizierungen und Sprachen. Standardmäßig werden Metadaten vom Softwareupdatepunkt am Standort der zentralen Verwaltung bzw. an einem eigenständigen primären Standort von Microsoft Update abgerufen. Anschließend sendet der Standortserver auf oberster Ebene eine Synchronisierungsanforderung an andere Standorte. Wenn die Synchronisierungsanforderung vom übergeordneten Standort bei einem Standort eingeht, werden die Metadaten für das Softwareupdate vom Softwareupdatepunkt des Standorts aus der Upstream[synchronisierungsquelle](../plan-design/plan-for-software-updates.md#BKMK_SyncSource) abgerufen. Weitere Informationen zur Synchronisierung von Softwareupdates finden Sie unter [Software updates synchronization (Informationen zur Softwaresynchronisierung)](../understand/software-updates-introduction.md#BKMK_Synchronization).

Sie legen für die Ausführung der Softwareupdatesynchronisierung einen Zeitplan fest, wenn Sie die Eigenschaften des Softwareupdatepunkts am Standort der obersten Ebene konfigurieren. Nachdem Sie den Synchronisierungszeitplan festgelegt haben, ändern Sie ihn in der Regel während des normalen Betriebs nicht mehr. Allerdings können Sie die Softwareupdatesynchronisierung bei Bedarf manuell initiieren.

  > [!NOTE]  
  >  Softwareupdatepunkte müssen mit der Upstreamsynchronisierungsquelle verbunden sein, damit Softwareupdates synchronisiert werden können. Wenn ein Softwareupdatepunkt von der Upstreamsynchronisierungsquelle getrennt ist, können Sie Softwareupdates mithilfe der Export-Import-Methode synchronisieren. Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates bei einem getrennten Softwareupdatepunkt](synchronize-software-updates-disconnected.md).  

## <a name="schedule-software-updates-synchronization"></a>Planen der Softwareupdatesynchronisierung
Wenn Sie einen Zeitplan für die Softwareupdatesynchronisierung konfigurieren, wird die Synchronisierung mit Microsoft Update vom Softwareupdatepunkt am Standort der obersten Ebene am geplanten Tag und zur geplanten Zeit gestartet. Mit einem benutzerdefinierten Zeitplan können Sie Softwareupdates zu einem Zeitpunkt synchronisieren, zu dem die Anforderungen des WSUS-Servers, Standortservers und Netzwerks gering sind. Beispielsweise können Sie den Zeitplan so festlegen, dass Softwareupdates jede Woche um 2:00 Uhr synchronisiert werden. Im Rahmen der geplanten Synchronisierung werden alle Änderungen, die seit der letzten geplanten Synchronisierung an den Metadaten für das Softwareupdate vorgenommen wurden, in die Standortdatenbank eingefügt. Dazu gehören neue Metadaten für das Softwareupdate und Metadaten, die geändert oder entfernt wurden bzw. zwischenzeitlich abgelaufen sind.

Gehen Sie am Standort der obersten Ebene wie folgt vor, um die Softwareupdatesynchronisierung zu planen.  

#### <a name="to-schedule-software-updates-synchronization"></a>So planen Sie die Softwareupdatesynchronisierung  

  1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

  2.  Erweitern Sie im Arbeitsbereich **Verwaltung**den Bereich **Standortkonfiguration**, und klicken Sie dann auf "Standorte".  

  3.  Klicken Sie im Ergebnisbereich auf den Standort der zentralen Verwaltung oder einen eigenständigen primären Standort.  

  4.  Erweitern Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** den Eintrag **Standortkomponenten konfigurieren**, und klicken Sie dann auf **Softwareupdatepunkt**.  

  5.  Wählen Sie im Dialogfeld "Eigenschaften der Softwareupdatepunktkomponente" die Option **Synchronisierung nach Zeitplan aktivieren**aus, und geben Sie dann den Synchronisierungszeitplan an.  

## <a name="manually-start-software-updates-synchronization"></a>Manuelles Initiieren der Softwareupdatesynchronisierung
Sie können die Softwareupdatesynchronisierung am Standort der obersten Ebene in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** über den Knoten **Alle Softwareupdates** manuell initiieren.  

Gehen Sie am Standort der obersten Ebene wie folgt vor, um die Softwareupdatesynchronisierung manuell zu initiieren.  

#### <a name="to-manually-start-software-updates-synchronization"></a>So initiieren Sie die Softwareupdatesynchronisierung manuell  

  1.  Klicken Sie in der mit dem Standort der zentralen Verwaltung, oder einem eigenständigen primären Standort verbundenen Configuration Manager-Konsole auf **Softwarebibliothek**.  

  2.  Erweitern Sie im Arbeitsbereich "Softwarebibliothek" den Eintrag **Softwareupdates** , und klicken Sie auf **Alle Softwareupdates** oder **Softwareupdategruppen**.  

  3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Softwareupdates synchronisieren**. Bestätigen Sie im Dialogfeld, dass Sie die Synchronisierung initiieren möchten, indem Sie auf **Ja** klicken.  

   Nach dem Start der Synchronisierung auf dem Softwareupdatepunkt können Sie den Synchronisierungsprozess in der Configuration Manager-Konsole bei allen Softwareupdatepunkten in der Hierarchie überwachen. Gehen Sie wie folgt vor, um die Softwareupdatesynchronisierung zu überwachen.  


## <a name="monitor-software-updates-synchronization"></a>Überwachen der Softwareupdatesynchronisierung
Nach dem Start der Synchronisierung können Sie den Prozess in der Configuration Manager-Konsole für alle Softwareupdatepunkte in der Hierarchie überwachen. Gehen Sie wie folgt vor, um die Softwareupdatesynchronisierung zu überwachen. Weitere Informationen zur Überwachung von Softwareupdates und der Synchronisierung finden Sie unter [Monitor software updates (Überwachen von Softwareupdates)](../deploy-use/monitor-software-updates.md).

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>So überwachen Sie die Softwareupdatesynchronisierung  

  1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

  2.  Klicken Sie im Arbeitsbereich **Überwachung** auf **Synchronisierungsstatus der Softwareupdatepunkte**.  

    Die Softwareupdatepunkte in der Configuration Manager-Hierarchie werden im Ergebnisbereich angezeigt. Von hier können Sie den Synchronisierungsstatus aller Softwareupdatepunkte überwachen. Ausführlichere Informationen zum Synchronisierungsprozess finden Sie in der Datei „wsyncmgr.log“, die sich auf jedem Standortserver im Ordner „<*Installationspfad von Configuration Manager*>\Logs“ befindet.  

## <a name="next-steps"></a>Nächste Schritte
Nachdem Softwareupdates zum ersten Mal synchronisiert wurden, oder wenn neue Klassifizierungen oder Produkte verfügbar sind, müssen Sie [die neuen Klassifizierungen und Produkte so konfigurieren](configure-classifications-and-products.md), dass Softwareupdates mit den neuen Kriterien synchronisiert werden.

Nachdem Sie Softwareupdates mit den erforderlichen Kriterien synchronisiert haben, [verwalten Sie Einstellungen für Softwareupdates](manage-settings-for-software-updates.md).  
