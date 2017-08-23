---
title: "Überwachen von Inhalt | Microsoft-Dokumentation"
description: "Hier finden Sie Informationen zur Überwachung von verteiltem Inhalt mithilfe der Configuration Manager-Konsole."
ms.custom: na
ms.date: 4/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7659d5789b8ce4e9e0b585a331c8f68869c9492d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Überwachen von mit System Center Configuration Manager verteilten Inhalten

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit der System Center Configuration Manager-Konsole können Sie unter anderem die folgenden verteilten Inhalte überwachen:  

-   Den Status aller Pakettypen im Zusammenhang mit den zugeordneten Verteilungspunkten.  
-   Den Inhaltsprüfungsstatus des Paketinhalts.  
-   Den Status von Inhalt, der einer bestimmten Verteilungspunktgruppe zugeordnet ist.  
-   Den Zustand von Inhalt, der einem Verteilungspunkt zugeordnet ist.  
-   Den Status optionaler Features jedes Verteilungspunkts (Inhaltsprüfung, PXE und Multicast).  

> [!NOTE]  
>  Von Configuration Manager wird nur der Inhalt auf einem Verteilungspunkt überwacht, der sich in der Inhaltsbibliothek befindet. Inhalt, der auf dem Verteilungspunkt in Paketfreigaben oder benutzerdefinierten Freigaben gespeichert ist, wird nicht überwacht.  

##  <a name="BKMK_ContentStatus"></a> Überwachung des Inhaltsstatus  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Inhaltsstatus** Informationen zu Inhaltspaketen. In der Configuration Manager-Konsole können Sie z.B. folgende Informationen überprüfen:  

-   Den Paketnamen.  
-   Den Typ.  
-   An wie viele Verteilungspunkte ein Paket gesendet wurde.  
-   Die Kompatibilitätsrate.  
-   Wann das Paket erstellt wurde.  
-   Die Paket-ID.  
-   Die Quellversion.  

Außerdem finden Sie hier detaillierte Statusinformationen zu allen Paketen sowie den Verteilungsstatus eines Pakets, einschließlich:  

-   Fehleranzahl.  
-   Ausstehende Verteilungen.  
-   Anzahl der Installationen.

Sie können außerdem Verteilungen an einen Verteilungspunkt verwalten, die noch in Bearbeitung sind bzw. aufgrund von Fehlern nicht erfolgreich ausgeführt werden konnten:  

-   Die Option zum Abbrechen oder erneuten Verteilen des Inhalts ist verfügbar, wenn Sie im Fensterbereich **Bestandsdetails** die Bereitstellungsstatusmeldung zu einem Verteilungsauftrag an einen Verteilungspunkt anzeigen. Diesen Bereich finden Sie entweder auf der Registerkarte **In Bearbeitung** oder auf der Registerkarte **Fehler** des Knotens **Inhaltsstatus**.  
-   Darüber hinaus wird in den Auftragsdetails der Prozentsatz des Auftrags angezeigt, der beim Anzeigen der Details eines Auftrags auf der Registerkarte **In Bearbeitung** abgeschlossen wurde. Außerdem werden in den Auftragsdetails die Anzahl der für einen Auftrag verbleibenden Wiederholungsversuche und der Zeitraum bis zur nächsten Wiederholung angezeigt, wenn Sie die Details eines Auftrags aufrufen, der auf der Registerkarte **Fehler** verfügbar ist.  

Beim Abbrechen einer Bereitstellung, die noch nicht abgeschlossen ist, wird der Verteilungsauftrag zur Übertragung des betreffenden Inhalts beendet:  

-   Der Status der Bereitstellung wird dann aktualisiert, um anzuzeigen, dass die Verteilung nicht durchgeführt werden konnte und von einer Benutzeraktion abgebrochen wurde.  
-   Dieser neue Status wird auf der Registerkarte **Fehler** angezeigt.  

> [!TIP]  
>  Wenn eine Bereitstellung fast abgeschlossen ist, kann es sein, dass ein Befehl zum Abbruch der Verteilung nicht rechtzeitig vor Ende der Verteilung an den Verteilungspunkt verarbeitet werden kann. In diesem Fall wird der Abbruch der Bereitstellung ignoriert, und der Status der Bereitstellung wird als erfolgreich angezeigt.  

