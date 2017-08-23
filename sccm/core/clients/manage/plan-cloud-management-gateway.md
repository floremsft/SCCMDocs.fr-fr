---
title: Planen von Cloud Management Gateway | Microsoft-Dokumentation
description: 
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: a7380ae781447880ffcba0778694ea62e10c4889
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planen von Cloud Management Gateway in Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1610 stellt das Cloudverwaltungsgateway eine einfache Methode für die Verwaltung von Configuration Manager-Clients im Internet dar. Der Cloudverwaltungsgateway-Dienst wird für Microsoft Azure bereitgestellt und erfordert ein Azure-Abonnement. Er stellt mithilfe einer neuen Rolle, die als Cloudverwaltungsgateway-Connectorpunkt bezeichnet wird, eine Verbindung mit der lokalen Configuration Manager-Infrastruktur her. Nachdem er bereitgestellt und konfiguriert wurde, können Clients auf lokale Configuration Manager-Standortsystemrollen zugreifen, unabhängig davon, ob sie sich im internen, privaten Netzwerk oder im Internet befinden.

> [!TIP]  
> In Version 1610 wird das Cloudverwaltungsgateway als vorab veröffentlichtes Feature vorgestellt. Wie Sie es aktivieren, erfahren Sie unter [Use pre-release features from updates (Verwenden von vorab veröffentlichten Features von Updates)](/sccm/core/servers/manage/pre-release-features).

Verwenden Sie die Configuration Manager-Konsole zum Bereitstellen des Diensts in Azure, zum Hinzufügen der Cloudverwaltungsgateway-Connectorpunktrolle sowie zum Konfigurieren von Standortsystemrollen, um den Cloudverwaltungsgateway-Datenverkehr zuzulassen. Der Cloudverwaltungsgateway unterstützt derzeit nur die Rollen „Verwaltungspunkt“ und „Softwareupdatepunkt“.

Client-Zertifikate und Zertifikate für Secure Socket Layer (SSL) sind erforderlich, um Computer zu authentifizieren und die Kommunikation zwischen den verschiedenen Ebenen des Diensts verschlüsseln. In der Regel erhalten die Clientcomputer ein Clientzertifikat über das Durchsetzen von Gruppenrichtlinien. Zum Verschlüsseln des Datenverkehrs zwischen Clients und Standortsystemserver, der die Rollen hostet, müssen Sie ein benutzerdefiniertes SSL-Zertifikat von der Zertifizierungsstelle erstellen. Darüber hinaus müssen Sie auch ein Verwaltungszertifikat in Azure einrichten, mit dem Configuration Manager den Cloudverwaltungsgateway-Dienst bereitstellen kann.

## <a name="requirements-for-cloud-management-gateway"></a>Anforderungen für das Cloudverwaltungsgateway

-   Die Clientcomputer und der Standortsystemserver führen den Cloudverwaltungsgateway-Connectorpunkt aus.

-   Benutzerdefinierte SSL-Zertifikate der internen Zertifizierungsstelle: Werden zum Verschlüsseln der Kommunikation der Clientcomputer und zum Authentifizieren der Identität des Cloudverwaltungsgateway-Diensts verwendet.

-   Azure-Abonnement für Clouddienste.

-   Azure-Verwaltungszertifikat ‒ Wird zur Authentifizierung von Configuration Manager mit Azure verwendet.

## <a name="specifications-for-cloud-management-gateway"></a>Spezifikationen für das Cloudverwaltungsgateway

