---
title: Bereitstellen von UNIX/Linux-Clients | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Clients auf UNIX- oder Linux-Servern in System Center Configuration Manager bereitstellen.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d61d53daa5ef3d9c986cba8791d4471fea94d29d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-system-center-configuration-manager"></a>Bereitstellen von Clients auf UNIX- und Linux-Servern in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bevor Sie einen Linux- oder UNIX-Server mit System Center Configuration Manager verwalten können, müssen Sie den Configuration Manager-Client für Linux und UNIX auf jedem Linux- oder UNIX-Server installieren. Sie können die Clientinstallation auf jedem Computer manuell ausführen oder ein Shellskript verwenden, um den Client remote zu installieren. Configuration Manager unterstützt keine Clientpushinstallation für Linux- oder UNIX-Server. Optional können Sie ein Runbook für System Center Orchestrator konfigurieren, um die Clientinstallation auf dem Linux- oder UNIX-Server zu automatisieren.  

 Unabhängig von der verwendeten Installationsmethode erfordert der Installationsvorgang die Verwendung eines Skripts namens **install** , um den Installationsvorgang zu verwalten. Dieses Skript ist enthalten, wenn Sie den Client für Linux und UNIX herunterladen.  

 Das Installationsskript für den Configuration Manager-Client für Linux und UNIX unterstützt Befehlszeileneigenschaften. Einige Befehlszeileneigenschaften sind erforderlich, während andere optional sind. Bei der Installation des Clients müssen Sie z. B. einen Verwaltungspunkt, von der Website angeben, die von Linux oder UNIX-Server für den ersten Kontakt mit dem Standort verwendet wird. Die vollständige Liste der Befehlszeileneigenschaften finden Sie unter [Befehlszeileneigenschaften zur Installation des Clients auf Linux- und UNIX-Servern](#BKMK_CmdLineInstallLnUClient).  

 Nach der Installation des Clients geben Sie die Clienteinstellungen in der Configuration Manager-Konsole an, um den Client-Agent auf die gleiche Weise wie Windows-basierte Clients zu konfigurieren. Weitere Informationen finden Sie unter  [Client settings for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="BKMK_AboutInstallPackages"></a> Informationen zu Clientinstallationspaketen und der universelle Agent  
 Um den Client für Linux und UNIX auf einer bestimmten Plattform zu installieren, müssen Sie das entsprechende Clientinstallationspaket für den Computer verwenden, auf dem Sie den Client installieren. Die jeweiligen Clientinstallationspakete sind in jedem Clientdownload aus dem [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184)enthalten. Zusätzlich zu den Clientinstallationspaketen umfasst das Clientdownload das **install** -Skript zur Verwaltung der Clientinstallation auf den einzelnen Computern.  

 Wenn Sie einen Client installieren, können Sie die gleichen Prozess und Befehlszeile Eigenschaften unabhängig von der Client-Installationspaket, die Sie verwenden.  

 Informationen zu den Betriebssystemen, Plattformen und Clientinstallationspaketen, die von den einzelnen Releases des Configuration Manager-Clients für Linux und UNIX unterstützt werden, finden Sie unter [Linux- und UNIX-Server](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#linux-and-unix-servers).  

##  <a name="BKMK_InstallLnUClient"></a> Installieren Sie den Client auf Linux- und UNIX-Servern  
 Zum Installieren des Clients für Linux und UNIX, führen Sie ein Skript auf jedem Linux- oder UNIX-Computer. Das Skript heißt **Installieren** und unterstützt Eigenschaften, über die Befehlszeile, die das Installationsverhalten zu ändern und das Client-Installationspaket zu verweisen. Das Skript und Client-Installation Installationspaket muss auf dem Client befinden. Das Clientinstallationspaket enthält die Configuration Manager-Clientdateien für ein bestimmtes Linux oder UNIX-Betriebssystem und die entsprechende Plattform.
Jeder Client-Installationspaket enthält die erforderlichen Dateien zum Abschließen der Clientinstallations und im Gegensatz zu Windows-basierten Computern wird nicht heruntergeladen zusätzliche Dateien aus einem Verwaltungspunkt oder andere Quellspeicherort.  

 Nach der Installation des Configuration Manager-Clients für Linux und UNIX muss der Computer nicht neu gestartet werden. Sobald die Softwareinstallation abgeschlossen ist, kann der Client betrieben werden. Wenn Sie den Computer neu starten, wird auch der Configuration Manager-Client automatisch neu gestartet.  

 Der installierte Client führt mit Root-Anmeldeinformationen. Stammanmeldeinformationen sind erforderlich, um Hardwareinventurdaten zu sammeln und die Softwarebereitstellung auszuführen.  

 Das Befehlsformat lautet wie folgt:  

 **./install -mp &lt;Computer\> -sitecode &lt;Standortcode\> &lt;Eigenschaft #1> &lt;<Eigenschaft #2> &lt;Clientinstallationspaket\>**  

-   **Installation** ist der Name der Skriptdatei, die vom Client für Linux und UNIX installiert. Diese Datei wird mit der Client-Software bereitgestellt.  

-   **-mp &lt;Computer** gibt den ersten Verwaltungspunkt an, der vom Client verwendet wird.  

     Beispiel: smsmp.contoso.com  

-   **-sitecode &lt;Standortcode\>** gibt den Standortcode an, dem der Client zugewiesen wurde.  

     Beispiel: S01  

-   &lt;Eigenschaft #1>&lt;Eigenschaft #2> gibt die mit dem Installationsskript zu verwendenden Befehlszeileneigenschaften an.  

    > [!NOTE]  
    >  Weitere Informationen finden Sie unter [Befehlszeileneigenschaften zur Installation des Clients auf Linux- und UNIX-Servern](#BKMK_CmdLineInstallLnUClient)  

-   Das**Clientinstallationspaket** ist der Name des TAR-Pakets der Clientinstallation für das Betriebssystem, die Version und die CPU-Architektur des Computers. Die Client-Installation TAR-Datei muss zuletzt angegeben werden.  

     Beispiel: ccm-Universal-x64.&lt;build\>.tar  

###  <a name="BKMK_ToInstallLnUClinent"></a> So installieren Sie Configuration Manager-Client auf Linux- und UNIX-Servern  

1.  Auf einem Windows-Computer müssen Sie [die entsprechende Clientdatei für den Linux- oder UNIX-Server herunterladen](http://go.microsoft.com/fwlink/?LinkID=525184) , den Sie verwalten möchten.  

2.  Führen Sie die selbstextrahierende EXE-Datei auf dem Windows-Computer aus, um das Installationsskript und die TAR-Datei für die Clientinstallation zu extrahieren.  

3.  Kopieren Sie das **install** -Skript und die TAR-Datei in einen Ordner auf dem Server, den Sie verwalten möchten.  

4.  Führen Sie auf dem UNIX- oder Linux-Server den folgenden Befehl aus, um die Ausführung des Skripts als Programm zu ermöglichen: **chmod +x install**  

    > [!IMPORTANT]  
    >  Sie müssen Anmeldeinformationen zum Installieren des Clients verwenden.  

5.  Führen Sie nun den folgenden Befehl aus, um den Configuration Manager-Client zu installieren: **./install -mp &lt;Hostname\> -sitecode &lt;code\> ccm-Universal-x64.&lt;build\>.tar**  

     Wenn Sie diesen Befehl eingeben, verwenden Sie zusätzliche Befehlszeileneigenschaften, die Sie benötigen.  Die Liste der Befehlszeileneigenschaften finden Sie unter [Befehlszeileneigenschaften zur Installation des Clients auf Linux- und UNIX-Servern](#BKMK_CmdLineInstallLnUClient).  

6.  Nachdem das Skript ausgeführt wurde, überprüfen Sie die Installation anhand der Datei **/var/opt/microsoft/scxcm.log** . Darüber hinaus können Sie überprüfen, ob der Client installiert wurde und mit dem Standort kommuniziert, indem Sie die Details für den betreffenden Client unter dem Knoten **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole anzeigen.  

###  <a name="BKMK_CmdLineInstallLnUClient"></a> Befehlszeileneigenschaften zur Installation des Clients auf Linux- und UNIX-Servern  
 Die folgenden Eigenschaften sind zum Ändern des Verhaltens des Installationsskripts verfügbar:  

> [!NOTE]  
>  Verwenden Sie die Eigenschaft **-h** Anzeigen der Liste der unterstützten Eigenschaften.  

-   **-mp &lt;FQDN des Servers\>**  

     Erforderlich. Gibt an, über den FQDN des Management Point Server, die vom Client als eine Anlaufstelle verwendet wird.  

    > [!IMPORTANT]  
    >  Diese Eigenschaft dient nicht zur Angabe des Verwaltungspunkts, dem der Client nach der Installation zugewiesen wird.  

    > [!NOTE]  
    >  Wenn Sie mit der **-mp** -Eigenschaft einen Verwaltungspunkt angeben, der ausschließlich für die Annahme von HTTPS-Clientverbindungen konfiguriert ist, müssen Sie außerdem die **-UsePKICert** -Eigenschaft verwenden.  

-   **-sitecode &lt;Standortcode\>**  

     Erforderlich. Gibt den primären Configuration Manager-Standort an, um diesem den Configuration Manager-Client zuzuweisen.  

     Beispiel: -sitecode S01  

-   **-fsp &lt;Server-FQDN>**  

     (Optional) Gibt an, über den FQDN der Fallbackstatuspunkt-Server, die der Client verwendet, um Status-Nachrichten zu senden.  

     Weitere Informationen zum Fallbackstatuspunkt finden Sie unter [Determine Whether You Require a Fallback Status Point](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point) .  


-   **-dir &lt;Verzeichnis\>**  

     (Optional) Gibt einen alternativen Speicherort zum Installieren der Configuration Manager-Clientdateien an.  

     Standardmäßig wird vom Client an den folgenden Speicherort installiert: **/opt/microsoft**.  

-   **-nostart**  

     (Optional) Verhindert den automatischen Start des Configuration Manager-Clientdiensts **ccmexec.bin**, nachdem die Clientinstallation abgeschlossen wurde.  

     Nach der Installation auf dem Client müssen Sie den Client-Dienst manuell starten.  

     Standardmäßig beginnt der Client-Dienst nach Abschluss der Clientinstallations und bei jedem des Computers Neustart.  

-   **-Bereinigen**  

     (Optional) Gibt an, dass alle Clientdateien und Daten von einem zuvor installierten Client für Linux und UNIX, vor Beginn der neue Installation. Dadurch werden Datenbank und Zertifikatspeicher des Clients entfernt.  

-   **-keepdb**  

     (Optional) Gibt an, dass die lokalen Client-Datenbank beibehalten und erneut verwendet, wenn Sie einen Client neu installieren. Wenn Sie einen Client neu installieren, wird standardmäßig dieser Datenbank gelöscht.  

-   **-UsePKICert &lt;Parameter\>**  

     (Optional) Gibt den vollständigen Pfad und Namen mit einem x. 509-PKI-Zertifikat im Format Public Key Certificate Standard (PKCS #12). Dieses Zertifikat wird zur Client-Authentifizierung verwendet. Wenn während der Installation kein Zertifikat angegeben wird und Sie ein Zertifikat hinzufügen oder ändern müssen, verwenden Sie das Hilfsprogramm **certutil** . Weitere Informationen zu „certutil“ finden Sie unter [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) .  

     Bei Verwendung von **-UsePKICert**müssen Sie außerdem den Befehlszeilenparameter **-certpw** verwenden, um das der PKCS#12-Datei zugeordnete Kennwort anzugeben.  

     Wenn Sie diese Eigenschaft nicht an eine PKI-Zertifikat verwenden, der Client ein selbstsigniertes Zertifikat verwendet, und die gesamte Kommunikation mit Standortsystemen erfolgt über HTTP.  

     Bei Angabe ein ungültiges Zertifikats auf den Client über die Befehlszeile zu installieren, werden keine Fehler zurückgegeben. Dies ist, da die zertifikatüberprüfung erfolgt nach der Installation auf dem Client. Wenn der Client gestartet wird, Zertifikate mit dem Verwaltungspunkt überprüft werden und bei einem Überprüfungsfehler für ein Zertifikat wird die folgende Meldung, in angezeigt **scxcm.log**, die Clientprotokolldatei UNIX- und Linux-Konfigurations-Manager: **Fehler überprüfen das Zertifikat für den Verwaltungspunkt**. Der Standardspeicherort der Protokolldatei ist:  **/var/opt/microsoft/scxcm.log**.  

    > [!NOTE]  
    >  Sie müssen diese Eigenschaft immer angeben, wenn Sie einen Client installieren, und die Eigenschaft **-mp** verwenden, um einen Verwaltungspunkt anzugeben, der ausschließlich für Clientverbindungen über HTTPS konfiguriert ist.  

     Beispiel: UsePKICert &lt;Vollständiger Pfad- und Dateiname\> -certpw &lt;Kennwort\>  

-   **-certpw &lt;Parameter\>**  

     (Optional) Gibt das Kennwort mit der angegebenen PKCS #12-Datei mithilfe der der **- UsePKICert** Eigenschaft.  

     Beispiel: UsePKICert &lt;Vollständiger Pfad- und Dateiname\> -certpw &lt;Kennwort\>  

-   **-NoCRLCheck**  

     (Optional) Gibt an, dass ein Client nicht der Zertifikatssperrliste (CRL überprüft) bei der Kommunikation über HTTPS mithilfe der PKI-Zertifikat. Wenn diese Option nicht angegeben wird, überprüft der Client die Zertifikatsperrliste vor dem Einrichten einer HTTPS-Verbindungs mithilfe von PKI-Zertifikaten. Weitere Informationen zu Client CRL-Prüfung finden Sie unter Planen der PKI-zertifikatsperrung.  

     Beispiel: -UsePKICert &lt;Vollständiger Pfad- und Dateiname\> -certpw &lt;Kennwort\> -NoCRLCheck  

-   **-rootkeypath &lt;Dateispeicherort\>**  

     (Optional) Hiermit werden der vollständige Pfad- und Dateiname des vertrauenswürdigen Configuration Manager-Stammschlüssels angegeben. Der vertrauenswürdige Configuration Manager-Stammschlüssel bietet einen Mechanismus, mit den Linux- und UNIX-Clients überprüfen können, ob sie mit einem Standortsystem verbunden sind, das der richtigen Hierarchie angehört.  

     Wenn Sie den vertrauenswürdigen Stammschlüssel nicht in der Befehlszeile angeben, vertraut der Client dem ersten Verwaltungspunkt, mit dem er kommuniziert, und ruft automatisch den vertrauenswürdigen Stammschlüssel von diesem Verwaltungspunkt ab.  

     Weitere Informationen finden Sie unter  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Beispiel: -rootkeypath &lt;Vollständiger Pfad- und Dateiname\>  

-   **-httpport &lt;Port\>**  

     (Optional) Gibt den Port an, der für Verwaltungspunkte konfiguriert ist, die vom Client verwendet wird, wenn die Kommunikation mit Verwaltungspunkten über HTTP. Wenn der Anschluss nicht angegeben wird, ist der Standardwert 80 verwendet.  

     Beispiel: -httpport 80  

-   **-httpsport &lt;Port\>**  

     (Optional) Gibt den Port an, der für Verwaltungspunkte, der Client konfiguriert ist bei der Kommunikation mit Verwaltungspunkten über HTTPS verwendet. Wenn der Anschluss nicht angegeben wird, ist der Standardwert 443 verwendet.  

     Beispiel: UsePKICert &lt;Vollständiger Pfad- und Zertifikatname\> -httpsport 443  

-   **-ignoreSHA256validation**  

     (Optional) Gibt an, dass die Clientinstallation SHA-256-Überprüfung übersprungen. Verwenden Sie diese Option bei der Installation des Clients unter Betriebssystemen, die ohne OpenSSL-Version mit SHA-256-Unterstützung freigegeben wurden. Weitere Informationen finden Sie unter [About Linux and UNIX Operating Systems That do not Support SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   **-signcertpath&lt; Dateispeicherort\>**  

     (Optional) Gibt den vollständigen Pfad und **CER** Dateinamen des exportierten selbstsignierten Zertifikats auf dem Standortserver. Wenn die PKI-Zertifikate nicht verfügbar sind, generiert der Configuration Manager-Standortserver automatisch selbstsignierte Zertifikate.  

     Diese Zertifikate werden verwendet, um sicherzustellen, dass die Clientrichtlinien vom Verwaltungspunkt heruntergeladen aus dem gewünschten Standort gesendet wurden. Wenn während der Installation kein selbstsigniertes Zertifikat angegeben wird und Sie das Zertifikat ändern müssen, verwenden Sie das Hilfsprogramm **certutil** . Weitere Informationen zu „certutil“ finden Sie unter [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) .  

     Dieses Zertifikat kann über den **SMS** -Zertifikatspeicher unter dem Antragstellernamen **Standortserver** und dem Anzeigenamen **Signaturzertifikat des Standortservers**abgerufen werden.  

     Wenn diese Option während der Installation nicht angegeben wird, vertrauen Linux- und UNIX-Clients den ersten Verwaltungspunkt kommunizieren, und das Signaturzertifikat wird automatisch vom Verwaltungspunkt abgerufen.  

     Beispiel: -Signcertpath &lt;Vollständiger Pfad- und Dateiname\>  

-   **-rootcerts**  

     (Optional) Gibt zusätzliche PKI-Zertifikate zu importieren, die nicht Teil einer Management Punkte Zertifizierungshierarchie Zertifizierungsstelle (CA). Wenn Sie mehrere Zertifikate in der Befehlszeile angeben, sollten sie durch Trennzeichen getrennt sein.  

     Verwenden Sie diese Option, wenn Sie PKI-Clientzertifikate verwenden, die nicht auf ein Zertifikat einer Stammzertifizierungsstelle verkettet, die vom Verwaltungspunkt Sites als vertrauenswürdig eingestuft wird. Verwaltungspunkte lehnen den Client ab, wenn das Clientzertifikat nicht mit einem vertrauenswürdigen Stammzertifikat in der Zertifikatausstellerliste des Standorts verkettet ist.  

     Wenn Sie diese Option nicht verwenden, überprüft der Client für Linux und UNIX die Vertrauenshierarchie nur das Zertifikat in der **- UsePKICert** Option.  

     Beispiel: -Rootcerts &lt;Vollständiger Pfad- und Dateiname\>,&lt; Vollständiger Pfad- und Dateiname\>  

###  <a name="BKMK_UninstallLnUClient"></a> So deinstallieren Sie den Client von Linux- und UNIX-Servern  
 Zum Deinstallieren des Configuration Manager-Clients für Linux und UNIX verwenden Sie das Hilfsprogramm **uninstall**. Standardmäßig befindet sich diese Datei der **/opt/Microsoft/Configuration Manager/Bin/** Ordner auf dem Clientcomputer. Dieser Befehl uninstall unterstützt keine Befehlszeilenparameter und alle Dateien, die im Zusammenhang mit der Clientsoftware, vom Server entfernt.  

 Um den Client zu deinstallieren, verwenden Sie die folgende Befehlszeile: **/opt/microsoft/configmgr/bin/uninstall**  

 Sie müssen nach der Deinstallation des Configuration Manager-Clients für Linux und UNIX den Computer nicht neu starten.  

##  <a name="BKMK_ConfigLnUClientCommuincations"></a> Konfigurieren von Anforderungsports für den Client für Linux und UNIX  
 Ähnlich wie Windows-basierte Clients verwendet der Configuration Manager-Client für Linux und UNIX HTTP und HTTPS zur Kommunikation mit Configuration Manager-Standortsystemen. Die Ports, die der Configuration Manager-Client für die Kommunikation verwendet, werden als Anforderungsports bezeichnet.  

 Wenn Sie den Configuration Manager-Client für Linux und UNIX installieren, können Sie die Standardanforderungsports des Clients ändern, indem Sie die Installationseigenschaften **-httpport** und **-httpsport** angeben. Wenn Sie nicht die Installationseigenschaft und einen benutzerdefinierten Wert angeben, verwendet der Client die Standardwerte. Die Standardwerte sind **80** für HTTP-Datenverkehr und **443** für HTTPS-Datenverkehr.  

 Die Anforderung Port-Konfiguration kann nicht geändert werden, nach der Installation des Clients. Stattdessen müssen Sie zum Ändern der Portkonfiguration neu zu installieren und die neue Portkonfiguration angeben. Führen Sie bei der Neuinstallation des Clients so ändern Sie die Portnummern für die Anforderung der **Installieren** Befehl ähnelt der neuen Client installieren, jedoch mit der zusätzlichen Befehlszeile-Eigenschaft des **- Keepdb**. Diese Option veranlasst die Installation der Clientdatenbank und Dateien, einschließlich des Clients GUID und Zertifikat-Speichers beibehalten werden sollen.  

 Weitere Informationen zu Portnummern, für die Clientkommunikation finden Sie unter [Konfigurieren von Clientkommunikationsports in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="BKMK_ConfigClientMP"></a> Konfigurieren Sie den Client für Linux und UNIX nach Verwaltungspunkten suchen  
 Beim Installieren des Configuration Manager-Clients für Linux und UNIX müssen Sie einen Verwaltungspunkt als ersten Kontaktpunkt angeben.  

 Der Configuration Manager-Client für Linux und UNIX stellt bei der Clientinstallation eine Verbindung mit diesem Verwaltungspunkt her. Wenn der Client keine Verbindung mit dem Verwaltungspunkt herstellen kann, wiederholt die Clientsoftware den Vorgang so lange, bis die Verbindung erfolgreich hergestellt wird.  

 Weitere Informationen dazu, wie Clients Verwaltungspunkte suchen, finden Sie unter [Locating Management Points](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points).
