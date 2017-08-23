---
title: Erstellen einer Tasksequenz zum Installieren eines Betriebssystems | Microsoft-Dokumentation
description: Verwenden Sie Tasksequenzen in System Center Configuration Manager, um automatisch ein Betriebssystemimage und andere Inhalte auf einem Zielcomputer zu installieren.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
caps.latest.revision: "13"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 41aa6cf69a746f0ab67d804f1ee0c70db05d65ee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-to-install-an-operating-system-in-system-center-configuration-manager"></a>Erstellen einer Tasksequenz zum Installieren eines Betriebssystems in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie Tasksequenzen in System Center Configuration Manager, um automatisch ein Betriebssystemimage auf einem Zielcomputer zu installieren. Sie erstellen eine Tasksequenz , in der auf Folgendes verwiesen wird: das zum Starten des Zielcomputers verwendete Startabbild, das auf dem Zielcomputer zu installierende Betriebssystemabbild und sämtlichen zusätzlich zu installierenden Inhalt, beispielsweise andere Anwendungen oder Softwareupdates. Stellen Sie dann die Tasksequenz für die Sammlung bereit, die den Zielcomputer enthält.  

##  <a name="BKMK_InstallOS"></a> Erstellen einer Tasksequenz zum Installieren eines Betriebssystems  
 Es gibt eine Vielzahl von Szenarien zum Bereitstellen eines Betriebssystems auf Computern in Ihrer Umgebung. In den meisten Fällen erstellen Sie eine Tasksequenz und wählen **Bestehendes Abbildpaket installieren** im Tasksequenzerstellungs-Assistenten aus, um das Betriebssystem zu installieren, die Benutzereinstellungen zu migrieren, Softwareupdates anzuwenden und Anwendungen zu installieren. Bevor Sie eine Tasksequenz zum Installieren eines Betriebssystems erstellen, muss Folgendes vorhanden sein:   

-   **Erforderlich**  

    -   Das [Startimage](../get-started/manage-boot-images.md) muss in der Configuration Manager-Konsole verfügbar sein.  

    -   Ein [Betriebssystemimage](../get-started/manage-operating-system-images.md) muss in der Configuration Manager-Konsole verfügbar sein.  

-   **Erforderlich (sofern verwendet)**  

    -   [Softwareupdates](../../sum/get-started/synchronize-software-updates.md) müssen in der Configuration Manager-Konsole synchronisiert werden.  

    -   [Anwendungen](../../apps/deploy-use/create-applications.md) müssen zur Configuration Manager-Konsole hinzugefügt werden.  

#### <a name="to-create-a-task-sequence-that-installs-an-operating-system"></a>So erstellen Sie eine Tasksequenz zum Installieren eines Betriebssystems  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenz erstellen** , um den Tasksequenzerstellungs-Assistenten zu starten.  

4.  Klicken Sie auf der Seite **Neue Tasksequenz erstellen** auf **Bestehendes Abbildpaket installieren**und dann auf **Weiter**.  

5.  Geben Sie auf der Seite **Informationen zur Tasksequenz** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Tasksequenzname**: Geben Sie einen Namen zur Identifikation der Tasksequenz an.  

    -   **Beschreibung**: Geben Sie eine Beschreibung der Aufgabe an, die von der Tasksequenz ausgeführt wird.  

    -   **Startabbild**: Geben Sie das Startabbild an, von dem das Betriebssystem auf dem Zielcomputer installiert wird. Das Startabbild enthält eine Version von Windows PE, die zum Installieren des Betriebssystems sowie aller zusätzlich erforderlichen Gerätetreiber verwendet wird. Weitere Informationen finden Sie unter [Manage boot images (Verwalten von Startimages)](../get-started/manage-boot-images.md).  

        > [!IMPORTANT]  
        >  Die Architektur des Startabbilds muss kompatibel mit der Hardwarearchitektur des Zielcomputers sein.  

