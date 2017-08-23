---
title: "Erstellen und Ausführen von Skripts mit Configuration Manager | Microsoft-Dokumentation"
description: "Erstellen und Ausführen von Skripts auf Clientgeräten mit Configuration Manager."
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: ed84f7900eee5c04728d0e4d1b46027c36327bec
ms.sourcegitcommit: b41d3e5c7f0c87f9af29e02de3e6cc9301eeafc4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/11/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole

*Gilt für: System Center Configuration Manager (Current Branch)*

In Configuration Manager können Sie nicht nur mithilfe von Paketen und Programmen Skripts bereitstellen, sondern auch folgende Funktionen nutzen:

- Importieren von PowerShell-Skripts in Configuration Manager
- Bearbeiten von Skripts in der Configuration Manager-Konsole (nur bei nicht signierten Skripts)
- Markieren von Skripts als „Genehmigt“ oder „Abgelehnt“ zum Verbessern der Sicherheit
- Anwenden von Skripts auf Sammlungen von Windows-Client-PCs und lokal verwaltete Windows-PCs. Skripts werden nicht bereitgestellt, sondern nahezu in Echtzeit auf Clientgeräten ausgeführt.
- Überprüfen der Ergebnisse, die vom Skript in der Configuration Manager-Konsole zurückgegeben werden

