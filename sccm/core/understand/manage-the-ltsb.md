---
title: Verwalten von LTSB | Microsoft-Dokumentation
description: Unterschiede bei der Verwaltung von LTSB von System Center Configuration Manager
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9c6f349ead906532a7a58df74609de976769e251
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Verwalten von Long-Term Servicing Branch von Configuration Manager

*Gilt für: System Center Configuration Manager (Long-Term Servicing Branch)*

Wenn Sie Long-Term Servicing Branch (LTSB) von System Center Configuration Manager verwenden, können Sie anhand der folgenden Informationen wichtige Änderungen verstehen, die sich auf die Verwaltung Ihrer Infrastruktur auswirken.

Da LTSB Version 1606 von Current Branch entspricht (mit einigen Ausnahmen wie Intune-Integration und cloudbezogenen Features), sind die meisten Aufgaben für die Planung, Bereitstellung und Konfiguration sowie alltägliche Verwaltung identisch.

LTSB unterstützt z.B. die gleiche Anzahl von Standorten, Standorttypen, Clients und allgemeine Infrastruktur wie Current Branch. Sie verwenden daher den Leitfaden, den Sie in der Standort- und Hierarchieplanung sowie in den Entwurfsthemen für Current Branch finden. Ähnlich ist es bei Funktionen von LTSB, die von beiden Branches unterstützt werden, wie z.B. Softwareupdates oder Betriebssystembereitstellung: Verwenden Sie den Leitfaden, den Sie in den Abschnitten der Current Branch-Dokumentation finden, die den Vorbehalt enthält, dass Sie über keinen Zugriff auf Funktionsänderungen verfügen, die nach Version 1606 von Current Branch eingeführt wurden.

Die folgenden Abschnitte enthalten Informationen zur Verwaltung von Aufgaben, die nicht ähnlich sind.

## <a name="updates-and-servicing"></a>Updates und Wartung
Nur wichtige Sicherheitsupdates werden in LTSB als konsoleninterne Updates verfügbar gemacht.  

Informationen zu herkömmlichen Updates für die nachfolgenden Current Branch-Versionen sind in der Konsole sichtbar, aber nicht auf LTSB verfügbar. Sie werden nicht heruntergeladen und können nicht installiert werden.

Um konsoleninterne Updates für wichtige Sicherheitskorrekturen zu unterstützen, erfordert ein LTSB-Standort die Verwendung des [Dienstverbindungspunkts](/sccm/core/servers/deploy/configure/about-the-service-connection-point). Sie können diese Standortsystemrolle wie Current Branch im Offline- oder Onlinemodus konfigurieren. LTSB sammelt und sendet die gleichen Telemetrie- und Nutzungsdaten wie Current Branch.

LTSB unterstützt die Verwendung des Hotfixinstallationsprogramms und des Tools zur Updateregistrierung, so wie für Current Branch dokumentiert.

Allgemeine Informationen zu Updates und zur Wartung finden Sie unter [Updates für System Center Configuration Manager](/sccm/core/servers/manage/updates).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Änderungen für die Standorterweiterung und den Ordner „CD.Latest“
Wenn Sie LTSB ausführen und einen eigenständigen primären Standort durch die Installation eines neuen Standorts der zentralen Verwaltung erweitern, müssen Sie das Setup und die Quelldateien des Baselinemediums von Version 1606 verwenden. Führen Sie das Setup für Current Branch aus und verwenden Sie die Quelldatei aus dem Ordner „CD.Latest“.

Obwohl Sie das Setup für die Standorterweiterung aus dem Ordner „CD.Latest“ nicht ausführen, verwenden Sie den Ordner „CD.Latest“ weiterhin für die Standortwiederherstellung und zum Installieren eines neuen untergeordneten primären Standorts, wenn Ihr erster LTSB-Standort ein Standort der zentralen Verwaltung war.

Weitere Informationen zur Standorterweiterung finden Sie unter [Erweitern eines eigenständigen primären Standorts](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site). Weitere Informationen über den Ordner „CD.Latest“ finden Sie unter [Der Ordner „CD.Latest“ für System Center Configuration Manager](/sccm/core/servers/manage/the-cd.latest-folder).


## <a name="recovery"></a>Wiederherstellung
Bei der Wiederherstellung eines Standorts müssen Sie den Standort oder die Standortdatenbank auf den ursprünglichen Branch wiederherstellen. Sie können keine Current Branch-Standortdatenbank auf einer LTSB-Installation wiederherstellen oder umgekehrt.
