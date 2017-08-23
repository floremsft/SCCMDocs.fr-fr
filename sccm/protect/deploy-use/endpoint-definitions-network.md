---
title: Endpoint Protection-Schadsoftwaredefinitionen von der Netzwerkfreigabe | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie die neuesten Definitionsupdates von Microsoft herunterladen und anschließend Clients so konfigurieren, dass sie diese Definitionen herunterladen."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 110bd9a9d04b27ef6794145fae66dbd910308bdc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share-for-configuration-manager"></a>Aktivieren der Endpoint Protection-Schadsoftwaredefinitionen zum Herunterladen aus der Netzwerkfreigabe für Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

 Sie können die neuesten Definitionsupdates von Microsoft manuell herunterladen und dann die Clients so konfigurieren, dass diese Definitionen aus einem freigegebenen Ordner im Netzwerk heruntergeladen werden. Bei Verwendung dieser Updatequelle können auch die Benutzer Definitionsupdates einleiten.

> [!NOTE]
>  Die Clients benötigen Lesezugriff auf den freigegebenen Ordner, um Definitionsupdates herunterladen zu können.

 Weitere Informationen zum Herunterladen der Definitions- und Modulupdates zum Speichern in der Dateifreigabe finden Sie unter [Installieren der neuesten Antischadsoftware und Antispyware von Microsoft](http://www.microsoft.com/security/portal/Definitions/HowToForeFront.aspx).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>So konfigurieren Sie das Herunterladen von Definitionen von einer Dateifreigabe

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie dann auf **Richtlinien für Antischadsoftware**.

3.  Öffnen Sie die Eigenschaftenseite für die **Standardrichtlinie für Antischadsoftware** , oder erstellen Sie eine neue Richtlinie für Antischadsoftware. Weitere Informationen zum Erstellen von Richtlinien für Antischadsoftware finden Sie unter [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).

4.  Klicken Sie im Abschnitt **Definitionsupdates** des Dialogfelds mit Eigenschaften von Antischadsoftware auf **Quelle festlegen**.

5.  Wählen Sie im Dialogfeld **Definitionsupdatequellen konfigurieren** die Option **Updates von UNC-Dateifreigaben**aus.

6.  Klicken Sie auf **OK** , um das Dialogfeld **Definitionsupdatequellen konfigurieren** zu schließen.

7.  Klicken Sie auf **Pfade festlegen**. Fügen Sie dann im Dialogfeld **UNC-Pfade für Definitionsupdates konfigurieren** mindestens einen UNC-Pfad zum Speicherort der Definitionsupdatedateien in einer Netzwerkfreigabe hinzu.

8.  Klicken Sie auf **OK** , um das Dialogfeld **UNC-Pfade für Definitionsupdates konfigurieren** zu schließen.


> [!div class="button"]
[Nächster Schritt >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Zurück >](endpoint-configure-alerts.md)
