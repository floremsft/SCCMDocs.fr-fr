---
title: Inhaltsbibliothek | Microsoft-Dokumentation
description: "Erfahren Sie mehr über die Inhaltsbibliothek, die System Center Configuration Manager verwendet, um die Gesamtgröße der verteilten Inhalte zu reduzieren."
ms.custom: na
ms.date: 2/14/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fa9f431c00476d71b2b08f92f914d76636d1a27
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="the-content-library-in-system-center-configuration-manager"></a>Die Inhaltsbibliothek in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Inhaltsbibliothek ist ein Einzelinstanz-Inhaltsspeicher, der von System Center Configuration Manager verwendet wird, um die Gesamtgröße des kombinierten Inhaltstexts, den Sie verteilen, zu reduzieren. In der Inhaltsbibliothek werden alle Inhaltsdateien für Softwareupdates, Anwendungen, Betriebssystembereitstellungen usw. gespeichert.

 - Auf jedem **Standortserver** und auf jedem **Verteilungspunkt** wird automatisch eine Kopie der Inhaltsbibliothek erstellt und verwaltet.

 - Bevor von Configuration Manager Inhaltsdateien auf den Standortserver heruntergeladen oder die Dateien auf Verteilungspunkte kopiert werden, überprüft Configuration Manager, ob die einzelnen Inhaltsdateien bereits in der Inhaltsbibliothek vorhanden sind.
 - Wenn die entsprechende Inhaltsdatei verfügbar ist, wird die Datei von Configuration Manager nicht kopiert. Stattdessen wird der Anwendung oder dem Paket die vorhandene Inhaltsdatei zugeordnet.

Auf Computern, auf denen Sie einen Verteilungspunkt installieren, können Sie Folgendes konfigurieren:

- Mindestens ein Laufwerk, auf dem Sie die Inhaltsbibliothek erstellen möchten.
- Eine Priorität für jedes verwendete Laufwerk.

Von Configuration Manager werden die Inhaltsdateien auf das Laufwerk mit der höchsten Priorität kopiert, sofern auf dem Laufwerk der von Ihnen angegebene freie Mindestspeicherplatz verfügbar ist.
- Sie konfigurieren die Laufwerkseinstellungen bei der Installation des Verteilungspunkts.
- Nach Abschluss der Installation können Sie die Laufwerkseinstellungen in den Verteilungspunkteigenschaften nicht mehr konfigurieren.


Weitere Informationen zum Konfigurieren der Laufwerkseigenschaften für den Verteilungspunkt finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


>  [!IMPORTANT]  
>  Wenn Sie die Inhaltsbibliothek auf einem Verteilungspunkt nach der Installation in ein anderes Verzeichnis verschieben möchten, verwenden Sie dazu das im System Center 2012 R2 Configuration Manager-Toolkit enthaltene Tool zum Übertragen der Inhaltsbibliothek (**Content Library Transfer Tool**). Das Toolkit steht im [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=279566)als Download zur Verfügung.  

## <a name="about-the-content-library-on-the-central-administration-site"></a>Informationen zur Inhaltsbibliothek am Standort der zentralen Verwaltung  
 Von Configuration Manager wird beim Installieren des Standorts standardmäßig eine Inhaltsbibliothek am Standort der zentralen Verwaltung erstellt. Die Inhaltsbibliothek wird auf dem Standortserver auf dem Laufwerk mit dem meisten freien Speicherplatz gespeichert. Da es Ihnen nicht möglich ist, am Standort der zentralen Verwaltung einen Verteilungspunkt zu installieren, können Sie keine Prioritäten für die Laufwerke zur Verwendung der Inhaltsbibliothek festlegen. Wenn auf dem Laufwerk, auf dem die Inhaltsbibliothek gespeichert ist, nicht mehr genügend Speicherplatz verfügbar ist, wird die Inhaltsbibliothek auf vergleichbare Weise wie eine Inhaltsbibliothek auf anderen Standortservern und Verteilungspunkten automatisch auf das nächste verfügbare Laufwerk ausgedehnt.  

 Die Inhaltsbibliothek wird in den folgenden Szenarios von Configuration Manager am Standort der zentralen Verwaltung verwendet:  

-   Beim Erstellen von Inhalt am Standort der zentralen Verwaltung.  

-   Beim Migrieren von Inhalt von einem anderen Configuration Manager-Standort und Festlegen des Standorts der zentralen Verwaltung als Standort für die Inhaltsverwaltung.  

> [!NOTE]  
>  Wenn Sie Inhalt an einem primären Standort erstellen und den Inhalt dann an einen anderen primären Standort oder an einen sekundären Standort unterhalb eines anderen primären Standorts verteilen, wird der Inhalt vorübergehend am Standort der zentralen Verwaltung in der Eingangsbox des Planers gespeichert. Der Inhalt wird jedoch nicht der zugehörigen Inhaltsbibliothek hinzugefügt.  

 Verwenden Sie die folgenden Optionen zum Verwalten der Inhaltsbibliothek am Standort der zentralen Verwaltung:  

-   Wenn die Inhaltsbibliothek nicht auf einem bestimmten Laufwerk installiert werden soll, erstellen Sie eine leere Datei mit dem Namen **no_sms_on_drive.sms**, und kopieren Sie die Datei vor dem Erstellen der Inhaltsbibliothek in den Stammordner des Laufwerks.  

-   Verwenden Sie nach dem Erstellen der Inhaltsbibliothek das im System Center 2012 R2 Configuration Manager-Toolkit enthaltene Tool zum Übertragen der Inhaltsbibliothek (**Content Library Transfer Tool**), um den Speicherort der Inhaltsbibliothek zu verwalten. Das Toolkit steht im [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=279566)als Download zur Verfügung.  
