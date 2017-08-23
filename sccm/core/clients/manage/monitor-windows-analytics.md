---
title: "Verwenden von Windows Analytics mit Configuration Manager zum Überwachen von Clients | Microsoft-Dokumentation"
description: "Windows Analytics umfasst Lösungen, die Teil der Operations Management Suite sind und Ihnen wertvolle Einblicke in den aktuellen Status Ihrer Umgebung geben. Dies geschieht durch die Nutzung von Windows-Telemetriedaten, die von Geräten in Ihrer Umgebung gesendet werden."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: "23"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: adabe8f475eb12dd44005ec07344e8565be20582
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Verwenden von Windows Analytics mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) umfasst Lösungen, die Teil der [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview) sind. Mit diesen Lösungen erhalten Sie wertvolle Einblicke in den aktuellen Status Ihrer Umgebung. Die Geräte in Ihrer Umgebung senden Windows-Telemetriedaten, auf die mit Lösungen des [Operations Management Suite-Webportals](https://mms.microsoft.com) zugegriffen werden kann. Auch eine Analyse der Daten ist möglich. Im Fall von [Upgradebereitschaft](/sccm/core/clients/manage/upgrade/upgrade-analytics) können die Daten auch direkt im Knoten "Überwachung" der Configuration Manager-Konsole zur Verfügung gestellt werden, indem Upgradebereitschaft und Configuration Manager verbunden werden.

Die von Windows Analytics analysierten Windows-Telemetriedaten werden nicht direkt an den Configuration Manager-Standortserver weitergeleitet. Stattdessen senden Client-Computer Windows-Telemetriedaten an den Telemetriedienst. Die relevanten Daten werden anschließend an Windows Analytics-Lösungen weitergeleitet, die in einem OMS-Arbeitsbereich Ihrer Organisation gehostet sind. Mit Configuration Manager können Sie entweder über kontextbezogene Links auf relevante Daten im Webportal zugreifen oder sich direkt Daten der Lösungen anzeigen lassen, die Sie mit Configuration Manager verbunden haben. Über das Operation Management Suite-Webportal können Sie außerdem die Daten direkt abfragen.

>[!Important]
>[Diagnose- und Nutzungsdaten von Configuration Manager](../../plan-design/diagnostics/diagnostics-and-usage-data.md), die über den Configuration Manager-Standortserver an Microsoft gesendet werden, sind nicht Bestandteil der Datensammlung von Windows Analytics oder der Windows-Telemetriedaten.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Konfigurieren von Clients zum Senden von Daten an Windows Analytics

Damit Clientgeräte Daten an Windows Analytics senden können, müssen Geräte mit einem kommerziellen ID-Schlüssel konfiguriert werden, der dem Operations Management Suite-Arbeitsbereich zugeordnet ist, in dem die Daten von Windows-Analytics für Ihre Organisation gehostet werden. Die Geräte müssen außerdem so konfiguriert sein, dass sie Telemetriedaten auf einer Telemetriestufe senden, die für Ihre gewünschten Lösungen geeignet sind. 

### <a name="configure-windows-analytics-client-settings"></a>Konfigurieren von Clienteinstellungen für Windows Analytics
Wählen Sie zum Konfigurieren von Windows Analytics in der Configuration Manager-Konsole **Verwaltung** > **Clienteinstellungen** aus, doppelklicken Sie auf **Benutzerdefinierte Clienteinstellungen für Geräte erstellen**, und aktivieren Sie dann **Windows Analytics**.  

Wechseln Sie zur Registerkarte mit den Einstellungen für **Windows Analytics**, und konfigurieren Sie Folgendes:
  -  **Kommerzielle ID**  
Der Schlüssel „Kommerzielle ID“ ordnet Informationen der von Ihnen verwalteten Geräte zu dem OMS-Arbeitsbereich zu, der die Windows Analytics-Daten Ihrer Organisation hostet. Wenn Sie bereits einen kommerziellen ID-Schlüssel für die Verwendung mit der Upgradebereitschaft konfiguriert haben, verwenden Sie diese ID. Wenn Sie noch nicht über einen kommerziellen ID-Schlüssel verfügen, finden Sie weitere Informationen unter [Generieren des kommerziellen ID-Schlüssels]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Telemetriestufe für Windows 10-Geräte**   
Informationen darüber, was auf jeder Telemetriestufe von Windows 10 gesammelt wird, finden Sie unter [Konfigurieren der Windows-Telemetrie in Ihrem Unternehmen](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

  -  **Abonnieren Sie die Sammlung kommerzieller Daten auf Geräten unter Windows 7, 8 und 8.1**   
Informationen zu gesammelten Daten von diesen Betriebssystemen bei der Anmeldung, finden Sie in der PDF-Datei [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields (Appraiser-Telemetrieereignisse und -felder unter Windows 7, Windows 8 und 8.1)](https://go.microsoft.com/fwlink/?LinkID=822965).

  -  **Konfigurieren der Datensammlung von Internet Explorer**  
Auf Geräten unter Windows 8.1 oder früher kann die Internet Explorer-Datensammlung es der Upgradebereitschaft ermöglichen, Inkompatibilitäten von Webanwendungen zu erkennen, die ein reibungsloses Upgrade auf Windows 10 verhindern könnten. Die Internet Explorer-Datensammlung kann für einzelne Internetzonen aktiviert werden. Weitere Informationen zu Internetzonen finden Sie unter [About URL Security Zones](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx) (Informationen zu URL-Sicherheitszonen).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Verwenden von Upgradebereitschaft zum Identifizieren von Windows 10-Kompatibilitätsproblemen

Mit Upgradebereitschaft (ehemals Upgrade Analytics) können Sie die Gerätebereitschaft und Kompatibilität unter Windows 10 analysieren. Durch diese Bewertung werden reibungslose Upgrades ermöglicht. Nach dem Verbinden von Upgradebereitschaft mit Configuration Manager können Sie direkt auf Daten zur Kompatibilität von Clientupgrades in der Configuration Manager-Konsole zuzugreifen. Dort können Sie auch Geräte aus der Geräteliste für ein Upgrade oder Wartungsaufgaben auswählen.

Weitere Informationen und Details zum Konfigurieren und Verbinden mit Upgradebereitschaft finden Sie unter [Upgradebereitschaft](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Verwenden von Windows Analytics zur Identifizierung von Lücken in Windows Information Protection-Richtlinien

Geräte unter der Windows 10-Version 1703 und höher, die mit den [Windows Information Protection-Richtlinien](https://docs.microsoft.com/en-us/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) konfiguriert sind, senden Telemetriedaten über Anwendungen, die zwar Zugriff auf Unternehmensdaten in Ihrer Umgebung haben, jedoch nicht in den Anwendungsregeln der WIP-Richtlinien berücksichtigt werden. Hierbei handelt es sich möglicherweise um Anwendungen, die blockiert werden, obwohl diese zur Produktivität der Benutzer in Ihrer Umgebung beitragen. Kenntnisse über den Zugriff auf Unternehmensdaten durch derartige Anwendungen können daher bei der Wartung Ihrer Windows Information Protection-Richtlinien in Configuration Manager sinnvoll sein. 

Auf die Windows Information Protection-Daten greifen Sie über die [Operations Management Suite-Abfrage](https://go.microsoft.com/fwlink/?linkid=849952) zu.