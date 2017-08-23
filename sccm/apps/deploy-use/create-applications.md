---
title: Erstellen von Anwendungen | Microsoft-Dokumentation
description: Erstellen Sie mit System Center Configuration Manager eine Anwendung und Bereitstellungstypen und stellen Sie diese bereit.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 4d048d4f9ab01b28e6c21a38cca4d82c85030618
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-applications-with-system-center-configuration-manager"></a>Erstellen von Anwendungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Eine System Center Configuration Manager-Anwendung verfügt über die Dateien und Informationen, die zur Bereitstellung von Software auf einem Gerät erforderlich sind. In einer Anwendung ist mindestens ein Bereitstellungstyp enthalten, der die Installationsdateien und Informationen enthält, die zur Installation der Software erforderlich sind. Bereitstellungstypen verfügen auch über Regeln, aus denen hervorgeht, wann und wie die Software bereitgestellt wird.  

 Es gibt die folgenden Möglichkeiten zum Erstellen von Anwendungen:  

-   Erstellen Sie die Anwendungen und Bereitstellungstypen durch Lesen der Installationsdateien der Anwendung automatisch.  

-   Erstellen Sie die Anwendung manuell, und fügen Sie Bereitstellungstypen später hinzu.  

-   Importieren Sie eine Anwendung aus einer Datei.  

> [!NOTE]  
>  Unter [Create applications for mobile devices (Erstellen von Anwendungen für mobile Geräte)](../../mdm/deploy-use/create-applications.md) erhalten Sie ausführliche Informationen zum Erstellen von Anwendungen für iOS, Windows Phone und Android.  

Führen Sie die folgenden Schritte aus, um mithilfe von Configuration Manager Anwendungen und Bereitstellungstypen zu erstellen.  

## <a name="start-the-create-application-wizard"></a>Starten des Assistenten zum Erstellen von Anwendungen  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Anwendung erstellen** aus.  

## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>Geben Sie an, ob die Anwendungsinformationen automatisch erkannt oder manuell definiert werden sollen.  

-   Sie können Anwendungsinformationen automatisch erkennen, wenn Sie eine einfache Anwendung mit einem einzelnen Bereitstellungstyp erstellen möchten, z.B. eine Windows Installer-Datei, die über keine Abhängigkeiten oder Anforderungen verfügt. Wenn Sie mithilfe dieses Verfahrens eine Anwendung erstellt haben, können Sie diese nach Bedarf bearbeiten, um Bereitstellungstypen hinzuzufügen oder zu ändern und um Erkennungsmethoden, Abhängigkeiten oder Anforderungen hinzuzufügen.  

-   Geben Sie Anwendungsinformationen manuell an, um komplexere Anwendungen mit mehreren Bereitstellungstypen, Abhängigkeiten, Erkennungsmethoden oder Anforderungen zu erstellen.  

### <a name="automatically-detect-application-information"></a>Automatische Erkennung von Anwendungsinformationen  

1.  Wählen Sie auf der Registerkarte **Allgemein** des Assistenten zum Erstellen von Anwendungen die Option **Informationen zu dieser Anwendung automatisch anhand der Installationsdateien erkennen**aus.  

2.  Wählen Sie in der Dropdownliste **Typ** den Installationsdateityp der Anwendung aus, den Sie für die automatische Erkennung verwenden möchten. Informationen zu den verfügbaren Installationstypen finden Sie unter [Von Configuration Manager unterstützte Bereitstellungstypen](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) in diesem Thema.  

3.  Geben Sie im Feld **Speicherort** den UNC-Pfad im Format *\\\\server\\freigabe\\\dateiname* oder den Store-Link zur Anwendungsinstallationsdatei an, die Sie zur Erkennung von Anwendungsinformationen verwenden möchten. Alternativ dazu können Sie auf **Durchsuchen** klicken, um zur Installationsdatei zu navigieren.  

    > [!IMPORTANT]  
    >  Wenn Sie als Anwendungstyp **Windows Installer (\*msi-Datei)** auswählen, werden alle Dateien im angegebenen Ordner mit der Anwendung importiert und an Verteilungspunkte gesendet. Vergewissern Sie sich, dass der angegebene Ordner ausschließlich Dateien enthält, die zur Installation der Anwendung erforderlich sind. Configuration Manager wird getestet, um bis zu 20.000 Anwendungsdateien im Anwendungspaket zu unterstützen. Wenn Ihre Anwendung mehr Dateien enthält, sollten Sie mehrere Anwendungen mit jeweils geringerer Anzahl Dateien erstellen.  

    >  Sie benötigen Zugriff auf den UNC-Pfad mit der Anwendung sowie auf alle Unterordner, die Anwendungsinhalt enthalten.  

4.  Überprüfen Sie die importierten Informationen auf der Seite **Informationen importieren** des Assistenten zum Erstellen von Anwendungen, und wählen Sie anschließend **Weiter** aus. Bei Bedarf können Sie **Zurück** auswählen, um Fehler zu korrigieren.  

5.  Geben Sie auf der Seite **Allgemeine Informationen** des Assistenten zum Erstellen von Anwendungen die folgenden Informationen an:  

    > [!NOTE]  
    >  Einige Informationen sind möglicherweise schon vorhanden, wenn sie aus den Anwendungsinstallationsdateien abgerufen wurden. Zudem werden je nach erstelltem Anwendungstyp möglicherweise unterschiedliche Optionen angezeigt.  

    -   Allgemeine Informationen zur Anwendung wie der Anwendungsname, Kommentare, die Version und eine optionale Referenz für die Suche nach der Anwendung in der Configuration Manager-Konsole.  

    -   **Installationsprogramm**: Geben Sie das Installationsprogramm und alle zur Installation des Anwendungsbereitstellungstyps erforderlichen Eigenschaften an.  

        > [!TIP]  
        >  Wenn das Installationsprogramm nicht angezeigt wird, wählen Sie **Durchsuchen** aus, um auf den Speicherort des Installationsprogramms zuzugreifen.  

    -   **Installationsverhalten**: Geben Sie an, ob der Anwendungsbereitstellungstyp nur für den aktuell angemeldeten Benutzer oder für alle Benutzer installiert werden soll. Sie können auch angeben, dass der Bereitstellungstyp für alle Benutzer installiert werden soll, wenn er für ein Gerät bereitgestellt wird, oder für einen bestimmten Benutzer, wenn er für einen Benutzer bereitgestellt wird.  

    -   **Use an automatic VPN connection (if configured)**: (Automatische VPN-Verbindung verwenden (sofern konfiguriert))Wenn ein VPN-Profil auf dem Gerät bereitgestellt wurde, auf dem die App gestartet wird, starten Sie die VPN-Verbindung beim Starten der App (nur Windows 8.1 und Windows Phone 8.1).  

         Auf Geräten mit Windows Phone 8.1 werden automatische VPN-Verbindungen nicht unterstützt, wenn mehrere VPN-Profile auf dem Gerät bereitgestellt wurden.  

         Weitere Informationen zu VPN-Profilen finden Sie unter [VPN-Profile](../../protect/deploy-use/vpn-profiles.md).  