- Jede Cloudverwaltungsgateway-Instanz unterstützt 4.000 Clients.
- Es wird empfohlen, zur Verbesserung der Verfügbarkeit mindestens zwei Cloudverwaltungsgateway-Instanzen zu erstellen.
- Der Cloudverwaltungsgateway unterstützt nur die Rollen „Verwaltungspunkt“ und „Softwareupdatepunkt“.
-   Die folgenden Funktionen in Configuration Manager werden derzeit für den Cloudverwaltungsgateway nicht unterstützt:

    -   Clientbereitstellung
    -   Automatische Standortzuweisung
    -   Richtlinien für Benutzer
    -   Anwendungskatalog (einschließlich Softwaregenehmigungsanforderungen)
    -   Vollständige Betriebssystembereitstellung (OSD)
    -   Configuration Manager-Konsole
    -   Remotetools
    -   Berichterstellungswebsite
    -   Wake-On-LAN
    -   Mac-, Linux- und UNIX-Clients
    -   Azure Resource Manager
    -   Peercache
    -   Lokale Verwaltung mobiler Geräte

## <a name="cost-of-cloud-management-gateway"></a>Kosten des Cloudverwaltungsgateways

>[!IMPORTANT]
>Die nachfolgenden Kosteninformationen stellen lediglich Schätzwerte dar. Ihre Umgebung weist möglicherweise andere Variablen auf, die sich auf die Gesamtkosten für die Verwendung eines Cloudverwaltungsgateways auswirken.

Das Cloudverwaltungsgateway verwendet die folgende Funktionen von Microsoft Azure, die das Azure-Abonnementkonto belasten:

