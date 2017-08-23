---
title: "Funktionen in Technical Preview 1611 für Configuration Manager"
description: "Erfahren Sie mehr über Funktionen, die in System Center Configuration Manager Technical Preview 1611 zur Verfügung stehen."
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
caps.latest.revision: "2"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 5e77ebbfd3f3d573d903fe58024a22feb9884e4a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1611-for-system-center-configuration-manager"></a>Funktionen in Technical Preview 1611 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*



In diesem Artikel werden die Funktionen beschrieben, die in der Technical Preview 1611 für System Center Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen, und zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    

**Bekannte Probleme in dieser Technical Preview:**   
- ***Voraussetzungsstatus***: Bei der Installation von Version 1611 wird möglicherweise für den Gesamtstatus der Voraussetzungen „mit Warnungen bestanden“ angezeigt, allerdings wird nicht angegeben, welche Voraussetzungen die Warnungen verursacht haben. Diese Warnung kann durch die beiden folgenden Voraussetzungen verursacht werden:
  - Optionen für „SQL-Speicher für Indexerstellung“
  - Überprüfungen auf unterstützte SQL Server-Version  

 Da es sich nur um Warnungen handelt, können sie ignoriert werden.

- ***PowerShell***: Wenn Sie über die Configuration Manager-Konsole eine Verbindung zu Windows PowerShell herstellen, wird möglicherweise folgende Fehlermeldung angezeigt: **Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml ist nicht digital signiert**.  

   Sie können dieses Problem beheben, indem Sie bestimmte Dateien durch signierte Versionen aus Version 1610 ersetzen. Kopieren Sie alle Dateien mit den folgenden Erweiterungen in Ihrem Ordner **&lt;Installationsverzeichnis>\AdminConsole\bin\** Ihrer Installation von Version 1610: **.psd1**, **.ps1xml** und **.psm1**. Fügen Sie diese Dateien im Ordner *&lt;Installationsverzeichnis>\AdminConsole\bin\** Ihrer Installation der Technical Preview 1611 ein, und überschreiben Sie so die Version 1611 der betreffenden Dateien.


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Zwischenspeichern von Inhalt für verfügbare Bereitstellungen und Tasksequenzen
In diesem Technical Preview können Sie für verfügbare Bereitstellungen und Tasksequenzen die Zwischenspeicherungsfunktion verwenden, damit Clients nur relevante Inhalte herunterladen, bevor ein Benutzer den Inhalt installiert.

Ein Beispiel: Es soll eine Tasksequenz für ein direktes Upgrade von Windows 10 bereitgestellt werden, es soll nur eine einzige Tasksequenz für alle Benutzer verwendet werden und es sollen mehrere Architekturen und/oder Sprachen verfügbar sein. Wenn Sie in Current Branch eine verfügbare Bereitstellung erstellen und der Benutzer anschließend im Software Center auf **Installieren** klickt, wird der Inhalt zu diesem Zeitpunkt heruntergeladen. Dadurch verzögert sich der Installationsstart. Wenn Sie alternativ in Current Branch eine verfügbare Tasksequenzbereitstellung erstellen, wird der gesamte in der Tasksequenz referenzierte Inhalt heruntergeladen. Dies schließt das Betriebssystem-Aktualisierungspaket für alle Sprachen und Architekturen mit ein. Wenn jede Sprache/Architektur ungefähr 3 GB groß ist, kann das Downloadpaket sehr groß sein.

Mit der Funktion zum Zwischenspeichern von Inhalten können Sie den Client dahingehend einschränken, dass er nur zutreffenden Inhalt herunterladen darf, wenn er die Bereitstellung empfängt. Wenn der Benutzer dann im Softwarecenter auf **Installieren** klickt, steht der Inhalt bereit, und die Installation startet sofort, da der Inhalt bereits auf der lokalen Festplatte gespeichert ist.

### <a name="to-configure-the-pre-cache-feature"></a>So konfigurieren Sie die Zwischenspeicherungsfunktion

