---
title: Pullverteilungspunkt | Microsoft-Dokumentation
description: "Erfahren Sie mehr über Konfigurationen und Einschränkungen zur Verwendung eines Pullverteilungspunkts mit System Center Configuration Manager."
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: db5039ff6cb93e3099b096196d49a1f06c315a6b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-pull-distribution-point-with-system-center-configuration-manager"></a>Verwenden eines Pullverteilungspunkts mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Ein Pullverteilungspunkt für System Center Configuration Manager ist ein Standardverteilungspunkt, der verteilte Inhalte abruft, indem diese aus einem Quellspeicherort wie einem Client heruntergeladen werden, ohne dass eine Pushübertragung der Inhalte vom Standortserver erfolgt.  

 Wenn Sie Inhalt für zahlreiche Verteilungspunkte an einem Standort bereitstellen, können Sie mithilfe von Pullverteilungspunkten nicht nur die Verarbeitungslast auf dem Standortserver verringern, sondern auch die Übertragung des Inhalts an die einzelnen Verteilungspunkte beschleunigen. Hierzu wird der Prozess der Inhaltsübertragung an jeden Verteilungspunkt vom Verteilungs-Manager-Prozess des Standortservers ausgelagert.  

-   Sie können einzelne Verteilungspunkte als Pullverteilungspunkte konfigurieren.  

-   Für jeden Pullverteilungspunkt müssen Sie mindestens einen Quellverteilungspunkt angeben, von dem Bereitstellungen abgerufen werden können (ein Pullverteilungspunkt kann Inhalte nur von einem Verteilungspunkt abrufen, der als Quellverteilungspunkt definiert ist).  

-   Wenn Sie Inhalte an einen Pullverteilungspunkt verteilen, wird der Pullverteilungspunkt vom Standortserver benachrichtigt. Daraufhin wird vom Pullverteilungspunkt das Herunterladen (Übertragen) des Inhalts von einem Quellverteilungspunkt eingeleitet. Die Inhaltsübertragung wird von jedem Pullverteilungspunkt separat verwaltet, und der Inhalt wird von einem Verteilungspunkt heruntergeladen, auf dem eine Kopie des Inhalts bereits verfügbar ist.  

Von Pullverteilungspunkten werden die gleichen Konfigurationen und Funktionen wie von herkömmlichen Configuration Manager-Verteilungspunkten unterstützt. Beispielsweise werden von einem als Pullverteilungspunkt konfigurierten Verteilungspunkt Multicast- und PXE-Konfigurationen, Inhaltsprüfung und bedarfsgesteuerte Inhaltsverteilung unterstützt. Von einem Pullverteilungspunkt werden neben der HTTP- bzw. HTTPS-Kommunikation von Clients die gleichen Zertifikatoptionen wie bei anderen Verteilungspunkten unterstützt. Zudem können Pullverteilungspunkte einzeln oder als Mitglied einer Verteilungspunktgruppe verwaltet werden.  

> [!IMPORTANT]
> Zwar wird von einem Pullverteilungspunkt die Kommunikation über HTTP und HTTPS unterstützt, doch wenn Sie Configuration Manager verwenden, können Sie nur für HTTP konfigurierte Quellverteilungspunkte angeben. Sie können mit dem Configuration Manager SDK einen Quellverteilungspunkt angeben, der für HTTPS konfiguriert ist.  

 **Im Folgenden wird die Abfolge der Ereignisse bei der Verteilung von Inhalten an einen Pullverteilungspunkt dargestellt:**  

-   Sobald Inhalt an einen Pullverteilungspunkt verteilt wird, wird vom Paketübertragungs-Manager auf dem Standortserver die Standortdatenbank überprüft, um zu ermitteln, ob der Inhalt auf einem Quellverteilungspunkt verfügbar ist. Wenn der Inhalt auf keinem Quellverteilungspunkt für den Pullverteilungspunkt verfügbar ist, wird diese Überprüfung alle 20 Minuten wiederholt, bis der Inhalt verfügbar ist.  

-   Wenn vom Paketübertragungs-Manager die Verfügbarkeit des Inhalts bestätigt wird, wird der Pullverteilungspunkt benachrichtigt, damit der Inhalt heruntergeladen wird. Nach Eingang dieser Benachrichtigung auf dem Pullverteilungspunkt wird versucht, den Inhalt von den Quellverteilungspunkten herunterzuladen.  

