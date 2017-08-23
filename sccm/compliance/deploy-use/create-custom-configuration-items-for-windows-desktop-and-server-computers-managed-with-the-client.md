---
title: "Erstellen von Konfigurationselementen für clientverwaltete Windows-Computer – Configuration Manager | Microsoft-Dokumentation"
description: "Verwalten Sie Windows-Computer und -Server mithilfe benutzerdefinierter Konfigurationselemente für Windows-Desktop- und -Servercomputer."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
caps.latest.revision: "9"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e040c6b3a951d1bdf5a46dd82f1bd92b45c2e71d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-system-center-configuration-manager-client"></a>Erstellen benutzerdefinierter Konfigurationselemente für Windows-Desktop- und -Servercomputer, die mit dem System Center Configuration Manager-Client verwaltet werden

*Gilt für: System Center Configuration Manager (Current Branch)*


Verwenden Sie das System Center Configuration Manager-Konfigurationselement des Typs **Windows-Desktops und -Server (benutzerdefiniert)** zum Verwalten der Einstellungen für Windows-Computer und -Server, die durch den Configuration Manager-Client verwaltet werden.  

## <a name="start-the-create-configuration-item-wizard"></a>Starten Sie den Assistenten zum Erstellen von Konfigurationselementen.

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationselemente**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen**einen Namen und optional eine Beschreibung für das Konfigurationselement an.  

5.  Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben**den Typ **Windows-Desktops und -Server (benutzerdefiniert)**aus.  

    > [!TIP]  
    >  Wenn Sie Einstellungen für Erkennungsmethoden bereitstellen möchten, mit denen überprüft wird, ob eine Anwendung vorhanden ist, wählen Sie **Dieses Konfigurationselement enthält Anwendungseinstellungen**aus.  

6.  Klicken Sie auf **Kategorien**, wenn Sie Kategorien erstellen und zuweisen, um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern.  

## <a name="provide-detection-method-information"></a>Bereitstellen von Informationen zur Erkennungsmethode  
 Verwenden Sie dieses Verfahren, um Informationen zur Erkennungsmethode für das Konfigurationselement bereitzustellen.  

> [!NOTE]  
>  Gilt nur, wenn Sie ausgewählt **dieses Konfigurationselement enthält Anwendungseinstellungen** auf der **Allgemeine** Seite des Assistenten.  

 Eine Erkennungsmethode in Configuration Manager enthält Regeln zur Erkennung, ob eine Anwendung auf einem Computer installiert ist. Diese Erkennung erfolgt, bevor die Kompatibilität des Konfigurationselements bewertet wird. Um zu erkennen, ob eine Anwendung installiert ist, können Sie die Anwesenheit einer Windows Installer-Datei für die Anwendung prüfen, ein benutzerdefiniertes Skript verwenden oder **Immer annehmen, dass die Anwendung installiert ist** auswählen, um die Kompatibilität des Konfigurationselements unabhängig davon zu bewerten, ob die Anwendung installiert ist.  

 Verwenden Sie diese Verfahren zum Konfigurieren von Erkennungsmethoden in System Center Configuration Manager.  

### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>So erkennen Sie eine Anwendungsinstallation anhand der Windows Installer-Datei  

1.  Auf der **Erkennungsmethoden** auf der Seite der **Assistenten zum Erstellen von Konfigurationselementen**, wählen die **mit Windows Installer-Erkennung** Kontrollkästchen.  

2.  Klicken Sie auf **Öffnen**, suchen Sie die Windows Installer (MSI)-Datei, die Sie verwenden möchten, zu erkennen, und klicken Sie dann auf **Öffnen**.  

3.  Die **Version** Feld wird automatisch ausgefüllt, mit der Versionsnummer des Windows Installer-Datei, die Sie ausgewählt haben. Sie können eine neue Versionsnummer in dieses Feld eingeben, wenn der angezeigte Wert nicht korrekt ist.  

4.  Aktivieren Sie das Kontrollkästchen **Diese Anwendung wurde für mindestens einen Benutzer installiert** , wenn jedes Benutzerprofil auf dem Computer erkannt werden soll.  

### <a name="to-detect-a-specific-application-and-deployment-type"></a>So erkennen Sie einen bestimmten Anwendungs- und Bereitstellungstyp  

