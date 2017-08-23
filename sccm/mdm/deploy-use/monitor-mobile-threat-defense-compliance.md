---
title: "Überwachen der Mobile Threat Defense-Kompatibilität | System Center Configuration Manager"
description: "Überwachen des Kompatibilitätsstatus von Mobile Threat Defense-Partnern über die Configuration Manager-Verwaltungskonsole"
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 8edf83a0f761dfc16274ce49c3aa2b878c7fe6cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**Überwachen der Mobile Threat Defense-Kompatibilität**

*Gilt für: System Center Configuration Manager (Current Branch)*

## <a name="to-monitor-the-overall-compliance-status"></a>So überwachen Sie den allgemeinen Konformitätsstatus

So überwachen Sie den Status von Mobile Threat Defense:

1.  Klicken Sie in der Configuration Manager-Konsole auf den Arbeitsbereich **Überwachung**.

2.  Klicken Sie im Arbeitsbereich **Überwachung** auf den Knoten **Sicherheit**.

Sie sehen eine Zusammenfassung des Kompatibilitätsstatus mit unterschiedlichen Bedrohungsstufen, die in einem visuellen Diagramm angezeigt werden. Klicken Sie auf die einzelnen Abschnitte der Diagramme, um weitere Informationen zu enthalten, z.B.: 

- Die Anzahl der Geräte, die als nicht kompatibel von der Plattform gemeldet wurden
- Alle Fehler im Zusammenhang mit dem Kompatibilitätsstatus des Geräts

![](http://i.imgur.com/bmPsiWk.png)

## <a name="to-monitor-the-individual-compliance-status"></a>So überwachen Sie den individuellen Konformitätsstatus

Sie können sich auch den Status eines einzelnen Gerät anzeigen lassen:

1.  Klicken Sie in der Configuration Manager-Konsole auf den Arbeitsbereich **Bestand und Konformität**.

2.  Klicken Sie auf **Geräte**.

> [!TIP] 
> Sie können die Spalten **Gerätebedrohung – Kompatibilität** und **Gerätebedrohungsebene** hinzufügen, um den Status anzuzeigen. Diese Spalten werden standardmäßig nicht angezeigt.

## <a name="device-threat-protection-tab"></a>Registerkarte „Schutz vor Gerätebedrohungen“

Sie können darüber hinaus auf dem Bildschirm **Geräte** bestimmte Geräte auswählen. Klicken Sie dann auf die Registerkarte **Schutz vor Gerätebedrohungen**, der weitere Details über den Kompatibilitätsstatus des Geräts bietet. Weiter unten helfen Ihnen die Spaltenbeschreibungen und ihre erwarteten Werte bei der Analyse des Kompatibilitätsstatus des Geräts.

> [!IMPORTANT] 
> Die Registerkarte „Schutz vor Gerätebedrohungen“ wir nur angezeigt, wenn das ausgewählte Gerät ein mobiles Gerät ist.

|Spaltenname|Standardmäßig sichtbar|Beschreibung| 
|-|-|-|
|**Beschreibung**| Ja | Details über die Bedrohung durch den Mobile Threat Defense-Partner |
|**Letzter Aktualisierungszeitpunkt**| Ja | Der letzte Zeitpunkt, an dem der Mobile Threat Defense-Partner aktualisierte Details über die Bedrohung an Intune gesendet hat |
|**Schweregrad der Bedrohung**| Ja | Schweregrad der Bedrohung ist die Definition für eine einzelne Bedrohung, basierend auf der Konfiguration des Administrators in der Mobile Threat Defense-Partnerkonsole. Es ist einer von drei Werten vorhanden: **Niedrig**, **Mittel** oder **Hoch** |
|**Bedrohungsstatus**| Ja | Der aktuelle Status der Bedrohung auf dem Gerät. Mögliche Zustände: **Aktiv**, **Gelöst** oder **Ignoriert:** Gibt an, dass der Benutzer die Bedrohung auf dem Gerät ignoriert hat, aber die Bedrohung noch vorhanden ist. |
|**Bedrohungstyp**| Ja | Typ der Bedrohung des Mobile Threat Defense-Partners Mögliche Werte: **App**, **Datei** oder **OS** |
|**AAD-Konto-ID**| Nein | Der eindeutige Bezeichner von Azure Active Directory. |
|**Klassifizierung**| Ja | Eine vom Mobile Threat Defense-Partner bereitgestellte Klassifizierung der Bedrohung. Mögliche Werte: **Root-Enabler, Riskware, Adware, Chargeware, DataLeak, Trojaner, Wurm, Virus, Exploit, Backdoor, Bot, AppDropper, ClickFraud, Spam, Spyware, SurveillanceWare, Sicherheitsrisiko, Unbekannt, Root Jailbrake, Connectivity, TollFraud, SideloadedApp** |
|**Geräte-ID**| Nein | Die Azure Active Directory-Objekt-ID, die das mit dem Arbeitsbereich verknüpfte Gerät mit Bedrohungsinformationen darstellt. |
|**Bedrohungs-ID**| Nein | Vom Mobile Threat Defense-Partner generierte eindeutige Bezeichner für die Bedrohung. Die Bedrohungs-ID wird zum Nachverfolgen von Lösungen verwendet. |
|**Bedrohungs-URL**| Nein | Wenn vorhanden, führt die Bedrohungs-URL zurück zur Verwaltungskonsolenansicht dieser bestimmten Drohung des Mobile Threat Defense-Partners. |

> [!TIP] 
> Stellen Sie sicher, dass die Spalten aktiviert sind, die nicht **standardmäßig sichtbar** sind, um weitere Details zum Kompatibilitätsstatus von Mobile Threat Defense für Ihre Geräte anzuzeigen.