-   Sobald das Herunterladen auf den Pullverteilungspunkt abgeschlossen ist, wird dieser Status an den Verwaltungspunkt übermittelt. Wenn dieser Status allerdings nach 60 Minuten nicht empfangen wurde, wird der Paketübertragungs-Manager aktiviert, um auf dem Pullverteilungspunkt zu überprüfen, ob der Inhalt heruntergeladen wurde. Ist das Herunterladen des Inhalts noch nicht abgeschlossen, wird der Paketübertragungs-Manager für 60 Minuten deaktiviert, bevor der Pullverteilungspunkt erneut überprüft wird. Dieser Zyklus wird bis zum Abschluss der Inhaltsübertragung an den Pullverteilungspunkt fortgesetzt.  

**Ein Pullverteilungspunkt kann bei der Installation des Verteilungspunkts bzw. danach konfiguriert werden** , indem Sie die Eigenschaften der Standortsystemrolle „Verteilungspunkt“ bearbeiten.  

**Die Konfiguration als Pullverteilungspunkt kann durch Bearbeiten der Eigenschaften des Verteilungspunkts entfernt werden**. Wenn Sie die Konfiguration als Pullverteilungspunkt entfernen, wird der normale Betrieb vom Verteilungspunkt wiederaufgenommen. Nachfolgende Inhaltsübertragungen an den Verteilungspunkt werden vom Standortserver verwaltet.  

## <a name="limitations-for-pull-distribution-points"></a>Einschränkungen für Pullverteilungspunkte  

-   Ein cloudbasierter Verteilungspunkt kann nicht als Pullverteilungspunkt konfiguriert werden.  

-   Ein Verteilungspunkt auf einem Standortserver kann nicht als Pullverteilungspunkt konfiguriert werden.  

-   **Mit der Konfiguration für vorab bereitgestellte Inhalte wird die Konfiguration des Pullverteilungspunkts überschrieben**. Von einem für vorab bereitgestellten Inhalt konfigurierten Verteilungspunkt wird auf den Inhalt gewartet. Der Inhalt wird nicht vom Quellverteilungspunkt mithilfe von Pull übertragen, und gleichermaßen wird auf einem Standardverteilungspunkt mit der Konfiguration für vorab bereitgestellten Inhalt kein Inhalt vom Standortserver empfangen.  

-   **Bei der Inhaltsübertragung werden von einem Pullverteilungspunkt keine Konfigurationen für die Begrenzung der Datenübertragungsrate verwendet** . Wenn Sie einen bereits installierten Verteilungspunkt als Pullverteilungspunkt konfigurieren, werden Konfigurationen für die Begrenzung der Datenübertragungsrate zwar gespeichert, aber nicht verwendet. Wenn Sie die Konfiguration des Pullverteilungspunkts zu einem späteren Zeitpunkt entfernen, werden die Konfigurationen für die Begrenzung der Datenübertragungsrate wie vorgesehen implementiert.  

    > [!NOTE]  
    >  Wenn ein Verteilungspunkt als Pullverteilungspunkt konfiguriert ist, wird die Registerkarte **Begrenzung der Datenübertragungsrate** in den Eigenschaften des Verteilungspunkts nicht angezeigt.  

-   Bei der Inhaltsverteilung werden von einem Verteilungspunkt die **Wiederholungseinstellungen** nicht verwendet. **Wiederholungseinstellungen** können als Teil der **Eigenschaften der Softwareverteilungskomponente** für jeden Standort konfiguriert werden. Sie können diese Einstellungen konfigurieren, indem Sie im Arbeitsbereich **Verwaltung** der Configuration Manager-Konsole **Standortkonfiguration** erweitern und anschließend **Standorte** auswählen. Wählen Sie im Ergebnisbereich einen Standort aus, und wählen Sie dann auf der Registerkarte **Startseite** die Option **Standortkomponenten konfigurieren** aus. Abschließend wählen Sie **Softwareverteilung** aus.  

-   Zur Übertragung von Inhalt von einem Quellverteilungspunkt in einer Remotegesamtstruktur muss auf dem Computer, auf dem der Pullverteilungspunkt gehostet wird, ein Configuration Manager-Client installiert sein. Außerdem muss ein Netzwerkzugriffskonto konfiguriert sein, über das der Zugriff auf den Quellverteilungspunkt möglich ist.  

-   Auf einem als Pullverteilungspunkt konfigurierten Computer mit einem Configuration Manager-Client muss die Version des Clients mit der des Configuration Manager-Standorts übereinstimmen, von dem der Pullverteilungspunkt installiert wird. Diese Anforderung gilt für den Pullverteilungspunkt, damit die Komponente „CCMFramework“ verwendet werden kann, die vom Pullverteilungspunkt und dem Configuration Manager-Client genutzt wird.  

## <a name="about-source-distribution-points"></a>Informationen zu Quellverteilungspunkten  
 Beim Konfigurieren des Pullverteilungspunkts müssen Sie mindestens einen Quellverteilungspunkt angeben.  

