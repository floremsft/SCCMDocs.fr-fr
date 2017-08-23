---
title: "Ausführen eines Upgrades von Windows-Geräten auf eine andere Version mit Configuration Manager | Microsoft-Dokumentation"
description: "Automatisches Upgrade von Geräten, die Windows 10 Desktop, Windows 10 Mobile, oder Windows 10 Holographic ausführen, auf eine andere Edition mit Configuration Manager."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: cd8c644d07dab0010dc211df8ce4f2dc6e1fa7ae
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Aktualisieren von Windows-Geräten mit der Editionsaktualisierungsrichtlinie in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Mit der **Upgraderichtlinie für die Edition** von System Center Configuration Manager können Sie für Geräte, auf denen eine der folgenden Windows 10-Versionen ausgeführt wird, automatisch ein Upgrade auf eine andere Version durchführen:

- Windows 10 Desktop
- Windows 10 Mobile
<!-- - Windows 10 Holographic -->

Die folgenden Upgradepfade werden unterstützt:

- Von Windows 10 Pro auf Windows 10 Enterprise
- Von Windows 10 Home auf Windows 10 Education
- Von Windows 10 Mobile auf Windows 10 Mobile Enterprise
<!-- - From Windows 10 Holographic Pro to Windows 10 Holographic Enterprise -->

Die Geräte müssen bei Microsoft Intune registriert sein oder die Configuration Manager-Clientsoftware ausführen. Diese Richtlinie ist derzeit nicht mit PCs konform, die von einer lokalen MDM verwaltet werden.

## <a name="before-you-start"></a>Vorbereitung  
 Bevor Sie beginnen, Geräte auf die neueste Version zu aktualisieren, benötigen Sie eines der folgenden Dinge:  

-   Einen gültigen Product Key für die Installation der neuen Version von Windows auf allen Geräten, die das Ziel dieser Richtlinie sind (für Desktopbetriebssysteme)  

-   Eine Lizenzdatei von Microsoft, die die Lizenzierungsinformationen zum Installieren der neuen Version von Windows auf allen Geräten enthält, die das Ziel dieser Richtlinie sind (für Windows 10 Mobile<!-- and Windows 10 Holographic-->).

- Zum Erstellen und Bereitstellen dieses Richtlinientyps muss Ihnen die Configuration Manager-Sicherheitsrolle **Hauptadministrator** zugewiesen sein.

## <a name="configure-the-edition-upgrade-policy"></a>Konfigurieren der Editionsaktualisierungsrichtlinie  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Windows 10-Editionsupgrade**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Editionsaktualisierungsrichtlinie erstellen**.  

4.  Klicken Sie auf **Richtlinie erstellen**.  

5.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Editionsaktualisierungsrichtlinien**die folgenden Informationen an:  

    -   **Name** : Geben Sie einen Namen für die Editionsaktualisierungsrichtlinie ein.  

    -   **Beschreibung** (optional): Geben Sie optional eine Beschreibung für die Richtlinie ein, damit Sie sie in der Intune-Konsole besser identifizieren können.  

    -   **SKU, auf die das Gerät aktualisiert werden soll**: Wählen Sie aus der Dropdownliste die Version von Windows 10 Desktop<!-- Windows 10 Holographic,--> oder Windows 10 Mobile aus, auf die die als Ziel angegebenen Geräte aktualisiert werden sollen.  

    -   **Lizenzinformationen** : Wählen Sie eine Option aus:  

        -   **Product Key** : Geben Sie einen gültigen Windows 10-Product Key ein, der zum Aktualisieren der als Ziel angegebenen Geräte mit Windows 10 Desktop-Betriebssystemen verwendet werden soll.  

            > [!NOTE]  
            >  Nach der Erstellung einer Richtlinie mit einem Product Key können Sie den Product Key später nicht mehr bearbeiten. Grund hierfür ist, dass der Schlüssel aus Sicherheitsgründen verborgen wird. Um den Product Key zu ändern, müssen Sie den gesamten Schlüssel erneut eingeben.  

        -   **Lizenzdatei**: Klicken Sie auf **Durchsuchen**, um eine gültige Lizenzdatei im XML-Format auszuwählen, mit der die als Ziel angegebenen Geräte mit <!--Windows 10 Holographic and -->Windows 10 Mobile-Betriebssystemen aktualisiert werden sollen.  

6.  Schließen Sie den Assistenten ab.  

Die neue Richtlinie wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Windows 10-Editionsaktualisierung** angezeigt.  

## <a name="deploy-the-edition-upgrade-policy"></a>Bereitstellen der Editionsaktualisierungsrichtlinie  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Windows 10-Editionsupgrade**.  

3.  Wählen Sie die Windows 10-Editionsaktualisierungsrichtlinie aus, die Sie bereitstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

4.  Wählen Sie im Dialogfeld **Deploy Windows 10 Edition Upgrade** (Windows 10-Editionsaktualisierung bereitstellen) die Sammlung aus, für die Sie die Richtlinie bereitstellen möchten. Wählen Sie ferner den Zeitplan aus, nach dem die Richtlinie ausgewertet werden soll. Klicken Sie anschließend auf **OK**. Für PCs, die mit dem Configuration Manager-Client verwaltet werden, müssen Sie die Richtlinie auf einer Gerätesammlung bereitstellen. Für PCs, die bei Intune registriert sind, können Sie die Richtlinie für eine Benutzer- oder Gerätesammlung bereitstellen. 



## <a name="next-steps"></a>Nächste Schritte

Wenn Sie die Bereitstellung überwachen, die Sie im Arbeitsbereich **Überwachung** über den Knoten **Bereitstellungen** erstellt haben, werden Ihnen unter Umständen folgende Fehler angezeigt, die darauf hindeuten, dass die Bereitstellung nicht erfolgreich war:
- **Für dieses Gerät nicht anwendbar**
- **Fehler bei der Konvertierung des Datentyps**

Diese Fehler bedeuten allerdings nicht, dass die Bereitstellung gescheitert ist. Vergewissern Sie sich am Ziel-PC, dass das Upgrade erfolgreich durchgeführt wurde.

Sobald die Richtlinie einen entsprechenden Windows-PC erreicht und ausgewertet wird, wird dieser innerhalb von zwei Stunden zum Installieren der Aktualisierung neu gestartet. Stellen Sie sicher, dass Sie jeden Benutzer informieren, dem Sie die Richtlinie bereitstellen, oder planen Sie die Ausführung der Richtlinie außerhalb der Arbeitsstunden der Benutzer.
