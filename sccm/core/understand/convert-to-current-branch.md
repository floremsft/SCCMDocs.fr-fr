---
title: Upgrade von Long-Term Servicing Branch auf Current Branch | Microsoft-Dokumentation
description: "Enthält Informationen zum Konvertieren eines Long-Term Servicing Branch-Standorts auf einen Current Branch-Standort."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6e7edc85630d22c5bbba1ff66bd1199903db76db
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Upgrade von Long-Term Servicing Branch auf Current Branch

*Gilt für: System Center Configuration Manager (Long-Term Servicing Branch)*

In diesem Thema erfahren Sie, wie man ein Upgrade eines Standorts und einer Hierarchie durchführt (konvertiert), die Long-Term Servicing Branch (LTSB) von Configuration Manager auf Current Branch ausführen.

Wenn Sie über einen aktuellen Software Assurance-Vertrag (oder ähnliche Lizenzrechte) verfügen, der Ihnen Rechte gewährt, Current Branch zu verwenden, können Sie Ihre Installation von LTSB auf Current Branch konvertieren.  Dies ist eine unidirektionale Konvertierung, weil das Konvertieren eines Current Branch-Standorts nach LTSB nicht unterstützt wird.

Wenn Sie über mehrere Standorte verfügen, müssen Sie nur den Standort der obersten Ebene Ihrer Hierarchie konvertieren. Nachdem der Standort der obersten Ebene konvertiert ist:
- Konvertieren untergeordnete primäre Standorte automatisch.
-   Müssen Sie sekundäre Standorte in der Configuration Manager-Konsole manuell aktualisieren.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Ausführen von Setup zum Konvertieren von Long-Term Servicing Branch
Sie können auf dem Standort der obersten Ebene Ihrer Hierarchie das Configuration Manager-Setup mit einem berechtigtem Baselinemedium ausführen, und **Standortwartung** auswählen.  Wählen Sie dann auf der Lizenzierungsseite die Option für Current Branch aus, und schließen Sie den Assistenten ab.

Sobald Ihr Standort in Current Branch konvertiert wurde, stehen Ihnen Features und Funktionen zur Verfügung, die bisher nicht verfügbar waren.

> [!NOTE]  
> Ein berechtigtes Baselinemedium ist ein Medium der gleichen oder höheren Version Ihrer LTSB-Installation.

Beispiel: Da LTSB auf Version 1606 basiert, können Sie kein Baselinemedium der Version 1511 verwenden, um in Current Branch zu konvertieren. Führen Sie Setup stattdessen von der gleichen Version 1606 des Baselinemediums aus, die Sie zur Installation des LTSB-Standorts verwendet haben, und wählen Sie die Lizenzierungsoption für Current Branch aus.  Alternativ können Sie das Setup auch von einer höheren Version des Baselinemediums von Current Branch ausführen.

Sie finden eine Liste der Baselineversionen unter **Baseline and update versions (Baseline- und Updateversionen)** in [Updates for Configuration Manager (Updates für Configuration Manager)](/sccm/core/servers/manage/updates).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Verwenden der Configuration Manager-Konsole zum Konvertieren von Long-Term Servicing Branch
Wenn Ihr Standort LTSB ausführt, können Sie die folgende Option in der Configuration Manager-Konsole ausführen, um auf Current Branch zu konvertieren:

 1. Wechseln Sie in der Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, und öffnen Sie dann die **Hierarchieeinstellungen**.  

 2. Wählen Sie die Option zum Konvertieren von Current Branch aus, und klicken Sie auf **Anwenden**.  

Sobald Ihr Standort in Current Branch konvertiert wurde, stehen Ihnen Features und Funktionen zur Verfügung, die bisher nicht verfügbar waren.
