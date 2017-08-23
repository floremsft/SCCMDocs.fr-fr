---
title: "Einführung in Long-Term Servicing Branch | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über Long-Term Servicing Branch von System Center Configuration Manager."
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 91c1ca860069c6ebe0d20230c4620bf3f68735a2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Einführung in Long-Term Servicing Branch von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Long-Term Servicing Branch)*

Long-Term Servicing Branch (LTSB) von System Center Configuration Manager ist ein eindeutiger Branch von Configuration Manager, der als Installationsoption für alle Kunden zur Verfügung steht. Sie ist jedoch die einzige Option für Kunden, die ihre Software Assurance (SA) oder entsprechende Abonnementrechte für Configuration Manager auslaufen lassen.


Basierend auf der Configuration Manager-Version 1606 weist LTSB im Vergleich zu Current Branch von Configuration Manager eine eingeschränkte Funktionalität auf.

 > [!TIP]   
 > Informationen zu den Branches von **Windows Server** finden Sie unter [Windows Server 2016 new Current Branch for Business servicing option]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/) (Neue Windows Server 2016-Wartungsoption „Current Branch for Business“).

## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Funktionen, die nicht in LTSB von Configuration Manager verfügbar sind
Current Branch von Configuration Manager unterstützt folgende Funktionen, die nicht bei der Verwendung von LTSB verfügbar sind:

-   Konsoleninterne Updates, die neue und verbesserte Funktionen bieten
-   Unterstützung für neu veröffentlichte Betriebssysteme zur Verwendung als Standortserver und Clients
-   Verwendung eines Microsoft Intune-Abonnements als Unterstützung für folgende Funktionen:
    -   Intune in einer MDM-Konfiguration (hybride Verwaltung mobiler Geräte)
    -   Lokale Verwaltung mobiler Geräte
-   Windows 10-Wartungsdashboards und -Wartungspläne, einschließlich Unterstützung für die aktuellen Current Branch(CB)- und Current Branch for Business(CBB)-Versionen von Windows 10  
-   Unterstützung für zukünftige LTSB-Versionen für Windows Server und Windows 10
-   Asset Intelligence
-   Cloudbasierte Verteilungspunkte
-   Exchange Online als Exchange Connector    

Obwohl die Unterstützung für diese Funktionen nicht in LTSB verfügbar ist, bleiben einige davon in der Configuration Manager-Konsole sichtbar, können jedoch nicht ausgewählt oder verwendet werden.


## <a name="find-documentation-for-the-ltsb"></a>Suche nach Dokumentation für LTSB
LTSB basiert auf der Current Branch-Version 1606. Verwenden Sie als Produktdokumentation die [Dokumentation zu Current Branch](https://docs.microsoft.com/sccm/), die Warnungen und Einschränkungen speziell zu LTSB enthält. Diese Warnungen und Einschränkungen werden in folgenden Onlinethemen behandelt:

-     [Einführung in Long-Term Servicing Branch](introduction-to-the-ltsb.md) (dieses Thema)
-     [Installieren von Long-Term Servicing Branch](install-the-ltsb.md)
-     [Upgrade von Long-Term Servicing Branch auf Current Branch](convert-to-current-branch.md)
-     [Unterstützte Konfigurationen für Long-Term Servicing Branch](supported-configurations-for-ltsb.md)
-   [Verwalten von Long-Term Servicing Branch von System Center Configuration Manager](manage-the-ltsb.md)

Wenn Sie sich auf die Current Branch-Dokumentation für LTSB beziehen, gelten die Informationen für Version 1606 auch für LTSB. Funktionen oder Informationen, die bei Version 1610 oder höher eingeführt bzw. angegeben werden, werden nicht von LTSB unterstützt.


## <a name="licensing-overview-for-the-ltsb"></a>Lizenzierung für LTSB – Übersicht   
Kunden mit aktiver Software Assurance (SA) für System Center Configuration Manager-Lizenzen oder mit entsprechenden Abonnementrechten ab dem 1. Oktober 2016, verfügen über Benutzungsrechte der System Center Configuration Manager-Version 1606 vom Oktober 2016. Kunden, die ab dem 1. Oktober 2016 oder danach über Rechte für System Center Configuration Manager verfügen, erhalten während der Installation zwei lizenzierte Optionen: Current Branch und Long-Term Servicing Branch (LTSB).

Kunden, die über unbefristete Rechte für System Center Configuration Manager verfügen, oder die die Software Assurance oder das Abonnement nach dem 1. Oktober auslaufen lassen, können die LTSB-Version von System Center Configuration Manager installieren, die zu dem Zeitpunkt vorhanden ist, an dem die Software Assurance oder das Abonnement ausläuft.

[Vollständige Geschäftsbedingungen für die Produkte, die Sie über Microsoft-Volumenlizenzierungsprogramme erwerben, finden Sie hier](http://go.microsoft.com/fwlink/?LinkId=800052).

Weitere Informationen zur Lizenzierung für Configuration Manager-Branches finden Sie unter [Lizenzierung und Branches für System Center Configuration Manager](learn-more-editions.md).

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie zu dem Schluss kommen sollten, dass Configuration Manager-LTSB der richtige Branch für Ihre Umgebung ist, [installieren Sie einen neuen LTSB-Standort](/sccm/core/understand/install-the-ltsb#install-a-new-site) als Teil einer neuen Hierarchie, oder [aktualisieren Sie einen System Center 2012 Configuration Manager-Standort](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager) und die jeweilige Hierarchie.

Wenn Sie keine Installationsmedien besitzen, finden Sie in der [Dokumentation zu System Center 2016](https://technet.microsoft.com/system-center-docs/system-center) Informationen zum Beziehen von System Center 2016, das Medien zur Installation von System Center Configuration Manager-LTSB enthält.  