1.  Aktivieren Sie auf der Seite **Erkennungsmethoden** des **Assistenten zum Erstellen von Konfigurationselementen**das Kontrollkästchen **Bestimmten Anwendungs- und Bereitstellungstyp erkennen** , und klicken Sie dann auf **Auswählen**.  

2.  Wählen Sie im Dialogfeld **Anwendung angeben** die Anwendung und einen zugeordneten Bereitstellungstyp aus, den Sie erkennen möchten.  

### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>So erkennen Sie eine Anwendungsinstallation mithilfe eines benutzerdefinierten Skripts  

1.  Auf der **Erkennungsmethoden** auf der Seite der **Assistenten zum Erstellen von Konfigurationselementen**, wählen die **Verwenden Sie ein benutzerdefiniertes Skript zum Erkennen dieser Anwendung** Kontrollkästchen.  

2.  Wählen Sie in der Liste die Sprache des Skripts, die Sie öffnen möchten. Wählen Sie aus den folgenden Skripts:  

    -   **VBScript**  

    -   **JScript**  

    -   **PowerShell**  

3.  Klicken Sie auf **Öffnen**, suchen Sie das Skript, das Sie verwenden möchten, und klicken Sie auf **Öffnen**.  

##  <a name="configure-settings"></a>Konfigurieren der Einstellungen  
 Verwenden Sie dieses Verfahren zum Konfigurieren der Einstellungen im Konfigurationselement.  

 Einstellungen repräsentieren die geschäftlichen oder technischen Maßnahmen, die zur Bewertung der Kompatibilität auf Clientcomputern verwendet werden. Sie können eine neue Einstellung konfigurieren oder eine bestehende Einstellung auf einem Referenzcomputer verwenden.  

1.  Klicken Sie im **Assistenten zum Erstellen von Konfigurationselementen** auf der Seite **Einstellungen**auf **Neu**.  

