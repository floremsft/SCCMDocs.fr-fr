---
title: "Erstellen von Konfigurationselementen für clientverwaltete Macs – Configuration Manager | Microsoft-Dokumentation"
description: "Verwenden Sie das System Center Configuration Manager-Konfigurationselement für Max OS X, um Einstellungen für Mac OS X-Geräte zu verwalten."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 541e5ad629a9e2ed9c353dff150f9b86b9d12b7d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-mac-os-x-devices-managed-with-the-system-center-configuration-manager-client"></a>Erstellen von Konfigurationselementen für Mac OS X-Geräte, die mit dem System Center Configuration Manager-Client verwaltet werden
Verwenden Sie das System Center Configuration Manager-Konfigurationselement **Mac OS X (benutzerdefiniert)**, um Einstellungen für Mac OS X-Geräte zu verwalten, die mit dem Configuration Manager-Client verwaltet werden.  
  
 Anwendungseinstellungen werden im Mac OS X-Betriebssystem in Eigenschaftenlistendateien (bzw. Plist-Dateien) gespeichert. Verwenden Sie Kompatibilitätseinstellungen zum Auswerten und Wiederherstellen von Einstellungen in einer Eigenschaftenlistendatei. Sie können Mac OS X-Einstellungen auch mithilfe eines Shellskripts verwalten, das einen Wert zurückgibt, den Sie zum Auswerten und Wiederherstellen der Kompatibilität verwenden können.  
  
### <a name="to-create-a-custom-mac-os-x-configuration-item"></a>So erstellen Sie ein benutzerdefiniertes Konfigurationselement für Mac OS X  
  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Konformität**.  
  
2.  Erweitern Sie im Arbeitsbereich **Bestand und Konformität** die **Konformitätseinstellungen**, und klicken Sie auf **Konfigurationselemente**.  
  
3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  
  
4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen**einen Namen und optional eine Beschreibung für das Konfigurationselement an.  
  
5.  Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben**den Typ **Mac OS X (benutzerdefiniert)**aus.  
  
6.  Klicken Sie auf **Kategorien**, wenn Sie Kategorien erstellen und zuweisen, um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern.  
  
7.  Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten die jeweiligen Mac OS X-Versionen zur Auswertung des Konfigurationselements aus.  
  
8.  Fügen Sie auf der Seite **Einstellungen** des Assistenten  neue Einstellungen hinzu, die hinsichtlich ihrer Kompatibilität auf Macintosh-Computern ausgewertet werden. Klicken Sie auf **Neu** , um das Dialogfeld **Einstellung erstellen** zu öffnen.  
  
9. Geben Sie im Dialogfeld **Einstellung erstellen** einen eindeutigen Namen und eine Beschreibung für die Einstellung ein.  
  
