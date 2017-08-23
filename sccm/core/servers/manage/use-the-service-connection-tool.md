---
title: Dienstverbindungstools | Microsoft-Dokumentation
description: "Erfahren Sie mehr über das Dienstverbindungstool, mit dem Sie eine Verbindung mit dem Configuration Manager-Clouddienst herstellen können, um manuell Nutzungsinformationen hochzuladen."
ms.custom: na
ms.date: 4/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
caps.latest.revision: "11"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0da80521bf223a765c3731f8ad59623d85a4c9fa
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="use-the-service-connection-tool-for-system-center-configuration-manager"></a>Verwenden des Dienstverbindungstools für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie das **Dienstverbindungstool**, wenn sich Ihr Dienstverbindungspunkt im Offline-Modus befindet, oder wenn Ihre Standortsystemserver von Configuration Manager nicht mit dem Internet verbunden sind. Mit diesem Tool ist Ihr Standort immer auf dem neuesten Stand was Configuration Manager-Updates angeht.  

Wenn Sie dieses Tool ausführen, stellt es manuell eine Verbindung mit dem Configuration Manager-Clouddienst her, um Nutzungsinformationen für Ihre Hierarchie hochzuladen und Updates herunterzuladen. Das Hochladen der Nutzungsdaten ist erforderlich, damit der Clouddienst die richtigen Updates für Ihre Bereitstellung liefern kann.  

## <a name="prerequisites-for-using-the-service-connection-tool"></a>Voraussetzungen für die Verwendung des Dienstverbindungstools
Im Folgenden finden Sie Voraussetzungen und bekannte Probleme.

**Voraussetzungen:**

-   Sie haben einen Dienstverbindungspunkt installiert und diesen auf **Offline, On-Demand-Verbindung**festgelegt.  

-   Das Tool muss von einer Eingabeaufforderung aus ausgeführt werden.  