1. Erstellen Sie Betriebssystem-Aktualisierungspakete für bestimmte Architekturen und Sprachen. Geben Sie die Architektur und die Sprache auf der Registerkarte **Datenquelle** des Pakets an. Verwenden Sie für die Sprache die Dezimalkonvertierung (1033 ist beispielsweise der Dezimalwert für Englisch, 0x0409 seine hexadezimale Entsprechung). Weitere Informationen finden Sie unter [Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Die Architektur- und Sprachwerte werden verwendet, um Tasksequenz-Schrittbedingungen abzugleichen, die Sie im nächsten Schritt erstellen, um festzulegen, ob das Betriebssystem-Aktualisierungspaket zwischengespeichert werden soll.
2. Erstellen Sie eine Tasksequenz mit bedingten Schritten für die verschiedenen Sprachen und Architekturen. Für die englische Version könnten Sie z.B. wie folgt einen Schritt erstellen:

    ![Zwischenspeicherungseigenschaften](media/precacheproperties2.png)

    ![Zwischenspeicherungsoptionen](media/precacheoptions2.png)  

3. Bereitstellen der Tasksequenz Konfigurieren Sie für die Zwischenspeicherungsfunktion Folgendes:
    - Wählen Sie auf der Registerkarte **Allgemein** die Option **Inhalt für diese Tasksequenz vorab herunterladen** aus.
    - Konfigurieren Sie auf der Registerkarte **Bereitstellungseinstellungen** die Tasksequenz mit der Einstellung **Verfügbar** für **Zweck**. Bei der Erstellung einer Bereitstellung des Typs **Erforderlich** ist die Zwischenspeicherfunktion nicht verfügbar.
    - Wählen Sie auf der Registerkarte **Planung** für die Einstellung **Verfügbarkeitsdatum der Bereitstellung festlegen** einen in der Zukunft liegenden Zeitpunkt aus, der Clients genügend Zeit bietet, um den Inhalt zwischenzuspeichern, bevor die Bereitstellung für Benutzer verfügbar gemacht wird. Sie können den Verfügbarkeitszeitpunkt beispielsweise auf drei Stunden später setzen, um ausreichend Zeit für das Zwischenspeichern des Inhalts vorzusehen.  
    - Konfigurieren Sie auf der Registerkarte **Verteilungspunkte** die Einstellungen der **Bereitstellungsoptionen**. Wenn der Inhalt noch nicht auf einem Client zwischengespeichert ist, wenn ein Benutzer die Installation startet, werden diese Einstellungen verwendet.


### <a name="user-experience"></a>Benutzerfreundlichkeit
- Wenn der Client die Bereitstellungsrichtlinie erhält, startet er mit der Zwischenspeicherung des Inhalts. Dies umfasst alle referenzierten Inhalte (alle anderen Pakettypen) und nur das Betriebssystem-Aktualisierungspaket, das dem Client entspricht, und zwar basierend auf den von Ihnen in der Tasksequenz festgelegten Bedingungen.
- Wenn die Bereitstellung Benutzern verfügbar gemacht wird (Einstellung auf der Registerkarte **Planung** der Bereitstellung), wird eine Benachrichtigung angezeigt, um Benutzer über die neue Bereitstellung zu informieren. Die Bereitstellung wird dann ferner im Softwarecenter angezeigt. Der Benutzer kann zum Softwarecenter navigieren und auf **Installieren** klicken, um die Installation zu starten.
- Wenn der Inhalt nicht vollständig zwischengespeichert ist, werden die Einstellungen verwendet, die auf der Registerkarte **Bereitstellungsoptionen** der Bereitstellung angegeben wurden. Es wird empfohlen, genügend Zeit zwischen der Erstellung der Bereitstellung und dem Zeitpunkt der Verfügbarmachung der Bereitstellung für Benutzer vorzusehen, damit Clients ausreichend Zeit haben, um den Inhalt zwischenzuspeichern.


## <a name="see-also"></a>Siehe auch
[Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md)