-   Virtuelle Maschine

    -   Das Cloudverwaltungsgateway erfordert derzeit einen virtuellen Computer der Größe Standard\_A2. Beim Erstellen des Diensts können Sie auswählen, wie viele virtuelle Computer der Dienst unterstützen soll (die Standardeinstellung lautet „1“).

    -   Beachten Sie für Ihre Schätzung, dass ein einzelner virtueller Azure-Computer der Größe Standard\_A2 ca. 2.000 internetbasierte Clients gleichzeitig unterstützen kann.

    -   Der [Azure-Preisrechner](https://azure.microsoft.com/en-us/pricing/calculator/) hilft Ihnen, die potenziellen Kosten zu ermitteln.

      >[!NOTE]
      >Die Kosten für virtuelle Computer variieren je nach Region.

-   Ausgehende Datenübertragungen

    -   Für die von dem Dienst übertragenen Daten fallen Gebühren an. Beachten Sie die [Preisübersicht „Bandbreite“ für Azure](https://azure.microsoft.com/en-us/pricing/details/bandwidth/), um die potenziellen Kosten zu ermitteln.

    -   Rechnen Sie als Schätzwert mit ca. 100 MB pro Client und Monat für internetbasierte Clients, mit denen stündlich Richtlinien aktualisiert werden.

    >[!NOTE]
    > Durch das Ausführen weiterer unterstützter Aktionen über das Cloudverwaltungsgateway (wie z.B. die Bereitstellung von Softwareaktualisierungen oder Anwendungen) erhöht sich die Menge der ausgehenden Datenübertragungen aus Azure.

-   Inhaltsspeicher

    -   Internetbasierte Clients, die mit dem Cloudverwaltungsgateway verwaltet werden, erhalten Softwareaktualisierungsinhalte von Windows Update kostenlos.

    -   Alle anderen benötigten Inhalte (wie Anwendungen) müssen mit einem cloudbasierten Verteilungspunkt verteilt werden. Cloud Management Gateway unterstützt derzeit nur den Cloudverteilungspunkt für das Senden von Inhalten an Clients.

    - Im Artikel über die [cloudbasierte Verteilung](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution) finden Sie weitere Informationen zu den Kosten.

## <a name="frequently-asked-questions-about-the-cloud-management-gateway-cmg"></a>Häufig gestellte Fragen zu Cloud Management Gateway (CMG)

### <a name="why-use-the-cloud-management-gateway"></a>Was spricht für die Verwendung von Cloud Management Gateway?

Verwenden Sie diese Rolle, um die Verwaltung internetbasierter Clients zu vereinfachen. Dazu führen Sie in der Configuration Manager-Konsole drei Schritte aus.

1. Stellen Sie Cloud Management Gateway mithilfe des Assistenten zum [Erstellen von Cloud Management Gateway](/sccm/core/clients/manage/setup-cloud-management-gateway) in Azure bereit.
2. Konfigurieren Sie die Standortsystemrolle [Verbindungspunkt für Cloud Management Gateway](/sccm/core/servers/deploy/configure/install-site-system-roles).
3. [Konfigurieren Sie Rollen für den Datenverkehr von Cloud Management Gateway](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic) wie den Verwaltungspunkt und den Softwareupdatepunkt.

### <a name="how-does-the-cloud-management-gateway-work"></a>Wie funktioniert Cloud Management Gateway?

- Der Verbindungspunkt von Cloud Management Gateway ermöglicht eine konsistente Verbindung mit hoher Leistung zwischen Internet und Cloud Management Gateway.
- Configuration Manager veröffentlicht Einstellungen in Cloud Management Gateway, einschließlich Verbindungsinformationen und Sicherheitseinstellungen.
- Cloud Management Gateway authentifiziert Clientanforderungen von Configuration Manager und leitet sie an den Verbindungspunkt von Cloud Management Gateway weiter. Diese Anforderungen werden gemäß URL-Zuordnungen an Rollen im Unternehmensnetzwerk weitergeleitet.

### <a name="how-is-the-cloud-management-gateway-deployed"></a>Wie wird Cloud Management Gateway bereitgestellt?

Die Clouddienst-Manager-Komponente im Dienstverbindungspunkt verarbeitet alle Bereitstellungstasks für Cloud Management Gateway. Darüber hinaus überwacht die Komponente alle Informationen von Azure AD zu Dienstintegrität und -protokollierung und erstellt entsprechende Berichte.

#### <a name="certificate-requirements"></a>Zertifikatanforderungen

Sie benötigen die folgenden Zertifikate, um Cloud Management Gateway zu sichern:

- **Verwaltungszertifikat**: Hierbei kann es sich um ein beliebiges Zertifikat handeln – einschließlich selbstsignierten Zertifikaten. Sie können ein öffentliches, in Azure AD hochgeladenes Zertifikat oder eine in Configuration Manager importierte [PFX-Datei mit privatem Schlüssel](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) für die Authentifizierung bei Azure AD verwenden.
- **Webdienstzertifikat**: Es wird empfohlen, ein Zertifikat einer öffentlichen Zertifizierungsstelle zu verwenden, um eine native Vertrauensstellung bei Clients zu erzielen. Der CName-Eintrag muss in der öffentlichen DNS-Registrierungsstelle erstellt werden. Platzhalterzertifikate werden nicht unterstützt.
- **In Cloud Management Gateway hochgeladene Zertifikate von Stammzertifizierungsstellen bzw. untergeordneten Zertifizierungsstellen**: Cloud Management Gateway muss PKI-Clientzertifikate in der gesamten Zertifikatkette überprüfen. Wenn Sie eine Unternehmenszertifizierungsstelle zum Ausstellen von PKI-Clientzertifikaten verwenden und das Stammzertifikat oder die untergeordnete Zertifizierungsstelle im Internet nicht verfügbar ist, müssen Sie das Zertifikat in Cloud Management Gateway hochladen.

#### <a name="deployment-process"></a>Bereitstellungsprozess

Die Bereitstellung besteht aus zwei Phasen:

- Bereitstellen des Clouddiensts
    - Hochladen der Datei mit dem [Azure-Dienstdefinitionsschema](https://msdn.microsoft.com/library/azure/ee758711.aspx) (CSDEF-Datei)
    - Hochladen der Datei mit dem [Azure-Dienstkonfigurationsschema](https://msdn.microsoft.com/library/azure/ee758710.aspx) (CSCFG-Datei)
- Einrichten der CMG-Komponente auf dem Azure AD-Server und Konfigurieren von Endpunkten, HTTP-Handlern und Diensten in den Internetinformationsdiensten (Internet Information Services, IIS)

Wenn Sie die Konfiguration von Cloud Management Gateway ändern, wird in Cloud Management Gateway eine Konfigurationsbereitstellung initiiert.

### <a name="how-does-the-cloud-management-gateway-help-ensure-security"></a>Wie sorgt Cloud Management Gateway für mehr Sicherheit?

Cloud Management Gateway trägt auf folgende Weise zur Sicherheit bei:

- Verbindungen von CMG-Verbindungspunkten werden akzeptiert und verwaltet, einschließlich gegenseitiger SSL-Authentifizierung mithilfe interner Zertifikate und Verbindungs-IDs.
- Clientanforderungen werden akzeptiert und weitergeleitet.
    - Verbindungen werden mithilfe von gegenseitigem SSL im PKI-Clientzertifikat vorab authentifiziert.
    - Über die Zertifikatsvertrauensliste wird der Stamm des PKI-Clientzertifikats überprüft. Sie können diese Einstellung in den Standorteigenschaften bei den Einstellungen für die Clientkommunikation angeben. Es werden auch die gleichen Überprüfungen ausgeführt wie durch den Verwaltungspunkt für den Client.
    - Empfangene URLs werden überprüft.
    - Empfangene URLs werden gefiltert, um zu prüfen, ob ein verbundener CMG-Verbindungspunkt die URL-Anforderung verarbeiten kann.  
    - Die Inhaltslänge für jeden veröffentlichenden Endpunkt wird überprüft.
    - Mithilfe eines Roundrobinverfahrens wird für Lastenausgleich zwischen CMG-Verbindungspunkten des gleichen Standorts gesorgt.

- Der CMG-Verbindungspunkt wird gesichert.
    - Es werden konsistente HTTP/TCP-Verbindungen mit allen virtuellen Instanzen der verbundenen CMG-Instanz erstellt. Verbindungen werden minütlich überprüft und verwaltet.
    - Mithilfe interner Zertifikate wird eine gegenseitige SSL-Authentifizierung mit Cloud Management Gateway durchgeführt.
    - HTTP-Anforderungen werden basierend auf URL-Zuordnungen weitergeleitet.
    - Der Verbindungsstatus wird gemeldet, um den Dienstintegritätsstatus anzuzeigen.
    - Der Datenverkehr auf Endpunkten wird alle 5 Minuten gemeldet.

- Clientseitige Configuration Manager-Rollen auf dem veröffentlichenden Endpunkt, z.B. der Verwaltungspunkt, werden gesichert, ebenso wie die Hostendpunkte für Softwareupdatepunkte in IIS, die der Verarbeitung von Clientanforderungen dienen. Jeder in Cloud Management Gateway veröffentlichte Endpunkt verfügt über eine URL-Zuordnung.
Die externe URL ist die URL, über die der Client mit Cloud Management Gateway kommuniziert.
Die interne URL ist der CMG-Verbindungspunkt, der zum Weiterleiten von Anforderungen an den internen Server verwendet wird.

#### <a name="example"></a>Beispiel:
Wenn Sie CMG-Datenverkehr auf einem Verwaltungspunkt aktivieren, erstellt Configuration Manager intern einen Satz URL-Zuordnungen für jeden Verwaltungspunktserver, z.B. „ccm_system“, „ccm_incoming“ und „sms_mp“.
Die externe URL für den ccm_system-Endpunkt des Verwaltungspunkts könnte beispielsweise folgendermaßen aussehen: **https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System**.
Die URL ist eindeutig für jede Verwaltungspunkt. Der Configuration Manager-Client setzt den für CMG aktivierten Verwaltungspunkt – z.B. **<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>** – auf die Liste der Internetverwaltungspunkte.
Alle veröffentlichten externen URLs werden automatisch in Cloud Management Gateway hochgeladen, sodass CMG die URL-Filterung durchführen kann. Alle URL-Zuordnungen werden auf den CMG-Verbindungspunkt repliziert, sodass dieser Datenverkehr gemäß der externen URL des anfordernden Clients an interne Server weiterleiten kann.

### <a name="what-ports-are-used-by-the-cloud-management-gateway"></a>Welche Ports werden von Cloud Management Gateway verwendet?

- Im lokalen Netzwerk sind keine eingehenden Ports erforderlich. Bei der Bereitstellung von Cloud Management Gateway wird automatisch eine Reihe von Ports in Cloud Management Gateway erstellt.
- Der CMG-Verbindungspunkt erfordert zusätzlich zu Port 443 einige ausgehende Ports.

|||||
|-|-|-|-|
|Datenfluss|Server|Serverports|Client|
|CMG-Bereitstellung|Azure|443|Configuration Manager-Dienstverbindungspunkt|
|Erstellen des CMG-Kanals|CMG|VM-Instanz: 1 Port: 443<br>VM-Instanz: N (N>=2 und N<= 16) Ports: 10124~N 10140~N|CMG-Verbindungspunkt|
|Client an CMG|CMG|443|Client|
|CMG-Connector an Standortrolle (zurzeit Verwaltungspunkte und Softwareupdatepunkte)|Standortrolle|In der Standortrolle konfigurierte Protokolle/Ports|CMG-Verbindungspunkt|

### <a name="how-can-you-improve-performance-of-the-cloud-management-gateway"></a>Wie lässt sich die Leistung von Cloud Management Gateway verbessern?

- Konfigurieren Sie Cloud Management Gateway, den CMG-Verbindungspunkt und den Configuration Manager-Standortserver nach Möglichkeit in der gleichen Netzwerkregion, um die Latenz zu verringern.
- Zurzeit wird bei der Verbindung zwischen dem Configuration Manager-Client und Cloud Management Gateway nicht zwischen Regionen unterschieden.
- Um eine hohe Verfügbarkeit zu erzielen, empfiehlt es sich, mindestens zwei virtuelle Instanzen von Cloud Management Gateway und zwei CMG-Verbindungspunkte pro Standort einzurichten.
- Sie können Cloud Management Gateway skalieren, um durch Hinzufügen weiterer VM-Instanzen mehr Clients zu unterstützen. Der Lastenausgleich erfolgt über den Azure AD Load Balancer.
- Erstellen Sie weitere CMG-Verbindungspunkte, um die Last auf diese aufzuteilen. Cloud Management Gateway leitet den Datenverkehr per Roundrobin an die verbundenen CMG-Verbindungspunkte weiter.
- In Release 1702 werden pro CMG-VM-Instanz 6.000 Clients unterstützt. Wenn der CMG-Kanal stark ausgelastet ist, werden Anforderungen weiterhin verarbeitet, die Ausführung dauert aber möglicherweise länger als normal.

### <a name="how-can-you-monitor-the-cloud-management-gateway"></a>Wie können Sie Cloud Management Gateway überwachen?

Verwenden Sie zur Problembehandlung der Bereitstellung **CloudMgr.log** und **CMGSetup.log**.
Verwenden Sie zur Problembehandlung der Dienstintegrität **CMGService.log** und **SMS_CLOUD_PROXYCONNECTOR.log**.
Verwenden Sie zur Problembehandlung des Clientdatenverkehrs **CMGHttpHandler.log**, **CMGService.log** und **SMS_CLOUD_PROXYCONNECTOR.log**.

Eine Liste aller auf Cloud Management Gateway bezogenen Protokolldateien finden Sie unter [Protokolldateien in Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).

## <a name="next-steps"></a>Nächste Schritte

[Einrichten des Cloudverwaltungsgateways](setup-cloud-management-gateway.md)
