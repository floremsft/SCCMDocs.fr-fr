---
title: Clienteinstellungen | Microsoft Docs
description: Auswahl von Clienteinstellungen mithilfe der Verwaltungskonsole in System Center Configuration Manager.
ms.custom: na
ms.date: 08/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: "15"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: a8233c361e1a78b14a02f328da445814624e38d8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Informationen zu Clienteinstellungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Alle Clienteinstellungen in System Center Configuration Manager werden in der Configuration Manager-Konsole über den Knoten **Clienteinstellungen** im Arbeitsbereich **Verwaltung** verwaltet. Mit Configuration Manager wird ein Satz Standardeinstellungen geliefert. Wenn Sie die Clientstandardeinstellungen verändern, werden diese Einstellungen auf alle Clients in der Hierarchie angewendet. Sie können auch benutzerdefinierte Clienteinstellungen konfigurieren. Wenn Sie diese Einstellungen Sammlungen zuweisen, werden die Clientstandardeinstellungen überschrieben. Informationen zum Konfigurieren von Clienteinstellungen finden Sie unter [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

Viele der Clienteinstellungen sind selbsterklärend. Andere werden hier beschrieben.  

## <a name="background-intelligent-transfer-service"></a>Background Intelligent Transfer Service  

-   **Maximale Netzwerkbandbreite für BITS-Übertragungen im Hintergrund begrenzen**  

   Wenn für diese Option **Wahr** oder **Ja** festgelegt ist, verwenden die Clients die BITS-Bandbreiteneinschränkung.  

-   **Beginn des Einschränkungszeitfensters**  

   Geben Sie die lokale Startzeit für das BITS-Einschränkungszeitfenster an.  

-   **Ende des Einschränkungszeitfensters**  

   Geben Sie die lokale Endzeit für das BITS-Einschränkungszeitfenster an. Entspricht dieser Wert dem Wert von **Throttling window start time** (Beginn des Einschränkungszeitfensters), ist die BITS-Einschränkung immer aktiviert.  

-   **Maximale Übertragungsrate während des Einschränkungszeitfensters (KBit/s)**  

   Geben Sie die maximale Übertragungsrate an, die den Clients während des Zeitfensters zur Verfügung steht.  

-   **BITS-Downloads außerhalb des Einschränkungszeitfensters zulassen**  

   Wählen Sie diese Option aus, damit Configuration Manager-Clients separate BITS-Einstellungen außerhalb des angegebenen Fensters verwenden können.  

-   **Maximale Übertragungsrate außerhalb des Einschränkungszeitfensters (KBit/s)**  

   Geben Sie die maximale Übertragungsrate an, die von Clients außerhalb des BITS-Einschränkungszeitfensters verwendet werden kann, sofern die BITS-Einschränkung außerhalb des Zeitfensters zugelassen wurde.  

## <a name="client-cache-settings"></a>Einstellungen des Clientcaches

- **BranchCache konfigurieren**

  Ab Version 1606 wird diese Einstellung verwendet, um den Clientcomputer für [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache) einzurichten. Um die BranchCache-Zwischenspeicherung auf dem Client zuzulassen, legen Sie **BranchCache aktivieren** auf **Ja** fest.

- **BranchCache aktivieren**

aktiviert BranchCache auf Clientcomputern.

- **Maximale BranchCache-Cachegröße (Prozentsatz des Datenträgers)**

- **Konfigurieren der Cachegröße des Clients**

  Der Clientcache auf Windows-Computern speichert temporäre Dateien, die zum Installieren von Anwendungen und Programmen verwendet werden. Klicken Sie auf **Ja** und geben Sie Folgendes an:
    - **Maximale Cachegröße** (MB) 
    - **Maximale Cachegröße** (Prozentsatz des Datenträgers)
Die Cachegröße kann auf die maximale Größe in MB oder den Prozentsatz des Datenträgers erweitern werden, je nach dem, **welcher Wert kleiner ist**. Wenn die Option **Nein** festgelegt ist, beträgt die Standardgröße 5.120 MB.

- **Configuration Manager-Client in vollständigem Betriebssystem zur Freigabe von Inhalten aktivieren**

Aktiviert den Peercache für Configuration Manager-Clients. Geben Sie dann die Portinformationen ein, über die der Client mit dem Peercomputer kommuniziert. Configuration Manager wird Windows-Firewall-Regeln automatisch so konfigurieren, dass dieser Datenverkehr zugelassen wird. Bei Verwendung einer anderen Firewall müssen Sie die Regeln manuell konfigurieren, um diesen Datenverkehr zuzulassen.




## <a name="client-policy"></a>Clientrichtlinie  

-   **Clientrichtlinien-Abrufintervall (Minuten)**  

   Geben Sie an, wie häufig die Clientrichtlinie von den folgenden Configuration Manager-Clients heruntergeladen werden soll:  

  -   Windows-Computer (z. B. Desktops, Server, Laptops)  

  -   Von Configuration Manager registrierte mobile Geräte  

  -   Macintosh-Computer  

  -   Computer, auf denen Linux oder UNIX ausgeführt wird  

-   **Benutzerrichtlinienabruf auf Clients aktivieren**  

   Wenn Sie diese Option auf **Wahr** oder **Ja** festlegen, und Configuration Manager [den Benutzer ermittelt hat](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), erhalten Clients auf Computern speziell auf den angemeldeten Benutzer abgestimmte Anwendungen und Programme.  

   Da die Liste der für Benutzer verfügbaren Software vom Standortserver an den Anwendungskatalog übertragen wird, muss für diese Einstellung die Option **Wahr** oder **Ja** ausgewählt werden, damit Benutzer die Anwendungen über den Anwendungskatalog anzeigen und anfordern können. Wenn diese Einstellung aber auf **Falsch** oder **Nein**festgelegt wurde, wird die Verwendung des Anwendungskatalogs wie folgt eingeschränkt:  

  -   Den Benutzern ist es nicht möglich, die im Anwendungskatalog angezeigten Anwendungen zu installieren.  

  -   Benutzer sehen keine Benachrichtigungen zu ihren Genehmigungsanforderungen für Anwendungen. Sie müssen stattdessen den Anwendungskatalog aktualisieren und den Genehmigungsstatus überprüfen.  

  -   Benutzer erhalten keine Revisionen und Updates für Anwendungen, die im Anwendungskatalog veröffentlicht werden. Sie können jedoch im Anwendungskatalog Änderungen an Anwendungsinformationen sehen.  

  -   Wenn Sie eine Anwendungsbereitstellung nach der Installation der Anwendung aus dem Anwendungskatalog entfernen, wird noch bis zu 2 Tage lang von den Clients geprüft, ob die Anwendung installiert ist.  

   Wenn für diese Einstellung die Option **Falsch** oder **Nein** gewählt wurde, erhalten Benutzer zudem keine erforderlichen Anwendungen, die Sie für Benutzer bereitstellen, und auch keine anderen Verwaltungsaufgaben, die in Benutzerrichtlinien enthalten sind.  

   Diese Einstellung gilt für Benutzer, deren Computer mit dem Intranet und dem Internet verbunden sind. Es muss **Wahr** oder **Ja** festgelegt sein, wenn Sie auch Benutzerrichtlinien im Internet aktivieren möchten.  

-   **Benutzerrichtlinienanforderungen von Internetclients aktivieren**  

   Wenn der Client und der Standort für die internetbasierte Clientverwaltung konfiguriert sind, und Sie diese Option auf **Wahr** oder **Ja** setzen, erhalten Benutzer eine Benutzerrichtlinie, wenn ihr Computer mit dem Internet verbunden ist, und die beiden folgenden Bedingungen erfüllt sind:  

  -   Die Clienteinstellung **Enable user policy polling on clients** (Benutzerrichtlinie auf Clients aktivieren) ist auf **Wahr** oder **Enable user policy polling on clients** (Benutzerrichtlinie auf Clients aktivieren) ist auf **Ja** festgesetzt.  

  -   Der Benutzer wird vom internetbasierten Verwaltungspunkt erfolgreich mithilfe der Windows-Authentifizierung (Kerberos oder NTLM) authentifiziert.  

   Wenn Sie für diese Einstellungen **Falsch** oder **Nein**verwenden oder eine der Bedingungen nicht zutrifft, werden an einen Computer im Internet nur Computerrichtlinien übertragen. In diesem Fall können Benutzer weiterhin Anwendungen über einen internetbasierten Anwendungskatalog anzeigen, anfordern und installieren. Wenn diese Einstellung auf **Falsch** oder **Nein** gesetzt wurde, aber die Option **Enable user policy polling on clients** (Benutzerrichtlinienabruf auf Clients aktivieren) auf **Wahr** oder die Option **Benutzerrichtlinie auf Clients aktivieren** auf **Ja**gesetzt ist, erhalten Benutzer erst nach Trennen der Internetverbindung Benutzerrichtlinien.  

   Weitere Informationen zur Clientverwaltung im Internet finden Sie unter [Considerations for client communications from the Internet or an untrusted forest (Überlegungen zur Clientkommunikation aus dem Internet oder aus einer nicht vertrauenswürdigen Gesamtstruktur)](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in [Communications between endpoints in System Center Configuration Manager(Datenübertragungen zwischen Endpunkten in System Center Configuration Manager)](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

  > [!NOTE]  
  >  Genehmigungsanforderungen für Anwendungen von Benutzern erfordern keine Benutzerrichtlinien oder Benutzerauthentifizierung.  

##  <a name="compliance-settings"></a>Kompatibilitätseinstellungen  

-   **Kompatibilitätsauswertung planen**  

     Wählen Sie **Zeitplan** aus, um den Standardzeitplan zu erstellen, der Benutzern angezeigt, wenn diese eine Konfigurationsbaseline bereitstellen. Dieser Wert kann im Dialogfeld **Konfigurationsbasislinie bereitstellen** für jede Basislinie konfiguriert werden.  

-   **Benutzerdaten und Profile aktivieren**  

     Wählen Sie **Ja** aus, wenn Sie Konfigurationselemente für [Benutzerdaten und Profile](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) auf Windows 8-Computern in der Hierarchie bereitstellen möchten.  

## <a name="computer-agent"></a>Computer-Agent  

-   **Websitepunkt des Standardanwendungskatalogs**  

     Diese Einstellung wird von Configuration Manager verwendet, um Benutzer über das Softwarecenter mit dem Anwendungskatalog zu verbinden. Sie können für einen Server, von dem der Anwendungskatalog-Websitepunkt gehostet wird, den NetBIOS-Namen oder FQDN angeben. Alternativ können Sie die automatische Erkennung verwenden oder eine URL für benutzerdefinierte Bereitstellungen angeben. Die automatische Erkennung stellt aus folgenden Gründen meist die beste Lösung dar:  

    -   Clients wird automatisch ein Anwendungskatalog-Websitepunkt von ihrem Standort zugewiesen, sofern ihr Standort über einen Anwendungskatalog-Websitepunkt verfügt.  

    -   Anwendungskatalog-Websitepunkte im Intranet, die für HTTPS konfiguriert sind, haben Vorrang vor Anwendungskatalog-Websitepunkten, die nicht für HTTPS konfiguriert sind. Dadurch wird der Schutz vor nicht autorisierten Servern verstärkt.

    -   Clients, die für die intranet- und internetbasierte Clientverwaltung konfiguriert sind, wird ein internetbasierter Anwendungskatalog-Websitepunkt zugewiesen, wenn sie sich im Internet befinden. Wenn sie sich im Intranet befinden, wird ihnen ein intranetbasierter Anwendungskatalog-Websitepunkt zugewiesen.  

     Bei der automatischen Ermittlung kann nicht garantiert werden, dass Clients der nächstgelegene Anwendungskatalog-Websitepunkt zugewiesen wird. Aus den folgenden Gründen ist die Verwendung von **Automatisch ermitteln** für Ihre Zwecke möglicherweise nicht geeignet:  

     -   Sie möchten den nächstgelegenen Server für Clients manuell konfigurieren oder dafür sorgen, dass die Verbindung mit dem Server nicht über eine langsame Netzwerkverbindung erfolgt.  

     -   Sie möchten steuern, von welchen Clients mit welchen Servern eine Verbindung hergestellt wird. Dies kann zu Testzwecken bzw. aus leistungsbezogenen oder geschäftlichen Gründen erforderlich sein.  

     -   Sie möchten nicht bis zu 25 Stunden auf eine Netzwerkänderung für Clients warten, die mit einem anderen Anwendungskatalog-Websitepunkt konfiguriert werden sollen.  

     Wenn Sie den Anwendungskatalog-Websitepunkt angeben, anstatt die automatische Erkennung zu verwenden, geben Sie anstelle des Intranet-FQDN den NetBIOS-Namen an. Dadurch verringert sich die Wahrscheinlichkeit, dass Benutzer zur Eingabe von Anmeldeinformationen aufgefordert werden, wenn Sie eine Verbindung mit dem Anwendungskatalog im Intranet herstellen. Sie können den NetBIOS-Namen nur verwenden, wenn die folgenden Bedingungen erfüllt sind:  

     -   Der NetBIOS-Name ist in den Eigenschaften des Anwendungskatalog-Websitepunkts angegeben.  

     -   Sie verwenden WINS, oder alle Clients befinden sich in der gleichen Domäne wie der Anwendungskatalog-Websitepunkt.  

     -   Der Anwendungskatalog-Websitepunkt ist für HTTP- oder HTTPS-Clientverbindungen konfiguriert. Das Webserverzertifikat enthält den NetBIOS-Namen.  

     Benutzer werden in der Regel zur Eingabe von Anmeldeinformationen aufgefordert, wenn die URL über einen FQDN verfügt. Dies ist nicht der Fall, wenn die URL ein NetBIOS-Name ist. Sie können davon ausgehen, dass Benutzer beim Herstellen einer Verbindung über das Internet immer zur Eingabe von Anmeldeinformationen aufgefordert werden, da für diese Verbindung der Internet-FQDN verwendet werden muss. Wenn Benutzer im Internet zur Eingabe von Anmeldeinformationen aufgefordert werden, achten Sie darauf, dass von dem Server, von dem der Anwendungskatalog-Websitepunkt ausgeführt wird, eine Verbindung mit einem Domänencontroller für das Benutzerkonto hergestellt werden kann, damit die Authentifizierung des Benutzers über Kerberos möglich ist.  

    > [!NOTE]  
    >  Funktionsweise der automatischen Erkennung:  
    >   
    >  Vom Client wird eine Dienstidentifizierungsanforderung an einen Verwaltungspunkt gesendet. Wenn es an dem Standort, an dem der Client sich befindet, einen Anwendungskatalog-Websitepunkt gibt, wird der Client angewiesen, diesen Server als Anwendungskatalog-Server zu verwenden. Wenn an dem Standort mehrere Anwendungskatalog-Websitepunkte verfügbar sind, hat ein HTTPS-fähiger Server Vorrang vor einem Server, der nicht für HTTPS aktiviert ist. Nach dieser Filterung wird allen Clients einer der Server als Anwendungskatalog zugewiesen. In Configuration Manager wird kein Lastenausgleich zwischen mehreren Servern ausgeführt. Wenn der Standort des Clients nicht über einen Anwendungskatalog-Websitepunkt verfügt, wird vom Verwaltungspunkt auf nicht deterministische Weise ein Anwendungskatalog-Websitepunkt aus der Hierarchie zurückgegeben.  
    >   
    >  Wenn der Client sich im Intranet befindet und der ausgewählte Anwendungskatalog-Websitepunkt mit einem NetBIOS-Namen für die Anwendungskatalog-URL konfiguriert ist, wird dieser NetBIOS-Name anstelle des Intranet-FQDN an Clients übermittelt. Wenn der Client sich im Internet befindet, wird nur der Internet-FQDN an ihn übermittelt.  
    >   
    >  Diese Dienstidentifizierungsanforderung wird vom Client alle 25 Stunden sowie bei jeder Netzwerkänderung gestellt. Wenn der Client beispielsweise vom Internet zum Internet verschoben und ein internetbasierter Verwaltungspunkt gefunden wird, werden den Clients vom internetbasierten Verwaltungspunkt Server für internetbasierte Anwendungskatalog-Websitepunkte zugewiesen.  

-   **Standardanwendungskatalog-Website zur Internet Explorer-Zone der vertrauenswürdigen Sites hinzufügen**  

     Wenn diese Option auf **Wahr** oder **Ja**eingestellt ist, wird die URL für die Website des aktuellen Standardanwendungskatalogs im Internet Explorer auf Clients automatisch der Zone der vertrauenswürdigen Sites hinzugefügt.  

     Durch diese Einstellung wird sichergestellt, dass die Internet Explorer-Einstellung für Geschützter Modus nicht aktiviert wird. Ist der geschützte Modus aktiviert, können vom Configuration Manager-Client möglicherweise keine Anwendungen aus dem Anwendungskatalog installiert werden. Von der Zone der vertrauenswürdigen Sites wird standardmäßig auch die Benutzeranmeldung beim Anwendungskatalog unterstützt, für die die Windows-Authentifizierung erforderlich ist.  

     Wenn Sie diese Option als **Falsch**konfigurieren, können von Configuration Manager-Clients möglicherweise keine Anwendungen aus dem Anwendungskatalog installiert werden, es sei denn, diese Internet Explorer-Einstellungen sind für die von den Clients verwendete Anwendungskatalog-URL in einer anderen Zone konfiguriert.  

    > [!NOTE]  
    >  Wenn ein Standardanwendungskatalog von Configuration Manager der Zone der vertrauenswürdigen Standorte hinzugefügt wird, wird von Configuration Manager zunächst eine frühere Standardanwendungskatalog-URL entfernt, die von Configuration Manager hinzugefügt wurde. Danach wird ein neuer Eintrag hinzugefügt.  
    >   
    >  Die URL kann von Configuration Manager nicht hinzugefügt werden, wenn sie bereits in einer der Sicherheitszonen angegeben ist. In diesem Fall müssen Sie entweder die URL aus der anderen Zone entfernen, oder die erforderlichen Internet Explorer-Einstellungen manuell konfigurieren.  

-   **Ausführen von Silverlight-Anwendungen im Modus mit höherer Vertrauensstellung zulassen**  

     Diese Einstellung muss auf **Ja** festgelegt sein, wenn Benutzer den Configuration Manager-Client ausführen und den Anwendungskatalog verwenden.  

     Eine Änderung dieser Einstellung wird wirksam, wenn Benutzer ihren Browser das nächste Mal laden oder wenn sie das gegenwärtig geöffnete Browserfenster aktualisieren.  

     Weitere Informationen zu dieser Einstellung finden Sie unter [Certificates for Microsoft Silverlight 5 and Elevated Trust Mode Required for the Application Catalog (Zertifikate für Microsoft Silverlight 5 und für den Anwendungskatalog erforderlicher Modus mit höherer Vertrauensstellung)](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5) in [Security and Privacy for Application Management in System Center Configuration Manager (Sicherheit und Datenschutz für die Anwendungsverwaltung in System Center Configuration Manager)](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   **Im Softwarecenter angezeigter Organisationsname**  

     Geben Sie den Namen ein, den Benutzer im Softwarecenter sehen. Diese Branding-Informationen helfen den Benutzern, diese Anwendung als vertrauenswürdige Quelle zu identifizieren.  

-   **Verwenden des neuen Softwarecenters**  

     Wenn aktiviert, verwenden alle Clientcomputer, für die diese Clienteinstellungen gelten, das neue Softwarecenter. Das Softwarecenter zeigt für Benutzer verfügbare Apps an, auf die vorher nur im Silverlight-abhängigen Anwendungskatalog zugegriffen werden konnte.  

     Die Standortsystemrollen „Anwendungskatalog-Websitepunkt“ und „Anwendungskatalog-Webdienstpunkt“ sind nach wie vor erforderlich, damit für Benutzer verfügbare Apps im Softwarecenter angezeigt werden.  

     Weitere Informationen finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung in System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Installationsberechtigungen**  

    > [!WARNING]  
    >  Diese Einstellung gilt für den Anwendungskatalog und das Softwarecenter. Diese Einstellung hat keine Auswirkungen, wenn Benutzer das Unternehmensportal verwenden.  

     Konfigurieren Sie, wie Benutzer die Installation von Software, Softwareupdates und Tasksequenzen initiieren können:  

    -   **Alle Benutzer**: Benutzer, die sich mit einer beliebigen Berechtigung mit Ausnahme von "Gast" bei einem Clientcomputer angemeldet haben, können die Installation von Software, Softwareupdates und Tasksequenzen initiieren.  

    -   **Nur Administratoren**: Benutzer, die sich bei einem Clientcomputer angemeldet haben, müssen der lokalen Administratorengruppe angehören, um die Installation von Software, Softwareupdates und Tasksequenzen zu initiieren.  

    -   **Nur Administratoren und Hauptbenutzer**: Benutzer, die sich bei einem Clientcomputer angemeldet haben, müssen der lokalen Administratorengruppe angehören oder ein Hauptbenutzer des Computers sein, um die Installation von Software, Softwareupdates und Tasksequenzen zu initiieren.  

    -   **Keine Benutzer**: Keiner der Benutzer, die sich bei einem Clientcomputer angemeldet haben, kann die Installation von Software, Softwareupdates und Tasksequenzen initiieren. Erforderliche Bereitstellungen für den Computer werden immer am Stichtag installiert. Benutzer können die Installation von Software über den Anwendungskatalog oder das Softwarecenter nicht initiieren.  

-   **BitLocker-PIN-Eingabe bei Neustart anhalten**  

     Wenn die BitLocker-PIN-Eingabe auf Computern konfiguriert ist, kann die obligatorische Eingabe einer PIN bei einem Computerneustart nach einer Softwareinstallation umgangen werden.  

    -   **Immer**: BitLocker wird von Configuration Manager nach der Installation von Software, für die ein Neustart erforderlich ist, und der Initiierung eines Computerneustarts vorübergehend ausgesetzt. Diese Einstellung gilt nur für einen Computerneustart, der von Configuration Manager initiiert wird. Wenn der Benutzer den Computer neu startet, ist die Eingabe einer BitLocker-PIN weiterhin erforderlich. Die BitLocker-Anforderung zur Eingabe einer PIN wird nach dem Start von Windows wieder eingesetzt.

    -   **Nie**: BitLocker wird von Configuration Manager nach der Installation von Software, für die ein Neustart erforderlich ist, nicht ausgesetzt. In diesem Fall kann die Softwareinstallation erst abgeschlossen werden, wenn der Benutzer die PIN eingibt, um den Standardstartprozess abzuschließen und Windows zu laden.

-   **Bereitstellung von Anwendungen und Softwareupdates wird von zusätzlicher Software verwaltet**  

     Aktivieren Sie diese Option nur, wenn eine der folgenden Bedingungen zutrifft:  

    -   Sie verwenden eine Anbieterlösung, für die diese Einstellung aktiviert werden muss.  

    -   Sie verwalten Client-Agent-Benachrichtigungen und die Installation von Anwendungen und Softwareupdates mit dem Configuration Manager SDK (Software Development Kit).  

    > [!WARNING]  
    >  Wenn Sie diese Option auswählen, obwohl keine dieser Bedingungen erfüllt ist, werden Softwareupdates und erforderliche Anwendungen nicht auf Clients installiert. Durch diese Einstellung wird nicht verhindert, dass Benutzer Anwendungen über den Anwendungskatalog installieren, oder dass Pakete, Programme und Tasksequenzen auf Clientcomputern installiert werden.  

-   **PowerShell-Ausführungsrichtlinie**  

     Konfigurieren Sie, wie Windows PowerShell-Skripts von Configuration Manager-Clients ausgeführt werden können. Diese Skripts werden oft zur Erkennung von Konformitätseinstellungen in Konfigurationselementen eingesetzt. Sie können aber auch als Standardskripts in einer Bereitstellung gesendet werden.  

    -   **Umgehen**: Die Windows PowerShell-Konfiguration auf dem Clientcomputer wird vom Configuration Manager-Client umgangen, sodass nicht signierte Skripts ausgeführt werden können.  

    -   **Eingeschränkt**: Der Configuration Manager-Client verwendet die aktuelle Windows PowerShell-Konfiguration auf dem Client-Computer. Diese Konfiguration bestimmt, ob nicht signierte Skripts ausgeführt werden können.  

    -   **Alle signiert**: Nur die von einem vertrauenswürdigen Herausgeber signierten Skripts werden vom Configuration Manager-Client ausgeführt. Diese Einschränkung gilt unabhängig von der aktuellen Windows PowerShell-Konfiguration auf dem Clientcomputer.  

     Für diese Option ist mindestens Windows PowerShell 2.0 erforderlich. Der Standardwert ist **Alle Signiert**.  

    > [!TIP]  
    >  Wenn nicht signierte Skripts wegen dieser Clienteinstellung nicht ausgeführt werden können, wird dieser Fehler von Configuration Manager wie folgt gemeldet:  
    >   
    > -   Die Fehler-ID **0X87D00327** und die Beschreibung **Das Skript wurde nicht signiert** werden in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** als Bereitstellungsstatusfehler angezeigt.  
    > -   Der Fehlercode **0X87D00327** mit der Beschreibung **Script is not signed** (Das Skript wurde nicht signiert) bzw. **0X87D00320** mit der Beschreibung **The script host has not been installed yet** (Der Skripthost wurde noch nicht installiert) und dem Fehlertyp **Ermittlungsfehler** wird in Berichten angezeigt. Ein Beispiel ist **Details zu Fehlern von Konfigurationselementen in einer Konfigurationsbaseline für einen Bestand**.  
    > -   Die Meldung **Script is not signed (Error: 87D00327; Source: CCM)** wird in der Datei **DcmWmiProvider.log** angezeigt.  

-   **Benachrichtigung für neue Bereitstellungen anzeigen**  

     Wählen Sie **Ja** aus, wenn eine Benachrichtigung für Bereitstellungen angezeigt werden soll, die erst seit weniger als einer Woche verfügbar sind.  Diese Nachricht wird jedes Mal angezeigt, wenn der Client-Agent startet wird.

-   **Zufällige Stichtaganordnung deaktivieren**  

     Mit dieser Einstellung bestimmen Sie, ob vom Client bei der Installation erforderlicher Softwareupdates eine Aktivierungsverzögerung von bis zu zwei Stunden verwendet wird, wenn der Stichtag erreicht wurde. Die Aktivierungsverzögerung ist standardmäßig deaktiviert.  

     Bei Verwendung einer virtuellen Desktopinfrastruktur (VDI) lassen sich dank dieser Verzögerung die Prozessorauslastung und die Datenübertragung für einen Computer, der mehrere virtuelle Maschinen mit dem Configuration Manager-Client hat, verteilen. Selbst wenn Sie VDI nicht verwenden, und die gleichen Updates von vielen Clients gleichzeitig installiert werden, kann dies zu einer negativen Steigerung der CPU-Auslastung auf dem Standortserver führen. Außerdem kann es zu einer Verlangsamung der Verteilungspunkte und einer erheblichen Verringerung der verfügbaren Netzwerkbandbreite kommen.  

     Wenn erforderliche Softwareupdates am Stichtag ohne Verzögerung installiert werden müssen, wählen Sie für diese Einstellung **Ja** aus.  

-   **Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)**

     In einigen Fällen empfiehlt es sich, Benutzern mehr Zeit zum Installieren von erforderlichen Anwendungsbereitstellungen oder Softwareupdates, über die von Ihnen konfigurierten Fristen hinaus, zu geben. Dies kann erforderlich sein, wenn ein Computer für einen längeren Zeitraum ausgeschaltet war und eine große Anzahl von Anwendungs- oder Updatebereitstellungen installieren muss. Wenn z.B. ein Endbenutzer gerade aus dem Urlaub zurückgekehrt ist, muss er möglicherweise sehr lange warten, bis überfällige Anwendungsbereitstellungen installiert werden. Sie können eine Karenzzeit für die Erzwingung definieren, um dieses Problem zu lösen, indem Sie die Configuration Manager-Clienteinstellungen für eine Sammlung bereitstellen.

     Sie können eine Karenzzeit von 1 bis 120 Stunden festlegen. Diese Einstellung wird in Verbindung mit der Bereitstellungseigenschaft **Erzwingung für diese Bereitstellung basierend auf den Benutzereinstellungen verzögern** verwendet. Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](/sccm/apps/deploy-use/deploy-applications).

##  <a name="computer-restart"></a>Computerneustart  
 Achten Sie beim Angeben dieser Einstellungen für den Computerneustart darauf, dass die Intervalle für die temporäre Neustartbenachrichtigung und den endgültigen Countdown kürzer sind als das kürzeste auf den Computer angewendete Wartungsfenster.  

 Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="endpoint-protection"></a>Endpoint Protection  

-   **Verwalten des Endpoint Protection-Clients auf Clientcomputern**  

     Wählen Sie **Wahr** oder **Ja** aus, wenn Sie vorhandene Endpoint Protection-Clients auf Computern in Ihrer Hierarchie verwalten möchten.  

     Wählen Sie diese Option aus, wenn der Endpoint Protection-Client bereits installiert ist, und Sie ihn mit Configuration Manager verwalten möchten.  

     Wählen Sie diese Option auch dann aus, wenn Sie ein Skript zum Deinstallieren einer bestehenden Antischadsoftwarelösung sowie zum Installieren des Endpoint Protection-Clients erstellen und das Skript mithilfe einer Configuration Manager-Anwendung bzw. eines Pakets und Programms bereitstellen möchten.  

-   **Installieren des Endpoint Protection-Clients auf Clientcomputern**  

     Wählen Sie **Wahr** oder **Ja** aus, um den Endpoint Protection-Client auf Clientcomputern zu installieren und zu aktivieren, auf denen er noch nicht installiert wurde.  

    > [!NOTE]  
    >  Wenn der Endpoint Protection-Client bereits installiert ist, wird dieser durch die Auswahl von **Falsch** oder **Nein** nicht deinstalliert. Legen Sie zum Deinstallieren des Endpoint Protection-Clients die Clienteinstellung **Endpoint Protection-Client auf Clientcomputern verwalten** auf **Falsch** oder **Nein** fest. Stellen Sie dann ein Paket und Programm zum Deinstallieren des Endpoint Protection-Clients bereit.  

-   **Für Windows Embedded-Geräte mit Schreibfiltern Commit für Endpoint Protection-Clientinstallation ausführen (hierdurch werden Neustarts erforderlich)**  

     Wählen Sie **Ja** aus, um den Schreibfilter auf dem Windows Embedded-Gerät zu deaktivieren und das Gerät neu zu starten. Hierdurch wird für die Installation auf dem Gerät ein Commit ausgeführt.  

     Bei Angabe von **Nein** wird der Client auf einem temporären Overlay installiert, das beim Neustart des Geräts gelöscht wird. In diesem Fall wird für den Endpoint Protection-Client erst dann ein Commit ausgeführt, wenn von einer anderen Installation Änderungen auf dem Gerät ausgeführt werden. Dies ist die Standardeinstellung.  

-   **Erforderliche Neustarts nach der Installation des Endpoint Protection-Clients unterdrücken**  

     Wählen Sie **Wahr** oder **Ja** aus, um einen Computerneustart zu unterdrücken, sofern dieser nach der Installation des Endpoint Protection-Clients erforderlich ist.  

    > [!IMPORTANT]  
    >  Wenn für den Endpoint Protection-Client ein Computerneustart erforderlich ist und diese Einstellung als **Falsch** festgelegt ist, wird der Neustart unabhängig von konfigurierten Wartungsfenstern ausgeführt.  

-   **Zulässiges Zeitintervall (Stunden), um das Benutzer einen für den Abschluss der Installation von Endpoint Protection erforderlichen Neustart verschieben können**  

     Geben Sie die Anzahl der Stunden an, um die Benutzer einen Computerneustart verschieben können, sofern dieser nach der Installation des Endpoint Protection-Clients erforderlich ist. Diese Option kann nur dann konfiguriert werden, wenn für die Option **Erforderliche Neustarts nach der Installation des Endpoint Protection-Clients unterdrücken** die Einstellung **Falsch** festgelegt wird.  

-   **Disable alternate sources (like Windows Update, Microsoft Windows Server Update Services, or UNC shares) for the initial definition update on client computers** (Alternative Quellen (wie z.B. Windows Update, Microsoft Windows Server Update Services oder UNC-Freigaben) für das erste Definitionsupdate auf Clientcomputern deaktivieren)  

     Wählen Sie **Wahr** oder **Ja** aus, wenn durch Configuration Manager nur das erste Definitionsupdate auf Clientcomputern installiert werden soll. Diese Einstellung kann hilfreich sein, um bei der ersten Installation des Definitionsupdates überflüssige Netzwerkverbindungen zu vermeiden und die Auslastung der Netzwerkbandbreite zu verringern.  

##  <a name="hardware-inventory"></a>Hardwareinventur  

-   **Maximale benutzerdefinierte MIF-Dateigröße (KB)**  

     Geben Sie die maximale zulässige Größe (in Kilobytes) einer einzelnen benutzerdefinierten MIF-Datei (Management Information Format) an, die auf einem Client während eines Hardwareinventurzyklus gesammelt wird. Wenn eine MIF-Datei diese Größe überschreitet, wird sie von der Configuration Manager-Hardwareinventur nicht verarbeitet. Sie können eine Größe von 1 bis 5.000 KB angeben. Standardmäßig ist diese Option auf 250 KB festgelegt. Diese Einstellung wirkt sich nicht auf die Größe der regulären Hardwareinventur-Datendatei aus.  

    > [!NOTE]  
    >  Diese Einstellung ist nur in den Clientstandardeinstellungen verfügbar.  

-   **Hardwareinventurklassen**  

     In Configuration Manager können Sie die von Clients gesammelten Hardwareinformationen ohne manuelles Editieren der Datei sms_def.mof erweitern. Wählen Sie **Klassen festlegen** aus, wenn Sie die Configuration Manager-Hardwareinventur erweitern möchten. Weitere Informationen finden Sie unter [How to configure hardware inventory in System Center Configuration Manager (Konfigurieren der Hardwareinventur in System Center Configuration Manager)](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **MIF-Dateien sammeln**  

     Mit dieser Einstellung können Sie angeben, ob bei der Hardwareinventur MIF-Dateien von Configuration Manager-Clients gesammelt werden sollen.  

     Damit eine MIF-Datei durch die Hardwareinventur gesammelt werden kann, muss sie sich im korrekten Verzeichnis auf dem Clientcomputer befinden. Standardmäßig befinden sich die Dateien in folgenden Verzeichnissen:  

    -   IDMIF-Dateien sollten sich im Ordner „Windows\System32\CCM\Inventory\Idmif“ befinden.  

    -   NOIDMIF-Dateien sollten sich im Ordner „Windows\System32\CCM\Inventory\Noidmif“ befinden.  

    > [!NOTE]  
    >  Diese Einstellung ist nur in den Clientstandardeinstellungen verfügbar.

-   **Maximale zufällige Verzögerung**

    Die Sammlung von Hardwareinformationen wird um bis zu vier Stunden zufällig festgelegt, damit der Vorgang nicht auf allen Clients gleichzeitig stattfindet. Sie können die maximale Verzögerung festlegen, um die Zeit zu beschränken, während der Vorgang durchgeführt wird.      

##  <a name="metered-internet-connections"></a>Getaktete Internetverbindungen  
 Sie können die Kommunikation zwischen Windows 8-Clientcomputern und Configuration Manager-Standorten verwalten, sofern getaktete Internetverbindungen verwendet werden. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.  

> [!NOTE]  
>  Die konfigurierte Clienteinstellung wird in den folgenden Fällen nicht auf Windows 8-Clientcomputer angewendet:  
>   
> -   Der Computer befindet sich in einer Roamingdatenverbindung: Vom Configuration Manager-Client werden keine Vorgänge ausgeführt, bei denen Daten an Configuration Manager-Standorte übertragen werden müssen.  
> -   Die Eigenschaften der Windows-Netzwerkverbindung sind als nicht getaktet konfiguriert: Die Daten werden vom Configuration Manager-Client wie bei nicht getakteten Internetverbindungen an die Configuration Manager-Standorte übertragen.  

-   **Clientkommunikation über getaktete Internetverbindungen**  

     Wählen Sie in der Dropdownliste eine der folgenden Optionen für Windows 8-Clientcomputer aus:  

    -   **Zulassen**: Die gesamte Clientkommunikation kann über die getaktete Internetverbindung stattfinden, es sei denn, vom Clientgerät wird eine Roamingdatenverbindung verwendet.  

    -   **Grenzwert**: Nur die folgende Clientkommunikation ist über die getaktete Internetverbindung zulässig:  

        -   Clientrichtlinienabruf  

        -   An den Standort zu sendende Meldungen zum Clientzustand  

        -   Softwareinstallationsanforderungen über den Anwendungskatalog  

        -   Erforderliche Bereitstellungen (bei Erreichen des Installationsstichtags)  

        > [!IMPORTANT]  
        >  Softwareinstallationen, die von einem Benutzer über das Softwarecenter oder den Anwendungskatalog initiiert werden, sind unabhängig von den Einstellungen der getakteten Internetverbindung stets zulässig.  

         Wenn das Datenübertragungslimit der getakteten Internetverbindung erreicht wurde, wird vom Client nicht mehr versucht, mit Configuration Manager-Standorten zu kommunizieren.  

    -   **Blockieren**: Vom Configuration Manager-Client wird nicht versucht, mit Configuration Manager-Standorten zu kommunizieren, wenn eine getaktete Internetverbindung vorliegt. Dies ist der Standardwert.  

##  <a name="power-management"></a>Energieverwaltung  

-   **Benutzern das Ausschließen ihres Geräts aus der Energieverwaltung gestatten**  

     Wählen Sie in der Dropdownliste **Wahr** oder **Ja** aus, damit Softwarecenter-Benutzer ihre Computer von den konfigurierten Energieverwaltungseinstellungen ausschließen können.  

-   **Aktivierungsproxy zulassen**  

     Geben Sie **Ja** an, um die Wake-On-LAN-Einstellung des Standorts zu ergänzen, wenn diese für Unicastpakete konfiguriert ist.  

     Weitere Informationen zum Aktivierungsproxy finden Sie unter [Plan how to wake up clients in System Center Configuration Manager (Planen der Aktivierung von Clients in System Center Configuration Manager)](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  Machen Sie sich mit der Funktionsweise eines Aktivierungsproxys vertraut, und bewerten Sie ihn in einer Testumgebung, bevor Sie ihn in einem Produktionsnetzwerk aktivieren.  

-   **Portnummer für Aktivierungsproxy (UDP)**  

     Übernehmen Sie den Standardwert für die Portnummer, über die Aktivierungspakete von Manager-Computern an Computer im Energiesparmodus gesendet werden. Sie können die Nummer auch durch einen beliebigen Wert ersetzen.  

     Die hier angegebene Portnummer wird automatisch für Clients konfiguriert, auf denen Windows-Firewall ausgeführt wird, wenn Sie die Option **Windows-Firewall-Ausnahme für Aktivierungsproxy** verwenden. Falls auf Clients eine andere Firewall ausgeführt wird, müssen Sie diese manuell so konfigurieren, dass die für diese Einstellung angegebene UDP-Portnummer zugelassen wird.  

-   **Wake-On-LAN-Portnummer (UDP)**  

     Behalten Sie den Standardwert 9 bei, es sei denn, Sie haben die Wake-On-LAN-Portnummer (UDP) in den **Eigenschaften** des Standorts auf der Registerkarte **Ports** geändert.  

    > [!IMPORTANT]  
    >  Dieser Wert muss mit dem Wert in den **Eigenschaften**des Standorts übereinstimmen. Wenn Sie den Wert an einem Ort ändern, wird er am anderen Ort nicht automatisch aktualisiert.  

##  <a name="remote-tools"></a>Remotetools  

-   **Remotesteuerung auf Clients aktivieren** mit der Beschreibung **Firewallausnahmeprofile**  

     Wählen Sie aus, ob die Configuration Manager-Remotesteuerung für alle Clientcomputer aktiviert wird, die diese Clienteinstellungen erhalten. Wählen Sie **Konfigurieren** aus, um die Remotesteuerung zu aktivieren. Konfigurieren Sie optional die Firewall-Einstellungen zum Zulassen der Remotesteuerung auf Clientcomputern.  

     Die Remotesteuerung ist standardmäßig deaktiviert.  

    > [!IMPORTANT]  
    >  Wenn die Firewall-Einstellungen nicht konfiguriert werden, funktioniert die Remotesteuerung möglicherweise nicht ordnungsgemäß.  

-   **Benutzer können Richtlinien- oder Benachrichtigungseinstellungen im Softwarecenter ändern**  

     Wählen Sie aus, ob Benutzer die Remotesteuerungsoptionen im Softwarecenter ändern können.  

-   **Remotesteuerung eines unbeaufsichtigten Computers zulassen**  

     Wählen Sie aus, ob ein Administrator die Remotesteuerung verwenden kann, um auf einen abgemeldeten oder gesperrten Computer zuzugreifen. Wenn diese Option deaktiviert ist, können nur angemeldete und nicht gesperrte Computer remote gesteuert werden.  

-   **Benutzer zur Vergabe der Berechtigung für Remotesteuerung auffordern**  

     Wählen Sie aus, ob vom Clientcomputer eine Meldung angezeigt werden soll, in der die Erlaubnis des Benutzers angefordert wird, bevor eine Remotesitzung zugelassen wird.  

-   **Der lokalen Administratorgruppe Berechtigung zur Remotesteuerung gewähren**  

     Wählen Sie aus, ob lokale Administratoren auf dem Server, von dem die Remotesteuerungsverbindung initiiert wurde, Remotesteuerungssitzungen auf Clientcomputern herstellen können.  

-   **Zulässige Zugriffsstufe**  

     Geben Sie die zulässige Zugriffsstufe für die Remotesteuerung an. Es gibt folgende Auswahlmöglichkeiten:  

    -   Vollzugriff  

    -   Nur anzeigen  

    -   Keine  

-   **Zugelassene Viewer**  

     Wählen Sie **Betrachter festlegen** aus, um das Dialogfeld **Clienteinstellung konfigurieren** zu öffnen, und geben Sie die Namen der Windows-Benutzer an, die Remotesteuerungssitzungen auf Clientcomputern herstellen können.  

-   **Benachrichtigungssymbol für Sitzung auf Taskleiste anzeigen**  

     Wählen Sie diese Option aus, um ein Symbol auf der Taskleiste von Clientcomputern anzuzeigen, mit dem angegeben wird, dass eine Remotesteuerungssitzung aktiv ist.  

-   **Sitzungsverbindungsleiste anzeigen**  

     Wählen Sie diese Option aus, um eine deutlich sichtbare Sitzungsverbindungsleiste auf Clientcomputern anzuzeigen, mit der angegeben wird, dass eine Remotesteuerungssitzung aktiv ist.  

-   **Sound auf Client wiedergeben**  

     Wählen Sie diese Option aus, damit über einen Sound angegeben wird, dass eine Remotesteuerungssitzung auf einem Clientcomputer aktiv ist. Sie können einen Sound wiedergeben, wenn die Sitzung hergestellt oder getrennt wird. Weiterhin können Sie einen Sound auch wiederholt während der Sitzung wiedergeben.  

-   **Einstellungen für nicht angeforderte Remoteunterstützung verwalten**  

     Wählen Sie diese Option aus, um die Verwaltung nicht angeforderter Remoteunterstützungssitzungen durch Configuration Manager zuzulassen.  

     Bei nicht angeforderten Remoteunterstützungssitzungen hat der Benutzer am Clientcomputer zum Initiieren einer Sitzung keine Unterstützung angefordert.  

-   **Einstellungen für angeforderte Remoteunterstützung verwalten**  

     Wählen Sie diese Option aus, um die Verwaltung angeforderter Remoteunterstützungssitzungen durch Configuration Manager zuzulassen.  

     Bei angeforderten Remoteunterstützungssitzungen hat der Benutzer am Clientcomputer zum Initiieren einer Sitzung Unterstützung angefordert.  

-   **Zugriffsstufe für Remoteunterstützung**  

     Wählen Sie die Zugriffsstufe für Remoteunterstützungssitzungen aus, die über die Configuration Manager-Konsole initiiert werden.  

    > [!NOTE]  
    >  Vor jeder Remoteunterstützungssitzung muss der Benutzer am Clientcomputer dafür die Berechtigung gewähren.  

-   **Einstellungen für Remotedesktop verwalten**  

     Wählen Sie diese Option aus, um die Verwaltung von Remotedesktopsitzungen für Computer durch Configuration Manager zuzulassen.  

-   **Zugelassenen Betrachtern das Herstellen einer Verbindung über Remotedesktopverbindung erlauben**  

     Wählen Sie diese Option aus, um das Hinzufügen von Benutzern, die in der Liste der zugelassenen Betrachter angegeben sind, zur lokalen Remotedesktop-Benutzergruppe auf Clientcomputern zuzulassen.  

-   **Bei Computern mit Windows Vista oder höher Authentifizierung auf Netzwerkebene verlangen**  

     Wählen Sie diese sicherere Option aus, wenn Sie die Authentifizierung auf Netzwerkebene für das Herstellen von Remotedesktopverbindungen zu Clientcomputern verwenden möchten, auf denen Windows Vista oder höher ausgeführt wird. Für die Authentifizierung auf Netzwerkebene werden anfangs weniger Remotecomputerressourcen verbraucht, da die Benutzerauthentifizierung abgeschlossen ist, bevor eine Remotedesktopverbindung hergestellt wird. Diese Methode ist sicherer, da hierdurch der Computer vor böswilligen Benutzern oder Schadsoftware besser geschützt werden kann und das Risiko von DoS-Angriffen verringert wird.  

## <a name="software-deployment"></a>Softwarebereitstellung  

-   **Erneute Auswertung für Bereitstellungen planen**  

     Konfigurieren Sie einen Zeitplan für die Neuauswertung der Anforderungsregeln für alle Bereitstellungen durch Configuration Manager. Der Standardwert ist 7 Tage.  

    > [!IMPORTANT]  
    >  Es wird empfohlen, diesen Wert nicht auf einen niedrigeren Wert als den Standardwert zu ändern. Dies könnte sich negativ auf die Leistung des Netzwerks und der Clientcomputer auswirken.  

     Sie können diese Aktion auch auf einem Configuration Manager-Clientcomputer initiieren, indem Sie in der Systemsteuerung im Modul **Configuration Manager** auf der Registerkarte **Aktionen** die Aktion **Evaluationszyklus für die Anwendungsbereitstellung** auswählen.  

##  <a name="software-inventory"></a>Softwareinventur  

-   **Inventurberichtsdetail**  

     Geben Sie die Ebene der zu inventarisierenden Dateiinformationen an. Sie können Details zu der Datei, Details zu dem mit der Datei verknüpften Produkt oder alle Informationen zur Datei inventarisieren.  

-   **Diese Dateitypen inventarisieren**  

     Wenn Sie die Typen der zu inventarisierenden Dateien festlegen möchten, wählen Sie **Typen festlegen...** aus, und konfigurieren Sie dann im Dialogfeld **Clienteinstellung konfigurieren** die folgenden Einstellungen:  

    > [!NOTE]  
    >  Wenn mehr als eine benutzerdefinierte Clienteinstellung auf einen Computer angewendet wurde, werden die von allen Einstellungen zurückgegebenen Inventare zusammengeführt.  

    -   Wählen Sie das Symbol **Neu** aus, um einen neuen Dateityp zum Inventar hinzuzufügen. Geben Sie anschließend im Dialogfeld **Eigenschaften für inventarisierte Datei(en)** die folgenden Informationen an:  

        -   **Name**: Geben Sie einen Namen für die Datei an, die Sie inventarisieren möchten. Sie können das Sternchen (*\**) stellvertretend für eine beliebige Textzeichenfolge und das Fragezeichen (**?** ) stellvertretend für ein beliebiges einzelnes Zeichen angeben. Geben Sie als Dateinamen z.B. **\*.doc** an, um alle Dateien mit der Erweiterung „.doc“ zu inventarisieren.  

        -   **Ort**: Wählen Sie **Festlegen** aus, um das Dialogfeld **Pfadeigenschaften** zu öffnen. Sie können die Softwareinventur so konfigurieren, dass alle Clientfestplatten nach der angegebenen Datei, nach einem angegebenen Pfad (z.B. **C:\Ordner**) oder nach einer angegebenen Variablen (z.B. *%windir%*) durchsucht werden. Sie können auch alle Unterordner unter dem angegebenen Pfad durchsuchen.  

        -   **Verschlüsselte und komprimierte Dateien ausschließen**: Wenn Sie diese Option aktivieren, werden alle komprimierten oder verschlüsselten Dateien nicht inventarisiert.  

        -   **Dateien im Windows-Ordner ausschließen**: Wenn Sie diese Option aktivieren, werden alle Dateien im Windows-Ordner und seinen Unterordnern nicht inventarisiert.  

    -   Wählen Sie **OK** aus, um das Dialogfeld **Eigenschaften für inventarisierte Datei(en)** zu schließen.  

    -   Fügen Sie alle zu inventarisierenden Dateien hinzu, und wählen Sie dann **OK** aus, um das Dialogfeld **Clienteinstellung konfigurieren** zu schließen.  

-   **Dateien sammeln**  

     Wenn Sie Dateien von Clientcomputern sammeln möchten, wählen Sie **Dateien festlegen** aus, und konfigurieren Sie dann Folgendes:  

    > [!NOTE]  
    >  Wenn mehr als eine benutzerdefinierte Clienteinstellung auf einen Computer angewendet wurde, werden die von allen Einstellungen zurückgegebenen Inventare zusammengeführt.  

    -   Wählen Sie im Dialogfeld **Clienteinstellung konfigurieren** das Symbol **Neu** aus, um eine zu sammelnde Datei hinzuzufügen.  

    -   Geben Sie im Dialogfeld **Eigenschaften für gesammelte Datei(en)** die folgenden Informationen an:  

        -   **Name**: Geben Sie einen Namen für die Datei an, die Sie sammeln möchten. Sie können das Sternchen (*\**) stellvertretend für eine beliebige Textzeichenfolge und das Fragezeichen (**?** ) stellvertretend für ein beliebiges einzelnes Zeichen angeben.  

        -   **Ort**: Wählen Sie **Festlegen** aus, um das Dialogfeld **Pfadeigenschaften** zu öffnen. Sie können die Softwareinventur so konfigurieren, dass alle Clientfestplatten nach der zu sammelnden Datei, nach einem angegebenen Pfad (z.B. **C:\Ordner**) oder nach einer angegebenen Variable (z.B. *%windir%*) durchsucht werden. Sie können auch alle Unterordner unter dem angegebenen Pfad durchsuchen.  

        -   **Verschlüsselte und komprimierte Dateien ausschließen**: Wenn Sie diese Option auswählen, werden keine komprimierten oder verschlüsselten Dateien gesammelt.  

        -   **Dateisammlung beenden, wenn die Gesamtgröße der Dateien folgenden Wert (KB) überschreitet**: Geben Sie die Dateigröße (in KB) an, ab der keine der unter **Name** angegebenen Dateien mehr gesammelt wird.  

          > [!NOTE]  
          >  Die fünf zuletzt geänderten Versionen von gesammelten Dateien werden vom Standortserver gesammelt und im Verzeichnis *&lt;ConfigMgr-Installationsverzeichnis\>*\Inboxes\Sinv.box\Filecol gespeichert. Wenn eine Datei seit der letzten Softwareinventursammlung nicht geändert wurde, wird die Datei nicht noch einmal gesammelt.  
          >   
          >  Dateien mit mehr als 20 MB werden von der Softwareinventur nicht gesammelt.  
          >   
          >  Im Dialogfeld **Clienteinstellung konfigurieren** wird mit dem Wert **Maximale Größe aller gesammelten Dateien (KB)** die maximale Größe für alle gesammelten Dateien angezeigt. Wenn diese Größe erreicht ist, wird die Dateisammlung beendet. Alle bereits gesammelten Dateien werden beibehalten und an den Standortserver gesendet.  

          > [!IMPORTANT]
          >  Wenn Sie die Softwareinventur so konfigurieren, dass viele große Dateien gesammelt werden, kann sich dies nachteilig auf die Leistung des Netzwerks und Standortservers auswirken.  

        Informationen zum Anzeigen gesammelter Dateien finden Sie unter [How to use Resource Explorer to view software inventory in System Center Configuration Manager (Verwenden von Ressourcen-Explorer zum Anzeigen des Softwarebestands in System Center Configuration Manager)](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Wählen Sie **OK** aus, um das Dialogfeld **Eigenschaften für gesammelte Datei(en)** zu schließen.  

    -   Fügen Sie alle zu sammelnden Dateien hinzu, und klicken Sie dann auf **OK**, um das Dialogfeld **Clienteinstellung konfigurieren** zu schließen.  

-   **Namen festlegen**  

     Während der Softwareinventur werden Hersteller- und Produktnamen aus den Kopfzeileninformationen der Dateien abgerufen, die auf Clients am Standort installiert sind. Da diese Namen in den Dateiheaderinformationen nicht immer in standardisierter Form vorliegen, werden beim Anzeigen der Softwareinventurinformationen im Ressourcen-Explorer oder beim Ausführen von Abfragen mitunter verschiedene Versionen desselben Hersteller- oder Produktnamens angezeigt. Wenn Sie diese Anzeigenamen standardisieren möchten, wählen Sie **Namen festlegen** aus, und konfigurieren Sie dann im Dialogfeld **Clienteinstellung konfigurieren** die folgenden Einstellungen:  

    -   **Namenstyp**: Von der Softwareinventur werden Informationen zu Herstellern und Produkten gesammelt. Wählen Sie in der Dropdownliste aus, ob Sie Anzeigenamen für einen **Hersteller** oder ein **Produkt**konfigurieren möchten.  

    -   **Anzeigename**: Dient zum Festlegen des Anzeigenamens, den Sie anstelle der Namen in der Liste **Inventarisierte Namen** verwenden möchten. Sie können das Symbol **Neu** auswählen, um einen neuen Anzeigenamen anzugeben.  

    -   **Inventarisierte Namen:**: Wählen Sie das Symbol **Neu** aus, um einen neuen inventarisierten Namen hinzuzufügen, der bei der Softwareinventur durch den in der Liste **Anzeigename** markierten Namen ersetzt wird. Sie können mehrere Namen hinzufügen, die ersetzt werden.  

##  <a name="software-updates"></a>Softwareupdates  

-   **Softwareupdates auf Clients aktivieren**  

     Verwenden Sie diese Einstellung, um Softwareupdates auf Configuration Manager-Clients zu aktivieren. Wenn Sie diese Einstellung deaktivieren, werden die vorhandenen Bereitstellungsrichtlinien von Configuration Manager vom Client entfernt. Wenn Sie diese Einstellung wieder aktivieren, wird vom Client die aktuelle Bereitstellungsrichtlinie heruntergeladen.  

    > [!IMPORTANT]  
    >  Wenn Sie diese Einstellung deaktivieren, funktionieren NAP- und Konformitätseinstellungsrichtlinien nicht mehr, die auf der Softwareupdate-Geräteeinstellung basieren.  

-   **Zeitplan für Softwareupdateprüfung**  

     Mit dieser Einstellung geben Sie an, wie häufig vom Client eine Überprüfung der Softwareupdatekompatibilität initiiert wird. Bei der Kompatibilitätsüberprüfung wird der Zustand von Softwareupdates auf dem Client (z. B. erforderlich oder installiert) bestimmt. Weitere Informationen zur Kompatibilitätsbewertung finden Sie unter [Software updates compliance assessment (Bewertung der Kompatibilität von Softwareupdates)](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     Standardmäßig wird ein einfacher Zeitplan verwendet. Die Konformitätsprüfung wird alle 7 Tage initiiert. Nach Wunsch können Sie einen benutzerdefinierten Zeitplan erstellen und die genaue Startzeit am gewünschten Tag angeben. Sie können außerdem angeben, ob UTC oder die lokale Zeit verwendet werden soll, und das Wiederholungsintervall für einen bestimmten Wochentag konfigurieren.  

    > [!NOTE]  
    >  Wenn Sie ein Intervall von weniger als 1 Tag angeben können, wird in Configuration Manager automatisch der Standardwert von 1 Tag angezeigt.  

    > [!WARNING]  
    >  Die tatsächliche Startzeit auf Clientcomputern ist die Startzeit plus ein zufälliger Zeitraum von maximal 2 Stunden. Dies verhindert, dass mehrere Clientcomputer am aktiven Softwareupdatepunkt auf dem Server gleichzeitig den Suchvorgang starten und eine Verbindung mit Windows Server Update Services (WSUS) herstellen.  

-   **Bereitstellungsneuauswertung planen**  

     Geben Sie mit dieser Einstellung an, wie oft der Installationsstatus von Softwareupdates auf Configuration Manager-Clientcomputern vom Softwareupdateclient-Agent erneut bewertet werden soll. Wenn bereits installierte Softwareupdates nicht mehr auf Clientcomputern vorhanden, aber weiterhin erforderlich sind, werden sie erneut installiert.

     Der Zeitplan für die erneute Bewertung der Bereitstellung sollte basierend auf Unternehmensrichtlinien für Softwareupdatekonformität, der Eigenschaft von Benutzern, Softwareupdates zu deinstallieren und Ähnlichem angepasst werden. Beachten Sie dabei, dass bei jedem Zyklus der Bereitstellungsneuauswertung das Netzwerk und die CPU der Clientcomputer in gewissem Umfang in Anspruch genommen werden. Standardmäßig wird ein einfacher Zeitplan verwendet. Die Bereitstellungsneuauswertung wird alle 7 Tage initiiert.  

    > [!NOTE]  
    >  Wenn Sie ein Intervall von weniger als 1 Tag angeben können, wird in Configuration Manager automatisch der Standardwert von 1 Tag angezeigt.  

-   **Wenn der Stichtag für eine beliebige Softwareupdatebereitstellung erreicht wird, auch alle anderen Softwarebereitstellungen mit Stichtag innerhalb eines angegebenen Zeitraums installieren**  

     Verwenden Sie diese Einstellung, um alle Softwareupdates in erforderlichen Bereitstellungen zu installieren, deren Stichtage innerhalb eines angegebenen Zeitraums liegen. Wenn der Stichtag für eine erforderliche Softwareupdatebereitstellung erreicht wird, wird auf den Clients die Installation der Softwareupdates in der Bereitstellung initiiert. Mit dieser Einstellung wird bestimmt, ob auch die Installation von Softwareupdates in anderen erforderlichen Bereitstellungen, deren konfigurierter Stichtag innerhalb des angegebenen Zeitraums liegt, initiiert wird.  

     Verwenden Sie diese Einstellung, um die Installation der erforderlichen Softwareupdates zu beschleunigen, die Sicherheit zu verbessern, Benachrichtigungsanzeigen zu reduzieren und Systemneustarts auf Clientcomputern zu verringern. Diese Einstellung ist standardmäßig deaktiviert.  

-   **Alle anstehenden Bereitstellungen mit Stichtag in diesem Zeitraum werden auch installiert**  

     Verwenden Sie diese Einstellung, um den Zeitrahmen für die vorherige Einstellung anzugeben. Sie können einen Wert von 1 bis 23 Stunden und von 1 bis 365 Tagen eingeben. Der Standardwert liegt bei 7 Tagen.  

-   **Installation von Express-Installationsdateien auf Clients aktivieren**

-   **Port zum Herunterladen von Inhalten für Express-Installationsdateien**

-   **Erneutes Aktivieren des Office 365-Clients** Verwenden Sie diese Einstellung zum Aktivieren der Verwaltung des Office 365-Client-Agents. Wenn Sie den Wert auf **Ja** festlegen, können Sie Office 365-Installationseinstellungen konfigurieren, Dateien aus Office Content Delivery Networks (CDNs) herunterladen und die Dateien als Anwendung in Configuration Manager bereitstellen.

##  <a name="user-and-device-affinity"></a>Affinität zwischen Benutzer und Gerät  

-   **Nutzungsschwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät**  

     Geben Sie die Nutzungsdauer in Minuten an, nach der von Configuration Manager eine Affinität zwischen Benutzer und Gerät erstellt wird.  

-   **Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät**  

     Geben Sie die Anzahl von Tagen an, über die der Nutzungsschwellenwert für die Affinität zwischen Benutzer und Gerät gemessen wird.  

    > [!NOTE]  
    >  Beispiel: Wenn für **Nutzungsschwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät** ein Wert von **60** Minuten angegeben ist und für **Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät** ein Wert von **5** Tagen, muss der Benutzer das Gerät über einen Zeitraum von fünf Tagen insgesamt 60 Minuten lang nutzen, damit eine Affinität zwischen Benutzer und Gerät automatisch erstellt wird.  

-   **Affinität zwischen Benutzer und Gerät automatisch aus Verwendungsdaten konfigurieren**  

     Wählen Sie **Wahr** oder **Ja** aus, damit von Configuration Manager automatisch Affinitäten zwischen Benutzern und Geräten erstellt werden, die auf gesammelten Nutzungsstatistiken beruhen.  

##  <a name="mobile-devices"></a>Mobile Geräte  

-   **Anmeldungsprofil für mobile Geräte**  

     Bevor Sie diese Einstellung konfigurieren können, müssen Sie zunächst die Benutzereinstellung **Benutzern das Anmelden mobiler Geräte gestatten** für das mobile Gerät auf **Wahr**festlegen. Anschließend können Sie **Profil festlegen** auswählen, um ein Anmeldungsprofil mit Informationen zur Zertifikatvorlage für die Anmeldung, zum Standort, der einen Anmeldungspunkt und einen Anmeldungsproxypunkt enthält, und zum Standort anzugeben, über den das Gerät nach der Anmeldung verwaltet wird.  

    > [!IMPORTANT]  
    >  Stellen Sie vor dem Konfigurieren dieser Option sicher, dass Sie eine Zertifikatvorlage zur Verwendung für die Anmeldung mobiler Geräte konfiguriert haben.  

##  <a name="enrollment"></a>Anmeldung  

-   **Anmeldungsprofil für mobile Geräte**  

     Bevor Sie diese Einstellung konfigurieren können, müssen Sie zunächst die Benutzereinstellung **Benutzern die Anmeldung mobiler Geräte und von Macintosh-Computern gestatten** für die Anmeldung auf **Ja**festlegen. Anschließend können Sie **Profil festlegen** auswählen, um ein Anmeldungsprofil mit Informationen zur Zertifikatvorlage für die Anmeldung, zum Standort, der einen Anmeldungspunkt und einen Anmeldungsproxypunkt enthält, und zum Standort anzugeben, über den das Gerät nach der Anmeldung verwaltet wird.  

    > [!IMPORTANT]  
    >  Stellen Sie vor dem Konfigurieren dieser Option sicher, dass Sie eine Zertifikatvorlage für die Anmeldung mobiler Geräte oder für die Anmeldung per Macintosh-Clientzertifikat konfiguriert haben.  

## <a name="user-and-device-affinity"></a>Affinität zwischen Benutzer und Gerät  

-   **Benutzer das Festlegen primärer Geräte gestatten**  

     Geben Sie an, ob es Benutzern gestattet werden soll, im Anwendungskatalog auf der Registerkarte **Eigene Geräte** ihre eigenen primären Geräte zu identifizieren.  