10. Wählen Sie den gewünschten **Einstellungstyp** aus, und geben Sie die erforderlichen Informationen ein, wie in der folgenden Tabelle dargestellt:  
  
    -   **Einstellungen für Mac OS X** -  
  
        -   **Anwendungs-ID** : Geben Sie die Anwendungs-ID der Eigenschaftenlistendatei an, aus der die Kompatibilität eines Schlüssels ausgewertet werden soll.  
  
             Beispielsweise, wenn Sie Einstellungen für den Safari-Webbrowser bearbeiten möchten, können **com.apple.Safari.plist**.  
  
        -   **Schlüssel** – Geben Sie den Namen des Schlüssels, der Kompatibilität auf Macintosh-Computer ausgewertet werden soll. Verwenden Sie die folgende Syntax: */<Wörterbuch\>/<Schlüsselname\>*.  
  
            > [!IMPORTANT]  
            >  Für den Schlüsselnamen muss die Groß-/Kleinschreibung beachtet werden, und er wird nicht ausgewertet, wenn er sich vom Schlüsselnamen auf dem Macintosh-Computer unterscheidet. Außerdem können Sie den Namen des Schlüssels nicht mehr bearbeiten, nachdem Sie ihn angegeben haben. Wenn Sie den Schlüsselnamen bearbeiten müssen, löschen und erstellen Sie dann die Einstellung erneut.  
  
    -   **Skript** -  
  
        -   **Ermittlungsskript** : Klicken Sie auf **Skript hinzufügen**, und geben Sie dann ein Shellskript ein, um Einstellungen auf dem Macintosh-Computer auf Kompatibilität zu untersuchen. Verwenden Sie den Befehl **echo** im Shellskript, um Werte zur Kompatibilität an Configuration Manager zurückzugeben. Configuration Manager verwendet die in **STDOUT** zurückgegebenen Ergebnisse, um die Kompatibilität auszuwerten.  
  
            > [!IMPORTANT]  
            >  Fügen Sie dem Ermittlungsskript nicht den Befehl **Neu starten** hinzu. Da das Ermittlungsskript bei jedem Neustart des Clients ausgeführt wird, würde dies dazu führen, dass der Macintosh-Computer immer wieder neu gestartet wird.  
  
        -   **Wiederherstellungsskript (optional)** : Optional können Sie auf **Skript hinzufügen** klicken und ein Shellskript eingeben, das zum Wiederherstellen aller auf dem Macintosh-Clientcomputer ermittelten nicht kompatiblen Einstellungen verwendet wird.  
  
            > [!IMPORTANT]  
            >  Um sicherzustellen, dass Sie keine Formatierungszeichen einfügen, die der Macintosh-Computer nicht interpretieren kann, geben Sie das Skript manuell und nicht per Kopieren und Einfügen ein.  
  
11. Wählen Sie den **Datentyp** aus, d. h., das Format, in dem die Daten von der Bedingung zurückgegeben werden, bevor sie zum Auswerten der Einstellung verwendet werden.  
  
    > [!NOTE]  
    >  Vom Datentyp **Gleitkomma** werden nur 3 Ziffern nach dem Dezimalkomma unterstützt.  
    >   
    >  Configuration Manager unterstützt für die Skripteinstellungen von Macintosh-Konfigurationselementen nicht den Datentyp **Boolesch**. Legen Sie den Datentyp stattdessen auf **Ganze Zahl** fest, und stellen Sie sicher, dass das Skript einen ganzzahligen Wert zurückgibt.  
  
12. Klicken Sie auf **OK** , um die Einstellung zu speichern und das Dialogfeld **Einstellung erstellen** zu schließen. Fügen Sie dann so viele weitere Einstellungen wie erforderlich hinzu.  
  
13. Geben Sie auf der Seite **Kompatibilitätsregeln** des Assistenten die Bedingungen an, mit denen die Kompatibilität eines Konfigurationselements definiert wird. Damit eine Einstellung auf Kompatibilität ausgewertet werden kann, muss sie über mindestens eine Kompatibilitätsregel verfügen. Klicken Sie auf **Neu** , um eine neue Regel hinzuzufügen.  
  
