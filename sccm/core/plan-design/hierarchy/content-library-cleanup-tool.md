---
title: Das Inhaltsbibliothek-Bereinigungstool | Microsoft-Dokumentation
description: Verwenden Sie das Inhaltsbibliothek-Bereinigungstool zum Entfernen von verwaistem Inhalt, der nicht mehr einer Bereitstellung von System Center Configuration Manager zugeordnet ist.
ms.custom: na
ms.date: 4/7/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 76e6772bdd5cbd32d525e728f6ebc988b045da78
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="the-content-library-cleanup-tool-for-system-center-configuration-manager"></a>Das Inhaltsbibliothek-Bereinigungstool in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

 Ab Version 1702 können Sie ein Befehlszeilentool (**ContentLibraryCleanup.exe**) für die Entfernung des Inhalts verwenden, der keinem Paket oder keiner Anwendung eines Verteilungspunktes mehr zugeordnet ist (verwaister Inhalt). Dieses Tool wird Inhaltsbibliothek-Bereinigungstool genannt und ersetzt ältere Versionen von ähnlichen Tools, die für frühere Configuration Manager-Produkte freigegeben wurden.  

Das Tool wirkt sich nur auf den Inhalt auf dem Verteilungspunkt aus, den Sie angeben, wenn Sie das Tool ausführen. Das Tool kann keinen Inhalt aus der Inhaltsbibliothek auf dem Standortserver entfernen.

Sie können **ContentLibraryCleanup.exe** im Ordner *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* auf dem Standortserver an einem Standort der zentralen Verwaltung oder einem primären Standort finden.

## <a name="requirements"></a>Anforderungen  
 Das Tool kann jeweils immer nur für einen einzelnen Verteilungspunkt ausgeführt werden.  
 - Es kann direkt auf dem Computer ausgeführt werden, der den Verteilungspunkt hostet, den Sie bereinigen möchten, oder remote auf einem anderen Server.
 - Das Benutzerkonto, das das Tool ausführt, muss über direkte rollenbasierte Administratorrechte verfügen, die in der Configuration Manager-Hierarchie einem vollständigen Administratorkonto entsprechen würden. Das Tool funktioniert nicht, wenn das Benutzerkonto Mitgliedsrechte einer Windows-Sicherheitsgruppe mit vollständigen Administratorrechten erhält.

## <a name="modes-of-operation"></a>Betriebsmodi
Das Tool kann in den folgenden zwei Modi ausgeführt werden. Wir empfehlen Ihnen das Tool im *Was-wäre-wenn*-Modus auszuführen, sodass Sie die daraus resultierenden Protokolldateien überprüfen können, bevor Sie das Tool im *Löschmodus* ausführen:
  1.    **Was-wäre-wenn-Modus**:   
      Wenn Sie den **/delete**-Schalter nicht angeben, wird das Tool im „Was-wäre-wenn“-Modus ausgeführt. Es identifiziert den Inhalt, der am Verteilungspunkt gelöscht werden würde.
   - Wenn das Tool in diesem Modus ausgeführt wird, löscht es keine Daten.
   - Informationen zum Inhalt, der gelöscht werden würde, wird in die Protokolldatei des Tools geschrieben, und Sie werden nicht aufgefordert, jeden möglichen Löschvorgang zu bestätigen.  
      </br>   

  2. **Löschmodus**:   
    Wenn Sie das Tool mit dem **/delete**-Schalter ausführen, wird das Tool im Löschmodus ausgeführt.

     - Wenn es in diesem Modus ausgeführt wird, können verwaiste Inhalte, die auf dem angegebenen Verteilungspunkt gefunden werden, aus der Inhaltsbibliothek des Verteilungspunktes gelöscht werden.
     -  Vor dem Löschen jeder Datei müssen Sie bestätigen, dass die Datei gelöscht werden soll.  Sie können **Y** für „Ja“, **N** für „Nein“, oder **Ja, alle** auswählen, um weitere Aufforderungen zu überspringen und alle verwaisten Inhalte zu löschen.  
     </br>

Wenn das Tool in einem der beiden Modi ausgeführt wird, erstellt es automatisch ein Protokoll mit einem Namen, in dem der vom Tool ausgeführte Modus, der Name des Verteilungspunktes sowie Datum und Uhrzeit des Vorgangs enthalten sind. Die Protokolldatei wird automatisch geöffnet, wenn das Tool fertig ist.

Standardmäßig wird die Protokolldatei in den temporären Ordner des Benutzerkontos geschrieben, das das Tool ausführt, auf dem Computer, auf dem das Tool ausgeführt wird. Sie können den **/log**-Schalter verwenden, um die Protokolldatei an einen anderen Speicherort, einschließlich einer Netzwerkfreigabe, umzuleiten.