6.  Wählen Sie **Weiter** aus, überprüfen Sie die Anwendungsinformationen auf der Seite **Zusammenfassung**, und schließen Sie den Assistenten zum Erstellen von Anwendungen ab.  

Die neue Anwendung wird im Knoten **Anwendungen** der Configuration Manager-Konsole angezeigt. Sie haben den Erstellungsvorgang einer Anwendung abgeschlossen. Wenn Sie der Anwendung weitere Bereitstellungstypen hinzufügen möchten, finden Sie weitere Informationen unter [Bereitstellungstypen für die Anwendung erstellen](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) in diesem Thema.  

### <a name="manually-specify-application-information"></a>Manuelles Angeben von Anwendungsinformationen  

1.  Wählen Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Anwendungen die Option **Anwendungsinformationen manuell angeben** aus, und wählen Sie anschließend **Weiter** aus.  

2.  Geben Sie allgemeine Informationen zur Anwendung wie den Anwendungsnamen, Kommentare, die Version und eine optionale Referenz für die Suche nach der Anwendung in der Configuration Manager-Konsole an.  

3.  Geben Sie auf der Seite **Anwendungskatalog** des Assistenten zum Erstellen von Anwendungen die folgenden Informationen an:  

    -   **Ausgewählte Sprache**: Wählen Sie in der Dropdownliste die Sprachversion der einzurichtenden Anwendung aus. Wählen Sie **Hinzufügen/Entfernen** aus, um weitere Sprachen für diese Anwendung zu konfigurieren.  

    -   **Lokalisierter Anwendungsname**: Geben Sie den Namen der Anwendung in der Sprache an, die Sie in der Dropdownliste **Ausgewählte Sprache** ausgewählt haben.  

        > [!IMPORTANT]  
        >  Sie müssen für jede Sprachversion, die eingerichtet werden soll, einen lokalisierten Anwendungsnamen angeben.  

    -   **Benutzerkategorien**: Wählen Sie **Bearbeiten** aus, um Anwendungskategorien in der Sprache anzugeben, die Sie in der Dropdownliste **Ausgewählte Sprache** ausgewählt haben. Benutzer des Softwarecenters können diese ausgewählten Kategorien verwenden, um die verfügbaren Anwendungen zu filtern und zu sortieren.  

    -   **Benutzerdokumentation**: Wählen Sie **Durchsuchen** aus, um durch Angabe einer URL, des UNC-Pfads und des Dateinamens eine Datei auszuwählen, in der Softwarecenter-Benutzer weitere Informationen zur Anwendung erhalten können.  

    -   **Linktext**: Geben Sie den Text an, der anstelle der URL für die Anwendung angezeigt wird.  

    -   **Application Privacy URL**: (URL der Datenschutzrichtlinien für die Anwendung) Geben Sie eine URL an, die mit der Datenschutzerklärung für die Anwendung verknüpft ist.  

    -   **Lokalisierte Beschreibung**: Geben Sie eine Beschreibung der Anwendung in der Sprache an, die Sie in der Dropdownliste **Ausgewählte Sprache** ausgewählt haben.  

    -   **Schlüsselwörter**: Geben Sie eine Liste mit Schlüsselwörtern in der Sprache an, die Sie in der Dropdownliste **Ausgewählte Sprache** ausgewählt haben. Mithilfe dieser Schlüsselwörter können Softwarecenter-Benutzer nach der Anwendung suchen.  

    -   **Symbol**: Wählen Sie **Durchsuchen** aus, um aus den verfügbaren Symbolen ein Symbol für diese Anwendung auszuwählen. Wenn Sie kein Symbol angeben, wird für die Anwendung ein Standardsymbol verwendet.  

    -   **Display this as a featured app and highlight it in the company portal**: (Als ausgewählte App anzeigen und im Unternehmensportal hervorheben) Wählen Sie diese Option aus, wenn Sie die App im Unternehmensportal hervorgehoben anzeigen möchten.  

4.  Wählen Sie auf der Seite **Bereitstellungstypen** des Assistenten zum Erstellen von Anwendungen **Hinzufügen** aus, um einen neuen Bereitstellungstyp zu erstellen.  

 Weitere Informationen finden Sie unter [Bereitstellungstypen für die Anwendung erstellen](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) in diesem Thema.  

5.  Wählen Sie **Weiter** aus, überprüfen Sie die Anwendungsinformationen auf der Seite **Zusammenfassung**, und schließen Sie den Assistenten zum Erstellen von Anwendungen ab.  

Die neue Anwendung wird im Knoten **Anwendungen** der Configuration Manager-Konsole angezeigt.  

##  <a name="create-deployment-types-for-the-application"></a>Bereitstellungstypen für die Anwendung erstellen  
 Wenn Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemein** die Option **Informationen zu diesem Bereitstellungstyp automatisch den Installationsdateien entnehmen** auswählen, müssen Sie einige der Schritte in den nachfolgenden Verfahren nicht ausführen.  

## <a name="start-the-create-deployment-type-wizard"></a>Starten des Assistenten zum Erstellen neuer Bereitstellungstypen  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** aus.  

3.  Wählen Sie eine Anwendung aus, und wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Anwendung** **Bereitstellungstyp erstellen** aus.  

> [!TIP]  
>  Sie können den Assistenten zum Erstellen neuer Bereitstellungstypen auch über den Assistenten zum Erstellen von Anwendungen sowie über die Registerkarte **Bereitstellungstypen** im Dialogfeld *<Anwendungsname\>* **Eigenschaften** starten.  

## <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-set-up-the-information"></a>Angeben, ob die Informationen zum Bereitstellungstyp automatisch erkannt oder manuell eingerichtet werden sollen  
 Wenden Sie eines der folgenden Verfahren an, um Informationen zum Bereitstellungstyp automatisch zu erkennen oder manuell einzurichten.  

### <a name="automatically-detect-deployment-type-information"></a>Automatisches Erkennen der Informationen zum Bereitstellungstyp  

1.  Wählen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemein** die Option **Informationen zu diesem Bereitstellungstyp automatisch den Installationsdateien entnehmen** aus.  

2.  Wählen Sie im Feld **Typ** den Installationsdateityp der Anwendung aus, den Sie zur Erkennung der Informationen zum Bereitstellungstyp verwenden möchten.  

3.  Geben Sie im Feld **Speicherort** den UNC-Pfad im Format *\\\\server\\freigabe\\dateiname* oder den Store-Link zu den Installationsdateien der Anwendung und zum Inhalt an, den Sie zur Erkennung von Bereitstellungstypinformationen verwenden möchten. Sie können auch **Durchsuchen** auswählen, um die Installationsdatei zu suchen.  

    > [!NOTE]  
    >  Sie benötigen Zugriff auf den UNC-Pfad mit der Anwendung sowie auf alle Unterordner, die den Anwendungsinhalt enthalten.  

