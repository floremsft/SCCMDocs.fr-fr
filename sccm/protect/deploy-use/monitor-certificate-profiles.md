---
title: "Überwachen von Zertifikatprofilen | Microsoft-Dokumentation"
description: "Enthält das Überwachen des Kompatibilitätsstatus von Zertifikatprofilen in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
caps.latest.revision: "7"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 84e275fa5b17bc703da22fb686ef9050d17e557f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-monitor-certificate-profiles-in-system-center-configuration-manager"></a>Überwachen von Zertifikatprofilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Anzeigen von Konformitätsergebnissen in der Configuration Manager-Konsole  

Zum Überwachen der SCEP-Zertifikatkonformität verwenden Sie nicht die Konsole, sondern [Berichte](#view-compliance-results-by-using-reports). 

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Überwachung**>  **Bereitstellungen** aus.  

3.  Wählen Sie die gewünschte Zertifikatprofilbereitstellung aus.  

4.  Überprüfen Sie die Zusammenfassung der Informationen zur Zertifikatskonformität auf der Hauptseite. Wählen Sie zum Anzeigen ausführlicherer Informationen das Zertifikatprofil aus, und klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen**, um die Seite **Bereitstellungsstatus** anzuzeigen.  

     Auf der Seite **Bereitstellungsstatus** sind die folgenden Registerkarten enthalten:  

    -   **Kompatibel**: Hiermit wird die Kompatibilität des Zertifikatprofils basierend auf der Anzahl der betroffenen Bestände angezeigt. Sie können auf eine Regel doppelklicken, um im Arbeitsbereich **Bestand und Kompatibilität** unter dem Knoten **Benutzer** einen temporären Knoten zu erstellen. In diesem Knoten sind alle Benutzer enthalten, die mit dem Zertifikatprofil kompatibel sind. Im Bereich **Bestandsdetails** werden zudem die Benutzer angezeigt, die mit diesem Profil kompatibel sind. Weitere Informationen erhalten Sie, wenn Sie in der Liste auf einen Benutzer doppelklicken.  

        > [!IMPORTANT]  
        >  Ein Zertifikatprofil wird nicht ausgewertet, wenn es für ein Clientgerät nicht gilt. Es wird jedoch als kompatibel zurückgegeben.  

    -   **Fehler**: Hiermit wird eine Liste aller Fehler für die ausgewählte Bereitstellung des Zertifikatprofils basierend auf der Anzahl der betroffenen Bestände angezeigt. Sie können auf eine Regel doppelklicken, um im Arbeitsbereich **Bestand und Kompatibilität** unter dem Knoten **Benutzer** einen temporären Knoten zu erstellen. In diesem Knoten sind alle Benutzer enthalten, für die bei diesem Profil Fehler erzeugt wurden. Wenn Sie einen Benutzer auswählen, werden im Bereich **Bestandsdetails** die Benutzer angezeigt, die vom ausgewählten Problem betroffen sind. Doppelklicken Sie in der Liste auf einen Benutzer, um weitere Informationen anzuzeigen.  

    -   **Nicht kompatibel**: Hiermit wird eine Liste aller nicht kompatiblen Regeln im Zertifikatprofil basierend auf der Anzahl der betroffenen Bestände angezeigt. Sie können auf eine Regel doppelklicken, um im Arbeitsbereich **Bestand und Kompatibilität** unter dem Knoten **Benutzer** einen temporären Knoten zu erstellen. In diesem Knoten sind alle Benutzer enthalten, für die bei diesem Profil Fehler erzeugt wurden. Wenn Sie einen Benutzer auswählen, werden im Bereich **Bestandsdetails** die Benutzer angezeigt, die vom ausgewählten Problem betroffen sind. Doppelklicken Sie auf einen Benutzer in der Liste, um weitere Informationen über das Problem anzuzeigen.  

    -   **Unbekannt**: Hiermit wird eine Liste aller Benutzer angezeigt, von denen keine Kompatibilität der ausgewählten Bereitstellung des Zertifikatprofils zusammen mit dem aktuellen Clientstatus von Geräten gemeldet wurde.  

5.  Auf der Seite **Bereitstellungsstatus** finden Sie ausführliche Informationen zur Konformität des bereitgestellten Zertifikatprofils. Unter dem Knoten **Bereitstellungen** wird ein temporärer Knoten erstellt, mit dessen Hilfe Sie die Informationen schnell wiederfinden können.  

     Der Anmeldungsstatus des Zertifikats wird als Zahl angezeigt. Der folgenden Tabelle können Sie die Bedeutungen der einzelnen Zahlen entnehmen:  

    |Anmeldungsstatus|Beschreibung|  
    |-----------------------|-----------------|  
    |0x00000001|Die Anmeldung war erfolgreich. Das Zertifikat wurde ausgestellt.|  
    |0x00000002|Die Anforderung wurde übermittelt, und die Anmeldung ist ausstehend, oder eine Out-of-Band-Anforderung wurde ausgestellt.|  
    |0x00000004|Die Anmeldung muss verschoben werden.|  
    |0x00000010|Ein Fehler ist aufgetreten.|  
    |0x00000020|Der Anmeldungsstatus ist unbekannt.|  
    |0x00000040|Die Statusinformationen wurden übersprungen. Dies kann vorkommen, wenn eine HYPERLINK "http://msdn.microsoft.com/en-us/windows/ms721572" \l "_security_certification_authority_gly" Zertifizierungsstelle ungültig ist oder nicht zur Überwachung ausgewählt wurde.|  
    |0x00000100|Die Anmeldung wurde abgewiesen.|  

##  <a name="view-compliance-results-by-using-reports"></a>Anzeigen von Konformitätsergebnissen mithilfe von Berichten

 Kompatibilitätseinstellungen in System Center Configuration Manager schließen integrierte Berichte ein, mit deren Hilfe Sie Informationen zu Zertifikatprofilen überwachen können. Diese Berichte verfügen über die Berichtskategorie **Kompatibilitäts- und Einstellungsverwaltung**.  

> [!IMPORTANT]  
>  Sie müssen ein Platzhalterzeichen (%) verwenden, wenn Sie in Berichten zu Kompatibilitätseinstellungen die Parameter **Gerätefilter** und **Benutzerfilter** eingestellt haben.  

Verwenden Sie zum Überwachen der SCEP-Zertifikatkonformität die folgenden Zertifikatberichte unter dem Berichtsknoten **Zugriff auf Unternehmensressourcen**:  

 -   Zertifikatausstellung – Verlauf  
 -   Liste von Beständen mit Zertifikaten, die demnächst ablaufen  
 -   Liste von Beständen nach Zertifikatausstellungsstatus  



 Weitere Informationen zum Konfigurieren der Berichterstellung in System Center Configuration Manager finden Sie unter [Berichterstellung in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
