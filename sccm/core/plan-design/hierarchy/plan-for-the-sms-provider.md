---
title: Planen des SMS-Anbieters | Microsoft-Dokumentation
description: Erfahren Sie, wie der SMS-Anbieter Ihnen bei der Verwaltung von System Center Configuration Manager helfen kann.
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 547dc39d5659c7c2e6f1ca670caddc127dbf22c4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-the-sms-provider-for-system-center-configuration-manager"></a>Planen des SMS-Anbieters für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie zum Verwalten von System Center Configuration Manager eine Configuration Manager-Konsole, die eine Verbindung mit einer Instanz des **SMS-Anbieters** herstellt. Standardmäßig wird ein SMS-Anbieter auf dem Standortserver installiert, wenn Sie einen Standort der zentralen Verwaltung oder einen primären Standort installieren. 


##  <a name="BKMK_PlanSMSProv"></a> Informationen zum SMS-Anbieter  
 Der SMS-Anbieter ist ein Anbieter der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation; WMI), über den der Configuration Manager-Datenbank an einem Standort **Lese-** und **Schreibzugriff** erteilt wird:  

-   Für jeden Standort der zentralen Verwaltung und für jeden primären Standort ist mindestens ein SMS-Anbieter erforderlich. Sie können bei Bedarf zusätzliche Anbieter installieren.  
-   Die Sicherheitsgruppe **SMS-Administratoren** ermöglicht den Zugriff auf den SMS-Anbieter. Configuration Manager erstellt diese Gruppe automatisch auf dem Standortserver und auf jedem Computer, auf dem Sie eine Instanz des SMS-Anbieters installieren.  

-   Der SMS-Anbieter wird von sekundären Standorten nicht unterstützt.  


Configuration Manager-Administratoren verwenden einen SMS-Anbieter für den Zugriff auf Informationen, die in der Datenbank gespeichert sind. Hierzu können Administratoren die Configuration Manager-Konsole, den Ressourcen-Explorer, Tools und benutzerdefinierte Skripts verwenden. Es gibt keine Interaktion zwischen dem SMS-Anbieter und Configuration Manager-Clients. Wenn für eine Configuration Manager-Konsole eine Verbindung zu einem Standort hergestellt wird, dann erfolgt eine Abfrage von WMI auf dem Standortserver durch die Configuration Manager-Konsole, um eine verwendbare Instanz des SMS-Anbieters zu finden.  

 Der SMS-Anbieter unterstützt die Durchsetzung der Configuration Manager-Sicherheit. Es werden nur die Informationen zurückgegeben, zu deren Anzeige der die Configuration Manager-Konsole ausführende Administrator berechtigt ist.  

> [!IMPORTANT]  
>  Wenn alle Computer mit einem SMS-Anbieter für einen Standort offline sind, kann von den Configuration Manager-Konsolen keine Verbindung zur Datenbank dieses Standorts hergestellt werden.  

 Informationen zum Verwalten des SMS-Anbieters finden Sie unter [Manage the SMS Provider](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) in [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md).  

## <a name="prerequisites-to-install-the-sms-provider"></a>Voraussetzungen für das Installieren des SMS-Anbieters  

 So unterstützen Sie den SMS-Anbieter  

-   Der Computer muss sich in einer Domäne befinden, die eine bidirektionale Vertrauensstellung mit dem Standortserver und den Standortsystemen der Standortdatenbank aufweist.  

-   Dem Computer darf keine Standortsystemrolle eines anderen Standorts zugewiesen sein.  

-   Auf dem Computer darf kein SMS-Anbieter installiert sein.  

-   Auf dem Computer muss ein Betriebssystem ausgeführt werden, das für Standortserver geeignet ist.  