4.  Überprüfen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Informationen importieren** die importierten Informationen, und wählen Sie anschließend **Weiter** aus. Sie können auch **Zurück** auswählen, um zurückzugehen und mögliche Fehler zu beheben.  

5.  Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemeine Informationen** die folgenden Informationen an:  

    > [!NOTE]  
    >  Einige Informationen zum Bereitstellungstyp können schon vorhanden sein, wenn sie aus den Anwendungsinstallationsdateien gelesen wurden. Zudem werden je nach erstelltem Bereitstellungstyp möglicherweise unterschiedliche Optionen angezeigt.  

    -   Allgemeine Informationen zum Bereitstellungstyp, darunter Name, Administratorkommentare und verfügbare Sprachen.  

    -   **Installationsprogramm**: Geben Sie das Installationsprogramm und alle zur Installation des Bereitstellungstyps erforderlichen Eigenschaften an.  

    -   **Installationsverhalten**: Geben Sie an, ob der Bereitstellungstyp für den gegenwärtig angemeldeten Benutzer oder für alle Benutzer installiert werden soll. Sie können auch angeben, ob der Bereitstellungstyp für alle Benutzer installiert werden soll, wenn er für ein Gerät bereitgestellt wird, oder ob der Bereitstellungstyp nur für einen Benutzer installiert wird, wenn er für einen Benutzer bereitgestellt wird.  

    -   **Use an automatic VPN connection (if configured)**: (Automatische VPN-Verbindung verwenden (sofern konfiguriert))Wenn ein VPN-Profil auf dem Gerät bereitgestellt wurde, auf dem die App gestartet wird, starten Sie die VPN-Verbindung beim Starten der App (nur Windows 8.1 und Windows Phone 8.1). Wenn mehrere VPN-Profile auf einem Windows 8.1-Gerät bereitgestellt wurden, wird standardmäßig das erste bereitgestellte VPN-Profil verwendet.  

         Auf Geräten mit Windows Phone 8.1 werden automatische VPN-Verbindungen nicht unterstützt, wenn mehrere VPN-Profile auf dem Gerät bereitgestellt wurden.  

         Weitere Informationen zu VPN-Profilen finden Sie unter [VPN-Profile in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

6.  Wählen Sie **Weiter** aus, und fahren Sie mit [Specify content options for the deployment type](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type) (Angeben von Inhaltsoptionen für den Bereitstellungstyp) fort.  

### <a name="manually-set-up-the-deployment-type-information"></a>Manuelles Einrichten der Informationen zum Bereitstellungstyp  

1.  Wählen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Registerkarte **Allgemein** die Option **Informationen zum Bereitstellungstyp manuell angeben** aus.  

2.  Wählen Sie im Feld **Typ** den Installationsdateityp der Anwendung aus, den Sie zur Erkennung der Informationen zum Bereitstellungstyp verwenden möchten. Sie können dieselben Installationstypen wie bei einer automatischen Erkennung der Informationen zum Bereitstellungstyp auswählen, und ein Skript zur Installation des Bereitstellungstyps angeben.  

3.  Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemeine Informationen** einen Namen für den Bereitstellungstyp, eine optionale Beschreibung und die Sprachen an, in denen dieser Bereitstellungstyp verfügbar sein soll. Wählen Sie anschließend **Weiter** aus.  

4.  Fahren Sie mit [Angeben von Inhaltsoptionen für den Bereitstellungstyp](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type) fort.  

##  <a name="specify-content-options-for-the-deployment-type"></a>Angeben von Inhaltsoptionen für den Bereitstellungstyp  

1.  Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Inhalt** die folgenden Informationen an:  

    -   **Inhaltsort**: Geben Sie den Speicherort des Inhalts für diesen Bereitstellungstyp an, oder klicken Sie auf **Durchsuchen**, um den Inhaltsordner für den Bereitstellungstyp auszuwählen.  

        > [!IMPORTANT]  
        >  Das Systemkonto des Standortservercomputers muss zum Zugriff auf den angegebenen Inhaltsort berechtigt sein.  

    -   **Einstellungen für zu deinstallierenden Inhalt** – wählen Sie eine der folgenden Optionen aus:
        - **Übereinstimmend mit zu installierendem Inhalt**– wählen Sie diese Option aus, wenn die Inhalte für die Installation und die Deinstallation identisch sind. Dies ist das Standardverhalten.
        - **Nicht zu deinstallierender Inhalt** – wählen Sie diese Option aus, wenn Ihre Anwendung für die Deinstallation keine Inhalte benötigt.
        - **Abweichend von zu installierendem Inhalt** – wählen Sie diese Option aus, wenn die für die Deinstallation benötigten Inhalten von den Inhalten für die Installation abweichen.

4. Wenn Sie **Abweichend von zu installierendem Inhalt** ausgewählt haben, können Sie den Speicherort der Anwendungsinhalte aufrufen eingeben, die zum Deinstallieren der Anwendung verwendet werden.
5. Klicken Sie auf **OK**, um das Dialogfeld zu Bereitstellungstyp-Eigenschaften zu schließen.

    -   **Inhalt dauerhaft in Clientcache speichern**: Mit dieser Option geben Sie an, ob der Inhalt im Cache des Clientcomputers selbst dann dauerhaft beibehalten werden soll, wenn er bereits ausgeführt wurde. Diese Option kann sich bei einigen Bereitstellungen als nützlich erweisen, beispielsweise bei Windows Installer-basierter Software, bei der für die Anwendung von Updates eine lokale Quellkopie erforderlich ist. Allerdings wird der verfügbare Cachespeicher hierdurch verringert. Wenn Sie diese Option auswählen, kann es bei einer umfangreichen Bereitstellung im späteren Verlauf zu einem Fehler kommen, falls der Cache nicht über ausreichend Speicherplatz verfügt.  

    -   **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Wählen Sie diese Option aus, um das Herunterladen von Inhalten von anderen lokalen Clients zuzulassen, von denen die Inhalte bereits heruntergeladen und zwischengespeichert wurden, und so die Netzwerkauslastung zu reduzieren. Diese Option nutzt Windows BranchCache-Technologie.  

    -   **Installationsprogramm**: Geben Sie den Namen des Installationsprogramms und alle erforderlichen Installationsparameter an, oder wählen Sie **Durchsuchen** aus, um den Speicherort der Installationsdatei zu suchen.  

    -   **Installationsstart in**: Geben Sie bei Bedarf den Ordner an, in dem sich das Installationsprogramm für den Bereitstellungstyp befindet. Dabei kann es sich um einen absoluten Pfad auf dem Client oder um einen Pfad zum Verteilungspunktordner handeln, in dem sich die Installationsdateien befinden.  

    -   **Deinstallationsprogramm**: Geben Sie bei Bedarf den Namen des Deinstallationsprogramms und alle erforderlichen Parameter an, oder klicken Sie auf **Durchsuchen**, um den Speicherort zu suchen.  

    -   **Deinstallationsstart in**: Geben Sie bei Bedarf den Ordner an, in dem sich das Deinstallationsprogramm für den Bereitstellungstyp befindet. Dieser Ordner kann als absoluter Pfad auf dem Client oder relativ zu dem Verteilungspunktordner angegeben werden, in dem das Paket enthalten ist.  

    -   **Installationsprogramm ausführen und Programm als 32-Bit-Prozess auf 64-Bit-Clients deinstallieren**: Verwenden Sie die 32-Bit-Dateipfade und 32-Bit-Registrierungspfade auf Windows-Computern zum Ausführen des Installationsprogramms für den Bereitstellungstyp.  

2.  Wählen Sie **Weiter** aus.  

## <a name="set-up-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>Einrichten von Methoden zum Erkennen vorhandener Bereitstellungstypen (nur Windows-PCs)  
 Mit dem folgenden Verfahren richten Sie eine Erkennungsmethode ein, durch die angegeben wird, ob der Bereitstellungstyp bereits installiert ist.  

1.  Wählen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Erkennungsmethode** die Option **Regeln konfigurieren, um zu erkennen, ob dieser Bereitstellungstyp vorhanden ist** aus. Wählen Sie anschließend **Klausel hinzufügen** aus.  

    > [!NOTE]  
    >  Sie können auch **Mithilfe eines benutzerdefinierten Skripts erkennen, ob dieser Bereitstellungstyp vorhanden ist** auswählen. Weitere Informationen finden Sie unter [Use a custom script to check for the presence of a deployment type (So erkennen Sie einen vorhandenen Bereitstellungstyp mithilfe eines benutzerdefinierten Skripts)](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type).  

2.  Wählen Sie im Dialogfeld **Erkennungsregel** in der Dropdownliste **Einstellungstyp** die Methode aus, die Sie zum Erkennen des Vorhandenseins des Bereitstellungstyps verwenden möchten. Folgende Methoden stehen zur Auswahl:  

    -   **Dateisystem**: Mit dieser Methode können Sie erkennen, ob eine angegebene Datei oder ein angegebener Ordner auf einem Clientgerät vorhanden und die Anwendung somit installiert ist.  

        > [!NOTE]  
        >  Die Angabe eines UNC-Pfads zu einer Netzwerkfreigabe im Feld "Pfad" wird vom Einstellungstyp **Dateisystem** nicht unterstützt. Sie können nur einen lokalen Pfad auf dem Clientgerät angeben.  
        >   
        >  Wählen Sie erst die Option **Diese Datei/dieser Ordner ist einer 32-Bit-Anwendung auf 64-Bit-Systemen zugeordnet** aus, um die angegebene Datei bzw. den angegebenen Order zuerst an 32-Bit-Speicherorten zu suchen. Wenn die Datei oder der Ordner nicht gefunden wird, werden die 64-Bit-Speicherorte durchsucht.  

    -   **System Center Configuration Manager**: Verwenden Sie diese Methode, um festzustellen, ob ein angegebener Registrierungsschlüssel oder -wert auf einem Clientgerät vorhanden und die Anwendung somit installiert ist.  

        > [!NOTE]  
        >  Wählen Sie zuerst die Option **Dieser Registrierungsschlüssel ist mit einer 32-Bit-Anwendung auf 64-Bit-Systemen verknüpft** aus, um den angegebenen Registrierungsschlüssel in 32-Bit-Registrierungspfaden zu suchen. Wenn der Registrierungsschlüssel nicht gefunden wird, werden 64-Bit-Pfade durchsucht.  

    -   **Windows Installer**: Mit dieser Methode können Sie erkennen, ob eine angegebene Windows Installer-Datei auf einem Clientgerät vorhanden und die Anwendung somit installiert ist.  

3.  Geben Sie Details zu dem Element an, anhand dessen erkannt werden soll, ob dieser Bereitstellungstyp installiert ist. Beispielsweise können Sie eine Datei, einen Ordner, einen Registrierungsschlüssel oder -wert oder einen Windows Installer-Produktcode verwenden.  

4.  Geben Sie Details zu dem Wert an, den Sie anhand des zur Erkennung des installierten Bereitstellungstyps verwendeten Elements auswerten möchten. Wenn Sie beispielsweise anhand einer Datei bestimmen, ob der Bereitstellungstyp installiert ist, können Sie **The file system setting must exist on the target system to indicate presence of this application** (Die Dateisystemeinstellung muss auf dem Zielsystem vorhanden sein, um das Vorhandensein dieser Anwendung anzuzeigen) auswählen.  

5.  Wählen Sie **Weiter** aus, um das Dialogfeld **Erkennungsregel** zu schließen.  

###  <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a>Verwenden eines benutzerdefinierten Skripts zum Überprüfen eines vorhandenen Bereitstellungstyps  

1.  Aktivieren Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Erkennungsmethode** das Kontrollkästchen **Mithilfe eines benutzerdefinierten Skripts erkennen, ob dieser Bereitstellungstyp vorhanden ist**, und wählen Sie dann**Bearbeiten** aus.  

2.  Wählen Sie im Dialogfeld **Skript-Editor** in der Dropdownliste **Skripttyp** die Skriptsprache aus, die Sie zum Erkennen des Bereitstellungstyps verwenden möchten.  

3.  Geben Sie das gewünschte Skript in das Feld **Skriptinhalte** ein. Sie können auch den Inhalt eines vorhandenen Skripts in dieses Feld einfügen oder **Öffnen** auswählen, um ein vorhandenes gespeichertes Skript zu suchen. Von Configuration Manager werden dann die Ergebnisse des Skripts überprüft, indem die Werte, die in der Standardausgabe (STDOUT) und im Standardfehler (STDERR) geschrieben wurden, sowie der Exitcode des Skripts ausgelesen werden. Ein Exitcode ungleich null bedeutet, dass es bei der Ausführung des Skripts zu einem Fehler gekommen ist, und dass der Erkennungszustand der Anwendung „Unbekannt“ ist. Wenn der Exitcode gleich null ist und in „STDOUT“-Daten enthalten sind, ist der Erkennungszustand der Anwendung „Installiert“.  

 Anhand der folgenden Tabelle können Sie sehen, wie Sie die Ausgabe eines Skripts verwenden können, um zu überprüfen ob eine Anwendung installiert ist.  

|Exitcode des Skripts|Details|
|--------------------------------|-----------------|
|0|**Data read from STDOUT (Aus „STDOUT“ gelesene Daten):** Leer<br /><br /> **Data read from STDERR (Aus „STDERR“ gelesene Daten):** Leer<br /><br /> **Script result (Skriptergebnis):** Erfolg<br /><br /> **Application detection state (Erkennungszustand der Anwendung):** Nicht installiert|  
|0|**Data read from STDOUT (Aus „STDOUT“ gelesene Daten):** Leer<br /><br /> **Data read from STDERR (Aus „STDERR“ gelesene Daten):** Nicht leer<br /><br /> **Script result (Skriptergebnis):** Fehler<br /><br /> **Application detection state (Erkennungszustand der Anwendung):** Unbekannt|  
|0|**Data read from STDOUT (Aus „STDOUT“ gelesene Daten):** Nicht leer<br /><br /> **Data read from STDERR (Aus „STDERR“ gelesene Daten):** Leer<br /><br /> **Script result (Skriptergebnis):** Erfolg<br /><br /> **Application detection state (Erkennungszustand der Anwendung)** Installiert|  
|0|**Data read from STDOUT (Aus „STDOUT“ gelesene Daten):** Nicht leer<br /><br /> **Data read from STDERR (Aus „STDERR“ gelesene Daten):** Nicht leer<br /><br /> **Script result (Skriptergebnis):** Erfolg<br /><br /> **Application detection state (Erkennungszustand der Anwendung)** Installiert|  
|Wert ungleich null|**Data read from STDOUT (Aus „STDOUT“ gelesene Daten):** Leer<br /><br /> **Data read from STDERR (Aus „STDERR“ gelesene Daten):** Leer<br /><br /> **Script result (Skriptergebnis):** Fehler<br /><br /> **Application detection state (Erkennungszustand der Anwendung):** Unbekannt|  
|Wert ungleich null|**Data read from STDOUT (Aus „STDOUT“ gelesene Daten):** Leer<br /><br /> **Data read from STDERR (Aus „STDERR“ gelesene Daten):** Nicht leer<br /><br /> **Script result (Skriptergebnis):** Fehler<br /><br /> **Application detection state (Erkennungszustand der Anwendung):** Unbekannt|  
|Wert ungleich null|**Data read from STDOUT (Aus „STDOUT“ gelesene Daten):** Nicht leer<br /><br /> **Data read from STDERR (Aus „STDERR“ gelesene Daten):** Leer<br /><br /> **Script result (Skriptergebnis):** Fehler<br /><br /> **Application detection state (Erkennungszustand der Anwendung):** Unbekannt|  
|Wert ungleich null|**Data read from STDOUT (Aus „STDOUT“ gelesene Daten):** Nicht leer<br /><br /> **Data read from STDERR (Aus „STDERR“ gelesene Daten):** Nicht leer<br /><br /> **Script result (Skriptergebnis):** Fehler<br /><br /> **Application detection state (Erkennungszustand der Anwendung):** Unbekannt|  

In der folgenden Tabelle sind Beispielskripte für Microsoft Visual Basic (VB) aufgeführt, mit deren Hilfe Sie eigene Skripte für die Anwendungserkennung schreiben können.  

|Visual Basic-Beispielskript|Beschreibung|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|Vom Skript wird ein Exitcode ungleich null zurückgegeben, was darauf hindeutet, dass es nicht erfolgreich ausgeführt werden konnte. In diesem Fall ist der Erkennungszustand der Anwendung Unbekannt.|  
|**WScript.StdErr.Write "Script failed"**<br /><br /> **WScript.Quit(0)**|Vom Skript wird ein Exitcode gleich null zurückgegeben, der Wert für „STDERR“ ist jedoch nicht leer, was darauf hindeutet, dass das Skript nicht erfolgreich ausgeführt werden konnte. In diesem Fall ist der Erkennungszustand der Anwendung Unbekannt.|  
|**WScript.Quit(0)**|Vom Skript wird ein Exitcode gleich null zurückgegeben, was darauf hindeutet, dass es erfolgreich ausgeführt wurde. Der Wert für „STDOUT“ ist jedoch leer, was darauf hindeutet, dass die Anwendung nicht installiert ist.|  
|**WScript.StdOut.Write "The application is installed"**<br /><br /> **WScript.Quit(0)**|Vom Skript wird ein Exitcode gleich null zurückgegeben, was darauf hindeutet, dass es erfolgreich ausgeführt wurde. Der Wert für „STDOUT“ ist nicht leer, was darauf hindeutet, dass die Anwendung installiert ist.|  
|**WScript.StdOut.Write "The application is installed"**<br /><br /> **WScript.StdErr.Write "Completed"**<br /><br /> **WScript.Quit(0)**|Vom Skript wird ein Exitcode gleich null zurückgegeben, was darauf hindeutet, dass es erfolgreich ausgeführt wurde. Die Werte für „STDOUT“ und „STDERR“ sind nicht leer, was darauf hindeutet, dass die Anwendung installiert ist.|  

 > [!NOTE]  
 >  Die maximal zulässige Größe für ein Skript beträgt 32 KB.  

4.  Wählen Sie **OK** aus, um das Dialogfeld **Skript-Editor** zu schließen.  

## <a name="specify-user-experience-options-for-the-deployment-type"></a>Angeben von Optionen für die Benutzerfreundlichkeit des Bereitstellungstyps  
 Durch diese Einstellungen wird angegeben, wie die Anwendung auf Geräten installiert wird und was dem Benutzer angezeigt wird.  

1.  Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Benutzerfreundlichkeit** die folgenden Informationen an:  

    -   **Installationsverhalten**: Wählen Sie in der Dropdownliste eine der folgenden Optionen aus:  

        -   **Für Benutzer installieren**: Die Anwendung wird nur für den Benutzer installiert, für den sie bereitgestellt wird.  

        -   **Für System installieren**: Die Anwendung wird nur einmal installiert und ist für alle Benutzer verfügbar.  

        -   **Für System installieren, wenn Ressource ein Gerät ist, andernfalls für Benutzer installieren**: Wenn die Anwendung auf einem Gerät bereitgestellt wird, wird sie für alle Benutzer installiert. Wenn die Anwendung für einen Benutzer bereitgestellt wird, wird sie nur für diesen Benutzer installiert.  

    -   **Anmeldeanforderung**: Geben Sie die Anmeldeanforderungen für diesen Bereitstellungstyp anhand der folgenden Optionen an:  

        -   **Nur wenn ein Benutzer angemeldet ist**  

        -   **Unabhängig von Benutzeranmeldung**  

        -   **Nur wenn kein Benutzer angemeldet ist**  

        > [!NOTE]  
        >  Für diese Option wird standardmäßig **Nur wenn ein Benutzer angemeldet ist** ausgewählt. Die Option kann nicht geändert werden, wenn Sie in der Dropdownliste **Installationsverhalten** die Option **Für Benutzer installieren** ausgewählt haben.  

    -   **Sichtbarkeit des Installationsprogramms**: Gibt den Modus an, in dem der Bereitstellungstyp auf Clientgeräten ausgeführt wird. Die folgenden Optionen sind verfügbar:  

        -   **Maximiert**: Der Bereitstellungstyp wird auf Clientgeräten im maximierten Modus ausgeführt. Benutzer sehen alle Installationsaktivitäten.  

        -   **Normal**: Der Bereitstellungstyp wird basierend auf den Standardeinstellungen des Systems und Programms im normalen Modus ausgeführt. Dies ist der Standardmodus.  

        -   **Minimiert**: Der Bereitstellungstyp wird auf Clientgeräten im minimierten Modus ausgeführt. Benutzer können die Installationsaktivität möglicherweise im Infobereich oder in der Taskleiste sehen.  

        -   **Ausgeblendet**: Der Bereitstellungstyp wird auf Clientgeräten im ausgeblendeten Modus ausgeführt, und Benutzer sehen keine Installationsaktivitäten.  

    -   **Benutzern gestatten, die Programminstallation anzuzeigen und mit ihr zu interagieren**: Hiermit geben Sie an, ob der Benutzer bei der Installation des Bereitstellungstyps die Installationsoptionen einrichten darf.  

        > [!NOTE]  
        >  Diese Option ist standardmäßig aktiviert, wenn in der Dropdownliste **Installationsverhalten** die Option **Für Benutzer installieren** ausgewählt wurde.  

    -   **Maximal zulässige Laufzeit (Minuten):** Geben Sie hier an, wie lange die Ausführung des Programms auf dem Clientcomputer voraussichtlich maximal dauert. Sie können für diese Einstellung eine ganze Zahl größer oder gleich Null angeben. Die Standardeinstellung ist 120 Minuten.  

         Dieser Wert wird verwendet:  

        -   Überwachen Sie die Ergebnisse des Bereitstellungstyps.  

        -   Überprüfen Sie, ob ein Bereitstellungstyp installiert wird, wenn auf Clientgeräten Wartungsfenster definiert wurden. Wenn ein Wartungsfenster vorhanden ist, wird ein Programm nur gestartet, wenn die verbleibende Dauer des Wartungsfensters noch mindestens der Einstellung unter **Maximal zulässige Laufzeit** entspricht.  

        > [!IMPORTANT]  
        >  Wenn der Zeitraum für **Maximal zulässige Laufzeit** länger ist als das geplante Wartungsfenster, kann dies zu einem Problem führen. Wird die maximale Laufzeit vom Benutzer auf einen Wert festgelegt, der die Länge der verfügbaren Wartungsfenster überschreitet, wird dieser Bereitstellungstyp nicht ausgeführt.  

2.  **Geschätzte Installationszeit (Minuten)**: Geben Sie an, wie lange die Installation des Bereitstellungstyps voraussichtlich dauert. Dies wird Benutzern des Softwarecenters angezeigt.  

## <a name="specify-requirements-for-the-deployment-type"></a>Angeben von Anforderungen für den Bereitstellungstyp  

1.  Wählen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Anforderungen** **Hinzufügen** aus, um das Dialogfeld **Anforderung erstellen** zu öffnen und eine neue Anforderung hinzuzufügen.  

    > [!NOTE]  
    >  Sie können neue Anforderungen auch im Dialogfeld **Eigenschaften** von *<Name des Bereitstellungstyps\>* auf der Registerkarte **Anforderungen** hinzufügen.  

2.  Wählen Sie in der Dropdownliste **Kategorie** aus, ob diese Anforderung für ein Gerät oder einen Benutzer bestimmt ist, oder wählen Sie **Benutzerdefiniert** aus, um eine zuvor erstellte globale Bedingung zu verwenden. Bei Auswahl von **Benutzerdefiniert** können Sie auch **Erstellen** auswählen, um eine neue globale Bedingung zu erstellen. Weitere Informationen über globale Bedingungen finden Sie unter [Erstellen von globalen Bedingungen](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  Alle Anforderungen mit der Kategorie **Benutzer** und der Bedingung **Primäres Gerät** werden ignoriert, wenn Sie die Anwendung für eine Gerätesammlung bereitstellen.  
    >   
    >  Wenn Sie ein Windows-Paket und -Programm oder eine Tasksequenz erstellt haben, was Windows 10 erfordert und dies mit System Center 2012 R2 Configuration Manager SP1 geschah, und Sie dann ein Upgrade auf System Center Configuration Manager ausführen, werden die Anforderungen für Windows 10 möglicherweise entfernt. Um dieses Problem zu beheben, geben Sie die Anforderungen erneut an. Die Anforderung wird auf Geräten weiterhin ordnungsgemäß verarbeitet, obwohl sie aus der Anforderungsanzeige entfernt wurde.  

3.  Wählen Sie in der Dropdownliste **Bedingung** die Bedingung aus, anhand derer bewertet werden soll, ob der Benutzer bzw. das Gerät den Installationsanforderungen entspricht. Der Inhalt dieser Liste ist von der ausgewählten Kategorie abhängig.  

4.  Wählen Sie in der Dropdownliste **Operator** den Operator aus, der zum Vergleichen der ausgewählten Bedingung mit dem angegebenen Wert verwendet werden soll, um zu bewerten, ob der Benutzer bzw. das Gerät den Installationsanforderungen entspricht. Welche Operatoren verfügbar sind, ist von der ausgewählten Bedingung abhängig.  

    > [!IMPORTANT]  
    >  Die verfügbaren Anforderungen variieren je nach Gerätetyp, die der Bereitstellungstyp verwendet.  

5.  Geben Sie im Feld **Wert** die Werte ein, die zusammen mit der ausgewählten Bedingung und dem Operator verwendet werden sollen, um zu bewerten, ob der Benutzer bzw. das Gerät die Installationsanforderungen erfüllt. Welche Werte verfügbar sind, ist von der ausgewählten Bedingung und dem ausgewählten Operator abhängig.  

6.  Wählen Sie **OK** aus, um die Anforderung zu speichern und das Dialogfeld **Anforderung erstellen** zu schließen.  

## <a name="specify-dependencies-for-the-deployment-type"></a>Angeben von Abhängigkeiten für den Bereitstellungstyp  
 Mit Abhängigkeiten wird mindestens ein Bereitstellungstyp einer anderen Anwendung definiert, der installiert sein muss, bevor ein Bereitstellungstyp installiert wird. Sie können die abhängigen Bereitstellungstypen einrichten, die vor der Installation eines Bereitstellungstyps automatisch installiert werden.  

> [!IMPORTANT]  
>  In einigen Fällen ist ein Bereitstellungstyp von einem Bereitstellungstyp abhängig, der ebenfalls über Abhängigkeiten verfügt. Die maximale Anzahl unterstützter Abhängigkeiten in der Kette beträgt fünf.  

1.  Wählen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Abhängigkeiten** **Hinzufügen** aus, um die Bereitstellungstypen anzugeben, die installiert werden müssen, damit dieser Bereitstellungstyp installiert werden kann.  

    > [!IMPORTANT]  
    >  Sie können neue Abhängigkeiten auch im Dialogfeld *<Name des Bereitstellungstyps\>***Eigenschaften** auf der Registerkarte **Abhängigkeiten** hinzufügen.  

2.  Wählen Sie im Dialogfeld **Abhängigkeit hinzufügen** **Hinzufügen** aus.  

3.  Wählen Sie im Dialogfeld **Erforderliche Anwendung angeben** eine vorhandene Anwendung aus sowie einen der Anwendungsbereitstellungstypen, der als Abhängigkeit verwendet werden soll.  

    > [!TIP]  
    >  Sie können **Anzeigen** auswählen, um die Eigenschaften der ausgewählten Anwendung bzw. des ausgewählten Bereitstellungstyps anzuzeigen.  

4.  Wählen Sie **OK** aus, um das Dialogfeld **Erforderliche Anwendung angeben** zu schließen.  

5.  Wenn eine abhängige Anwendung automatisch installiert werden soll, aktivieren Sie das Kontrollkästchen **Automatisch installieren** neben der abhängigen Anwendung.  

    > [!NOTE]  
    >  Eine abhängige Anwendung muss nicht bereitgestellt werden, damit sie automatisch installiert werden kann.  

6.  Geben Sie im Dialogfeld **Abhängigkeit hinzufügen** unter **Name der Abhängigkeitsgruppe** einen Namen für diese Gruppe von Anwendungsabhängigkeiten ein.  

7.  Über die Schaltflächen **Priorität erhöhen** und **Priorität verringern** können Sie bei Bedarf die Auswertungsreihenfolge der Abhängigkeiten ändern.  

8.  Wählen Sie **OK** aus, um das Dialogfeld **Abhängigkeit hinzufügen** zu schließen.  

## <a name="confirm-the-deployment-type-settings-and-finish-the-wizard"></a>Bestätigen der Bereitstellungstypeinstellungen und Abschließen des Assistenten  

1.  Überprüfen Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Zusammenfassung** die Aktionen, die vom Assistenten ausgeführt werden sollen. Wählen Sie **Weiter** aus, um den Bereitstellungstyp zu erstellen, oder **Zurück**, um die Einstellungen für den Bereitstellungstyp zu ändern.  

2.  Nachdem die Seite **Fortschritt** geschlossen wurde, überprüfen Sie die ausgeführten Aktionen. Wählen Sie anschließend **Schließen** aus, um den Assistenten abzuschließen.  

3.  Wenn der Assistent zum Erstellen neuer Bereitstellungstypen aus dem Assistenten zum Erstellen von Anwendungen heraus gestartet wurde, wird nun wieder die Seite **Bereitstellungstypen** des Assistenten zum Erstellen von Anwendungen angezeigt.  

## <a name="set-up-additional-options-for-deployment-types-that-contain-virtual-applications"></a>Einrichten zusätzlicher Optionen für Bereitstellungstypen, die virtuelle Anwendungen enthalten  
 Wenden Sie die folgenden Verfahren an, um zusätzliche Optionen für Bereitstellungstypen einzurichten, die virtuelle Anwendungen enthalten.  

### <a name="set-up-content-options-for-application-virtualization-app-v-deployment-types"></a>Einrichten von Inhaltsoptionen für Application Virtualization-Bereitstellungstypen (App-V)  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungen** aus.  

2.  Wählen Sie in der Liste **Anwendungen** eine Anwendung aus, die über ein App-V-Bereitstellungstyp verfügt. Wählen Sie anschließend auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

3.  Wählen Sie im Dialogfeld Eigenschaften von *<Anwendungsname\>* **Properties** auf der Registerkarte **Bereitstellungstypen** einen App-V-Bereitstellungstyp aus, und wählen Sie dann **Bearbeiten** aus.  

4.  Konfigurieren Sie im Dialogfeld *<Name des Bereitstellungstyps\>* **Eigenschaften** auf der Registerkarte **Inhalt** bei Bedarf die folgenden Optionen:  

    -   **Inhalt dauerhaft in Clientcache speichern:** Bei Auswahl dieser Option werden die Inhalte für diesen Bereitstellungstyp nicht aus dem Configuration Manager-Clientcache gelöscht.  

    -   **Inhalt vor dem Start in den App-V-Cache laden:** Bei Auswahl dieser Option werden alle Inhalte für die virtuelle Anwendung vor dem Starten der Anwendung in den App-V-Cache geladen. Darüber hinaus wird der Anwendungsinhalt nicht im Cache fixiert und kann bei Bedarf gelöscht werden.  

5.  Wählen Sie **OK** aus, um das Dialogfeld *<Name des Bereitstellungstyps\>* **Eigenschaften** zu schließen.  

6.  Wählen Sie **OK** aus, um das Dialogfeld **Eigenschaften von** *<Anwendungsname\>* zu schließen.  

### <a name="set-up-publishing-options-for-app-v-deployment-types"></a>Einrichten von Veröffentlichungsoptionen für App-V-Bereitstellungstypen  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungen** aus.  

3.  Wählen Sie in der Liste **Anwendungen** eine Anwendung aus, die über ein App-V-Bereitstellungstyp verfügt. Wählen Sie anschließend auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

4.  Wählen Sie im Dialogfeld Eigenschaften von *<Anwendungsname\>* **Properties** auf der Registerkarte **Bereitstellungstypen** einen App-V-Bereitstellungstyp aus, und wählen Sie dann **Bearbeiten** aus.  

5.  Wählen Sie im Dialogfeld **Eigenschaften** von *<Name des Bereitstellungstyps\>* auf der Registerkarte **Veröffentlichung** die Elemente in der virtuellen Anwendung aus, die veröffentlicht werden sollen.  

6.  Wählen Sie **OK** aus, um das Dialogfeld *<Name des Bereitstellungstyps\>* **Eigenschaften** zu schließen.  

7.  Wählen Sie **OK** aus, um das Dialogfeld **Eigenschaften von** *<Anwendungsname\>* zu schließen.  

## <a name="import-an-application"></a>Importieren einer Anwendung  
 Gehen Sie wie folgt vor, um eine Anwendung in Configuration Manager zu importieren. Informationen zum Exportieren von Anwendungen finden Sie unter [Management tasks for System Center Configuration Manager applications (Verwaltungsaufgaben für System Center Configuration Manager-Anwendungen)](../../apps/deploy-use/management-tasks-applications.md).  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** aus.   

3.  Wählen Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** **Anwendung importieren** aus.  

4.  Klicken Sie auf der Seite **Allgemein** des **Assistenten zum Importieren von Anwendungen** auf **Durchsuchen**, und geben Sie einen UNC-Pfad zur ZIP-Datei an, in der die zu importierende Anwendung enthalten ist.  

5.  Wählen Sie auf der Seite **Dateiinhalt** die Aktion aus, die ausgeführt werden soll, wenn die zu importierende Anwendung das Duplikat einer vorhandenen Anwendung ist. Sie können eine neue Anwendung erstellen, oder das Duplikat ignorieren, und eine neue Revision zur vorhandenen Anwendung hinzufügen.  

6.  Überprüfen Sie auf der Seite **Zusammenfassung** die durchzuführenden Aktionen, und schließen Sie dann den Assistenten ab.  

 Die neue Anwendung wird im Knoten **Anwendungen** angezeigt.  

> [!TIP]  
>  Das Windows PowerShell-Cmdlet **Import-CMApplication** hat die gleiche Funktion wie dieses Verfahren. Weitere Informationen finden Sie unter [Import-CMApplication](https://technet.microsoft.com/library/jj821738.aspx) in der Cmdlet-Referenzdokumentation von Microsoft System Center 2012 Configuration Manager SP1.  

##  <a name="deployment-types-supported-by-configuration-manager"></a>Von Configuration Manager unterstützte Bereitstellungstypen  

|Name des Bereitstellungstyps|Weitere Informationen|  
|--------------------------|----------------------|  
|**Windows Installer (\*msi-Datei)**|Hiermit wird ein Bereitstellungstyp aus einer Windows Installer-Datei erstellt.|  
|**Windows-App-Paket (\*.appx, \*.appxbundle)**|Erstellt einen Bereitstellungstyp für die Betriebssysteme Windows 8, Windows RT oder höher aus einer Windows-App-Paketdatei oder einem gebündelten Windows-App-Paket.|  
|**Windows-App-Paket (im Windows Store)**|Erstellt einen Bereitstellungstyp für Windows 8, Windows RT oder höher, indem ein Link zur App im Windows Store angegeben und der Store durchsucht wird, um die erforderliche App auszuwählen.<br /><br /> Wenn Sie die App als Link zum Windows Store bereitstellen möchten, müssen Sie die Gruppenrichtlinieneinstellung **Store-Anwendung deaktivieren** auf **Deaktiviert** oder **Nicht konfiguriert festlegen**. Wenn diese Einstellung aktiviert ist, kann von Clients keine Verbindung mit dem Windows Store zum Herunterladen und Installieren von Anwendungen hergestellt werden.<br /><br /> Windows 8-Bereitstellungstypen, bei denen ein Link zu einem Store verwendet wird, werden unabhängig von ihrer Priorität immer vor anderen Bereitstellungstypen ausgewertet.|  
|**Skriptinstallationsprogramm**|Hiermit wird ein Bereitstellungstyp erstellt, in dem ein Skript angegeben wird. Dieses Skript wird auf Clientgeräten ausgeführt und dient zur Installation von Inhalten oder zur Ausführung einer Aktion.|  
|**Microsoft Application Virtualization 4**|Erstellt einen Bereitstellungstyp aus einem Microsoft Application Virtualization 4-Manifest.|  
|**Microsoft Application Virtualization 5**|Hiermit wird ein Bereitstellungstyp aus einer Microsoft Application Virtualization 5-Paketdatei erstellt.|  
|**Windows Phone-App-Paket (\*.xap-Datei)**|Hiermit wird ein Bereitstellungstyp aus einer Windows Phone-App-Paketdatei erstellt.|  
|**Windows Phone-App-Paket (in Windows Phone Store)**|Erstellt einen Bereitstellungstyp, indem ein Link zur App im Windows Phone-Store angegeben wird.|  
|**Windows Mobile-CAB-Datei**|Erstellt einen Bereitstellungstyp für Windows Mobile-Geräte anhand einer Windows Mobile-CAB (Cabinet)-Datei.|  
|**App-Paket für iOS (\*.ipa-Datei)**|Hiermit wird ein Bereitstellungstyp aus einer iOS-App-Paketdatei erstellt.|  
|**App-Paket für iOS aus App Store**|Hiermit wird ein Bereitstellungstyp erstellt, indem ein Link zur iOS-App im App Store angegeben wird.|  
|**App-Paket für Android (\*.apk-Datei)**|Hiermit wird ein Bereitstellungstyp aus einer Android-App-Paketdatei erstellt.|  
|**App-Paket für Android auf Google Play**|Hiermit wird ein Bereitstellungstyp erstellt, indem ein Link zur App auf Google Play angegeben wird.|  
|**Mac OS X**|Hiermit wird ein Bereitstellungstyp für Macintosh-Computer aus einer CMMAC-Datei erstellt, die Sie mit dem Tool „CMAppUtil“ erstellt haben.<br /><br /> Gilt nur für Macintosh-Computer, auf denen der Configuration Manager-Client ausgeführt wird.|  
|**Webanwendung**|Hiermit wird ein Bereitstellungstyp erstellt, der einen Link zu einer Webanwendung angibt. Mit dem Bereitstellungstyp wird auf dem Gerät des Benutzers eine Verknüpfung mit der Webanwendung installiert.<br /><br /> Wenn Intune Managed Browser auf den von Ihnen verwalteten iOS- oder Android-Geräten installiert wurde, können Sie sicherstellen, dass die Benutzer die App nur über Managed Browser öffnen. Zu diesem Zweck geben Sie den Link zur App in einem der folgenden Formate an – Sie ersetzen dabei **http:** durch **http-intunemam:** oder **https:** durch **https-intunemam:**<br /><br /> - **http-intunemam://<Pfad zur Web-App\>**<br /><br /> - **https-intunemam://<Pfad zur Web-App\>**<br /><br /> Sie können mithilfe der Configuration Manager-Anwendungsanforderungen sicherstellen, dass die Apps, die Sie mit Managed Browser verknüpfen möchten, nur auf iOS- und Android-Geräten installiert werden.<br /><br /> Weitere Informationen zu Intune Managed Browser finden Sie unter [Verwalten des Internetzugriffs mittels Richtlinien für verwaltete Browser mit System Center Configuration Manager](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).|  
|**Windows Installer über die Verwaltung mobiler Geräte (\*.msi)**|Mit diesem Installationstyp können Sie Windows Installer-basierte Apps auf Windows 10-PCs erstellen und bereitstellen.<br /><br /> Folgendes muss berücksichtigt werden, wenn Sie diese Art Installationsprogramm verwenden:<br><br>– Sie können nur eine einzelne Datei mit der Erweiterung „.msi“ hochladen.<br /><br /> – Produktcode und Produktversion der Datei werden zur Erkennung der App verwendet.<br /><br /> – Es wird das standardmäßige Neustartverhalten der App verwendet. Dies wird nicht von Configuration Manager gesteuert.<br /><br /> – Pro Benutzer definierte MSI-Pakete werden für einen einzelnen Benutzer installiert.<br /><br /> – Pro Gerät definierte MSI-Pakete werden für alle Benutzer des Geräts installiert.<br /><br /> – MSI-Pakete im Dualmodus werden zurzeit nur für alle Benutzer des Geräts installiert.<br /><br /> – App-Updates werden unterstützt, wenn jede Version den gleichen MSI-Produktcode aufweist.|  