> [!NOTE]  
>  Zwar können Sie die Option zum Abbrechen einer Verteilung an einen Verteilungspunkt auf einem Standortserver auswählen, aber diese Auswahl ist unwirksam. Dies liegt daran, dass der Standortserver und der Verteilungspunkt auf einem Standortserver den gleichen Single Instance Content Store verwenden. Es gibt keinen tatsächlichen Verteilungsauftrag, der abgebrochen werden könnte.  

Beim erneuten Verteilen von Inhalt an einen Verteilungspunkt, bei dessen Übertragung zuvor ein Fehler auftrat, beginnt der Configuration Manager sofort mit der erneuten Bereitstellung des Inhalts an den Verteilungspunkt. Der Status der Bereitstellung wird entsprechend aktualisiert, um den laufenden Stand der erneuten Bereitstellung widerzuspiegeln.  

Gehen Sie wie folgt vor, um den Inhaltsstatus anzuzeigen und Verteilungen zu verwalten, die noch in Bearbeitung sind oder aufgrund von Fehlern nicht abgeschlossen werden konnten.  

### <a name="to-monitor-content-status"></a>So überwachen Sie den Inhaltsstatus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Inhaltsstatus**. Die Pakete werden angezeigt.  

3.  Wählen Sie das Paket aus, für das Sie detaillierte Statusinformationen anzeigen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** auf **Status anzeigen**. Detaillierte Statusinformationen zum Paket werden angezeigt.  

### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>So brechen Sie eine Verteilung ab, die noch in Bearbeitung ist  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Inhaltsstatus**. Die Pakete werden angezeigt.  

3.  Wählen Sie das Paket aus, das Sie verwalten wollen, und klicken Sie im Detailbereich auf **Status anzeigen**.  

4.  Klicken Sie im Fensterbereich **Bestandsdetails** auf der Registerkarte **In Bearbeitung** mit der rechten Maustaste auf den Eintrag der Verteilung, die Sie abbrechen möchten, und wählen Sie **Abbrechen**.  

5.  Klicken Sie auf **Ja** , um den Vorgang zu bestätigen und den Verteilungsauftrag an den betreffenden Verteilungspunkt abzubrechen.  

### <a name="to-redistribute-content-that-failed-to-distribute"></a>So verteilen Sie Inhalt erneut, dessen Verteilung aufgrund von Fehlern nicht abgeschlossen werden konnte  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Inhaltsstatus**. Die Pakete werden angezeigt.  

3.  Wählen Sie das Paket aus, das Sie verwalten wollen, und klicken Sie im Detailbereich auf **Status anzeigen**.  

4.  Klicken Sie im Fensterbereich **Bestandsdetails** auf der Registerkarte **Fehler** mit der rechten Maustaste auf den Eintrag der Verteilung, die Sie erneut verteilen möchten, und wählen Sie **Neu verteilen**.  

5.  Klicken Sie auf **Ja**, um die Aktion zu bestätigen und den erneuten Verteilungsvorgang an den betreffenden Verteilungspunkt zu starten.  

## <a name="distribution-point-group-status"></a>Status der Verteilungspunktgruppe  
Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktgruppe** Informationen zu Verteilungspunktgruppen. Sie können z. B. folgende Informationen überprüfen:  

-   Den Namen der Verteilungspunktgruppe.  
-   Die Beschreibung.  
-   Wie viele Verteilungspunkte zur Verteilungspunktgruppe gehören.  
-   Wie viele Pakete der Gruppe zugewiesen wurden.  
-   Den Status der Verteilungspunktgruppe.  
-   Die Kompatibilitätsrate.  

Außerdem werden folgende detaillierte Statusinformationen angezeigt:  

-   Fehler für die Verteilungspunktgruppe.  
-   Wie viele Verteilungen aktuell in Bearbeitung sind.
-   Wie viele erfolgreich verteilt wurden.  

### <a name="to-monitor-distribution-point-group-status"></a>So überwachen Sie den Status einer Verteilungspunktgruppe  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Status der Verteilungspunktgruppe**. Die Verteilungspunktgruppen werden angezeigt.  

3.  Wählen Sie die Verteilungspunktgruppe aus, für die detaillierte Statusinformationen angezeigt werden sollen.  

4.  Klicken Sie auf der Registerkarte **Startseite** auf **Status anzeigen**. Detaillierte Statusinformationen zur Verteilungspunktgruppe werden angezeigt.  