14. Geben Sie im Dialogfeld **Regel erstellen** die folgenden Informationen an:  
  
    -   **Name:** Geben Sie einen Namen für die Kompatibilitätsregel ein.  
  
    -   **Beschreibung:** Geben Sie eine Beschreibung für die Kompatibilitätsregel ein.  
  
    -   **Ausgewählte Einstellung:** Klicken Sie auf **Durchsuchen** So öffnen die **Einstellung auswählen** (Dialogfeld). Wählen Sie die Einstellung, die Sie verwenden möchten, eine Regel definieren, oder klicken Sie auf **neue Einstellung**. Klicken Sie dann auf **Auswählen**.  
  
        > [!TIP]  
        >  Sie können zum Anzeigen von Informationen über die derzeit ausgewählte Einstellung auch auf **Eigenschaften** klicken.  
  
    -   **Regeltyp** Wählen Sie den zu verwendenden Kompatibilitätsregeltyp aus:  
  
        -   **Wert** : Erstellen Sie eine Regel, mit deren Hilfe der vom Konfigurationselement zurückgegebene Wert mit einem von Ihnen angegebenen Wert verglichen wird.  
  
        -   **Existenziell** : Erstellen Sie eine Regel, mit der die Einstellung abhängig davon ausgewertet wird, ob sie auf einem Gerät vorhanden ist.  
  
    -   Geben Sie für eine Regel des Typs **Wert**die folgenden Informationen an:  
  
        -   Die folgende Regel muss von der Einstellung erfüllt werden. Wählen Sie einen Operator und einen Wert aus, die mit der ausgewählten Einstellung auf Kompatibilität ausgewertet werden. Folgende Operatoren können verwendet werden:  
  
            -   **Gleich**  
  
            -   **Ungleich**  
  
            -   **Größer als**  
  
            -   **Kleiner als**  
  
            -   **Zwischen**  
  
            -   **Größer oder gleich**  
  
            -   **Kleiner oder gleich**  
  
            -   **Eine von** : Geben Sie im Textfeld pro Zeile einen Eintrag an.  
  
            -   **Keine von** : Geben Sie im Textfeld pro Zeile einen Eintrag an.  
  
        -   **Nicht kompatible Regeln wiederherstellen, falls dies unterstützt wird** : Wählen Sie diese Option aus, wenn nicht kompatible Regeln von Configuration Manager automatisch wiederhergestellt werden sollen.  
  
            > [!IMPORTANT]  
            >  Sie können nicht kompatible Regeln nur wiederherstellen, wenn der Regeloperator auf **Ist gleich**festgelegt ist.  
  
        -   **Nichtkompatibilität melden, wenn diese Einstellungsinstanz nicht gefunden wird** : Vom Konfigurationselement wird eine Nichtkompatibilität gemeldet, wenn diese Einstellung auf dem Macintosh-Computern nicht gefunden wird.  
  
    -   **Schweregrad der Nichtkompatibilität für Berichte** : Geben Sie den Schweregrad an, der gemeldet wird, wenn bei dieser Kompatibilitätsregel ein Fehler auftritt. Die folgenden Schweregrade sind verfügbar:  
  
        -   **Keine**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.  
  
        -   **Information**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.  
  
        -   **Warnung**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.  
  
        -   **Kritisch**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.  
  
        -   **Kritisch mit Ereignis**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Dieser Schweregrad wird auch vom Macintosh-Clientcomputer protokolliert.  
  
    -   Geben Sie für eine Regel des Typs **Existenziell**die folgenden Informationen an:  
  
        -   Wählen Sie eine der folgenden:  
  
            -   **Diese Einstellung muss auf Clientgeräten vorhanden sein**  
  
            -   **Diese Einstellung darf auf Clientgeräten nicht vorhanden sein**  
  
        -   **Schweregrad der Nichtkompatibilität für Berichte:** Geben Sie den Schweregrad, der gemeldet wird, wenn es sich bei dieser Kompatibilitätsregel ein Fehler auftritt. Die folgenden Schweregrade sind verfügbar:  
  
            -   **Keine**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.  
  
            -   **Information**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.  
  
            -   **Warnung**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.  
  
            -   **Kritisch**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.  
  
            -   **Kritisch mit Ereignis**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Dieser Schweregrad wird auch vom Macintosh-Clientcomputer protokolliert.  
  
        > [!NOTE]  
        >  Die angezeigten Optionen sind möglicherweise unterschiedlich, je nach Einstellungstyp, für den Sie eine Regel konfigurieren.  
  
    -   Klicken Sie auf **OK** , um das Dialogfeld **Regel erstellen** zu schließen.  
  
15. Bestätigen Sie auf der Seite **Zusammenfassung** die Einstellungen für das neue Konfigurationselement, und schließen Sie dann den Assistenten.  
  
 Das neue Konfigurationselement wird anschließend im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Konfigurationselement** angezeigt.  
  
 Wenn Sie jetzt dieses Konfigurationselement einer Konfigurationsbasislinie hinzufügen möchten, gehen Sie zu [Erstellen von Konfigurationsbasislinien in System Center Configuration Manager](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurationselemente für Geräte, die mit dem System Center Configuration Manager-Client verwaltet werden](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)
