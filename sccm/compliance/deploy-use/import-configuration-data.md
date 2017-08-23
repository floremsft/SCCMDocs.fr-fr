---
title: Importieren von Konfigurationsdaten | Microsoft-Dokumentation
description: "Konfigurationsdaten können importiert werden, wenn sie sich in einer CAB-Datei befinden und dem unterstützten SML-Schema (Service Modeling Language) entsprechen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 60d0642618a3074fc50a848f1189f4d6559ca916
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="import-configuration-data-with-system-center-configuration-manager"></a>Importieren von Konfigurationsdaten mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zusätzlich zur Erstellung von Konfigurationsbaselines und Konfigurationselementen mit der System Center Configuration Manager-Konsole können Sie Konfigurationsdaten importieren, wenn diese im CAB-Dateiformat vorliegen und dem unterstützten SML-Schema (Service Modeling Language) entsprechen. Folgende Konfigurationsdaten können importiert werden:  

-   Bewährte Konfigurationsdaten (Konfigurationspakete), die von der Microsoft-Website oder Websites anderer Softwarehersteller heruntergeladen wurden.  

-   Konfigurationsdaten, die aus System Center 2012 Configuration Manager und höher exportiert wurden.  

-   Konfigurationsdaten, die extern erstellt wurden und dem SML-Schema entsprechen.  

 Ein Beispiel für ein Konfigurationspaket, das Sie bei der Verwaltung der Kompatibilität von Standortserverrollen für System Center 2012 Configuration Manager unterstützt, finden Sie unter [Konfigurationspaket für System Center 2012 Configuration Manager](http://www.microsoft.com/en-us/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all).  

Wenn Sie eine Konfigurationsbasislinie importieren, können einige oder alle der Konfigurationselemente, auf die in der Konfigurationsbasislinie verwiesen wird, auch in der CAB-Datei enthalten sein. Während des Imports überprüft Configuration Manager, ob alle Konfigurationselemente, auf die in der Konfigurationsbaseline verwiesen wird, in der CAB-Datei enthalten oder bereits am Configuration Manager-Standort vorhanden sind. Der Import kann nicht ausgeführt werden, wenn Sie versuchen, eine Konfigurationsbaseline zu importieren, die auf durch Configuration Manager nicht auffindbare Konfigurationsdaten verweist.  

In den folgenden Szenarien kann der Import ebenfalls nicht ausgeführt werden:  

-   Die Konfigurationdaten verweisen auf Konfigurationsdaten, die Configuration Manager weder in seiner Datenbank, noch in der CAB-Datei selbst finden kann.  

-   Die Konfigurationsdaten sind bereits in der Configuration Manager-Datenbank mit demselben Namen und derselben Konfigurationsdatenversion, jedoch mit einer anderen Inhaltsversion vorhanden.  

-   Die Konfigurationsdaten sind bereits in der Configuration Manager-Datenbank mit derselben Inhaltsversion vorhanden, doch die Hashberechnung identifiziert sie als unterschiedliche Daten.  

-   In der Configuration Manager-Datenbank ist bereits eine neuere Version der Konfigurationsdaten mit demselben Namen vorhanden oder wurde vor kurzem gelöscht.  

-   In einer Configuration Manager-Hierarchie mit mehreren Standorten wurden die Konfigurationsdaten ursprünglich von einem übergeordneten Standort importiert. Sie müssen von demselben Standort aus aktualisiert werden und nicht von einem untergeordneten Standort aus.  

### <a name="import-configuration-data"></a>Importieren von Konfigurationsdaten  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Konfigurationselement** oder **Konfigurationsbaselines**
2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationsdaten importieren**.  
3.  Klicken Sie im **Assistenten zum Importieren von Konfigurationsdaten** auf der Seite **Dateien auswählen**auf **Hinzufügen**, und wählen Sie dann im Dialogfeld **Öffnen** die zu importierenden CAB-Dateien aus.  
4.  Aktivieren Sie das Kontrollkästchen **Kopie der importierten Konfigurationsbaselines und Konfigurationselemente erstellen**, um die Bearbeitung der importierten Konfigurationsdaten in der Configuration Manager-Konsole zu ermöglichen.  
5.  Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die auszuführenden Aktionen, und schließen Sie anschließend den Assistenten ab.  

Die importierten Konfigurationsdaten werden im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Kompatibilitätseinstellungen** angezeigt.  