>[!TIP]
>In dieser Version von Configuration Manager sind Skripts Vorabfeatures. Informationen zum Aktivieren von Skripts finden Sie unter [Features der Vorabversion in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="prerequisites"></a>Voraussetzungen

Um PowerShell-Skripts ausführen zu können, muss auf dem Client PowerShell 3.0 installiert sein. Enthält ein Skript jedoch Funktionen aus einer neueren PowerShell-Version, muss diese auch auf dem ausführenden Client installiert sein.

Das Ausführen von Skripts ist nur auf Clients mit Configuration Manager 1706 oder neuer möglich.

Um Skripts zu verwenden, müssen Sie Mitglied der entsprechenden Configuration Manager-Sicherheitsrolle sein.

- Erstellen und Importieren von Skripts: Ihr Konto benötigt in der Sicherheitsrolle **Konformitätseinstellungs-Manager** für **SMS-Skript** die Berechtigung **Erstellen**.
- Genehmigen und Ablehnen von Skripts: Ihr Konto benötigt in der Sicherheitsrolle **Konformitätseinstellungs-Manager** die Berechtigung **Genehmigen** für **SMS-Skripts**.
- Ausführen von Skripts: Ihr Konto benötigt in der Sicherheitsrolle **Konformitätseinstellungs-Manager** die Berechtigung **Skript ausführen** für **Sammlungen**.

Weitere Informationen zu Configuration Manager-Sicherheitsrollen finden Sie unter [Grundlagen der rollenbasierten Verwaltung für System Center Configuration Manager](/sccm/core/understand/fundamentals-of-role-based-administration).

Standardmäßig können Benutzer kein Skript genehmigen, das sie erstellt haben. Da Skripts leistungsstark und vielseitig sind und auf vielen Geräten bereitgestellt werden können, muss ein von einer Person erstelltes Skript von einer anderen Person genehmigt werden. Dies bietet Ihnen zusätzliche Sicherheit vor der unbeaufsichtigten Ausführung eines Skripts. Die sekundäre Genehmigung lässt sich deaktivieren, um das Testen zu vereinfachen.

## <a name="allow-users-to-approve-their-own-scripts"></a>Benutzern erlauben, eigene Skripts zu genehmigen

1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.
2. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.
3. Wählen Sie in der Liste der Standorte Ihren Standort aus, und klicken Sie dann auf der Registerkarte **Start** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.
4. Deaktivieren Sie im Dialogfeld **Eigenschaften von Hierarchieeinstellungen** auf der Registerkarte **Allgemein** das Kontrollkästchen **Skriptautoren nicht das Genehmigen ihrer eigenen Skripts erlauben**.

## <a name="import-and-edit-a-script"></a>Importieren und Bearbeiten eines Skripts

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.
2. Klicken Sie im Arbeitsbereich **Softwarebibliothek** auf **Skripts**.
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Skript erstellen**.
4. Konfigurieren Sie im Assistenten **Skript erstellen** auf der Seite **Skript** die folgenden Einstellungen:
    - **Skriptname**: Geben Sie einen Namen für das Skript ein. Sie können zwar mehrere Skripts mit dem gleichen Namen erstellen, dies erschwert aber das Auffinden des benötigten Skripts in der Configuration Manager-Konsole.
    - **Skriptsprache**: Derzeit werden nur PowerShell-Skripts unterstützt.
    - **Importieren**: Importieren Sie ein PowerShell-Skript in die Konsole. Das Skript wird im Feld **Skript** angezeigt.
    - **Löschen**: Entfernt das aktuelle Skript aus dem Feld „Skript“
    - **Skript**: Zeigt das gerade importierte Skript. Sie können das Skript in diesem Feld nach Bedarf bearbeiten.
5. Schließen Sie den Assistenten ab. Das neue Skript wird in der Liste **Skript** mit dem Status **Warten auf Genehmigung** angezeigt. Bevor Sie dieses Skript auf Clientgeräten ausführen können, müssen Sie es genehmigen.

### <a name="script-examples"></a>Beispiele für Skripts

Hier finden Sie einige Beispiele für Skripts, die sich mit dieser Funktion verwenden lassen.

#### <a name="create-a-folder"></a>Erstellen eines Ordners

*New-Item "c:\scripts" -type folder name* 
 
 
#### <a name="create-a-file"></a>Erstellen einer Datei

*New-Item c:\scripts\new_file.txt -type file name*


## <a name="approve-or-deny-a-script"></a>Genehmigen oder Ablehnen eines Skripts

Bevor Sie ein Skript ausführen können, muss es genehmigt werden. So genehmigen Sie ein Skript

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.
2. Klicken Sie im Arbeitsbereich **Softwarebibliothek** auf **Skripts**.
3. Wählen Sie in der Liste **Skript** das Skript, das Sie genehmigen oder ablehnen möchten. Klicken Sie dann in der Gruppe **Skript** auf der Registerkarte **Start** auf **Genehmigen/Ablehnen**.
4. Im Dialogfeld **Skript genehmigen oder ablehnen** können Sie es **genehmigen** oder **ablehnen** und optional einen Kommentar zu Ihrer Entscheidung eingeben. Wenn Sie ein Skript ablehnen, kann es nicht auf Clientgeräten ausgeführt werden.
5. Schließen Sie den Assistenten ab. In der Liste **Skript** ändert sich die Spalte **Genehmigungsstatus** abhängig von der Aktion, die Sie ausgeführt haben.

## <a name="run-a-script"></a>Ausführen eines Skripts
Nachdem ein Skript genehmigt wurde, kann es für die von Ihnen gewählte Sammlung ausgeführt werden.

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2. Klicken Sie im Arbeitsbereich Bestand und Kompatibilität auf **Gerätesammlungen**.
3. Klicken Sie in der Liste **Gerätesammlungen** auf die Sammlung von Geräten, auf denen das Skript ausgeführt werden soll.
4. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Alle Systeme** auf **Skript ausführen**.
5. Wählen Sie im Assistenten **Skript ausführen** auf der Seite **Skript** ein Skript in der Liste aus. Es werden nur genehmigte Skripts angezeigt.
6. Klicken Sie auf **Weiter**, und schließen Sie den Assistenten ab.

>[!IMPORTANT]
>Dem Skript wird für die Ausführung ein einstündiger Zeitraum zugewiesen. Wenn es in diesem Zeitraum nicht ausgeführt wird (z.B. weil der Computer ausgeschaltet ist), müssen Sie die Ausführung erneut anstoßen.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie ein Skript auf Clientgeräten ausgeführt haben, gehen Sie wie folgt vor, um den Erfolg des Vorgangs zu überwachen.

1. Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.
2. Klicken Sie im Arbeitsbereich **Überwachung** auf **Skriptstatus**.
3. In der Liste **Skriptstatus** sehen Sie die Ergebnisse für jedes Skript, das Sie auf Clientgeräten ausgeführt haben. Der Exitcode **0** eines Skripts bedeutet im Allgemeinen, dass das Skript erfolgreich ausgeführt wurde.