6.  Geben Sie auf der Seite **Windows installieren** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Abbildpaket**: Geben Sie das Paket an, welches das zu installierende Betriebssystemabbild enthält. Weitere Informationen finden Sie unter [Manage operating system images (Verwalten von Betriebssystemimages)](../get-started/manage-operating-system-images.md).  

    -   **Abbild**: Wenn das Betriebssystemabbildpaket mehrere Abbilder enthält, geben Sie den Indes des zu installierenden Betriebssystemabbilds an.  

    -   **Zielcomputer vor Installation des Betriebssystems partitionieren und formatieren**: Geben Sie an, ob der Zielcomputer vor Installation des Betriebssystems von der Tasksequenz partitioniert und formatiert werden soll.  

    -   **Product Key**: Geben Sie den Product Key für das zu installierende Windows-Betriebssystem an. Sie können codierte Volumenlizenzschlüssel und standardmäßige Product Keys angeben. Wenn Sie einen nicht codierten Product Key verwenden, muss jede Gruppe aus 5 Zeichen mit einen Bindestrich (-) getrennt werden. Beispiel: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Serverlizenzierungsmodus**: Geben Sie an, ob die Serverlizenz **Pro Arbeitsplatz**oder **Pro Server**bzw. dass keine Lizenz angegeben ist. Wenn die Serverlizenz **Pro Server**gilt, geben Sie auch die maximale Anzahl von Serververbindungen an.  

    -   Geben Sie an, wie das Administratorkonto verarbeitet werden soll, das bei der Bereitstellung des Betriebssystemabbilds verwendet wird.  

        -   **Lokales Administratorkonto deaktivieren**: Geben Sie an, ob das lokale Administratorkonto deaktiviert werden soll, wenn das Betriebssystemabbild bereitgestellt ist.  

        -   **Immer das gleiche Administratorkennwort verwenden**: Geben Sie an, ob während der Bereitstellung des Betriebssystemabbilds auf allen Computern das gleiche Kennwort für das lokale Administratorkonto verwendet werden soll.  

7.  Geben Sie auf der Seite **Netzwerkeinstellungen konfigurieren** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Einer Arbeitsgruppe beitreten**: Geben Sie an, ob der Zielcomputer einer Arbeitsgruppe hinzugefügt werden soll.  

    -   **Einer Domäne beitreten**: Geben Sie an, ob der Zielcomputer einer Domäne hinzugefügt werden soll. Geben Sie unter **Domäne**den Namen der Domäne an.  

        > [!IMPORTANT]  
        >  Domänen in der lokalen Gesamtstruktur können Sie suchen, doch bei Domänen in remoten Gesamtstrukturen müssen Sie den Domänennamen angeben.  

         Sie können auch eine Organisationseinheit angeben. Dies ist eine optionale Einstellung, mit welcher der LDAP X.500-definierte Name der Organisationseinheit angegeben wird, in der das Computerkonto erstellt werden soll, sofern das Konto noch nicht vorhanden ist.  

    -   **Konto**: Geben Sie Benutzernamen und Kennwort für das Konto an, das die Berechtigungen hat, um der angegebenen Domäne beizutreten. Beispiel: *Domäne\Benutzer* oder *%Variable%*.  

        > [!IMPORTANT]  
        >  Sie müssen die richtigen Domänenanmeldeinformationen eingeben, wenn Sie entweder die Domäneneinstellungen oder die Arbeitsgruppeneinstellungen migrieren möchten.  

8.  Geben Sie auf der Seite **Configuration Manager installieren** das Configuration Manager-Clientpaket an, das auf dem Zielcomputer installiert werden sollen, und klicken Sie auf **Weiter**.  

9. Geben Sie auf der Seite **Zustandsmigration** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   **Benutzereinstellungen erfassen**: Geben Sie an, ob der Benutzerstatus von der Tasksequenz erfasst werden soll. Weitere Informationen zum Erfassen und Wiederherstellen des Benutzerstatus finden Sie unter [Verwalten des Benutzerstatus](../get-started/manage-user-state.md).  

    -   **Netzwerkeinstellungen erfassen**: Geben Sie an, ob die Netzwerkeinstellungen des Zielcomputers von der Tasksequenz erfasst werden sollen. Sie können zusätzlich zu den Netzwerkadaptereinstellungen auch die Domänen- oder Arbeitsgruppenmitgliedschaft erfassen.  

    -   **Microsoft Windows-Einstellungen erfassen**:  Geben Sie an, ob die Windows-Einstellungen des Zielcomputers von der Tasksequenz erfasst werden sollen, bevor das Betriebssystemabbild installiert wird. Sie können den Computernamen, Namen von registrierten Benutzern und Unternehmen sowie Zeitzoneneinstellungen erfassen.  

