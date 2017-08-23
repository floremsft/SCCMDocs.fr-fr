---
title: Installieren der Konsole | Microsoft-Dokumentation
description: "Erfahren Sie mehr über das Installieren der Configuration Manager-Konsole, um eine Verbindung zu einem Standort der zentralen Verwaltung oder einem primären Standort herzustellen."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 88ecbc48fd03ce988f04408d0378844cbed1de2b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="install-the-system-center-configuration-manager-console"></a>Installieren der System Center Configuration Manager-Konsole

*Gilt für: System Center Configuration Manager (Current Branch)*

Administratoren verwenden die System Center Configuration Manager-Konsole zum Verwalten der Configuration Manager-Umgebung. Jede Configuration Manager-Konsole kann eine Verbindung zu einem Standort der zentralen Verwaltung oder zu einem primären Standort herstellen. Sie können eine Configuration Manager-Konsole jedoch nicht mit einem sekundären Standort verbinden.

> [!NOTE]  
>  Welche Objekte ein Administrator sieht, der die Konsole ausführt, hängt von den Berechtigungen ab, die seinem Benutzerkonto zugeordnet sind. Weitere Informationen zur rollenbasierten Verwaltung finden Sie unter [Grundlagen der rollenbasierten Verwaltung für System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Sie können die Configuration Manager-Konsole während der Installation des Standortservers mit dem Setup-Assistenten installieren, oder Sie können eine eigenständige Installationsanwendung ausführen, die den Setup-Assistenten verwendet.  

 Gehen Sie wie folgt vor, um eine Configuration Manager-Konsole mithilfe der eigenständigen Anwendung zu installieren.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>So installieren Sie die Configuration Manager-Konsole mithilfe des Setup-Assistenten  

1.  Stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:  

    -  Sie haben **lokale Administratorrechte** auf dem Computer, auf dem die Konsole ausgeführt wird.  

    -   Sie haben eine **Leseberechtigung** für den Speicherort der Installationsdateien der Configuration Manager-Konsole.  

2.  Wechseln Sie zu einem der folgenden Speicherorte:  

    -   Navigieren Sie auf dem Standortserver zu **<*Installationspfad des Configuration Manager-Standortservers*>\Tools\ConsoleSetup**.  

    -   Navigieren Sie auf dem Configuration Manager-Quellmedium zu **<*Configuration Manager-Quelldateien*>\Smssetup\Bin\I386**.  

    > [!TIP]  
    >  Es wird empfohlen, die Installation der Configuration Manager-Konsole statt über das Installationsmedium für System Center Configuration Manager über einen Standortserver zu initiieren. Bei der Installationsmethode über den Standortserver werden die Configuration Manager-Konsoleninstallationsdateien sowie die unterstützten Language Packs für den Standort in den Unterordner **Tools\ConsoleSetup** kopiert. Bei der Installation der Configuration Manager-Konsole über das Installationsmedium wird stets die englische Version installiert, unabhängig von den unterstützten Sprachen auf dem Standortserver oder den Spracheinstellungen für das Betriebssystem auf dem Computer. Optional können Sie den Ordner **ConsoleSetup** an einen anderen Speicherort kopieren, um mit der Installation zu beginnen.

3.  Um den Setup-Assistenten für die Configuration Manager-Konsole zu öffnen, doppelklicken Sie auf **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Installieren Sie die Configuration Manager-Konsole immer mithilfe der Datei „consolesetup.exe“. Die Configuration Manager-Konsole kann zwar durch Ausführen von „adminconsole.msi“ installiert werden, bei dieser Methode werden allerdings keine Voraussetzungs- oder Abhängigkeitsprüfungen vorgenommen, sodass die Installation u.U. nicht ordnungsgemäß verläuft.  

4.  Wählen Sie im Assistenten **Weiter** aus.  

5.  Geben Sie auf der Seite **Standortserver** den vollqualifizierten Domänennamen (FQDN) des Standortservers an, mit dem sich die Configuration Manager-Konsole verbindet.  

6.  Geben Sie auf der Seite **Installationsordner** den Installationsordner für die Configuration Manager-Konsole ein. Der Ordnerpfad darf nicht auf Leerzeichen enden und darf keine Unicode-Zeichen enthalten.  

7.  Wählen Sie auf der Seite **Programm zur Verbesserung der Benutzerfreundlichkeit** (CEIP) aus, ob Sie an diesem Programm teilnehmen möchten.  

8.  Wählen Sie auf der Seite **Installationsbereit** die Option **Installieren** aus, um die Configuration Manager-Konsole zu installieren.  

## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>So installieren Sie die Configuration Manager-Konsole mithilfe einer Eingabeaufforderung  

1.  Öffnen Sie auf dem Server, von dem aus Sie die Configuration Manager-Konsole installieren möchten, ein Eingabeaufforderungsfenster, und navigieren Sie zu einem der folgenden Speicherorte:  

    -   **<*Installationspfad des Configuration Manager-Standortservers*>\Tools\ConsoleSetup**  

    -   **<*Configuration Manager-Installationsmedium*>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  Wenn Sie eine Configuration Manager-Konsole über eine Eingabeaufforderung installieren, wird stets die englische Version installiert, unabhängig von den Spracheinstellungen für das auf dem Computer ausgeführte Betriebssystem. Um die Configuration Manager-Konsole in einer anderen Sprache als Englisch zu installieren, müssen Sie die [Configuration Manager-Konsole mithilfe des Setup-Assistenten installieren](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  Geben Sie an der Eingabeaufforderung den Befehl **consolesetup.exe** ein. Wählen Sie aus den folgenden Befehlszeilenoptionen aus:  

|  .     | Beschreibung     |
  | :------------- | :------------- |
  |/q|Installiert die Configuration Manager-Konsole unbeaufsichtigt Wenn Sie diese Option verwenden, sind die Optionen **EnableSQM**, **TargetDir**und **DefaultSiteServerName** erforderlich.|  
  |/uninstall|Deinstalliert die Configuration Manager-Konsole Sie müssen diese Option zuerst angeben, wenn Sie sie mit der Option **/q** verwenden.|  
  |LangPackDir|Gibt den Pfad zu dem Ordner an, der die Sprachdateien enthält. Sie können die Sprachdateien mit dem **Setup-Downloadprogramm** herunterladen. Wenn Sie diese Option nicht verwenden, wird von Setup im aktuellen Ordner nach dem Sprachordner gesucht. Wenn der Sprachordner nicht gefunden wird, wird nur die Sprache Englisch installiert. Weitere Informationen finden Sie unter [Setup-Downloadprogramm](setup-downloader.md).|  
  |TargetDir|Gibt den Installationsordner zur Installation der Configuration Manager-Konsole an. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.|  
  |EnableSQM|Hiermit wird angegeben, ob Sie am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP) teilnehmen möchten. Verwenden Sie den Wert **1**, um die CEIP-Funktion zu verknüpfen, und den Wert **0**, um nicht am Programm teilzunehmen. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.|  
  |DefaultSiteServerName|Damit wird der FQDN des Standortservers angegeben, mit dem beim Start der Konsole eine Verbindung hergestellt wird. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.|  


  **Beispiele:**

  -  **consolesetup.exe /q TargetDir="D:\Programme\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Programme\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  