-   Auf dem Computer muss zur Unterstützung der mit dem SMS-Anbieter installierten Windows ADK-Komponenten (Windows Automated Deployment Kit) mindestens 650 MB freier Festplattenspeicher verfügbar sein. Weitere Informationen zum Windows-ADK und SMS-Anbieter finden Sie unter [Anforderungen der Betriebssystembereitstellung für den SMS-Anbieter](#BKMK_WAIKforSMSProv) in diesem Thema.  

##  <a name="bkmk_location"></a> Standorte des SMS-Anbieters  
 Bei der Installation eines Standorts wird der erste SMS-Anbieter für diesen Standort automatisch installiert. Sie können für den SMS-Anbieter einen der folgenden unterstützten Speicherorte angeben:  

-   Den Standortservercomputer  

-   Den Standortdatenbankcomputer  

-   Einen Servercomputer, auf dem kein SMS-Anbieter oder keine Standortsystemrolle eines anderen Standorts vorhanden ist  


Um die Speicherorte der einzelnen SMS-Anbieter anzuzeigen, die an einem Standort installiert sind, wählen Sie im Dialogfeld mit den **Standorteigenschaften** die Registerkarte **Allgemein** aus.  

 Jeder SMS-Anbieter unterstützt gleichzeitige Verbindungen von mehreren Anforderungen. Diese Verbindungen unterliegen nur zwei Einschränkungen. Dabei handelt es sich um die Anzahl der Serververbindungen sowie um die zur Bearbeitung der Verbindungsanforderungen erforderlichen Ressourcen, die jeweils auf dem SMS-Anbietercomputer verfügbar sind.  

 Nach der Installation eines Standorts können Sie Setup erneut auf dem Standortserver ausführen, um den Speicherort eines vorhandenen SMS-Anbieters zu ändern oder weitere SMS-Anbieter an diesem Standort zu installieren. Sie können nur einen SMS-Anbieter auf einem Computer installieren. Einem Computer ist es nicht möglich, SMS-Anbieter von mehreren Standorten zu installieren.  

 Die folgende Aufstellung enthält die Vor- und Nachteile der verschiedenen unterstützten Speicherorte für den SMS-Anbieter:  

 **Configuration Manager-Standortserver**  

-   **Vorteile:**  

    -   Vom SMS-Anbieter werden keine Systemressourcen des Standortdatenbankcomputers beansprucht.  

    -   Mit diesem Speicherort für den SMS-Anbieter kann eine bessere Leistung erzielt werden als mit Speicherorten auf Computern, die keine Standortserver- oder Standortdatenbankcomputer sind.  

-   **Nachteile:**  

    -   Vom SMS-Anbieter werden System- und Netzwerkressourcen beansprucht, die anderen Standortservervorgängen zugewiesen werden könnten.  


**SQL Server, von dem die Standortdatenbank gehostet wird**  

-   **Vorteile:**  

    -   Vom SMS-Anbieter werden keine Standortsystemressourcen auf dem Standortserver beansprucht.  

    -   Mit diesem Speicherort kann die beste Leistung von allen drei Speicherorten erzielt werden, sofern genügend Serverressourcen verfügbar sind.  

-   **Nachteile:**  

    -   Vom SMS-Anbieter werden System- und Netzwerkressourcen beansprucht, die anderen Standortdatenbankvorgängen zugewiesen werden könnten.  

    -   Wenn die Standortdatenbank auf einer gruppierten SQL Server-Instanz gehostet wird, können Sie diesen Speicherort nicht verwenden.  


**Anderer Computer als der Standortserver oder Standortdatenbankcomputer**  

-   **Vorteile:**  

    -   Vom SMS-Anbieter werden keine Ressourcen des Standortservers oder Standortdatenbankcomputers beansprucht.  

    -   Bei diesem Speicherorttyp können Sie zusätzliche SMS-Anbieter bereitstellen, um für die Verbindungen eine hohe Verfügbarkeit zu erzielen.  

-   **Nachteile:**  

    -   Die Leistung des SMS-Anbieters kann durch die zusätzliche Netzwerkaktivität beeinträchtigt werden, die zur Koordinierung mit dem Standortserver und dem Standortdatenbankserver erforderlich ist.  

    -   Dieser Server muss für den Standortdatenbankcomputer und alle Computer mit installierter Configuration Manager-Konsole stets zugänglich sein.  

    -   Von diesem Speicherort werden möglicherweise Systemressourcen beansprucht, die andernfalls anderen Diensten zugewiesen würden.  

##  <a name="BKMK_SMSProvLanguages"></a> Informationen zu den Sprachen des SMS-Anbieters  
 Die vom SMS-Anbieter verwendeten Sprachen sind nicht von der Anzeigesprache des Computers, auf dem er installiert ist, abhängig.  

 Wenn ein Administrator oder Configuration Manager-Prozess Daten über den SMS-Anbieter anfordert, versucht der SMS-Anbieter, die Daten in einem Format zurückzugeben, das der Betriebssystemsprache des anfordernden Computers entspricht.

Zum Abgleich der Sprache wird eine etwas indirekte Methode verwendet. Informationen werden vom SMS-Anbieter nicht aus einer Sprache in eine andere übersetzt. In welcher Sprache die zurückgegebenen Daten in der Configuration Manager-Konsole angezeigt werden, hängt vielmehr von der Quelle des Objekts und vom Speichertyp ab.  

 Die Sprachen, in denen die in der Datenbank gespeicherten Objektdaten verfügbar sind, richten sich nach Folgendem:  

-   Objekte, die von Configuration Manager erstellt werden, werden in der Datenbank gespeichert, die mehrere Sprachen unterstützt. Das Objekt wird in den Sprachen gespeichert, die an dem Standort konfiguriert sind, an dem das Objekt mit Setup erstellt wurde. Diese Objekte werden in der Configuration Manager-Konsole in der Anzeigesprache des anfordernden Computers angezeigt, sofern diese Sprache für das Objekt verfügbar ist. Kann das Objekt nicht in der Anzeigesprache des anfordernden Computers angezeigt werden, wird es in der Standardsprache (Englisch) angezeigt.  

-   Objekte, die von einem Administrator erstellt werden, werden in der Datenbank in der Sprache gespeichert, in der das Objekt erstellt wurde. Diese Objekte werden in der Configuration Manager-Konsole in der gleichen Sprache angezeigt. Sie können nicht vom SMS-Anbieter übersetzt werden, und es sind keine weiteren Sprachoptionen für sie verfügbar.  

##  <a name="BKMK_MultiSMSProv"></a> Verwenden mehrerer SMS-Anbieter  
 Wenn Sie eine Standortinstallation abgeschlossen haben, können Sie zusätzliche SMS-Anbieter für den Standort installieren. Führen Sie zu diesem Zweck Configuration Manager-Setup auf dem Standortserver aus. Erwägen Sie, zusätzliche SMS-Anbieter zu installieren, wenn eine der folgenden Bedingungen erfüllt ist:  

-   Es ist geplant, dass viele Administratoren gleichzeitig eine Configuration Manager-Konsole ausführen und Verbindungen mit einem Standort herstellen.  

-   Sie planen, das Configuration Manager SDK oder andere Produkte zu verwenden, von denen häufig Aufrufe an den SMS-Anbieter erfolgen.  

-   Sie möchten eine hohe Verfügbarkeit des SMS-Anbieters gewährleisten.  


Wenn an einem Standort mehrere SMS-Anbieter installiert sind, erfolgt die Zuweisung jeder neuen Verbindungsanforderung zur Verwendung eines installierten SMS-Anbieters nach dem Zufallsprinzip. Es ist nicht möglich, den Speicherort eines SMS-Anbieters zur Verwendung für eine bestimmte Sitzungsverbindung anzugeben.  

> [!NOTE]  
>  Betrachten Sie die Vor- und Nachteile der einzelnen Speicherorte für SMS-Anbieter. Wägen Sie diese Betrachtungen gegen die Information ab, dass Sie nicht steuern können, welcher SMS-Anbieter für jede neue Verbindung verwendet wird.  

Wenn Sie z.B. zum ersten Mal eine Configuration Manager-Konsole mit einem Standort verbinden, fragt die Verbindung die WMI auf dem Standortserver ab, um eine von der Konsole verwendete Instanz des SMS-Anbieters zu ermitteln. Diese spezifische Instanz des SMS-Anbieters wird bis zum Ende der Configuration Manager-Konsolensitzung von der Configuration Manager-Konsole verwendet. Wenn das Ende der Sitzung auf die Nichtverfügbarkeit eines SMS-Anbietercomputers im Netzwerk zurückzuführen ist, wiederholt der Standort beim erneuten Herstellen einer Verbindung mit der Configuration Manager-Konsole einfach den Task zum Identifizieren einer Instanz des SMS-Anbieters. Es ist möglich, dass eine Zuweisung zum gleichen nicht verfügbaren SMS-Anbietercomputer erfolgt. Wenn dies der Fall ist, können Sie versuchen, die Configuration Manager-Konsole neu zu verbinden, bis ein verfügbarer SMS-Anbietercomputer zugewiesen wird.  

##  <a name="BKMK_AboutSMSAdmins"></a> Informationen zur Gruppe „SMS-Administratoren“  
 Sie verwenden die Gruppe SMS-Administratoren, um Administratoren Zugriff auf den SMS-Anbieter zu gewähren. Diese Gruppe wird bei der Standortinstallation automatisch auf dem Standortserver sowie auf jedem Computer mit installiertem SMS-Anbieter erstellt. Hier finden Sie zusätzliche Informationen zur Gruppe „SMS-Administratoren“:  

-   Wenn der Computer ein Mitgliedsserver ist, wird die Gruppe SMS-Administratoren als lokale Gruppe erstellt.  

-   Wenn der Computer ein Domänencontroller ist, wird die Gruppe SMS-Administratoren als lokale Gruppe der Domäne erstellt.  

-   Bei der Deinstallation eines SMS-Anbieters von einem Computer wird die Gruppe SMS-Administratoren nicht von dem Computer entfernt.  


Damit ein Benutzer erfolgreich eine Verbindung mit einem SMS-Anbieter herstellen kann, muss sein Benutzerkonto Mitglied in der Gruppe SMS-Administratoren sein. Administratoren, die Sie in der Configuration Manager-Konsole konfigurieren, werden automatisch der Gruppe SMS-Administratoren auf jedem Standortserver und jedem SMS-Anbietercomputer in der Hierarchie hinzugefügt. Wenn Sie einen Administrator aus der Configuration Manager-Konsole löschen, wird dieser Benutzer aus der SMS-Administratorengruppe jedes Standortservers und jedes SMS-Anbietercomputers in der Hierarchie entfernt.  

Wenn ein Benutzer erfolgreich eine Verbindung mit dem SMS-Anbieter hergestellt hat, wird von der rollenbasierten Verwaltung bestimmt, auf welche Configuration Manager-Ressourcen dieser Benutzer zugreifen und welche er verwalten kann.  

Sie können die Rechte und Berechtigungen der Gruppe SMS-Administratoren mithilfe des MMC-Snap-Ins WMI-Steuerung anzeigen und konfigurieren. Standardmäßig sind dem Konto **Jeder** die Berechtigungen **Methoden ausführen**, **Anbieterschreibzugriff**und **Konto aktivieren** erteilt. Wenn ein Benutzer eine Verbindung mit dem SMS-Anbieter herstellt, erhält er je nach den jeweiligen rollenbasierten Verwaltungssicherheitsrechten, die in der Configuration Manager-Konsole definiert sind, Zugriff auf Daten aus der Standortdatenbank. Der Gruppe „SMS-Administratoren“ werden ausdrücklich die Berechtigungen **Konto aktivieren** und **Remoteaktivierung** im Namespace **Root\SMS** erteilt.  

> [!NOTE]  
>  Administratoren, die eine Configuration Manager-Remotekonsole verwenden, benötigen DCOM-Berechtigungen für eine Remoteaktivierung auf dem Standortservercomputer und dem SMS-Anbietercomputer. Diese Rechte können zwar jedem Benutzer und jeder Gruppe erteilt werden, es wird jedoch empfohlen, dass Sie sie der Gruppe „SMS-Administratoren“ erteilen, um die Verwaltung zu vereinfachen. Weitere Informationen finden Sie im Abschnitt [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) des Themas [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) .  


##  <a name="BKMK_SMSProvNamespace"></a> Informationen zum Namespace des SMS-Anbieters  
Die Struktur des SMS-Anbieters wird vom WMI-Schema definiert. Schemanamespaces beschreiben den Speicherort von Configuration Manager-Daten innerhalb des SMS-Anbieterschemas. In der folgenden Tabelle sind einige der üblichen Namespaces, die vom SMS-Anbieter verwendet werden, aufgelistet:  

|Namespace|Beschreibung|  
|---------------|-----------------|  
|Root\SMS\site_*&lt;Standortcode\>*|Der SMS-Anbieter, der in umfangreichem Maß von der Configuration Manager-Konsole, dem Ressourcen-Explorer, den Configuration Manager-Tools und Skripts verwendet wird|  
|Root\SMS\SMS_ProviderLocation|Der Ort der SMS-Anbietercomputer für einen Standort.|  
|Root\CIMv2|Der während der Hardware- und Softwareinventur für WMI-Namespaceinformationen inventarisierte Speicherort.|  
|Root\CCM|Konfigurationsrichtlinien und Clientdaten von Configuration Manager|  
|root\CIMv2\SMS|Der Speicherort für Inventurberichterstattungsklassen, die vom Inventurclient-Agent gesammelt werden. Diese Einstellungen werden während der Computerrichtlinienbewertung von Clients kompiliert. Als Basis wird die Konfiguration der Clienteinstellungen für den Computer verwendet.|  

##  <a name="BKMK_WAIKforSMSProv"></a> Anforderungen der Betriebssystembereitstellung für den SMS-Anbieter  
Auf dem Computer, auf dem Sie eine SMS-Anbieterinstanz installieren, muss die Windows ADK-Version installiert sein, die für die von Ihnen verwendete Version von Configuration Manager erforderlich ist.  

 -   Version 1511 von Configuration Manager erfordert beispielsweise die Windows 10 RTM-Version (10.0.10240) von Windows ADK.  

 -   Weitere Informationen zu dieser Anforderung finden Sie unter [Anforderungen an die Infrastruktur für die Betriebssystembereitstellung](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

Beim Verwalten von Betriebssystembereitstellungen kann der SMS-Anbieter mithilfe des Windows ADK verschiedene Aufgaben erfüllen. Beispiel:  

-   Anzeigen von WIM-Dateidetails.  

-   Hinzufügen von Treiberdateien zu vorhandenen Startabbildern.  

-   Erstellen von ISO-Startdateien.  


Von der Windows ADK-Installation können auf jedem Computer, auf dem der SMS-Anbieter installiert wird, bis zu 650 MB Speicherplatz beansprucht werden. Der hohe Speicherplatzbedarf von Configuration Manager ist erforderlich, um Startimages von Windows PE zu installieren.  
