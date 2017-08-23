---
title: "Aktivieren einer Geräteschutzregel in einer Konformitätsrichtlinie | Microsoft-Dokumentation"
description: "Aktivieren einer Regel in der Gerätekonformitätsrichtlinie zum Schutz von Mobilgeräten vor Bedrohungen."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: faa92e150686e615164ce3f5435b77a65305aab3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>Aktivieren einer Regel zum Schutz vor Gerätebedrohungen in der Konformitätsrichtlinie

*Gilt für: System Center Configuration Manager (Current Branch)*

Intune mit Lookout Mobile Threat Protection (MTP) ermöglicht Ihnen, Bedrohungen für Mobilgeräte zu erkennen und eine Risikobewertung für das Gerät vorzunehmen. Sie können eine Konformitätsrichtlinienregel in Configuration Manager erstellen, die die Risikoanalyse einschließt, um festzustellen, ob das Gerät als konform eingestuft wird. Anschließend können Sie den Zugriff auf Exchange, SharePoint und andere Dienste mit der Richtlinie für den bedingten Zugriff basierend auf der Gerätekonformität zulassen oder blockieren.

So können Sie die Konformitätsrichtlinie für das Gerät von der Lookout-Bedrohungserkennung abhängig machen

* Die Regel **Schutz vor Gerätebedrohungen** muss in der Konformitätsrichtlinie aktiviert werden.

* Auf der Seite **Lookout-Status** in der **Intune-Administratorkonsole** muss **Aktiv** angezeigt werden. Weitere Informationen und Anweisungen zum Aktivieren der Lookout-Integration finden Sie im Thema [Aktivieren der Lookout-MTP-Verbindung in Intune](enable-lookout-connection-in-intune.md).


Vor dem Erstellen der Regel zum Schutz vor Gerätebedrohungen in der Konformitätsrichtlinie wird empfohlen, [für Ihr Abonnement den Lookout-Schutz vor Gerätebedrohungen einzurichten](set-up-your-subscription-with-lookout.md), [die Lookout-Verbindung in Intune zu aktivieren](enable-lookout-connection-in-intune.md) und [die Lookout for Work-App zu konfigurieren](configure-and-deploy-lookout-for-work-apps.md). Die Konformitätsregel wird erst nach Abschluss des Setups erzwungen.

Um die Regel zum Schutz vor Gerätebedrohungen zu aktivieren, können Sie entweder eine vorhandene Konformitätsregel verwenden oder eine neue erstellen.

Im Rahmen des Setups des Lookout-Schutzes vor Gerätebedrohungen in der [Lookout-Konsole](https://aad.lookout.com) haben Sie eine Richtlinie erstellen, die verschiedene Bedrohungen in die Stufen „Hoch“, „Mittel“ und „Niedrig“ klassifiziert. In der Intune-Konformitätsrichtlinie können Sie die maximal zulässige Bedrohungsstufe festlegen.

Definieren Sie auf der Seite **Regeln** im Konformitätsrichtlinien-Assistenten eine neue Regel mit den folgenden Informationen:
  * Bedingung: Schutz vor Gerätebedrohungen – maximale Risikostufe.
  * Wert: Folgende Werte sind möglich:
    * **Keine (Geschützt)**: Dies ist die sicherste Option. Das bedeutet, dass auf dem Gerät keinerlei Bedrohungen zulässig sind. Bei jeglichem Fund einer Bedrohung (egal welcher Stufe) wird das Gerät als nicht konform ausgewertet.
    * **Niedrig**: Das Gerät wird als konform ausgewertet, wenn nur Bedrohungen der Stufe „Niedrig“ vorhanden sind. Jegliche Bedrohung einer höheren Stufe bewirkt, dass das Gerät in den Status „Nicht konform“ eingestuft wird.
    * **Mittel**: Das Gerät wird als konform ausgewertet, wenn die auf dem Gerät gefundenen Bedrohungen zur Stufe „Niedrig“ oder „Mittel“ gehören. Wenn Bedrohungen der Stufe „Hoch“ erkannt werden, wird das Gerät als „Nicht konform“ eingestuft.
    * **Hoch**: Dies ist die am wenigsten sichere Option. Im Prinzip lässt diese Option alle Bedrohungsstufen zu. Sie ist somit eigentlich nur zu Berichtszwecken nützlich.

Wenn Sie Richtlinien für bedingten Zugriff für Office 365 und andere Dienste erstellen, wird die oben beschriebene Konformitätsbewertung berücksichtigt. Nicht konforme Geräte werden blockiert und dürfen auf Unternehmensressourcen erst wieder zugreifen, wenn die Bedrohung entfernt wurde.

Der Gerätebedrohungsschutz-Status wird auf dem Knoten **Sicherheit** im Arbeitsbereich **Überwachung** angezeigt.
In einem visuellen Diagramm wird eine Zusammenfassung des Status mit verschiedenen Bedrohungsstufen angezeigt. Klicken Sie auf die einzelnen Abschnitte des Diagramms, um weitere Informationen anzuzeigen, z.B. die Anzahl der als nicht kompatibel eingestuften Geräte nach Plattform und alle gemeldeten Fehler.
Den Status einzelner Geräte können Sie auch im Arbeitsbereich **Bestand und Kompatibilität** unter **Geräte** anzeigen.  Sie können die Spalten **Gerätebedrohung – Kompatibilität** und **Gerätebedrohungsebene** hinzufügen, um den Status anzuzeigen.  Diese Spalten werden standardmäßig nicht angezeigt.
