---
title: Anzeigen des Hardwareinventars | Microsoft-Dokumentation | Resource Explorer
description: Verwenden Sie den Ressourcen-Explorer zum Anzeigen des Hardwareinventars in System Center Configuration Manager.
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: "7"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: e39fa60a5d215fa1b0a98d4463058497e63a4d4f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Anzeigen des Hardwareinventars mit dem Ressourcen-Explorer in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zeigen Sie mithilfe des Ressourcen-Explorers in System Center Configuration Manager Hardwareinventarinformationen an, die von Clients in Ihrer Hierarchie gesammelt wurden.  

> [!NOTE]  
>  Im Ressourcen-Explorer werden keine Inventurdaten angezeigt, bis auf dem Client, mit dem eine Verbindung hergestellt wird, ein Hardwareinventurzyklus ausgeführt wurde.  

 Der Ressourcen-Explorer enthält die folgenden Bereiche im Zusammenhang mit Hardwareinventur:  

-   **Hardware**: Enthält das neueste Hardwareinventar, das vom angegebenen Clientgerät gesammelt wird.  **Status der Arbeitsstation**: Enthält Uhrzeit und Datum der letzten Ausführung einer Hardwareinventur.  

-   **Hardwareverlauf**: Enthält einen Verlauf inventarisierter Elemente, die sich seit der letzten Hardwareinventur geändert haben. Jedes Element verfügt über einen **Current**-Knoten (Aktuell) und mindestens einen *<date\>*-Knoten (Datum). Sie können die Daten im aktuellen Knoten mit denen eines Verlaufsknotens vergleichen, um Elemente zu ermitteln, die sich geändert haben.  

    > [!NOTE]  
    >  Der Hardwareinventurverlauf wird von Configuration Manager für die Anzahl von Tagen beibehalten, die Sie im Standortwartungstask **Veralteten Inventurverlauf löschen** festlegen.  

> [!NOTE]  
>  Informationen zum Anzeigen der Hardwareinventur von Clients, auf denen Linux und UNIX ausgeführt werden, finden Sie unter [Überwachen von Clients für Linux- und UNIX-Server in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Ausführen des Ressourcen-Explorers über die Configuration Manager-Konsole  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Konformität** > **Geräte** aus, oder öffnen Sie eine beliebige Sammlung, die Geräte anzeigt.  

3.  Wählen Sie den Computer aus, der die anzuzeigende Inventur enthält. Wählen Sie danach auf der Registerkarte **Start** > Gruppe **Geräte** **Start** >  **Ressourcen-Explorer** aus.   

4.  Klicken Sie mit der rechten Maustaste auf ein beliebiges Element im rechten Bereich des Fensters **Ressourcen-Explorer**, und wählen Sie anschließend **Eigenschaften** aus, um das Dialogfeld *<Elementname\>***Eigenschaften** zu öffnen. Dort werden die gesammelten Inventurinformationen in einem besser lesbaren Format angezeigt.  

