---
title: Grundlegendes zu Upgrade, Update und Installation | Microsoft-Dokumentation
description: "Erfahren Sie mehr über den Unterschied zwischen den Begriffen Installation, Update und Upgrade beim Verwalten einer Configuration Manager-Infrastruktur."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
caps.latest.revision: "0"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6bd6cd7ea3c41fa1d70e17a1290c9f1f74cc9e37
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Informationen zu Upgrade, Update und Installation für einen Standort und eine Hierarchieinfrastruktur

*Gilt für: System Center Configuration Manager (Current Branch)*


Beim Verwalten des System Center Configuration Manager-Standorts und der Hierarchieinfrastruktur werden die Begriffe *Upgrade*, *Update* und *Installation* verwendet, um drei verschiedene Konzepte zu beschreiben.

## <a name="upgrade"></a>Upgrade
Die Begriffe *Upgrade* oder *direktes Upgrade* werden verwendet, wenn Sie einen Configuration Manager 2012-Standort oder eine -Hierarchie in einen Standort oder eine Hierarchie mit System Center Configuration Manager konvertieren.
Wenn Sie ein Upgrade von System Center 2012 Configuration Manager auf System Center Configuration Manager durchführen, verwenden Sie weiterhin dieselben Server zum Hosten Ihrer Standorte und Standortserver und behalten vorhandene Daten und Konfigurationen für Configuration Manager bei.  Dies unterscheidet sich von der [Migration](/sccm/core/migration/migrate-data-between-hierarchies), die eine Möglichkeit darstellt, Ihre Konfigurationen und Daten zu verwalteten Geräten beizubehalten, während Sie neue System Center Configuration Manager-Standorte verwenden, die auf neuer Hardware installiert sind.

Weitere Informationen finden Sie unter [Upgrade auf System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).



## <a name="update"></a>Update
Der Begriff *Update* wird für die Installation von konsoleninternen Updates für System Center Configuration Manager und für Out-of-Band-Updates verwendet, die nicht von der Configuration Manager-Konsole aus übermittelt werden können. Konsoleninterne Updates können die Version des Current Branch-Standorts (oder des Technical Preview-Standorts) ändern, sodass eine höhere Version ausgeführt wird. Wenn an Ihrem Standort beispielsweise Version 1606 ausgeführt wird, können Sie ein Update für Version 1610 installieren. Mithilfe von Updates können auch bekannte Probleme behoben werden, ohne die Standortversion zu ändern.      

In der Regel werden mit Updates Sicherheitsfixes, Qualitätsverbesserungen und neue Funktionen zu Ihren vorhanden Bereitstellung hinzugefügt. Wenn Sie Technical Preview Branch verwenden, können Sie mit einem Update eine neuere Version der Technical Preview installieren.
-   Sie entscheiden, wann das konsoleninterne Update – beginnend mit dem Standort der obersten Ebene Ihrer Hierarchie – installiert werden soll.
- Sie können jedes Update installieren, das in der Konsole verfügbar ist. Beispiel: Wenn auf Ihrem Standort Version 1602 ausgeführt wird und Version 1606 und 1610 angeboten werden, sollten Sie Version 1610 installieren, weil jede Version die Funktionen in zuvor veröffentlichten Versionen einschließt.
- Wenn die Installation eines neuen Updates an Ihrem Standort der obersten Ebene abgeschlossen wurde, wird auch beim untergeordneten primären Standort das Update gestartet. Sie können jedoch [Dienstfenster](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkservicewindowa-service-windows-for-site-servers) einrichten, um den Installationszeitpunkt von Updates zu bestimmen.
- An sekundären Standorten werden Updates nicht automatisch installiert. Dort müssen Sie Updates in der Configuration Manager-Konsole manuell starten.

Weitere Informationen finden Sie unter [Updates für System Center Configuration Manager](/sccm/core/servers/manage/updates) und [Technical Preview für System Center Configuration Manager](/sccm/core/get-started/technical-preview).



## <a name="install"></a>Installation
Der Begriff *Installation* wird verwendet, wenn eine neue Configuration Manager-Hierarchie von Grund auf neu erstellt wird oder zusätzliche Standorte zu einer vorhandenen Hierarchie hinzufügt werden.  

Bei der Installation eines neuen primären Standorts oder eines Standorts der zentralen Verwaltung ist der Speicherort der Datei „Setup.exe“ und die damit verbundenen und von Ihnen verwendeten Quelldateien von Ihrem Installationsszenario abhängig.

Weitere Informationen finden Sie unter [Vorbereitung zur Installation von Standorten ](/sccm/core/servers/deploy/install/prepare-to-install-sites).
