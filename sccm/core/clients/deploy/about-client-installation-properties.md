---
title: Clientinstallationseigenschaften | Microsoft-Dokumentation
description: Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager.
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: "15"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 36bcbbca4fdee3e95d293c436a105a41a6e3953e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie den Befehl „CCMSetup.exe“ von System Center Configuration Manager, um den Configuration Manager-Client manuell zu installieren.  

##  <a name="aboutCCMSetup"></a> Informationen zu „CCMSetup.exe“  
 Der Befehl „CCMSetup.exe“ lädt die Dateien herunter, die zum Installieren des Clients über einen Verwaltungspunkt oder einen Quellspeicherort erforderlich sind. Dazu zählen unter anderem folgende Dateien:  

-   Windows Installer-Paket „Client.msi“ zur Installation der Clientsoftware  

-   BITS-Installationsdateien (Background Intelligent Transfer Service, intelligenter Hintergrundübertragungsdienst) von Microsoft  

-   Windows Installer-Installationsdateien  

-   Updates und Korrekturen für den Configuration Manager-Client.  

> [!NOTE]  
>  In Configuration Manager können Sie die Datei client.msi nicht direkt ausführen.  

 Die Datei CCMSetup.exe enthält mehrere [Befehlszeileneigenschaften](#ccmsetup-exe-command-line-properties), mit denen das Installationsverhalten angepasst werden kann. Sie können auch Eigenschaften angeben, um das Verhalten von Client.msi mithilfe der Befehlszeile CCMSetup.exe zu ändern.  

> [!IMPORTANT]  
>  Geben Sie alle erforderlichen CCMSetup-Eigenschaften an, bevor Sie die Eigenschaften für Client.msi angeben.  

 Die Datei CCMSetup.exe und die unterstützenden Dateien befinden sich auf dem -Standortserver im Ordner **Client** des Configuration Manager-Installationsordners. Dieser Ordner ist im Netzwerk unter **&lt;Standortservername\>\SMS_&lt;Standortcode\>\Client** freigegeben.  

 Bei der Eingabeaufforderung wird vom Befehl CCMSetup.exe das folgende Format verwendet:  

 `CCMSetup.exe [<Ccmsetup properties>] [<client.msi setup properties>]`  

 Beispiel:  

 „CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01“  

 Dieses Beispiel dient zu Folgendem:  

-   Gibt den Verwaltungspunkt mit dem Namen SMSMP01 an, um eine Liste mit Verteilungspunkten zum Herunterladen der Clientinstallationsdateien anzufordern.  

-   Gibt an, dass die Installation beendet wird, wenn bereits eine Version des Clients auf dem Computer vorhanden ist.  

-   Weist „client.msi“ an, den Client dem Standortcode „S01“ zuzuweisen.  

-   Weist „client.msi“ an, den Fallbackstatuspunkt „SMSFP01“ zu verwenden.  

> [!NOTE]  
>  Wenn eine Eigenschaft Leerzeichen enthält, setzen Sie sie zwischen Anführungszeichen.  


> [!IMPORTANT]  
>  Wenn Sie das Active Directory-Schema für Configuration Manager erweitert haben, werden viele Clientinstallationseigenschaften in den Active Directory-Domänendiensten veröffentlicht und automatisch vom Configuration Manager-Client gelesen. Eine Liste der in den Active Directory-Domänendiensten veröffentlichten Clientinstallationseigenschaften finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager, die in Active Directory-Domänendiensten veröffentlicht wurden](about-client-installation-properties-published-to-active-directory-domain-services.md).  

##  <a name="ccmsetupexe-command-line-properties"></a>Befehlszeileneigenschaften der Datei „CCMSetup.exe“  

### <a name=""></a>/?  

Hiermit wird das Dialogfeld **CCMSetup** geöffnet, in dem Befehlszeileneigenschaften für "ccmsetup.exe" angezeigt werden.  

Beispiel: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;Pfad\>  

 Gibt den Speicherort für den Dateidownload an. Verwenden Sie einen lokalen oder einen UNC-Pfad. Die Dateien werden mithilfe des SMB-Protokolls (Server Message Block) heruntergeladen.  Zum Verwenden von **/source** muss das Windows-Benutzerkonto der Clientinstallation über Leseberechtigungen für den Speicherort verfügen.

> [!NOTE]  
>  Sie können die Eigenschaft **/source** mehrmals in der Befehlszeile verwenden, um alternative Downloadspeicherorte anzugeben.  

 Beispiel: **ccmsetup.exe /source:"\\\Computer\Ordner"**  

### <a name="mpltcomputer"></a>/mp:&lt;Computer\>

 Gibt einen Quellverwaltungspunkt an, mit dem Computer eine Verbindung herstellen können, um den nächsten Verteilungspunkt für die Installationsdateien zu ermitteln. Wenn keine Verteilungspunkte vorhanden sind oder Computer die Dateien auch nach Ablauf von vier Stunden nicht von den Verteilungspunkten herunterladen können, werden die Dateien von den Clients vom angegebenen Verwaltungspunkt heruntergeladen.  