-   Es werden nur Verteilungspunkte angezeigt, die als Quellverteilungspunkte infrage kommen.  

-   Ein Pullverteilungspunkt kann als Quellverteilungspunkt für einen anderen Pullverteilungspunkt angegeben werden.  

-   Nur Verteilungspunkte, von denen HTTP unterstützt wird, können als Quellverteilungspunkte angegeben werden, wenn Sie Configuration Manager verwenden.  

-   Sie können mit dem Configuration Manager SDK einen Quellverteilungspunkt angeben, der für HTTPS konfiguriert ist. Damit Sie einen für HTTPS konfigurierten Quellverteilungspunkt verwenden können, muss sich der Pullverteilungspunkt auch auf einem Computer mit dem Configuration Manager-Client befinden.  

Jedem Verteilungspunkt in einer Punktliste mit Pull- und Quellverteilungspunkten kann eine Priorität zugewiesen werden:  

-   Sie können jedem Quellverteilungspunkt eine gesonderte Priorität zuweisen, Sie können aber auch mehreren Quellverteilungspunkten die gleiche Priorität zuweisen.  

-   Über die Priorität wird bestimmt, in welcher Reihenfolge vom Pullverteilungspunkt Inhalt von dessen Quellverteilungspunkten angefordert wird.  

-   Zuerst wird vom Pullverteilungspunkt eine Verbindung mit einem Quellverteilungspunkt mit dem niedrigsten Wert für die Priorität hergestellt.  Wenn es mehrere Quellverteilungspunkte mit der gleichen Priorität gibt, wird vom Pullverteilungspunkt auf nicht deterministische Weise einer der Quellverteilungspunkte mit dieser Priorität ausgewählt.  

-   Ist der Inhalt in der ausgewählten Quelle nicht verfügbar, wird vom Pullverteilungspunkt versucht, den Inhalt von einem anderen Verteilungspunkt mit der gleichen Priorität herunterzuladen.  

-   Wenn der Inhalt auf keinem der Verteilungspunkte mit einer bestimmten Priorität vorhanden ist, wird vom Pullverteilungspunkt versucht, den Inhalt von einem Verteilungspunkt herunterzuladen, dem eine Priorität mit dem nächstgrößeren Wert zugewiesen wurde. Dieser Prozess wird wiederholt, bis der Inhalt gefunden wurde, oder der Pullverteilungspunkt wird für 30 Minuten deaktiviert, bevor der Prozess erneut beginnt.  

Wenn von einem Pullverteilungspunkt Inhalt von einem Quellverteilungspunkt heruntergeladen wird, wird dieser Pullverteilungspunkt im Bericht **Verwendungsdatenzusammenfassung für Verteilungspunkt** in der Spalte **Clients mit Zugriff (eindeutig)** als Client gezählt.  

 Die Inhaltsübertragung von einem Quellverteilungspunkt erfolgt standardmäßig über das **Computerkonto** des Pullverteilungspunkts. Wenn aber Inhalt von einem Quellverteilungspunkt übertragen wird, der sich in einer Gesamtstruktur befindet, wird vom Pullverteilungspunkt immer das Netzwerkzugriffskonto verwendet. Dieser Vorgang setzt voraus, dass der Configuration Manager-Client auf dem Computer installiert ist. Außerdem muss ein Netzwerkzugriffskonto konfiguriert sein, über das der Zugriff auf den Quellverteilungspunkt möglich ist.  

## <a name="about-content-transfers"></a>Informationen zur Übertragung von Inhalten  
 Die Inhaltsübertragung wird von den Pullverteilungspunkten über die Komponente **CCMFramework** der Configuration Manager-Clientsoftware verwaltet.  

-   Dieses Framework wird von **Pulldp.msi** installiert, wenn Sie den Verteilungspunkt als Pullverteilungspunkt konfigurieren. Der Configuration Manager-Client ist für das Framework nicht erforderlich.  

-   Nach der Installation des Pullverteilungspunkts muss der Dienst „CCMExec“ auf dem Verteilungspunktcomputer funktionstüchtig sein, damit der Pullverteilungspunkt eingesetzt werden kann.  

-   Der Vorgang der Inhaltsübertragung wird vom Pullverteilungspunkt mithilfe der **intelligenten Hintergrundübertragung** (Background Intelligent Transfer Service, BITS) ausgeführt und auf dem Verteilungspunktcomputer in **datatransferservice.log** und **pulldp.log** protokolliert.  

## <a name="see-also"></a>Weitere Informationen:  
 [Grundlegende Konzepte für die Inhaltsverwaltung in System Center Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