2.  Geben Sie auf der Registerkarte **Allgemein** des Dialogfelds **Einstellung erstellen** die folgenden Informationen an:  

    -   **Name:** Geben Sie einen eindeutigen Namen für die Einstellung ein. Sie können maximal 256 Zeichen verwenden.  

    -   **Beschreibung:** Geben Sie eine Beschreibung für die Einstellung ein. Sie können maximal 256 Zeichen verwenden.  

    -   **Einstellungstyp:** Wählen Sie in der Liste einen der folgenden Einstellungstypen aus, der für diese Einstellung verwendet werden soll, und konfigurieren Sie ihn:  

        -   **Active Directory-Abfrage**  

             **LDAP-Präfix** : Geben Sie ein gültiges Präfix für die Active Directory-Domänendienste-Abfrage an, mit der die Kompatibilität auf Clientcomputern bewertet wird. Verwenden Sie entweder **LDAP: / /** für einen oder **GC: / /** globalen Katalog gesucht werden soll.  

             **Distinguished Name (DN)** – Geben Sie den definierten Namen des Active Directory-Domänendienste-Objekts, das auf Clientcomputern auf Kompatibilität bewertet wird.  

             Wenn Sie beispielsweise einen Wert im Zusammenhang mit einem Benutzer namens John Smith in der Domäne "corp.contoso.com" auswerten möchten, geben Sie Folgendes ein:  

            -   **Suchfilter** : Geben Sie einen optionalen LDAP-Filter an, mit dem die Ergebnisse der Active Directory-Domänendiensteabfrage zur Bewertung der Kompatibilität auf Clientcomputern optimiert werden.  

                 Geben Sie zum Zurückzugeben aller Ergebnisse der Abfrage **(objectclass=\*)** ein.  

            -   **Suchbereich:** Geben Sie den Suchbereich in den Active Directory-Domänendiensten an. Sie können Folgendes auswählen:  

                -   **Basis** -Abfragen nur die angegebenen Objekts.  

                -   **Eine Ebene** – Diese Option wird in dieser Version von Configuration Manager nicht verwendet.  

                -   **Unterstruktur** -Abfragen die angegebenen Objekts und dessen vollständige untergeordnete Struktur im Verzeichnis.  

            -   **Eigenschaft** -Geben Sie die Eigenschaft des Active Directory-Domänendienste-Objekts, das zur Bewertung der Kompatibilität auf Clientcomputern verwendet wird.  

                 Beispielsweise, wenn Sie die Active Directory-Eigenschaft abfragen möchten **BadPwdCount**, die an, wie oft ein Benutzer ein Kennwort falsch eingibt speichert, geben Sie **BadPwdCount** in dieses Feld.  

            -   **Abfrage** -zeigt die Abfrage erstellt, die aus den Einträgen in **LDAP-Präfix**, **Distinguished Name (DN)**, **Suchfilter** (falls angegeben), und **Eigenschaft**, die zum Bewerten der Kompatibilität auf Clientcomputern verwendet werden.  

             Weitere Informationen zu LDAP-Abfragen erstellen finden Sie in der Windows Server-Dokumentation.  

        -   **Assembly**  

             Konfigurieren Sie Folgendes für diesen Einstellungstyp:  

            -   **Assemblyname:** Gibt den Namen der Assembly-Objekts, das Sie suchen möchten. Der Name kann nicht mit dem anderer Assemblyobjekte des gleichen Typs identisch sein und muss im globalen Assemblycache (Global Assembly Cache, GAC) registriert werden. Der Assemblyname kann bis zu 256 Zeichen lang sein.  

             Eine Assembly ist ein Programmcode, der zwischen Anwendungen freigegeben werden kann. Assemblys können die Dateinamenerweiterung DLL oder EXE haben. Der globale Assemblycache ist ein Ordner namens *%systemroot%\Assembly* auf Clientcomputern, in dem alle freigegebenen Assemblys gespeichert werden.  

        -   **Dateisystem**  

            -   **Typ** : Wählen Sie in der Liste aus, ob Sie nach einer **Datei** oder nach einem **Ordner**suchen möchten.  

            -   **Pfad** – Geben Sie den Pfad der angegebenen Datei bzw. des Ordners auf Clientcomputern. Sie können Systemumgebungsvariablen und die Umgebungsvariable *%USERPROFILE%* im Pfad angeben.  

                > [!NOTE]  
                >  Wenn Sie die Umgebungsvariable *%USERPROFILE%* in den Feldern **Pfad** oder **Datei- oder Ordnername** verwenden, werden alle Benutzerprofile auf dem Clientcomputer durchsucht, was dazu führen kann, dass mehrere Instanzen einer Datei oder eines Ordners gefunden werden.  
                >   
                >  Wenn die Kompatibilitätseinstellungen keinen Zugriff auf den angegebenen Pfad haben, wird ein Ermittlungsfehler generiert. Wenn die gesuchte Datei zurzeit verwendet wird, wird außerdem ein Ermittlungsfehler generiert.  

            -   **Datei-oder Ordnernamen** – Geben Sie den Namen des zu suchenden Objekts Datei oder eines Ordners. Sie können Systemumgebungsvariablen und die *%USERPROFILE%* -Umgebungsvariable im Datei- oder Ordnernamen angeben. Sie können auch die Platzhalter * und ? im Dateinamen verwenden.  

                > [!NOTE]  
                >  Wenn Sie einen Datei- oder Ordnernamen angeben und Platzhalter verwenden, kann diese Kombination dazu führen, dass zahlreiche Ergebnisse generiert werden, die Ressourcen auf dem Clientcomputer stark beansprucht werden und bei der Übertragung der Ergebnisse an Configuration Manager ein hoher Netzwerkdatenverkehr entsteht.  

            -   **Unterordner einschließen** : Aktivieren Sie diese Option, wenn auch Unterordner unter dem angegebenen Pfad durchsucht werden sollen.  

            -   **Datei oder des Ordners ist ein 64-Bit-Anwendung zugeordnet** – Wenn aktiviert, nur 64-Bit-Speicherorte (wie z. B. *% ProgramFiles%*) wird auf 64-Bit-Computern aktiviert werden. Wenn diese Option nicht aktiviert ist, werden sowohl 32-Bit-Speicherorte (z. B. *%ProgramFiles(x86)%*) als auch 64-Bit-Speicherorte überprüft.  

                > [!NOTE]  
                >  Wenn dieselbe Datei bzw. derselbe Ordner sowohl am 64-Bit-Systemdatei- als auch am 32-Bit-Systemdateispeicherort desselben 64-Bit-Computers vorhanden ist, werden von der globalen Bedingung mehrere Dateien ermittelt.  

             Die Angabe eines UNC-Pfads zu einer Netzwerkfreigabe im Feld **Pfad** wird vom Einstellungstyp **Dateisystem** nicht unterstützt.  

        -   **IIS-Metabasis**  

            -   **Metabasispfad** : Geben Sie einen gültigen Pfad zur IIS-Metabasis (Internetinformationsdienste) an.  

            -   **Eigenschafts-ID** : Geben Sie die numerische Eigenschaft der IIS-Metabasiseinstellung an.  

        -   **Registrierungsschlüssel**  

            -   **Struktur** : Wählen Sie aus der Liste die Registrierungsstruktur aus, die durchsucht werden soll.  

            -   **Schlüssel** : Geben Sie den Namen des Registrierungsschlüssels an, nach dem gesucht werden soll. Verwenden Sie das Format *schlüssel\unterschlüssel*.  

            -   **Dieser Registrierungsschlüssel ist einer 64-Bit-Anwendung zugeordnet** -gibt an, ob die 64-Bit-Registrierungsschlüssel zusätzlich zu den 32-Bit-Registrierungsschlüsseln auf Clients durchsucht werden sollen, die eine 64-Bit-Version von Windows ausgeführt werden.  

                > [!NOTE]  
                >  Wenn derselbe Registrierungsschlüssel sowohl in der 64-Bit-Registrierung als auch in der 32-Bit-Registrierung desselben 64-Bit-Computers vorhanden ist, werden von der globalen Bedingung beide Registrierungsschlüssel ermittelt.  

        -   **Registrierungswert**  

            -   **Struktur** : Wählen Sie aus der Liste die Registrierungsstruktur aus, die durchsucht werden soll.  

            -   **Schlüssel** : Geben Sie den Namen des Registrierungsschlüssels an, nach dem gesucht werden soll. Verwenden Sie das Format *schlüssel\unterschlüssel*.  

            -   **Wert** : Geben Sie den Wert an, der im angegebenen Registrierungsschlüssel enthalten sein muss.  

            -   **Dieser Registrierungsschlüssel ist einer 64-Bit-Anwendung zugeordnet** : Gibt an, ob auf Clients mit einer 64-Bit-Version von Windows die 64-Bit-Registrierungsschlüssel zusätzlich zu den 32-Bit-Registrierungsschlüsseln gesucht werden sollen.  

                > [!NOTE]  
                >  Wenn derselbe Registrierungsschlüssel sowohl in der 64-Bit-Registrierung als auch in der 32-Bit-Registrierung desselben 64-Bit-Computers vorhanden ist, werden von der globalen Bedingung beide Registrierungsschlüssel ermittelt.  

             Sie können auch auf **Durchsuchen** klicken, um zu einem Registrierungspfad auf dem Computer oder einem Remotecomputer zu navigieren. Um einen Remotecomputer zu durchsuchen, benötigen Sie Administratorrechte auf dem Remotecomputer, und der Remotecomputer muss den Remoteregistrierungsdienst ausgeführt werden.  

        -   **Skript**  

            -   **Ermittlungsskript** – klicken Sie auf **Hinzufügen** , um ein zu verwendendes Skript einzugeben oder zu suchen. Sie können Windows PowerShell, VBScript oder Microsoft JScript-Skripts verwenden.  

            -   **Skripts durch Verwendung der Anmeldeinformationen angemeldeter Benutzer ausführen** : Wenn Sie diese Option aktivieren, wird das Skript auf Clientcomputern ausgeführt, die die Anmeldeinformationen der angemeldeten Benutzer verwenden.  

                > [!NOTE]  
                >  Der Wert, der vom Skript zurückgegeben wird, wird zur Bewertung der Kompatibilität der globalen Bedingung verwendet. Bei der Verwendung von VBScript können Sie beispielsweise den Befehl **WScript.Echo Result** verwenden, um den Wert der *Result* -Variablen an die globale Bedingung zurückzugeben.  

        -   **SQL-Abfrage**  

            -   **SQL Server-Instanz** – Wählen Sie aus, ob die SQL-Abfrage auf der Standardinstanz, allen Instanzen oder einem bestimmten Datenbankinstanznamen ausgeführt werden soll.  

                > [!NOTE]  
                >  Der Instanzname muss sich auf eine lokale Instanz von SQL Server beziehen. Verwenden Sie eine Skripteinstellung, um sich auf eine gruppierte SQL-Serverinstanz zu beziehen.  

            -   **Datenbank** – Geben Sie den Namen der Microsoft SQL Server-Datenbank für die SQL-Abfrage ausgeführt werden soll.  

            -   **Spalte** – Geben Sie den Namen der Spalte zurückgegeben, die von der Transact-SQL-Anweisung, die zur Bewertung der Kompatibilität der globalen Bedingung verwendet.  

            -   **Transact-SQL-Anweisung** – Geben Sie die vollständige SQL-Abfrage an, die Sie für die globale Bedingung verwenden möchten. Sie können zum Öffnen einer vorhandenen SQL-Abfrage auch auf **Öffnen** klicken.  

                > [!IMPORTANT]  
                >  SQL-Abfrageeinstellungen unterstützen keine SQL-Befehle, durch die die Datenbank geändert wird. Sie können nur SQL-Befehle verwenden, mit denen Informationen aus der Datenbank gelesen werden.  

        -   **WQL-Abfrage**  

            -   **Namespace** – Geben Sie den Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI)-Namespace dient zum Erstellen einer WQL-Abfrage, deren Kompatibilität auf Clientcomputern bewertet wird. Der Standardwert ist "Root\cimv2".  

            -   **Klasse** -gibt die WMI-Klasse dient zum Erstellen einer WQL-Abfrage, deren Kompatibilität auf Clientcomputern bewertet wird.  

            -   **Eigenschaft** -gibt die WMI-Eigenschaft dient zum Erstellen einer WQL-Abfrage, deren Kompatibilität auf Clientcomputern bewertet wird.  

            -   **WQL-Abfrage, WHERE-Klausel** : Mithilfe des Elements **WQL-Abfrage, WHERE-Klausel** können Sie eine WHERE-Klausel angeben, die auf Clientcomputern auf den angegebenen Namespace, die Klasse und die Eigenschaft angewendet wird.  

        -   **XPath-Abfrage**  

            -   **Pfad** – Geben Sie den Pfad zur XML-Datei auf Clientcomputern an, die zur Bewertung der Kompatibilität verwendet wird. Configuration Manager unterstützt im Pfadnamen die Verwendung aller Windows-Systemumgebungsvariablen und der Benutzervariablen *%USERPROFILE%*.  

            -   **XML-Dateiname** – Geben Sie den Dateinamen, die mit der XML-Abfrage, die zur Bewertung der Kompatibilität auf Clientcomputern verwendet wird.  

            -   **Unterordner einschließen** – Aktivieren Sie diese Option, wenn auch Unterordner unter dem angegebenen Pfad durchsucht werden sollen.  

            -   **Diese Datei ist mit einer 64-Bit-Anwendung verknüpft** – Geben Sie an, ob der Speicherort der 64-Bit-Systemdatei (*%windir%*\System32) zusätzlich zum Speicherort der 32-Bit-Systemdatei (*%windir%*\Syswow64) auf Configuration Manager-Clients durchsucht werden soll, auf denen eine 64-Bit-Version von Windows ausgeführt wird.  

            -   **XPath-Abfrage** – Geben Sie eine gültige vollständige XML Path Language (XPath)-Abfrage, die zur Bewertung der Kompatibilität auf Clientcomputern verwendet wird.  

            -   **Namespaces** – öffnet das Dialogfeld **XML-Namespaces** zum Identifizieren von Namespaces und Präfixen, die bei der XPath-Abfrage verwendet werden sollen.  

             Wenn Sie versuchen, eine verschlüsselte XML-Datei zu ermitteln, wird diese Datei zwar durch die Kompatibilitätseinstellungen gefunden, die XPath-Abfrage führt jedoch zu keinen Ergebnissen. Es wird auch kein Fehler generiert.  

             Wenn die XPath-Abfrage ungültig ist, wird die Einstellung auf Clientcomputern als nicht kompatibel bewertet.  

    -   **Datentyp** : Wählen Sie aus der Liste das Format aus, in dem die Daten von der Bedingung zurückgegeben werden, bevor sie zum Bewerten der Einstellung verwendet werden. Die **Datentyp** Liste ist nicht für alle Einstellungstypen angezeigt.  

        > [!NOTE]  
        >  Vom Datentyp **Gleitkomma** werden nur 3 Ziffern nach dem Dezimalkomma unterstützt.  

3.  Konfigurieren Sie zusätzliche Details zu dieser Einstellung unter der **Einstellungstyp** Liste. Die Elemente, die Sie konfigurieren können, variiert je nach Einstellung, die Sie ausgewählt haben.  

    > [!NOTE]  
    >  Beim Erstellen von Einstellungen des Typs **Dateisystem**, **Registrierungsschlüssel**, und **Registrierungswert**, klicken Sie auf **Durchsuchen** die Einstellung von Werten auf einem Referenzcomputer zu konfigurieren. Um einen Registrierungsschlüssel oder-Wert auf einem Remotecomputer zu suchen, muss der Remotecomputer den Remoteregistrierungsdienst aktiviert haben.  

4.  Klicken Sie auf **OK** , um die Einstellung zu speichern, und schließen Sie das Dialogfeld **Einstellung erstellen** .  

##  <a name="configure-compliance-rules"></a>Konfigurieren von Kompatibilitätsregeln  
 Gehen Sie wie folgt vor, um Kompatibilitätsregeln für das Konfigurationselement zu konfigurieren.  

 Mit Kompatibilitätsregeln werden die Bedingungen angegeben, mit denen die Kompatibilität eines Konfigurationselements definiert wird. Damit eine Einstellung auf Kompatibilität bewertet werden kann, muss sie über mindestens eine Kompatibilitätsregel verfügen. WMI, Registrierung und skripteinstellungen können Sie die Werte zu beheben, die gefunden werden, nicht kompatibel ist. Sie können neue Regeln erstellen oder suchen Sie eine vorhandene Einstellung innerhalb eines beliebigen Konfigurationselements auf Regeln aktivieren.  

### <a name="to-create-a-compliance-rule"></a>So erstellen Sie eine Kompatibilitätsregel  

1.  Klicken Sie im **Assistenten zum Erstellen von Konfigurationselementen** auf der Seite **Kompatibilitätsregeln**auf **Neu**.  

2.  Geben Sie im Dialogfeld **Regel erstellen** die folgenden Informationen an:  

    -   **Name:** Geben Sie einen Namen für die Kompatibilitätsregel ein.  

    -   **Beschreibung:** Geben Sie eine Beschreibung für die Kompatibilitätsregel ein.  

    -   **Ausgewählte Einstellung:** Klicken Sie auf **Durchsuchen** So öffnen die **Einstellung auswählen** (Dialogfeld). Wählen Sie die Einstellung, die Sie verwenden möchten, eine Regel definieren, oder klicken Sie auf **neue Einstellung**. Klicken Sie dann auf **Auswählen**.  

        > [!NOTE]  
        >  Sie können zum Anzeigen von Informationen über die derzeit ausgewählte Einstellung auch auf **Eigenschaften** klicken.  

    -   **Regeltyp:** Wählen Sie den Typ der Compliance-Regel, die Sie verwenden möchten:  

        -   **Wert** erstellen Sie eine Regel, die den Rückgabewert von das Konfigurationselement mit einem von Ihnen angegebenen Wert vergleicht.  

        -   **Existenziell** erstellen Sie eine Regel, die ausgewertet wird die Einstellung abhängig davon, ob es vorhanden ist, auf einem Client-Gerät oder an, wie oft sie gefunden wird.  

    -   Geben Sie für eine Regel des Typs **Wert**die folgenden Informationen an:  

        -   **Die Einstellung muss die folgende Regel entsprechen** – wählen Sie einen Operator und einen Wert, der mit der ausgewählten Einstellung auf Kompatibilität bewertet wird. Folgende Operatoren können verwendet werden:  

            |Operator|Weitere Informationen|  
            |--------------|----------------------|  
            |Gleich|keine zusätzlichen Informationen|  
            |Ungleich|keine zusätzlichen Informationen|  
            |Größer als|keine zusätzlichen Informationen|  
            |Kleiner als|keine zusätzlichen Informationen|  
            |Zwischen|keine zusätzlichen Informationen|  
            |Größer als oder gleich|keine zusätzlichen Informationen|  
            |Kleiner als oder gleich|keine zusätzlichen Informationen|  
            |Eine von|Geben Sie im Textfeld pro Zeile einen Eintrag an.|  
            |Keine von|Geben Sie im Textfeld pro Zeile einen Eintrag an.|  

        -   **Nicht kompatible Regeln wiederherstellen, falls dies unterstützt wird** : Wählen Sie diese Option aus, wenn nicht kompatible Regeln von Configuration Manager automatisch wiederhergestellt werden sollen. Von Configuration Manager können automatisch folgende Regeltypen behoben werden:  

            -   **Registrierungswert** – der Registrierungswert wurde wiederhergestellt, wenn er nicht konform ist, ist und erstellt, wenn er nicht vorhanden ist.  

            -   **Skript** – (durch das automatische Ausführen eines Wiederherstellungsskripts)  

            -   **WQL-Abfrage**  

            > [!IMPORTANT]  
            >  Sie können nicht kompatible Regeln nur wiederherstellen, wenn der Regeloperator auf **Ist gleich**festgelegt ist.  

        -   **Nichtkompatibilität gemeldet, wenn diese Einstellung nicht gefunden wird** – das Konfigurationselement meldet Nichtkompatibilität, wenn diese Einstellung nicht auf Clientcomputern gefunden wird.  

        -   **Schweregrad der Nichtkompatibilität für Berichte:** Geben Sie den Schweregrad an, der in Configuration Manager-Berichten gemeldet wird, wenn bei dieser Kompatibilitätsregel ein Fehler auftritt. Die folgenden Schweregrade sind verfügbar:  

            -   **Keine** – Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad gemeldet.  

            -   **Informationen** – Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Informationen** gemeldet.  

            -   **Warnung** – Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** gemeldet.  

            -   **Kritisch** – Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet.  

            -   **Kritisch mit Ereignis** – Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  

        -   Geben Sie für eine Regel des Typs **Existenziell**die folgenden Informationen an:  

            > [!NOTE]  
            >  Die angezeigten Optionen sind möglicherweise unterschiedlich, je nach Einstellungstyp, für den Sie eine Regel konfigurieren.  

            -   **Diese Einstellung muss auf Clientgeräten vorhanden sein.**  

            -   **Diese Einstellung darf auf Clientgeräten nicht vorhanden sein.**  

            -   **Häufigkeit des Auftretens dieser Einstellung:**  

        -   **Schweregrad der Nichtkompatibilität für Berichte:** Geben Sie den Schweregrad an, der in Configuration Manager-Berichten gemeldet wird, wenn bei dieser Kompatibilitätsregel ein Fehler auftritt. Die folgenden Schweregrade sind verfügbar:  

            -   **Keine** – Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad gemeldet.  

            -   **Informationen** – Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Informationen** gemeldet.  

            -   **Warnung** – Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** gemeldet.  

            -   **Kritisch** – Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet.  

            -   **Kritisch mit Ereignis** – Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  

3.  Klicken Sie auf **OK** , um das Dialogfeld **Regel erstellen** zu schließen.  

##  <a name="specify-supported-platforms"></a>Angeben unterstützter Plattformen  
 Unterstützte Plattformen sind die Betriebssysteme, auf denen die Kompatibilität von Konfigurationselementen bewertet wird.  

Wählen Sie aus der Liste auf der Seite **Unterstützte Plattformen** des **Assistenten zum Erstellen von Konfigurationselementen**die Windows-Versionen aus, auf denen die Kompatibilität des Konfigurationselements bewertet werden soll, oder klicken Sie auf **Alle auswählen**.  

## <a name="complete-the-wizard"></a>Abschließen des Assistenten  
 Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die auszuführenden Aktionen, und schließen Sie dann den Assistenten ab. Das neue Konfigurationselement wird angezeigt, der **Konfigurationselemente** Knoten in der **Bestand und Kompatibilität** Arbeitsbereich.  