> [!IMPORTANT]  
>  Mit dieser Eigenschaft wird ein erster Verwaltungspunkt für Computer angegeben, um eine Downloadquelle zu ermitteln. Hierfür kommt jeder Verwaltungspunkt jedes Standorts in Frage. Der Client wird nicht einem Verwaltungspunkt *zugewiesen*.   

 Computer laden die Dateien je nach Standortsystemrollen-Konfiguration für Clientverbindungen über eine HTTP- oder eine HTTPS-Verbindung herunter. Beim Herunterladen wird die BITS-Einschränkung verwendet, sofern sie konfiguriert ist. Wenn alle Verteilungspunkte und Verwaltungspunkte ausschließlich für HTTPS-Clientverbindungen konfiguriert sind, stellen Sie sicher, dass für den Clientcomputer ein gültiges Clientzertifikat verfügbar ist.  

Sie können die Befehlszeileneigenschaft **/mp** verwenden, um mehrere Verwaltungspunkte anzugeben, damit Computer bei einem Fehler bei der ersten Verbindungsherstellung den nächsten Verwaltungspunkt verwenden können usw. Wenn Sie mehrere Verwaltungspunkte angeben, trennen Sie die Werte durch Semikolons.

Wenn der Client per HTTPS eine Verbindung mit einem Verwaltungspunkt herstellt, müssen Sie anstelle des Computernamens normalerweise den vollqualifizierten Domänennamen (FQDN) angeben. Der Wert muss mit dem Antragstellernamen oder alternativen Antragstellernamen des PKI-Zertifikats für den Verwaltungspunkt übereinstimmen. Obwohl Configuration Manager einen Computernamen im Zertifikat für Verbindungen im Intranet unterstützt, wird als bewährte Sicherheitsmethode die Verwendung eines vollqualifizierten Domänennamens empfohlen.

Beispiel für die Verwendung des Computernamens: `ccmsetup.exe /mp:SMSMP01`  

Beispiel für die Verwendung des vollqualifizierten Domänennamens: `ccmsetup.exe /mp:smsmp01.contoso.com`  

### <a name="retryltminutes"></a>/retry:&lt;Minuten\>

Wiederholungsintervall, wenn „CCMSetup.exe“ die Installationsdateien nicht herunterladen kann.  Der Vorgang wird von CCMSetup wiederholt, bis die in der Eigenschaft **downloadtimeout** angegebene Grenze erreicht ist.  

Beispiel: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Verhindert, dass CCMSetup als Dienst ausgeführt wird, was das Standardverhalten ist. Wenn CCMSetup als Dienst ausgeführt wird, erfolgt die Ausführung im Kontext des lokalen Systemkontos des Computers, das möglicherweise nicht über ausreichende Rechte für den Zugriff auf die für die Installation erforderlichen Netzwerkressourcen verfügt. Mit **/noservice** wird „CCMSetup.exe“ im Kontext des Benutzerkontos ausgeführt, mit dem Sie die Installation starten. Wenn Sie zum Ausführen von „CCMSetup.exe“ mit der Eigenschaft **/service** ein Skript verwenden, wird „CCMSetup.exe“ nach dem Starten des Diensts beendet und meldet die Installationsdetails möglicherweise nicht ordnungsgemäß.   

Beispiel: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Hiermit wird angegeben, dass CCMSetup mithilfe des lokalen Systemkontos als Dienst ausgeführt werden soll.  

Beispiel: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Gibt an, dass die Clientsoftware deinstalliert werden soll. Weitere Informationen finden Sie unter [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md).  

Beispiel: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Gibt an, dass die Clientinstallation angehalten werden soll, wenn bereits eine Version des Clients installiert ist.  

Beispiel: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 Gibt an, dass CCMSetup einen Neustart des Clientcomputers erzwingen soll, wenn dies zum Abschließen der Installation erforderlich ist. Falls diese Option nicht angegeben ist, wird CCMSetup beendet, wenn ein Neustart erforderlich ist, und dann nach dem nächsten manuellen Neustart fortgesetzt.  

 Beispiel: `CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;Priorität\>

 Hiermit wird die Downloadpriorität beim Herunterladen von Clientinstallationsdateien über eine HTTP-Verbindung angegeben. Es sind folgende Werte möglich:  

-   FOREGROUND (Vordergrund)  

-   HIGH (Hoch)  

-   NORMAL (Mittel)  

-   LOW (Niedrig)  

 Der Standardwert ist NORMAL.  

 Beispiel: `ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;Minuten\>

Die Zeitspanne in Minuten, in der CCMSetup versucht, die Installationsdateien herunterzuladen, bevor der Vorgang angehalten wird. Der Standardwert beträgt **1440** Minuten (1 Tag).  

