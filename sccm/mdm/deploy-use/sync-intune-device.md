---
title: "Remotesynchronisierung von Richtlinien auf Intune-registrierten Geräten | Microsoft-Dokumentation"
description: "Lernen Sie, wie Sie Richtlinien auf Intune-registrierten Geräten von der Configuration Manager-Konsole aus synchronisieren"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: "18"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 337814fd5ba49ed17fc97aba49f79f02df817f4e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Remotesynchronisierung von Richtlinien auf Intune-registrierten Geräten von der Configuration Manager-Konsole

*Gilt für: System Center Configuration Manager (Current Branch)*


Sie können auf der Configuration Manager-Konsole eine Richtliniensynchronisierung für ein Gerät anfordern, das bei Intune registriert ist, anstatt diese Synchronisierung in der Unternehmensportal-App auf dem Gerät selbst anzufordern zu müssen. 

Dazu ist Folgendes erforderlich:

1.  Wählen Sie unter **Bestand und Konformität** > **Übersicht** > **Geräte** ein Gerät aus.
2.  Klicken Sie im Menü **Remotegeräteaktionen** auf **Send Sync Request** (Synchronisierungsanforderung senden).


Innerhalb von fünf bis zehn Minuten werden alle Änderungen an der Richtlinie auf dem Gerät synchronisiert. Sie können die Statusinformationen der Synchronisierungsanforderung in einer neuen Spalte namens **Remote Sync State** (Remotesynchronisierungsstatus) in den Geräteansichten und im Ermittlungsdatenbereich des Dialogfelds **Eigenschaften** jedes Geräts anzeigen.