## <a name="run-the-tool"></a>Ausführen des Tools
So führen Sie das Tool aus:
1. Öffnen Sie eine administrative Eingabeaufforderung in einen Ordner, in dem sich **ContentLibraryCleanup.exe** befindet.  
2. Geben Sie als nächstes eine Befehlszeile mit den erforderlichen Befehlszeilen-Switches ein sowie die optionalen Switches, die Sie verwenden möchten.

**Bekanntes Problem** Wenn das Tool ausgeführt wird, kann eine Fehlermeldung wie die folgende zurückgegeben werden, wenn ein Paket oder eine Bereitstellung fehlgeschlagen oder gerade in Bearbeitung ist:
-  *System.InvalidOperationException: Diese Inhaltsbibliothek kann jetzt nicht bereinigt werden, da das Paket <packageID> nicht vollständig installiert ist.*

**Problemumgehung:** Keiner Das Tool kann nicht zuverlässig verwaiste Dateien identifizieren, wenn der Inhalt in Bearbeitung ist oder nicht bereitgestellt werden konnte. Aus diesem Grund kann das Tool den Inhalt nicht bereinigen, bis das Problem gelöst wurde.

### <a name="command-line-switches"></a>Befehlszeilen-Switches  
Die folgenden Befehlszeilen-Switches können in jeglicher Reihenfolge verwendet werden.   

|Schalter|Details|
|---------|-------|
|**/delete**  |**Optional** </br> Verwenden Sie diesen Schalter, wenn Sie Inhalte vom Verteilungspunkt löschen möchten. Sie erhalten eine Aufforderung bevor Inhalt gelöscht wird. </br></br> Wenn dieser Schalter nicht verwendet wird, protokolliert das Tool, welcher Inhalt gelöscht werden würde, löscht aber keine Inhalte vom Verteilungspunkt. </br></br> Beispiel: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Optional** </br> Dieser Schalter führt das Tool in einem stillen Modus aus, der alle Eingabeaufforderungen unterdrückt (z.B. Aufforderungen zum Löschen von Inhalt), und öffnet die Protokolldatei nicht automatisch. </br></br> Beispiel: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;distribution point FQDN>**  | **Erforderlich** </br> Geben Sie den vollständig qualifizierten Domänennamen (FQDN) des Verteilungspunkts an, den Sie bereinigen möchten. </br></br> Beispiel:  ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;primary site FQDN>**       | **Optional** wenn Inhalt von einem Verteilungspunkt an einem primären Standort bereinigt wird.</br>**Erforderlich** wenn Inhalt von einem Verteilungspunkt an einem sekundären Standort bereinigt wird. </br></br>Das Tool stellt eine Verbindung mit dem übergeordneten primären Standort her, um Abfragen von SMS_Provider auszuführen. Mit diesen Abfragen kann das Tool bestimmen, welcher Inhalt sich auf dem Verteilungspunkt befinden sollte; so kann es den Inhalt identifizieren, der verwaist ist und entfernt werden kann. Die Verbindung zum übergeordneten primären Standort muss für Verteilungspunkte an einem sekundären Standort hergestellt werden, da die erforderlichen Angaben nicht direkt am sekundären Standort zur Verfügung stehen.</br></br> Geben Sie den FQDN des primären Standorts an, zu dem der Verteilungspunkt gehört, oder geben Sie den übergeordneten primären Standort an, wenn sich der Verteilungspunkt an einem sekundären Standort befindet. </br></br> Beispiel: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;primary site code>**  | **Optional** wenn Inhalt von einem Verteilungspunkt an einem primären Standort bereinigt wird.</br>**Erforderlich** wenn Inhalt von einem Verteilungspunkt an einem sekundären Standort bereinigt wird. </br></br> Geben Sie den Standordcode des primären Standorts an, zu dem der Verteilungspunkt gehört, oder geben Sie den übergeordneten primären Standort an, wenn sich der Verteilungspunkt an einem sekundären Standort befindet.</br></br> Beispiel: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/Protokoll <log file directory>**       |**Optional** </br> Geben Sie den Speicherort an, in den das Tool die Protokolldatei schreibt. Dies kann auf einem lokalen Laufwerk oder auf einer Netzwerkfreigabe sein.</br></br> Wenn dieser Schalter nicht verwendet wird, wird die Protokolldatei im temporären Ordner des Benutzers auf dem Computer gespeichert, in dem das Tool ausgeführt wird.</br></br> Beispiel für ein lokales Laufwerk: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Beispiel für ein geteiltes Netzwerk: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;share>\&lt;folder>***|
