---
title: "Überwachen von Konformitätseinstellungen | Microsoft-Dokumentation"
description: "Verwenden Sie eine oder mehrere der Verfahren aus diesem Thema, um den Kompatibilitätsstatus der Konfigurationsbaselines anzuzeigen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 75cd7e811262633d81d978265f21ec7ed3b61a58
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-compliance-settings-in-system-center-configuration-manager"></a>Überwachen von Kompatibilitätseinstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Nach dem Bereitstellen von Configuration Manager-Konfigurationsbaselines auf Computern in der Hierarchie können Sie eine oder mehrere der folgenden Vorgehensweisen verwenden, um den Kompatibilitätsstatus der Konfigurationsbaselines anzuzeigen:

> [!NOTE]  
>  In den Feldern für die Überprüfungskriterien in Berichten zu Kompatibilitätseinstellungen (dies entspricht bei Clientberichten **Einschränkungen**) wird das zugrunde liegende SML (Service Modeling Language) angezeigt. Dadurch wird Administratoren, die das Konfigurationselement in der Configuration Manager-Konsole erstellt haben und nicht mit SML vertraut sind, die Auswertung der Überprüfungskriterien erschwert. Verwenden Sie in diesem Fall den Arbeitsbereich **Überwachung** in der Configuration Manager-Konsole, um die Eigenschaften des Konfigurationselements und die entsprechenden Überprüfungskriterien anzuzeigen.  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Anzeigen von Kompatibilitätsergebnissen in der Configuration Manager-Konsole  
 Mit dieser Vorgehensweise können Sie Details zur Kompatibilität der bereitgestellten Konfigurationsbaselines in der Configuration Manager-Konsole anzeigen.  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Anzeigen von Kompatibilitätsergebnissen in der Configuration Manager-Konsole  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung** > **Bereitstellungen**.  

3.  Wählen Sie in der Liste **Bereitstellungen** die Bereitstellung der Konfigurationsbasislinie aus, für die Sie die Kompatibilitätsinformationen lesen möchten.  

4.  Zusammenfassende Informationen zur Kompatibilität der Konfigurationsbasislinienbereitstellung finden Sie auf der Hauptseite. Wählen Sie zum Anzeigen ausführlicherer Informationen die Bereitstellung der Konfigurationsbasislinie aus, und klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen** , um die Seite **Bereitstellungsstatus** anzuzeigen.  

     Auf der Seite **Bereitstellungsstatus** sind die folgenden Registerkarten enthalten:  

    -   **Kompatibel**: zeigt die Kompatibilität der Konfigurationsbasislinie basierend auf der Anzahl der betroffenen Bestände an. Sie können auf eine Regel klicken, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, die mit dieser Regel kompatibel sind. Im Bereich **Bestandsdetails** werden die Benutzer oder Geräte angezeigt, die mit der Konfigurationsbasislinie kompatibel sind. Doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste, um weitere Informationen anzuzeigen.  

        > [!IMPORTANT]  
        >  Eine Konfigurationselementregel wird nicht ausgewertet, wenn sie nicht erkannt wird oder auf einem Clientgerät nicht angewendet werden kann. Dennoch wird die Regel als kompatibel zurückgegeben.  

    -   **Fehler**:zeigt eine Liste aller Fehler für die ausgewählte Bereitstellung der Konfigurationsbasislinie basierend auf der Anzahl der betroffenen Bestände an. Sie können auf eine Regel klicken, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, durch die mit dieser Regel Fehler generiert wurden. Wenn Sie einen Benutzer oder ein Gerät auswählen, werden im Bereich **Bestandsdetails** die Benutzer oder Geräte angezeigt, die vom ausgewählten Problem betroffen sind. Doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste, um weitere Informationen zum Problem anzuzeigen.  

    -   **Nicht kompatibel**: Zeigt eine Liste aller nicht kompatiblen Regeln innerhalb der Konfigurationsbasislinie basierend auf der Anzahl der betroffenen Bestände an. Sie können auf eine Regel klicken, um unter dem Knoten **Benutzer** oder **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** einen temporären Knoten zu erstellen, in dem alle Benutzer oder Geräte enthalten sind, die nicht mit dieser Regel kompatibel sind. Wenn Sie einen Benutzer oder ein Gerät auswählen, werden im Bereich **Bestandsdetails** die Benutzer oder Geräte angezeigt, die vom ausgewählten Problem betroffen sind. Doppelklicken Sie auf einen Benutzer oder ein Gerät in der Liste, um weitere Informationen zu diesem Problem anzuzeigen.  

    -   **Unbekannt**: Zeigt eine Liste aller Benutzer und Geräte an, von denen keine Kompatibilität der ausgewählten Bereitstellung der Konfigurationsbasislinie zusammen mit dem aktuellen Clientstatus von Geräten gemeldet wurde.  

5.  Auf der Seite **Bereitstellungsstatus** finden Sie ausführliche Informationen zur Kompatibilität der bereitgestellten Konfigurationsbasislinie. Unter dem Knoten **Bereitstellungen** wird ein temporärer Knoten erstellt, mit dessen Hilfe Sie die Informationen schnell wiederfinden können.  

