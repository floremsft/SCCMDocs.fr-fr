---
title: Tool zur Updateregistrierung | Microsoft-Dokumentation
description: Erfahren Sie, wann und wie das Tool zur Updateregistrierung zum manuellen Importieren eines Updates in Configuration Manager verwendet wird.
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 35a4c201f73469fdfaa5bb8629e91886f7ae8751
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-system-center-configuration-manager"></a>Verwenden des Tools zur Updateregistrierung, um Hotfixes in System Center Configuration Manager zu importieren

*Gilt für: System Center Configuration Manager (Current Branch)*

Einige Updates für Configuration Manager sind nicht beim Microsoft-Clouddienst, sondern nur über den Out-of-Band-Zugriff verfügbar. Ein Beispiel ist ein Hotfix, dass mit Einschränkungen herausgegeben wird, um ein bestimmtes Problem zu beheben.   
Wenn Sie ein Out-of-Band-Release installieren müssen, und der Update- oder Hotfixdateiname mit der Erweiterung **update.exe** endet, verwenden Sie das **Tool zur Updateregistrierung**, um das Update manuell in die Configuration Manager-Konsole zu importieren. Mit dem Tool können Sie das Updatepaket extrahieren, auf den Standortserver übertragen und das Update mit der Configuration Manager-Konsole registrieren.  

 Wenn die Hotfixdatei über die Dateierweiterung **.exe** (nicht **update.exe**) verfügt, lesen Sie [Verwenden des Hotfixinstallationsprogramms zum Installieren von Updates für System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  Dieses Thema enthält allgemeine Informationen zum Installieren von Hotfixes, die System Center Configuration Manager aktualisieren. Einzelheiten zu einem bestimmten Hotfix oder Update finden Sie im entsprechenden Knowledge Base-Artikel (KB) auf der Microsoft Support-Website.  

 **Voraussetzungen für die Verwendung des Tools zur Updateregistrierung:**  

-   Nur Out-of-Band-Updates, die mit der Erweiterung **.update.exe** enden, können mit diesem Tool installiert werden  

-   Das Tool ist eigenständig mit den einzelnen Updates, die Sie direkt von Microsoft erhalten  

-   Das Tool ist nicht vom Modus des Dienstverbindungspunkts abhängig  

-   Das Tool muss auf dem Computer ausgeführt werden, der den Dienstverbindungspunkt hostet  

-   Auf dem Computer, auf dem das Tool ausgeführt wird (der Dienstverbindungspunkt-Computer), muss .NET Framework-4.52 installiert sein  

-   Das Konto, das Sie zum Ausführen des Tools verwenden, muss über **lokale Administratorrechte** auf dem Computer verfügen, auf dem der Dienstverbindungspunkt (auf dem das Tool ausgeführt wird) gehostet ist  

-   Das Konto, das Sie verwenden, um das Tool auszuführen, benötigt auf dem Computer, der den Dienstverbindungspunkt hostet, in folgendem Ordner die Berechtigung **Schreiben**: **&lt;ConfigMgr Installationsverzeichnis\>\EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>So verwenden Sie das Tool zur Updateregistrierung  

1.  Schritte auf dem Computer, von dem der Dienstverbindungspunkt gehostet wird.  

    -   Öffnen Sie eine Eingabeaufforderung mit Administratorrechten, und wechseln Sie dann in das Verzeichnis mit der Datei **&lt;Produkt\>-&lt;Produktversion\>-&lt;KB-Artikel-ID\>-ConfigMgr.Update.exe**  

2.  Führen Sie den folgenden Befehl aus, um das Tool zur Updateregistrierung zu starten:  

    -   **&lt;Produkt\>-&lt;Produktversion\>-&lt;KB-Artikel-ID\>-ConfigMgr.Update.exe**  

    Nachdem das Hotfix registriert wurde, wird es innerhalb von 24 Stunden als neues Update in der Konsole angezeigt.  Sie können den Vorgang beschleunigen:

    - Öffnen Sie in der Configuration Manager-Konsole **Verwaltung** > **Updates und Wartung**, und klicken Sie anschließend auf **Auf Updates prüfen**. (Vor Version 1702 befand sich „Updates und Wartung“ unter **Verwaltung** > **Clouddienste**.) 

    Das Tool zur Updateregistrierung protokolliert seine Aktionen in einer LOG-Datei auf dem lokalen Computer. Die Protokolldatei trägt den gleichen Namen wie die Datei „hotfix.exe“ und wird im Ordner **%SystemRoot%Temp** abgelegt.  

     Nach Registrierung des Updates können Sie das Update-Registrierungstool schließen.  

3.  Öffnen Sie die Configuration Manager-Konsole, und navigieren Sie zu **Verwaltung** > **Updates und Wartung**. Die importierten Hotfixes stehen jetzt zur Installation bereit. (Vor Version 1702 befand sich „Updates und Wartung“ unter **Verwaltung** > **Clouddienste**.)

 Weitere Informationen zum Installieren von Updates finden Sie unter [Installieren konsoleninterner Updates für System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  