Beispiel: `ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

 Wenn diese Option angegeben ist, verwendet der Client ein PKI-Zertifikat mit Clientauthentifizierung, sofern vorhanden. Wenn kein gültiges Zertifikat gefunden werden kann, verwendet der Client eine HTTP-Verbindung und ein selbstsigniertes Zertifikat. Der Client zeigt dieses Verhalten auch, wenn Sie diese Eigenschaft nicht verwenden.

> [!NOTE]  
>  In einigen Szenarios müssen Sie diese Eigenschaft nicht angeben, wenn Sie einen Client installieren und dennoch ein Clientzertifikat verwenden. Dazu gehören die Installation eines Clients mithilfe von Clientpushinstallation sowie die Installation eines Clients mithilfe eines Softwareupdatepunkts. Sie müssen diese Eigenschaft jedoch immer angeben, wenn Sie einen Client manuell installieren und die Eigenschaft **/mp** verwenden, um einen Verwaltungspunkt anzugeben, der ausschließlich für Clientverbindungen über HTTPS konfiguriert ist. Dies gilt auch beim Installieren eines Clients mit dem Kommunikationsstatus Nur Internet mithilfe der Eigenschaft CCMALWAYSINF=1 (zusammen mit den Eigenschaften des internetbasierten Verwaltungspunkts sowie dem Standortcode). Weitere Informationen zur internetbasierten Clientverwaltung finden Sie unter [Überlegungen zur Clientkommunikation aus dem Internet oder aus einer nicht vertrauenswürdigen Gesamtstruktur](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in [Datenübertragungen zwischen Endpunkten in System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Beispiel: `CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 Gibt an, dass ein Client die Zertifikatssperrlisten nicht überprüfen soll, wenn dieser über HTTPS unter Verwendung eines PKI-Zertifikats kommuniziert.  

 Wenn diese Option nicht angegeben ist, überprüft der Client die Zertifikatssperrliste, bevor er eine Verbindung über HTTPS herstellt.  

 Weitere Informationen zur Überprüfung der Zertifikatsperrlisten finden Sie unter [Planning for PKI certificate revocation](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) in[Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Beispiel: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;Konfigurationsdatei\>

Gibt den Namen der Textdatei mit den Clientinstallationseigenschaften an.

- Wenn Sie die CCMSetup-Eigenschaft **/noservice** nicht angeben, muss diese Datei im Ordner „CCMSetup“ abgelegt sein, d.h. bei 32-Bit- und 64-Bit-Betriebssystemen unter „%Windir%\\Ccmsetup“.
- Wenn Sie die Eigenschaft **/noservice** angeben, muss sich diese Datei in dem Ordner befinden, von dem aus Sie "CCMSetup.exe" ausführen.  

Beispiel: `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

Das richtige Dateiformat entnehmen Sie der Datei „mobileclienttemplate.tcf“, die sich auf dem Standortservercomputer im &lt;Verzeichnis Configuration Manager\>\\bin\\&lt;Plattform\> befindet. Die Datei enthält auch Kommentare zu den Abschnitten und deren Verwendung. Geben Sie die Clientinstallationseigenschaften im Abschnitt [Client Install] nach folgendem Text ein: **Install=INSTALL=ALL**.  

Beispiel für einen Abschnitteintrag [Client Install]: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;Dateiname\>

 Hiermit wird angegeben, dass das angegebene erforderliche Programm von „CCMSetup.exe“ nicht installiert werden darf, wenn der Configuration Manager-Client installiert wird. Diese Eigenschaft unterstützt die Eingabe mehrerer Werte. Verwenden Sie zum Trennen der Werte jeweils ein Semikolon (;).  


 Beispiele: `CCMSetup.exe /skipprereq:silverlight.exe` oder `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe`  

### <a name="forceinstall"></a>/forceinstall

 Gibt an, dass alle vorhandenen Clients deinstalliert werden und ein neuer Client installiert wird.  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;Funktion\>

Gibt an, dass CCMSetup.exe die angegebene Funktion nicht installiert, wenn der Client installiert ist.  

Beispiel: `CCMSetup.exe /ExcludeFeatures:ClientUI` installiert das Softwarecenter nicht auf dem Client.  

> [!NOTE]  
>  In dieser Version ist **ClientUI** die einzige Option, die für die Eigenschaft **/ExcludeFeatures** unterstützt wird.  

##  <a name="ccmsetupReturnCodes"></a> Rückgabecodes von „CCMSetup.exe“  
 Der Befehl „CCMSetup.exe“ gibt die im Folgenden aufgeführten Rückgabecodes aus. Zur Problembehandlung informieren Sie sich in der Datei „ccmsetup.log“ auf dem Clientcomputer über den jeweiligen Kontext und weitere Details zu Rückgabecodes.  

|Rückgabecode|Bedeutung|  
|-----------------|-------------|  
|0|Erfolgreich|  
|6|Fehler|  
|7|Neustart erforderlich|  
|8|Setup wird bereits ausgeführt|  
|9|Fehler beim Auswerten der Voraussetzungen|  
|10|Fehler beim Überprüfen des Hashs für das Setup-Manifest|  

##  <a name="clientMsiProps"></a> Eigenschaften der Datei „Client.msi“  
 Mit den folgenden Eigenschaften können Sie das Installationsverhalten von „client.msi“ ändern. Wenn Sie die Clientpushinstallationsmethode verwenden, können Sie außerdem die Eigenschaften im Dialogfeld **Eigenschaften von Clientpushinstallation** auf der Registerkarte **Client** angeben.  

### <a name="ccmadmins"></a>CCMADMINS  

Gibt eine oder mehrere Windows-Benutzerkonten oder -Gruppen an, denen der Zugriff auf die Clienteinstellungen und -richtlinien erlaubt werden soll. Dies ist nützlich, wenn der Configuration Manager-Administrator über keine lokalen Administratoranmeldeinformationen auf dem Clientcomputer verfügt. Geben Sie eine Liste von Konten an, die Sie durch Semikolons trennen.  

Beispiel: `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Geben Sie an, dass ein Neustart des Computers nach der Clientinstallation ggf. zulässig ist.  

> [!IMPORTANT]  
>  Der Computer führt den Neustart ohne vorherige Warnung aus, auch wenn ein Benutzer angemeldet ist.  

Beispiel: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 Legen Sie 1 fest, um anzugeben, dass der Client immer internetbasiert ist und keine Verbindung mit dem Intranet herstellt. Der angezeigte Clientverbindungstyp lautet **Immer Internet**.  

 Verwenden Sie diese Eigenschaft in Verbindung mit der Eigenschaft CCMHOSTNAME, die den FQDN des internetbasierten Verwaltungspunkts angibt. Sie sollte auch in Verbindung mit der CCMSetup-Eigenschaft /UsePKICert und mit dem Standortcode verwendet werden.  

 Weitere Informationen zur internetbasierten Clientverwaltung finden Sie unter [Überlegungen zur Clientkommunikation aus dem Internet oder aus einer nicht vertrauenswürdigen Gesamtstruktur](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in [Datenübertragungen zwischen Endpunkten in System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Beispiel: `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Hiermit wird die Liste der Zertifikataussteller angegeben. Dies ist eine Liste von Zertifikaten vertrauenswürdiger Zertifizierungsstellen (CA), denen vom Configuration Manager-Standort vertraut wird.  

 Weitere Informationen zur Liste der Zertifikataussteller und deren Verwendung durch Clients beim Zertifikatauswahlvorgang finden Sie unter [Planning for PKI client certificate selection](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Bei dieser Suche nach Übereinstimmungen für Antragstellerattribute im Stamm-Zertifizierungsstellenzertifikat wird die Groß-/Kleinschreibung beachtet. Attribute können durch ein Komma (,) oder ein Semikolon (;) getrennt werden. Mehrere Stamm-Zertifizierungsstellenzertifikate können mithilfe einer Trennlinie angegeben werden. Beispiel:  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  Verweisen Sie auf die Datei „mobileclient.tcf“ im &lt;Configuration Manager-Verzeichnis\>\bin\\&lt;Plattform\> auf dem Standortservercomputer, um den für den Standort konfigurierten Eintrag **CertificateIssuers=&lt;Zeichenfolge\>** zu kopieren.  

### <a name="ccmcertsel"></a>CCMCERTSEL

 Gibt die Zertifikatauswahlkriterien an, wenn der Client mehrere Zertifikate für die HTTPS-Kommunikation besitzt (ein gültiges Zertifikat mit Clientauthentifizierungsfunktionen).  

 Sie können in den Feldern „Antragstellername“ oder „Alternativer Antragstellername“ nach einer genauen Übereinstimmung (verwenden Sie **Subject:**:) oder nach einer teilweisen Übereinstimmung suchen (verwenden Sie **SubjectStr:)**. Beispiele:  

 `CCMCERTSEL="Subject:computer1.contoso.com"` sucht nach einem Zertifikat, das im Antragstellernamen oder im alternativen Antragstellernamen genau mit dem Computernamen „computer1.contoso.com“ übereinstimmt.  

 `CCMCERTSEL="SubjectStr:contoso.com"` sucht nach einem Zertifikat, das im Antragstellernamen oder alternativen Antragstellernamen „contoso.com“ aufweist.  

 Sie können für die Attribute „Antragstellername“ und „Alternativer Antragstellername“ auch Objekt-IDs (OIDs) oder einen definierten Namen verwenden. Beispiel:  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` sucht nach dem Organisationseinheitenattribut, das als Objektbezeichner angegeben wird und „Computers“ heißt.  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` sucht nach dem Organisationseinheitenattribut, das als definierter Name angegeben wird und „Computers“ heißt.  

> [!IMPORTANT]  
>  Wenn Sie das Feld „Antragstellername“ verwenden, muss bei **Subject:** die Groß-/Kleinschreibung beachtet werden, bei **SubjectStr:** dagegen nicht.  
>   
>  Wenn Sie das Feld „Alternativer Antragstellername“ verwenden, spielt die Groß-/Kleinschreibung bei **Subject:** und bei **SubjectStr:** keine Rolle.  

 Eine vollständige Liste der Attribute, die für die Zertifikatauswahl verwendet werden können, finden Sie unter [Unterstützte Attributwerte für die PKI-Zertifikatauswahlkriterien](#BKMK_attributevalues).  

 Wenn mehrere Zertifikate mit der Suche übereinstimmen und die Eigenschaft CCMFIRSTCERT auf 1 festgelegt ist, wird das PKI-Zertifikat mit der längsten Gültigkeitsdauer vom Client ausgewählt.  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 Gibt einen alternativen Zertifikatspeichernamen an, wenn das Clientzertifikat für HTTPS nicht im Standardzertifikatspeicher **Persönlich** im Computerspeicher abgelegt ist.  

 Beispiel: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  Aktiviert die Debugprotokollierung. Die Werte können auf 0 (aus, Standardeinstellung) oder 1 (ein) festgelegt werden. Hierdurch protokolliert der Client Basisinformationen für die Problembehandlung. Zur Vermeidung einer zu umfangreichen Protokollierung, durch die es schwierig werden kann, relevante Informationen in den Protokolldateien finden, sollte diese Eigenschaft an Produktionsstandorten möglichst nicht verwendet werden. CCMENABLELOGGING muss zudem auf TRUE festgelegt sein, damit die Debugprotokollierung aktiviert wird.  

  Beispiel: `CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  Standardmäßig ist TRUE eingestellt, damit die Protokollierung aktiviert wird. Die Protokolldateien werden im Configuration Manager-Clientinstallationsorder im Ordner **Logs** gespeichert. Standardmäßig ist dies der Ordner %Windir%\CCM\Logs.  

  Beispiel: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 Die Ausführungshäufigkeit des Tools zur Clientintegritätsauswertung (ccmeval.exe). Ein Wert zwischen **1** und **1440** Minuten ist hier möglich. Standardmäßig wird das Tool einmal täglich ausgeführt.  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 Der Ausführungszeitpunkt des Tools zur Clientintegritätsauswertung (ccmeval.exe) in Stunden, d.h. zwischen **0** (Mitternacht) und **23** (23 Uhr). Standardmäßig wird das Tool um Mitternacht ausgeführt.  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 Wenn für diese Eigenschaft der Wert 1 festgelegt ist, wird vom Client das PKI-Zertifikat mit der längsten Gültigkeitsdauer ausgewählt. Diese Einstellung ist möglicherweise erforderlich, wenn Sie Netzwerkzugriffsschutz mit IPsec-Erzwingung verwenden.  

 Beispiel: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  

### <a name="ccmhostname"></a>CCMHOSTNAME

 Gibt den FQDN des internetbasierten Verwaltungspunkts an, wenn der Client über das Internet verwaltet wird.  

 Geben Sie diese Option nicht mit der Installationseigenschaft „SMSSITECODE=AUTO“ an. Internetbasierte Clients müssen direkt ihrem internetbasierten Standort zugewiesen werden.  

 Beispiel: `CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

### <a name="ccmhttpport"></a>CCMHTTPPORT

 Hiermit wird der Port angegeben, der vom Client für die Kommunikation mit den Standortsystemservern über HTTP verwendet werden soll. Standardmäßig auf Port 80 festgelegt.  

 Beispiel: `CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Hiermit wird der Port angegeben, der vom Client für die Kommunikation mit den Standortsystemservern über HTTPS verwendet werden soll. Standardmäßig auf Port 443 festgelegt.  

Beispiel: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Weist den Ordner aus, in dem die Configuration Manager-Clientdateien installiert sind. Standardmäßig ist dies *%Windir%*\CCM. Unabhängig vom Installationsort dieser Dateien wird die Datei „Ccmcore.dll“ stets im Ordner *%Windir%\System32* installiert. Bei 64-Bit-Betriebssystemen wird außerdem immer eine Kopie der Datei „Ccmcore.dll“ im Ordner *%Windir%*\SysWOW64 installiert, um 32-Bit-Anwendungen zu unterstützen, von denen die 32-Bit-Version der Configuration Manager-Client-APIs aus dem Configuration Manager-Software Developer Kit (SDK) verwendet wird.  

 Beispiel: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Gibt die Detailebene für das Schreiben in die Configuration Manager-Protokolldateien an. Geben Sie eine ganze Zahl zwischen 0 und 3 an, wobei 0 für die ausführlichste Protokollierung und 3 für die reine Fehlerprotokollierung steht. Der Standardwert lautet 1.  

Beispiel: `CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Wenn eine Configuration Manager-Protokolldatei die Größe von 250000 Bytes erreicht (oder den Wert, der von der Eigenschaft CCMLOGMAXSIZE angegeben wird), wird sie als Sicherungsdatei umbenannt, und eine neue Protokolldatei wird erstellt.  

Diese Eigenschaft gibt an, wie viele vorherige Versionen der Protokolldatei beibehalten werden sollen. Der Standardwert lautet 1. Wird der Wert auf 0 festgelegt, werden keine alten Protokolldateien beibehalten.  

Beispiel: `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Die maximale Protokolldateigröße in Bytes. Wenn ein Protokoll die angegebene Größe erreicht, wird es als Verlaufsdatei umbenannt, und eine neue Datei wird erstellt. Diese Eigenschaft muss auf mindestens 10000 Bytes festgelegt werden. Der Standardwert beträgt 250000 Bytes.  

Beispiel: `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 Wenn diese Eigenschaft auf TRUE festgelegt ist, wird verhindert, dass Endbenutzer mit Administratoranmeldeinformationen auf dem Clientcomputer den für Configuration Manager zugewiesenen Standort in **Configuration Manager** in der Systemsteuerung ändern können.  

 Beispiel: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Wenn für diese Eigenschaft der Wert TRUE festgelegt wurde, können Endbenutzer, die über Administratoranmeldeinformationen auf dem Clientcomputer verfügen, die Einstellungen des Clientcacheordners für den Configuration Manager-Client nicht mithilfe von Configuration Manager in der Systemsteuerung des Clientcomputers ändern.  

Beispiel: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 Hiermit wird die DNS-Domäne angegeben, über die Clients Verwaltungspunkten finden können, die in DNS veröffentlicht wurden. Nachdem ein Verwaltungspunkt gefunden wurde, wird der Client über andere Verwaltungspunkte in der Hierarchie informiert. Dies heißt, dass der Verwaltungspunkt, der mittels der DNS-Veröffentlichung gefunden wird, nicht am Standort des Clients vorliegen muss, sondern dass jeder beliebige Verwaltungspunkt in der Hierarchie in Frage kommt.  

> [!NOTE]  
>  Sie müssen diese Eigenschaft nicht angeben, wenn der Client der gleichen Domäne angehört wie ein veröffentlichter Verwaltungspunkt. In diesem Fall wird die Clientdomäne automatisch verwendet, um DNS nach Verwaltungspunkten zu durchsuchen.  

 Weitere Informationen zur DNS-Veröffentlichung als Dienstidentifizierungsmethode für Configuration Manager-Clients finden Sie unter [Service Location and how clients determine their assigned management point (Dienstidentifizierung und wie Clients den ihnen zugewiesenen Verwaltungspunkt ermitteln)](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) in [Understand how clients find site resources and services for System Center Configuration Manager (Verstehen, wie Clients Standortressourcen und -dienste für System Center Configuration Manager suchen)](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

> [!NOTE]  
>  Die DNS-Veröffentlichung ist in Configuration Manager standardmäßig nicht aktiviert.  

 Beispiel: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

Gibt den Fallbackstatuspunkt an, von dem die von Configuration Manager-Clientcomputern gesendeten Zustandsmeldungen empfangen und verarbeitet werden.  

Weitere Informationen zum Fallbackstatuspunkt finden Sie unter [Bestimmen, ob ein Fallbackstatuspunkt erforderlich ist](/sccm/core/clients/deploy/plan#determine-if-you-need-a-fallback-status-point).  

Beispiel: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 Gibt an, dass vor der Clientinstallation nicht geprüft wird, ob die erforderliche Mindestversion von Microsoft Application Virtualization (App-V) vorhanden ist.  

> [!IMPORTANT]  
>  Wenn Sie den Configuration Manager-Client installieren, ohne App-V zu installieren, können Sie keine virtuellen Anwendungen bereitstellen.  

 Beispiel: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

Gibt an, dass der Clientstatus gemeldet wird, jedoch keine Probleme behoben werden, die in Verbindung mit dem Client auftreten.  

Beispiel: `CCMSetup.exe NOTIFYONLY=TRUE`  

Weitere Informationen finden Sie unter [Konfigurieren des Clientstatus in System Center Configuration Manager](configure-client-status.md).  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Wenn ein Configuration Manager-Client den falschen vertrauenswürdigen Configuration Manager-Stammschlüssel aufweist und keine Verbindung mit dem vertrauenswürdigen Verwaltungspunkt herstellen kann, um den neuen vertrauenswürdigen Stammschlüssel abzurufen, müssen Sie den alten vertrauenswürdigen Stammschlüssel manuell mithilfe dieser Eigenschaft entfernen. Dieser Fall tritt möglicherweise ein, wenn Sie einen Client aus einer Standorthierarchie in eine andere verschieben. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Clientkommunikation verwendet wird.  

 Beispiel: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Ermöglicht eine automatische Standortneuzuordnung für Clientupgrades bei Verwendung mit [SMSSITECODE](#smssitecode)=AUTO.

Beispiel: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Hiermit wird der Speicherort des Clientcacheordners angegeben, in dem temporäre Dateien auf dem Clientcomputer gespeichert werden. Standardmäßig ist dies der Speicherort *%Windir \ccmcache*.  

Beispiel: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Diese Eigenschaft kann in Verbindung mit der Eigenschaft SMSCACHEFLAGS verwendet werden, um den Speicherort des Clientcacheordners zu steuern.  

Beispiel: Mit `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` wird der Clientcacheordner auf dem größten verfügbaren Laufwerk des Clients installiert.  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Hiermit werden weitere Installationsdetails für den Clientcacheordner angegeben. Sie können die SMSCACHEFLAGS-Eigenschaften einzeln oder zusammen durch Kommas getrennt verwenden. Wenn diese Eigenschaft nicht angegeben wird, wird der Clientcacheordner der Eigenschaft SMSCACHEDIR entsprechend installiert und nicht komprimiert, und der Wert der Eigenschaft SMSCACHESIZE wird als Größe des Ordners in MB verwendet.  

Diese Einstellung wird ignoriert, wenn ein Upgrade eines vorhandenen Clients ausgeführt wird.  

Eigenschaften:  

-   PERCENTDISKSPACE: Gibt die Ordnergröße als Prozentsatz des gesamten Speicherplatzes an. Wenn Sie diese Eigenschaft angeben, müssen Sie auch die Eigenschaft SMSCACHESIZE als Prozentwert angeben.  

-   PERCENTFREEDISKSPACE: Gibt die Ordnergröße als Prozentsatz des freien Speicherplatzes an. Wenn Sie diese Eigenschaft angeben, müssen Sie auch die Eigenschaft SMSCACHESIZE als Prozentwert angeben. Wenn der Datenträger z. B. über 10 MB freien Speicherplatz verfügt und für SMSCACHESIZE 50 angegeben ist, wird die Ordnergröße auf 5 MB festgelegt. Diese Eigenschaft kann nicht in Verbindung mit der Eigenschaft PERCENTDISKSPACE verwendet werden.  

-   MAXDRIVE: Gibt an, dass der Ordner auf dem größten verfügbaren Datenträger installiert werden soll. Dieser Wert wird ignoriert, wenn ein Pfad mit der Eigenschaft SMSCACHEDIR angegeben wurde.  

-   MAXDRIVESPACE: Gibt an, dass der Ordner auf dem Laufwerk mit dem meisten verfügbaren Speicherplatz installiert werden soll. Dieser Wert wird ignoriert, wenn ein Pfad mit der Eigenschaft SMSCACHEDIR angegeben wurde.  

-   NTFSONLY: Gibt an, dass der Ordner nur auf NTFS-Laufwerken installiert werden kann. Dieser Wert wird ignoriert, wenn ein Pfad mit der Eigenschaft SMSCACHEDIR angegeben wurde.  

-   COMPRESS: Gibt an, dass der Ordner komprimiert gespeichert werden soll.  

-   FAILIFNOSPACE: Gibt an, dass die Clientsoftware entfernt werden soll, wenn ausreichend Speicherplatz zum Installieren des Ordners verfügbar ist.  

Beispiel: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Ab Configuration Manager Version 1606 sind neue Clienteinstellungen für die Angabe der Größe des Clientcacheordners verfügbar. Das Hinzufügen dieser Clienteinstellungen ersetzt SMSCACHESIZE als client.msi-Eigenschaft, um die Größe des Clientcaches anzugeben. Weitere Informationen zu den Clienteinstellungen finden Sie unter [client settings for cache size](about-client-settings.md#client-cache-settings) (Clienteinstellungen für Cachegröße).  

Wenn diese Eigenschaft für 1602 und früher in Verbindung mit der Eigenschaft PERCENTDISKSPACE oder PERCENTFREEDISKSPACE verwendet wird, gibt SMSCACHESIZE hiermit die Größe des Clientcacheordners in Megabyte (MB) oder als Prozentsatz an. Wenn diese Eigenschaft nicht festgelegt ist, wird für den Ordner standardmäßig die maximale Größe von 5120 MB verwendet. Der niedrigste Wert, den Sie angeben können, beträgt 1 MB.  

> [!NOTE]  
>  Wenn für den Download eines neuen Pakets die maximale Ordnergröße überschritten würde, der Ordnerinhalt jedoch nicht zur Freigabe von Speicherplatz geleert werden kann, wird der Downloadvorgang abgebrochen, und das Programm bzw. die Anwendung kann nicht ausgeführt werden.  

Diese Einstellung wird ignoriert, wenn ein Upgrade eines vorhandenen Clients ausgeführt wird und wenn Softwareupdates vom Client heruntergeladen werden.  

Beispiel: `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  Wenn Sie einen Client neu installieren, können Sie die Installationseigenschaften SMSCACHESIZE und SMSCACHEFLAGS nicht verwenden, um die Cachegröße auf einen niedrigeren Wert als vorher festzulegen. Wenn Sie dies versuchen, wird der Wert ignoriert und die Cachegröße wird automatisch auf die vorherige Größe festgelegt.  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Gibt den zu überprüfenden Speicherort und die Reihenfolge an, die das Configuration Manager-Installationsprogramm für die Überprüfung der Konfigurationseinstellungen verwendet. Bei der Eigenschaft handelt es sich um eine Zeichenfolge aus einem oder mehreren Zeichen, die jeweils eine spezielle Konfigurationsquelle angibt. Verwenden Sie die Zeichenwerte R, P, M und U alleine oder zusammen:  

-   R: Überprüfung der Konfigurationseinstellungen in der Registrierung.  

   Weitere Informationen finden Sie unter [Informationen zum Speichern von Clientinstallationseigenschaften in der Registrierung](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision).  

-   P: Überprüfung der Konfigurationseinstellungen in den Installationseigenschaften an der Eingabeaufforderung  

-   M: Überprüfung der vorhandenen Einstellungen beim Aktualisieren eines älteren Clients mit der Configuration Manager-Clientsoftware  

-   U: Upgrade des installierten Clients auf eine neuere Version (unter Verwendung des zugewiesenen Standortcodes)  

 Bei der Clientinstallation wird standardmäßig `PU` verwendet, um zuerst die Installationseinstellungen und dann die vorhandenen Einstellungen zu überprüfen.  

 Beispiel: `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 Hiermit wird angegeben, ob Windows Internet Name Service (WINS) vom Client verwendet werden kann, um einen Verwaltungspunkt zu finden, von dem HTTP-Verbindungen zugelassen werden. Diese Methode wird von den Clients verwendet, wenn kein Verwaltungspunkt in den Active Directory-Domänendiensten oder in DNS gefunden werden kann.  

 Diese Eigenschaft beeinflusst nicht, ob der Client WINS für die Namensauflösung verwendet.  

 Sie können zwei verschiedene Modi für diese Eigenschaft konfigurieren:  

-   NOWINS: Dies ist die sicherste Einstellung für diese Eigenschaft. Es wird verhindert, dass von Clients ein Verwaltungspunkt in WINS gefunden wird.  Wenn Sie diese Einstellung verwenden, ist eine alternative Methode für die Clients erforderlich, mit der ein Verwaltungspunkt im Intranet gefunden werden kann, beispielsweise Active Directory-Domänendienste oder DNS-Veröffentlichung.  

-   WINSSECURE (Standardeinstellung): In diesem Modus kann ein Client, der HTTP-Kommunikation verwendet, mithilfe von WINS einen Verwaltungspunkt suchen. Für den Client ist jedoch eine Kopie des vertrauenswürdigen Stammschlüssels erforderlich, bevor eine Verbindung mit dem Verwaltungspunkt hergestellt werden kann. Weitere Informationen finden Sie unter [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  


 Beispiel: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Hiermit wird ein erster Verwaltungspunkt für die Verwendung durch den Configuration Manager-Client angegeben.  

> [!IMPORTANT]  
>  Wenn der Verwaltungspunkt nur Clientverbindungen über HTTPS akzeptiert, müssen Sie dem Namen des Verwaltungspunkts das Präfix „https://“ voranstellen.  

Beispiel: `CCMSetup.exe SMSMP=smsmp01.contoso.com`

Beispiel: `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Gibt den vertrauenswürdigen Configuration Manager-Stammschlüssel für den Fall an, dass dieser nicht aus den Active Directory-Domänendiensten abgerufen werden kann. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Clientkommunikation verwendet wird. Weitere Informationen finden Sie unter [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Beispiel: `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Diese Eigenschaft wird verwendet, um den vertrauenswürdigen Configuration Manager-Stammschlüssel neu zu installieren. Hiermit werden der vollständige Pfad und der Dateiname einer Datei mit dem vertrauenswürdigen Stammschlüssel angegeben. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Clientkommunikation verwendet wird. Weitere Informationen finden Sie unter [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Beispiel: 'CCMSetup.exe SMSROOTKEYPATH=&lt;Vollständiger Pfad und Dateiname\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 Hiermit werden der vollständige Pfad und der CER-Dateiname des exportierten selbstsignierten Zertifikats auf dem Standortserver angegeben.  

 Dieses Zertifikat ist im **SMS** -Zertifikatspeicher unter dem Antragstellernamen **Standortserver** und dem Anzeigenamen **Signaturzertifikat des Standortservers**gespeichert.  

 Beispiel: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;Vollständiger Pfad und Dateiname\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Gibt den Configuration Manager-Standort an, um diesem den Configuration Manager-Client zuzuweisen. Dies kann entweder ein dreistelliger Standortcode oder das Wort AUTO sein. Wenn AUTO angegeben ist oder diese Eigenschaft nicht angegeben ist, wird vom Client versucht, die Configuration Manager-Standortzuweisung anhand der Active Directory-Domänendienste oder eines angegebenen Verwaltungspunkts zu bestimmen. Um AUTO für Clientupgrades festzulegen, müssen Sie ferner [SITEREASSIGN](#sitereassign) auf TRUE setzen.    

> [!NOTE]  
>  Verwenden Sie nicht „Automatisch“, wenn Sie auch den internetbasierten Verwaltungspunkt (CCMHOSTNAME) angegeben. In diesem Fall müssen Sie den Client direkt dem Standort zuweisen.  

 Beispiel: `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> Unterstützte Attributwerte für die PKI-Zertifikatauswahlkriterien  
 Configuration Manager unterstützt die folgenden Attributwerte für die PKI-Zertifikatauswahlkriterien:  

|OID-Attribut|DN-Attribut (Distinguished Name)|Attributdefinition|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Domänenkomponente|  
|1.2.840.113549.1.9.1|E oder E-mail|E-Mail-Adresse|  
|2.5.4.3|CN|Allgemeiner Name|  
|2.5.4.4|SN|Antragstellername|  
|2.5.4.5|SERIALNUMBER|Seriennummer|  
|2.5.4.6|C|Ländercode|  
|2.5.4.7|L|Ort|  
|2.5.4.8|S oder ST|Name des Bundeslands bzw. des Kantons|  
|2.5.4.9|STREET|Straße|  
|2.5.4.10|O|Organisationsname|  
|2.5.4.11|OU|Organisationseinheit|  
|2.5.4.12|T oder Title|Titel|  
|2.5.4.42|G oder GN oder GivenName|Vorname|  
|2.5.4.43|I oder Initials|Initialen|  
|2.5.29.17|(kein Wert)|Alternativer Antragstellername|  