##  <a name="view-compliance-results-by-using-reports"></a>Anzeigen von Kompatibilitätsergebnissen mithilfe von Berichten  
 Kompatibilitätseinstellungen in Configuration Manager umfassen mehrere integrierte Berichte, mit denen Sie Daten zu Konfigurationselementen, Konfigurationsbaselines und Bereitstellungen überwachen können. Diese Berichte verfügen über die Berichtskategorie **Kompatibilitäts- und Einstellungsverwaltung**.  

> [!IMPORTANT]  
>  Sie müssen ein Platzhalterzeichen (**%**) verwenden, wenn Sie in Berichten zu Kompatibilitätseinstellungen die Parameter **Gerätefilter** und „Benutzerfilter“ verwenden.  

 Weitere Informationen zum Konfigurieren der Berichterstellung in Configuration Manager finden Sie unter [Berichterstellung in System Center Configuration Manager](../../core/servers/manage/reporting.md)  

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Zeigen Sie Kompatibilitätsergebnisse auf einem Configuration Manager-Windows-Clientcomputer an

> [!NOTE]  
>  Sie können keine Daten auf dem Configuration Manager-Windows-Client anzeigen, wenn Sie mit einem Domänengastkonto angemeldet sind.    

1.  Doppelklicken Sie in der Systemsteuerung des Clientcomputers auf **Configuration Manager** , um die Eigenschaften anzuzeigen.  

2.  Klicken Sie auf die Registerkarte **Konfiguration** , und zeigen Sie die Liste der bereitgestellten Konfigurationsbasislinien an.  

3.  Zeigen Sie den **Kompatibilitätszustand** für jede Konfigurationsbasislinie an:  

    > [!IMPORTANT]  
    >  Die Bewertungsergebnisse werden 15 Minuten lang auf dem Client zwischengespeichert. Wenn Sie innerhalb der 15 Minuten eine erneute Auswertung initiieren, werden die Kompatibilitätsergebnisse aus dem Cache und nicht aus einer erneuten Auswertung zurückgegeben. Aus diesem Grund sollten Sie bei Änderungen am Client, die sich auf die Ergebnisse der Kompatibilitätsbewertung auswirken können, vor dem Initiieren einer erneuten Bewertung 15 Minuten warten.  

    -   **Kompatibel**: Der Clientcomputer ist mit der ausgewerteten Konfigurationsbasislinie kompatibel.  

    -   **Nicht kompatibel**: Der Clientcomputer ist mit der ausgewerteten Konfigurationsbasislinie nicht kompatibel.  

    -   **Unbekannt**: Die Konfigurationsbasislinie wurde vom Clientcomputer noch nicht bewertet. Wenn Sie die Bewertung außerhalb des Zeitplans für die Kompatibilitätsbewertung initiieren möchten, wählen Sie die zu bewertenden Konfigurationsbasislinien aus, und klicken Sie auf **Bewerten**.  

        > [!NOTE]  
        >  Falls Sie auf dem Clientcomputer lokale Administratoranmeldedaten verwenden, können Sie Details jeder ausgewerteten Konfigurationsbasislinie anzeigen, um zu bestimmen, welches Konfigurationselement den Status „Nicht kompatibel“ meldet. Dazu wählen Sie die Konfigurationsbasislinie aus, und klicken Sie auf **Bericht anzeigen**.  

4.  Klicken Sie auf **OK**.  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>Erstellen von Sammlungen auf Basis der Konfigurationsbaselinekompatibilität  
 Gehen Sie wie folgt vor, um eine Configuration Manager-Sammlung auf der Grundlage von Geräten mit einer angegebenen Kompatibilität zu erstellen. Sie können Sammlungen basierend auf den folgenden Kompatibilitätszuständen erstellen:  

-   **Kompatibel**  

-   **Fehler**  

-   **Non-compliant**  

-   **Unbekannt**  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationsbaselines**.  

3.  Wählen Sie in der Liste **Konfigurationsbasislinien** die Konfigurationsbasislinie aus, aus der Sie eine Sammlung erstellen möchten.  

4.  Klicken Sie auf der Registerkarte **Bereitstellung** in der Gruppe **Bereitstellung**auf **Neue Sammlung erstellen** , und wählen Sie dann aus der Dropdownliste die Kompatibilitätsstufe aus, für die Sie eine Sammlung erstellen möchten.  

5.  Der **Assistent zum Erstellen von Benutzersammlungen** oder der **Assistent zum Erstellen von Gerätesammlungen** wird geöffnet, je nachdem, ob das Konfigurationselement für Benutzer oder für Geräte bereitgestellt wird. Der Assistent wird automatisch mit den korrekten Werten zum Erstellen der Sammlung aufgefüllt. Sie können diese Werte jedoch auch bearbeiten.  

6.  Wenn Sie den Assistenten abgeschlossen haben, wird die Sammlung im Arbeitsbereich **Bestand und Kompatibilität** entweder im Knoten **Benutzersammlungen** oder im Knoten **Gerätesammlungen** angezeigt.  