## <a name="distribution-point-configuration-status"></a>Status der Verteilungspunktkonfiguration  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktkonfiguration** Informationen zum Verteilungspunkt. Sie können überprüfen, welche Attribute für den Verteilungspunkt aktiviert sind, wie z.B. PXE, Multicast, Inhaltsprüfung und Verteilungsstatus des Verteilungspunkts. Außerdem können Sie detaillierte Statusinformationen zum Verteilungspunkt anzeigen.  

> [!WARNING]  
>  Der Status der Verteilungspunktkonfiguration bezieht sich auf die letzten 24 Stunden. Wenn der Verteilungspunkt nach einem Fehler wiederhergestellt wird, wird der Fehlerstatus möglicherweise bis zu 24 Stunden nach der Wiederherstellung des Verteilungspunkts angezeigt.  

Gehen Sie wie folgt vor, um den Status einer Verteilungspunktkonfiguration anzuzeigen.  

### <a name="to-monitor-distribution-point-configuration-status"></a>So überwachen Sie den Status einer Verteilungspunktkonfiguration  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Status der Verteilungspunktkonfiguration**. Die Verteilungspunkte werden angezeigt.  

3.  Wählen Sie den Verteilungspunkt aus, für den Statusinformationen angezeigt werden sollen.  

4.  Klicken Sie im Ergebnisbereich auf die Registerkarte **Details** . Statusinformationen zum Verteilungspunkt werden angezeigt.  

## <a name="client-data-sources-dashboard"></a>Dashboard „Clientdatenquellen“
Ab Version 1610 können Sie auch das Dashboard **Clientdatenquellen** verwenden, um mehr über die Verwendung des [Peercaches](/sccm/core/plan-design/hierarchy/client-peer-cache) in Ihrer Umgebung zu erfahren. Das Dashboard zeigt Daten an, nachdem Clients Inhalt heruntergeladen haben und diese Informationen dem Standort gemeldet wurden. Dies kann bis zu 24 Stunden dauern.

> [!TIP]  
> **Clientpeercache** und das Dashboard **Clientdatenquellen** sind vorab veröffentlichte Funktionen, die mit Version 1610 eingeführt wurden. Sie müssen Clientpeercache aktivieren, bevor das Dashboard „Clientdatenquellen“ in der Konsole angezeigt wird. Informationen zum Aktivieren von Clientpeercache finden Sie unter [Verwenden von vorab veröffentlichten Features von Updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease). Es kann bis zu 24 Stunde nach der Aktivierung dauern, bis Daten angezeigt werden.

Wechseln Sie in der Konsole zu **Überwachung** > **Verteilungsstatus** > **Clientdatenquellen**. Hier können Sie einen Zeitraum auswählen, der auf das Dashboard angewendet werden soll. Anschließend können Sie in der Anzeige die Begrenzungsgruppe oder das Paket auswählen, für die bzw. das Sie Informationen anzeigen möchten. Beim Anzeigen der Informationen können Sie Ihre Maus über der Oberfläche bewegen, um weitere Details zu den verschiedenen Inhalts- oder Richtlinienquellen zu erhalten.

Diese Details umfassen Folgendes:  
- **Client Content Sources** (Clientinhaltsquelle): Zeigt die Quelle an, von der Clients Inhalte beziehen.
- **Verteilungspunkte**: Zeigt die Anzahl der Verteilungspunkte an, die zur ausgewählten Begrenzungsgruppe gehören.
- **Clients, die einen Verteilungspunkt verwendet haben**: Zeigt an, wie viele Clients in der ausgewählten Begrenzungsgruppe zum Abrufen von Inhalten einen Verteilungspunkt verwendet haben.
- **Peer Cache sources** (Peercachequellen): Zeigt für die ausgewählte Begrenzungsgruppe an, von wie vielen Peercachequellen ein Downloadverlauf gemeldet wurde.
- **Clients, die einen Peer verwendet haben**: Zeigt an, wie viele Clients in der ausgewählten Begrenzungsgruppe zum Abrufen von Inhalten eine Peercachequelle verwendet haben.



Sie können auch einen neuen Bericht **Clientdatenquellen – Zusammenfassung** verwenden, um eine Zusammenfassung der Clientdatenquellen für die einzelnen Begrenzungsgruppen anzuzeigen.