10. Geben Sie auf der Seite **Updates einschließen** an, ob erforderliche Softwareupdates, alle Softwareupdates oder keine Softwareupdates installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie angeben, dass Softwareupdates installiert werden sollen, werden von Configuration Manager nur Softwareupdates installiert, die für Sammlungen bestimmt sind, in denen der Zielcomputer Mitglied ist.  

11. Geben Sie auf der Seite **Anwendungen installieren** die Anwendungen an, die auf dem Zielcomputer installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie mehrere Anwendungen angeben, können Sie auch angeben, dass die Tasksequenz fortgesetzt werden soll, wenn bei der Installation einer bestimmten Anwendung ein Fehler auftritt.  

12. Schließen Sie den Assistenten ab.  

 Sie können jetzt die Tasksequenz für eine Sammlung von Computern bereitstellen.  Weitere Informationen finden Sie unter [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="BKMK_InstallExistingOSImageTSExample"></a> Beispiel einer Tasksequenz zum Installieren eines vorhandenen Betriebssystemabbilds  
 Orientieren Sie sich an der folgenden Tabelle, während Sie eine Tasksequenz zur Bereitstellung eines Betriebssystems mithilfe eines vorhandenen Betriebssystemabbilds erstellen. Mithilfe dieser Tabelle können Sie die allgemeine Sequenz für Ihre Tasksequenzschritte festlegen und diese Tasksequenzschritte in logischen Gruppen organisieren. Die von Ihnen erstellte Tasksequenz kann von diesem Beispiel abweichen und eine andere Anzahl von Tasksequenzschritten und Tasksequenzgruppen enthalten.  

> [!IMPORTANT]  
>  Sie müssen diese Tasksequenz stets mithilfe des Tasksequenzerstellungs-Assistenten erstellen.  

 Wenn Sie diese neue Tasksequenz mithilfe des Tasksequenzerstellungs-Assistenten erstellen, haben einige Tasksequenzschritte andere Namen, als wenn Sie diese Tasksequenzschritte manuell zu einer vorhandenen Tasksequenz hinzufügen. In der folgenden Tabelle sind die Namensunterschiede angezeigt:  

|Name des Tasksequenzschritts im Tasksequenzerstellungs-Assistenten|Name des entsprechenden Schritts im Tasksequenz-Editor|  
|---------------------------------------------------------|-----------------------------------------------|  
|Benutzerzustandsspeicher anfordern|Zustandsspeicher anfordern|  
|Benutzerdateien und Einstellungen erfassen|Benutzerzustand erfassen|  
|Benutzerzustandsspeicher freigeben|Zustandsspeicher freigeben|  
|Neustart mit Windows PE ausführen|Neustart mit Windows PE oder Festplatte ausführen|  
|Festplatte 0 partitionieren|Datenträger formatieren und partitionieren|  
|Benuterzdateien und -einstellungen wiederherstellen|Benutzerzustand wiederherstellen|  

|Tasksequenzgruppe/-schritt|Beschreibung|  
|---------------------------------|-----------------|  
|Dateien und Einstellungen erfassen – **(Neue Tasksequenzgruppe)**|Erstellen Sie eine Tasksequenzgruppe. Mithilfe einer Tasksequenzgruppe können Sie ähnliche Tasksequenzschritte zur besseren Organisation und Fehlersteuerung gruppieren.<br /><br /> Diese Gruppe enthält die zum Erfassen von Dateien und Einstellungen vom Betriebssystem des Referenzcomputers erforderlichen Schritte.|  
|Windows-Einstellungen erfassen|Mithilfe dieses Tasksequenzschritts können Sie die Microsoft Windows-Einstellungen identifizieren, die vom Referenzcomputer erfasst werden müssen. Sie können den Computernamen, Benutzer- und Unternehmensinformationen sowie Zeitzoneneinstellungen erfassen.|  
|Netzwerkeinstellungen erfassen|Mithilfe dieses Tasksequenzschritts können Sie die Netzwerkeinstellungen vom Referenzcomputer erfassen. Sie können die Domänen- oder Arbeitsgruppenmitgliedschaft des Referenzcomputers sowie Informationen zur Netzwerkkarteneinstellung erfassen.|  
|Benutzerdateien und Einstellungen erfassen – **(Neue Tasksequenz-Untergruppe)**|Erstellen Sie eine Tasksequenzgruppe innerhalb einer anderen Tasksequenzgruppe. Diese Untergruppe enthält die zum Erfassen der Benutzerzustandsdaten erforderlichen Schritte. Ähnlich wie mithilfe der ersten von Ihnen hinzugefügten Gruppe können Sie mithilfe dieser Untergruppe ähnliche Tasksequenzschritte zur besseren Organisation und Fehlersteuerung gruppieren.|  
|Benutzerzustandsspeicher anfordern|Mithilfe dieses Tasksequenzschritts können Sie Zugriff auf einen Zustandsmigrationspunkt anfordern, auf dem die Benutzerzustandsdaten gespeichert sind. Sie können diesen Tasksequenzschritt so konfigurieren, dass die Benutzerzustandsinformationen erfasst oder wiederhergestellt werden.|  
|Benutzerdateien und Einstellungen erfassen|Mithilfe dieses Tasksequenzschritts können Sie den Benutzerzustand und die Einstellungen unter Verwendung von Windows-EasyTransfer bzw. USMT von dem Referenzcomputer erfassen, auf dem die mit diesem Taskschritt verknüpfte Tasksequenz empfangen wird. Sie können die Standardoptionen erfassen oder die zu erfassenden Optionen konfigurieren.|  
|Benutzerzustandsspeicher freigeben|Mithilfe dieses Tasksequenzschritts können Sie den Zustandsmigrationspunkt darüber benachrichtigen, dass die Erfassungs- oder Wiederherstellungsaktion abgeschlossen ist.|  
|Betriebssystem installieren – **(Neue Tasksequenzgruppe)**|Erstellen Sie eine weitere Untergruppe der Tasksequenz. Diese Untergruppe enthält die zum Installieren und Konfigurieren der Windows PE-Umgebung erforderlichen Schritte.|  
|Neustart mit Windows PE|Mithilfe dieses Tasksequenzschritts können Sie die Neustartoptionen für den Zielcomputer angeben, auf dem diese Tasksequenz empfangen wird. In diesem Schritt wird eine Meldung angezeigt, um den Benutzer darüber zu informieren, dass der Computer zum Fortsetzen der Installation neu gestartet wird.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSInWinPE** verwendet. Wenn der Variablen der Wert **false** zugeordnet ist, wird der Tasksequenzschritt fortgesetzt.|  
|Festplatte 0 partitionieren|Mithilfe dieses Tasksequenzschritts werden die zum Formatieren der Festplatte auf dem Zielcomputer erforderlichen Aktionen angegeben. Die standardmäßige Datenträgernummer ist **0**.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSClientCache** verwendet. Der Schritt wird ausgeführt, wenn kein Configuration Manager-Clientcache vorhanden ist.|  
|Betriebssystem anwenden|Mithilfe dieses tasksequenzschritts das Betriebssystemabbild auf dem Zielcomputer installieren. In diesem Schritt werden alle in der WIM-Datei enthaltenen Volumeimages auf das entsprechende sequenzielle Datenträgervolume auf dem Bereitstellungszielcomputer angewendet, nachdem zuerst alle Dateien auf diesem Volume gelöscht wurden (mit Ausnahme Configuration Manager-spezifischer Steuerdateien). Sie können eine **sysprep** -Antwortdatei angeben und auch konfigurieren, welche Festplattenpartition für die Installation verwendet wird.|  
|Windows-Einstellungen anwenden|Mithilfe dieses Tasksequenzschritts können Sie die Konfigurationsinformationen für die Windows-Einstellungen des Zielcomputers angeben. Folgende Windows-Einstellungen können anwendet werden: Benutzer- und Unternehmensinformationen, Produkt- oder Lizenzschlüsselinformationen, Zeitzone und lokales Administratorkennwort.|  
|Netzwerkeinstellungen anwenden|Mithilfe dieses Tasksequenzschritts können Sie die Konfigurationsinformationen für das Netzwerk oder die Arbeitsgruppe des Zielcomputers angeben. Sie können auch angeben, ob vom Computer ein DHCP-Server verwendet wird, oder Sie können die IP-Adressinformationen statisch zuweisen.|  
|Gerätetreiber anwenden|Mithilfe dieses Tasksequenzschritts können Sie Gerätetreiber als Teil der Betriebssystembereitstellung installieren. Sie können durch Auswahl von **Treiber aller Kategorien berücksichtigen** zulassen, dass alle vorhandenen Treiberkategorien von Windows Setup durchsucht werden, oder die von Windows Setup zu durchsuchenden Treiberkategorien durch Auswahl von **Nur Treiber in bestimmten Kategorien berücksichtigen**einschränken.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSMediaType** verwendet. Dieser Tasksequenzschritt wird nur ausgeführt, wenn der Wert der Variablen ungleich **FullMedia**ist.|  
|Treiberpaket anwenden|Mithilfe dieses Tasksequenzschritts können Sie alle Gerätetreiber in einem Treiberpaket für Windows Setup zur Verfügung stellen.|  
|Betriebssystem einrichten – **(Neue Tasksequenzgruppe)**|Erstellen Sie eine weitere Untergruppe der Tasksequenz. Diese Untergruppe enthält die zum Einrichten des installierten Betriebssystems erforderlichen Schritte.|  
|Windows und ConfigMgr einrichten|Mit diesem Tasksequenzschritt können Sie die Configuration Manager-Clientsoftware installieren. Mit dem Configuration Manager wird die GUID des Configuration Manager-Clients installiert und registriert. Sie können die erforderlichen Installationsparameter im Fenster **Installationseinstellungen** zuweisen.|  
|Updates installieren|Mithilfe dieses Tasksequenzschritts können Sie angeben, wie Softwareupdates auf dem Zielcomputer installiert werden. Der Zielcomputer wird erst beim Ausführen dieses Tasksequenzschritts hinsichtlich anwendbarer Softwareupdates ausgewertet. An diesem Punkt wird der Zielcomputer ähnlich wie jeder andere von Configuration Manager verwaltete Client hinsichtlich Softwareupdates ausgewertet.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSMediaType** verwendet. Dieser Tasksequenzschritt wird nur ausgeführt, wenn der Wert der Variablen ungleich **FullMedia**ist.|  
|Benutzerdateien und -einstellungen wiederherstellen – **(Neue Tasksequenz-Untergruppe)**|Erstellen Sie eine weitere Untergruppe der Tasksequenz. Diese Untergruppe enthält die zum Wiederherstellen der Benutzerdateien und -einstellungen erforderlichen Schritte.|  
|Benutzerzustandsspeicher anfordern|Mithilfe dieses Tasksequenzschritts können Sie Zugriff auf einen Zustandsmigrationspunkt anfordern, auf dem die Benutzerzustandsdaten gespeichert sind.|  
|Benuterzdateien und -einstellungen wiederherstellen|Mithilfe dieses Tasksequenzschritts können Sie Windows-EasyTransfer bzw. USMT initiieren, um Benutzerzustand und -einstellungen auf einem Zielcomputer wiederzuherstellen.|  
|Benutzerzustandsspeicher freigeben|Mithilfe dieses Tasksequenzschritts können Sie den Zustandsmigrationspunkt darüber benachrichtigen, dass die Benutzerzustandsdaten nicht mehr benötigt werden.|  