-   Jeder Computer, auf dem das Tool ausgeführt wird (Dienstverbindungspunkt-Computer und mit dem Internet verbundener Computer), muss ein x64-System mit den folgenden installierten Komponenten sein:  

    -   **Visual C++ Redistributable** -Dateien für x86- und x64-Systeme.   Standardmäßig installiert Configuration Manager die x64-Version auf dem Computer, der den Dienstverbindungspunkt hostet.  

         Um eine Kopie der Visual C++-Dateien herunterzuladen, besuchen Sie die Seite für [Visual C++ Redistributable-Pakete für Visual Studio 2013](http://www.microsoft.com/download/details.aspx?id=40784) im Microsoft Download Center.  

    -   .NET Framework 4.5.2 oder höher.  

-   Das Konto, das Sie zum Ausführen des Tools verwenden, muss über Folgendes verfügen:
    -   **lokale Administratorrechte** auf dem Computer, auf dem der Dienstverbindungspunkt (auf dem das Tool ausgeführt wird) gehostet ist.
    -   **Leseberechtigungen** für die Standortdatenbank.  



-   Sie benötigen ein USB-Laufwerk mit genügend freiem Speicherplatz zum Speichern von Dateien und Updates, oder eine andere Methode zum Übertragen von Dateien zwischen dem Dienstverbindungspunkt-Computer und dem Computer mit Internetzugriff. (Bei diesem Szenario wird davon ausgegangen, dass Ihr Standort und die verwalteten Computer keine direkte Internetverbindung haben.)  



## <a name="use-the-service-connection-tool"></a>Verwenden des Dienstverbindungstools  

 Sie finden das Dienstverbindungstool (**serviceconnectiontool.exe**) auf dem Configuration Manager-Installationsmedium im Ordner **%path%\smssetup\tools\ServiceConnectionTool**. Verwenden Sie immer das Dienstverbindungstool, das der Version von Configuration Manager entspricht, die Sie verwenden.


 In diesem Verfahren werden in den Befehlszeilenbeispielen die folgenden Dateinamen und Ordnerpfade verwendet (die Verwendung dieser Pfade und Dateinamen ist nicht zwingend; stattdessen können Sie auch Alternativen verwenden, die auf Ihre Umgebung und die Voreinstellungen abgestimmt sind):  

-   Der Pfad zu einem USB-Stick mit Daten, die zwischen den Servern übertragen werden: **D:\USB\\**  

-   Der Name der CAB-Datei, die die vom Standort exportierten Daten enthält: **UsageData.cab**  

-   Der Name des leeren Ordners, in dem heruntergeladene Configuration Manager-Updates zur Übertragung zwischen Servern gespeichert werden: **UpdatePacks**  

Schritte auf dem Computer, von dem der Dienstverbindungspunkt gehostet wird.  

-   Öffnen Sie eine Eingabeaufforderung mit Administratorrechten, und wechseln Sie anschließend in das Verzeichnis mit der Datei **serviceconnectiontool.exe**.  

     Sie finden dieses Tool standardmäßig auf dem Configuration Manager-Installationsmedium im Ordner **%path%\smssetup\tools\ServiceConnectionTool**. Damit das Dienstverbindungstool funktioniert, müssen alle Dateien aus diesem Ordner im selben Ordner abgelegt werden.  

Wenn Sie den folgenden Befehl ausführen, bereitet das Tool eine CAB-Datei vor, die Informationen zur Verwendung und zum Kopieren an einen Speicherort Ihrer Wahl enthält. Die Daten in der CAB-Datei basieren auf der Ebene der Diagnosenutzungsdaten, zu deren Sammlung Ihre Website konfiguriert ist. (Siehe [Diagnose- und Nutzungsdaten für System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)).  Führen Sie den folgenden Befehl zum Erstellen der CAB-Datei aus:  

-   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

Sie müssen auch den Ordner ServiceConnectionTool mit seinem gesamten Inhalt auf das USB-Laufwerk kopieren, oder andernfalls auf dem Computer zur Verfügung stellen, den Sie für die Schritte 3 und 4 verwenden.  

### <a name="overview"></a>Übersicht
**Zur Verwendung des Dienstverbindungstools müssen Sie drei Hauptschritte ausführen:**  

1.  **Vorbereiten**: Dieser Schritt muss auf dem Computer ausgeführt werden, der den Dienstverbindungspunkt hostet. Wenn das Tool ausgeführt wird, werden Ihre Nutzungsdaten in einer CAB-Datei abgelegt und auf einem USB-Laufwerk (bzw. auf einem anderen angegebenen Umlagerungsort) gespeichert.  

2.  **Verbinden**: In diesem Schritt führen Sie das Tool auf einem Remotecomputer aus, der eine Verbindung mit dem Internet herstellt, um Daten hochzuladen und Updates herunterzuladen.  

3.  **Importieren**: Dieser Schritt muss auf dem Computer ausgeführt werden, der den Dienstverbindungspunkt hostet. Wenn das Tool ausgeführt wird, werden die von Ihnen heruntergeladenen Updates importiert und Ihrem Standort hinzugefügt; anschließend können Sie sich diese Updates anschauen und aus der Configuration Manager-Konsole installieren.  

Ab Version 1606 können Sie mehrere CAB-Dateien gleichzeitig hochladen (jede aus einer anderen Hierarchie), wenn Sie eine Verbindung mit Microsoft herstellen und einen Proxyserver sowie einen Benutzer für den Proxyserver angeben.   

**Hochladen mehrerer CAB-Dateien:**
 -  Speichern Sie jede CAB-Datei, die Sie aus separaten Hierarchien exportieren, im gleichen Ordner. Der Name jeder Datei muss eindeutig sein. Falls nötig, können Sie sie manuell umbenennen.
 -  Wenn Sie anschließend den Befehl zum Hochladen der Daten zu Microsoft ausführen, geben Sie den Ordner an, der die CAB-Dateien enthält. (Vor dem Update 1606 war nur ein Hochladen von Daten aus einer einzelnen Hierarchie gleichzeitig möglich, und das Tool forderte die Angabe des Namens der CAB-Datei im Ordner.)
 -  Wenn Sie später die Importaufgabe auf einem Dienstverbindungspunkt einer Hierarchie ausführen, importiert das Tool automatisch nur die Daten dieser Hierarchie.  

**So geben Sie einen Proxyserver an:**  
Sie können die folgenden optionalen Parameter zum Angeben eines Proxyservers verwenden (Weitere Informationen zur Verwendung dieser Parameter sind im Abschnitt „Befehlszeilenparameter“ dieses Themas aufgeführt):
  - **-proxyserveruri [FQDN_of_proxy_server]**  Mit diesem Parameter können Sie den Proxyserver angeben, der für diese Verbindung genutzt werden soll.
  -  **proxyusername [Benutzername]**  Verwenden Sie diesen Parameter, wenn Sie einen Benutzer für den Proxyserver angeben müssen.



### <a name="to-use-the-service-connection-tool"></a>So verwenden Sie das Dienstverbindungstool  

1.  Schritte auf dem Computer, von dem der Dienstverbindungspunkt gehostet wird.  

    -   Öffnen Sie eine Eingabeaufforderung mit Administratorrechten, und wechseln Sie anschließend in das Verzeichnis mit der Datei **serviceconnectiontool.exe**.   

2.  Führen Sie den folgenden Befehl aus, damit das Tool eine CAB-Datei vorbereitet, die Informationen zur Verwendung enthält, und um die Datei an einen Speicherort Ihrer Wahl zu kopieren.  

    -   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

    Wenn Sie CAB-Dateien von mehr als einer Hierarchie gleichzeitig hochladen möchten, muss jede CAB-Datei im Ordner einen eindeutigen Namen haben. Sie können manuell Dateien umbenennen, die Sie dem Ordner hinzufügen.

    Wenn Sie die Verwendungsinformationen anzeigen möchten, die gesammelt werden, damit Sie in den Configuration Manager-Clouddienst hochgeladen werden, führen Sie den folgenden Befehl aus, um die gleichen Daten als eine CSV-Datei zu exportieren, die Sie dann mithilfe einer Anwendung wie Excel anzeigen können:  

    -   **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3.  Nachdem der Vorbereitungsschritt abgeschlossen wurde, verschieben Sie das USB-Laufwerk auf einen Computer mit Internetzugriff (bzw. übertragen die exportierten Daten auf andere Weise).  

4.  Öffnen Sie auf dem Computer mit Internetzugriff eine Eingabeaufforderung mit Administratorrechten, und wechseln Sie in das Verzeichnis, in dem eine Kopie des Tools  **serviceconnectiontool.exe** und zusätzliche Dateien aus diesem Ordner gespeichert sind.  

5.  Führen Sie den folgenden Befehl aus, um den Upload der Nutzungsinformationen und den Download der Configuration Manager-Updates zu starten:  

    -   **serviceconnectiontool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**

    Weitere Beispiele für diese Befehlszeile finden Sie im Abschnitt [Befehlszeilenoptionen](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd) später in diesem Thema.

    > [!NOTE]  
    >  Wenn Sie in der Befehlszeile einen Befehl zur Verbindung mit dem Configuration Manager-Clouddienst ausführen, kann etwa folgende Fehlermeldung angezeigt werden:  
    >   
    >  -   Ausnahmefehler: System.UnauthorizedAccessException:  
    >   
    >      Der Zugriff auf den Pfad 'C:\  
    >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' wurde verweigert.  
    >   
    > Dieser Fehler kann ignoriert werden, und Sie können das Fehlerfenster schließen und fortfahren.  

6.  Nach dem Herunterladen der Configuration Manager-Updates verschieben Sie das USB-Laufwerk auf den Computer, von dem der Dienstverbindungspunkt gehostet wird (bzw. übertragen die exportierten Daten auf andere Weise).  

7.  Öffnen Sie auf dem Computer, von dem der Dienstverbindungspunkt gehostet wird, eine Eingabeaufforderung mit Administratorrechten, und wechseln Sie in das Verzeichnis, in dem eine Kopie des Tools **serviceconnectiontool.exe**vorhanden ist. Führen Sie anschließend den folgenden Befehl aus:  

    -   **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8.  Nachdem der Import abgeschlossen wurde, können Sie die Eingabeaufforderung schließen. (Es werden nur Updates für die entsprechende Hierarchie importiert).  

9. Öffnen Sie die Configuration Manager-Konsole, und navigieren Sie zu **Verwaltung** > **Updates und Wartung** aus. Die importierten Updates stehen jetzt zur Installation bereit. (Vor Version 1702 befand sich „Updates und Wartung“ unter **Verwaltung** > **Clouddienste**.)

 Weitere Informationen zum Installieren von Updates finden Sie unter [Installieren konsoleninterner Updates für System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

## <a name="bkmk_cmd"></a> Befehlszeilenoptionen  
 Um Hilfeinformationen für das Dienstverbindungspunkt-Tool anzuzeigen, öffnen Sie die Eingabeaufforderung mit dem Ordner, in dem das Tool enthalten ist, und führen Sie den folgenden Befehl aus:  **serviceconnectiontool.exe**.  

|Befehlszeilenoptionen|Details|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [Laufwerk:][Pfad][Dateiname.cab]**|Durch diesen Befehl werden die aktuellen Nutzungsdaten in einer CAB-Datei gespeichert.<br /><br /> Führen Sie diesen Befehl als **Lokaler Administrator** auf dem Server aus, von dem der Dienstverbindungspunkt gehostet wird.<br /><br /> Beispiel:   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [Laufwerk:][Pfad] -updatepackdest [Laufwerk:][Pfad] -proxyserveruri [FQDN von Proxyserver] -proxyusername [Benutzername]** <br /> <br /> Wenn Sie eine Version von Configuration Manager vor 1606 verwenden, müssen Sie den Namen der CAB-Datei angeben, und Sie können nicht die Optionen für einen Proxyserver verwenden.  Die unterstützten Befehlsparameter sind: <br /> **-connect -usagedatasrc [Laufwerk:][Pfad][Dateiname] -updatepackdest [Laufwerk:][Pfad]** |Dieser Befehl stellt eine Verbindung zum Configuration Manager-Clouddienst her, um die CAB-Dateien mit Nutzungsdaten aus dem angegebenen Speicherort hoch- und die verfügbaren Updatepakete und Konsoleninhalt herunterzuladen. Die Optionen für die Proxyserver sind optional.<br /><br /> Führen Sie diesen Befehl als **lokaler Administrator** auf einem Computer aus, der eine Verbindung mit dem Internet herstellen kann.<br /><br /> Beispiel für das Herstellen einer Verbindung ohne Proxyserver: **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> Beispiel für das Herstellen einer Verbindung unter Verwendung eines Proxyservers: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> Wenn Sie eine frühere Version als 1606 verwenden, müssen Sie den Dateinamen der CAB-Datei angeben und können keinen Proxyserver angeben. Verwenden Sie die folgende Beispielbefehlszeile: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [Laufwerk:][Pfad]**|Dieser Befehl importiert die Updatepakete und den Konsoleninhalt, die zuvor auf die Configuration Manager-Konsole heruntergeladen wurden.<br /><br /> Führen Sie diesen Befehl als **Lokaler Administrator** auf dem Server aus, von dem der Dienstverbindungspunkt gehostet wird.<br /><br /> Beispiel:  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [Laufwerk:][Pfad][Dateiname.csv]**|Dieser Befehl exportiert die Nutzungsdaten in eine CSV-Datei, die Sie anzeigen können.<br /><br /> Führen Sie diesen Befehl als **Lokaler Administrator** auf dem Server aus, von dem der Dienstverbindungspunkt gehostet wird.<br /><br /> Beispiel: **-export -dest D:\USB\usagedata.csv**|  
