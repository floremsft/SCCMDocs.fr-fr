---
title: Verwenden von Diagnosedaten | Microsoft-Dokumentation
description: "Erfahren Sie mehr darüber, wie Microsoft die Diagnose- und Nutzungsdaten verwendet, die System Center Configuration Manager sammelt."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9864f6ba7b9a2211c99b1a5d9ebd582e01ccfeb6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>Nutzung von Diagnose- und Verwendungsdaten für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die von System Center Configuration Manager erfassten Diagnose- und Nutzungsdaten stellen Microsoft ein nahezu unmittelbares Feedback zum Betrieb des Produkts bereit und dienen zur Anpassung zukünftiger Updates. Außerdem werden Konfigurationsdaten bereitgestellt, mit deren Hilfe in der Produktion befindliche Konfigurationen entwickelt und getestet werden können. Beispiel:  

-   Die vom Standortserver verwendeten Windows Server-Versionen  

-   Installierte Sprachpakete  

-   Das Delta zwischen SQL-Schema und Standardwert des Produkts  

Mithilfe dieser Daten kann das Entwicklungsteam zukünftige Tests planen, um die beste Lösung für die am häufigsten verwendeten Konfigurationen zu finden. Da Updates für Configuration Manager in kürzeren Intervallen veröffentlicht werden (um eine bessere Unterstützung für Technologien zu bieten, die schnellen Veränderungen unterliegen, wie Windows 10 und Microsoft Intune), sind diese Daten für eine rasche Anpassung und Optimierung von entscheidender Bedeutung.  

Ebenso wichtig ist, wofür die Diagnose- und Nutzungsdaten nicht eingesetzt werden. Microsoft verwendet diese Daten nicht zu folgenden Zwecken:  

-   Lizenzierungsüberwachung, z.B. Vergleich der Verwendung mit Lizenzverträgen  

-   Überwachung von Produkten, die nicht mehr unterstützt werden  

-   Werbung basierend auf verfügbaren Daten wie z.B. Featureverwendung oder geografischem Standort (Zeitzone)  

##  <a name="bkmk_improve"></a> Beispiele für die Verbesserung des Produkts anhand von Diagnose- und Nutzungsdaten  
Microsoft verwendet die verfügbaren Daten zur Verbesserung des Produkts. Im Folgenden sind einige Beispiele aufgeführt:  

-   **Überarbeitete Unterstützung für ältere Serverbetriebssysteme:**  

     In der anfänglichen Unterstützung, die vom aktuellen Branch von System Center Configuration Manager angeboten wurde, war der Unterstützungszeitraum für Windows Server 2008 R2 eingeschränkt. Nach der Untersuchung der Nutzungsdaten von Kunden, die ein Upgrade auf den aktuellen Branch von Configuration Manager durchgeführt haben, stellten wir fest, dass dieser Zeitraum überarbeitet und erweitert werden musste, um Kunden zu unterstützen, die dieses Serverbetriebssystem noch immer zum Hosten von Standortservern und Standortsystemrollen verwenden.  

-   **Verbesserte Voraussetzungsprüfungen:**  

     Anhand der Nutzungsdaten haben wir die Voraussetzungsprüfungen für die Installation eines Updates verbessert und veraltete Regeln entfernt sowie zusätzliche Fälle berücksichtigt. In einigen Fällen werden Probleme automatisch behoben.  
