---
title: Clientpeercache | System Center Configuration Manager
description: "Verwenden Sie Peercache für Quellspeicherorte für Clientinhalte beim Bereitstellen von Inhalten mit System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 89fcd16887ae77299f9d18472ee6a1ba56794eca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Peercache für Configuration Manager-Clients

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1610 von System Center Configuration Manager können Sie **Peercache** zum Verwalten der Bereitstellung von Inhalten für Clients an Remotestandorten verwenden. Peercache ist eine integrierte Configuration Manager-Lösung, mit deren Hilfe Clients Inhalte für andere Clients direkt aus ihrem lokalen Cache freigeben können.   

> [!TIP]  
> Peercache und das Dashboard „Clientdatenquellen“ sind vorab veröffentlichte Funktionen, die mit Version 1610 eingeführt wurden. Informationen zum Aktivieren dieser Funktionen finden Sie unter [Verwenden von vorab veröffentlichten Features von Updates](/sccm/core/servers/manage/pre-release-features).

## <a name="overview"></a>Übersicht
Ein Peercacheclient ist ein Configuration Manager-Client, der für die Verwendung von Peercache aktiviert ist. Ein Peercacheclient, der über Inhalte verfügt, die für weitere Clients freigegeben werden können, ist eine Peercachequelle.
 -  Sie verwenden Clienteinstellungen, um Clients für die Verwendung des Peercaches zu aktivieren.
 -  Zum Freigeben von Inhalten als Peercachequelle muss ein Peercacheclient folgende Voraussetzungen erfüllen:
    -  Muss in eine Domäne eingebunden sein. Ein Client, der nicht in eine Domäne eingebunden ist, kann jedoch Inhalte von einer in eine Domäne eingebundenen Peercachequelle abrufen.
    -  Muss Mitglied der aktuellen Begrenzungsgruppe des Clients sein, der die Inhalte sucht. Ein Peercacheclient in einer benachbarten Begrenzungsgruppe ist im Pool der verfügbaren Quellspeicherorte für Inhalt nicht enthalten, wenn ein Client eine Ausweichaktion verwendet, um nach Inhalten in einer benachbarten Begrenzungsgruppe zu suchen. Weitere Informationen zu aktuellen und benachbarten Begrenzungsgruppen finden Sie unter [Begrenzungsgruppen](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Jede Art von Inhalten, die im Cache eines Configuration Manager-Clients gespeichert sind, kann mithilfe von Peercache für andere Clients bereitgestellt werden.
 -  Peercache ersetzt nicht die Verwendung anderer Lösungen wie BranchCache, sondern wird parallel eingesetzt, um Ihnen weitere Optionen bereitzustellen und herkömmliche Lösungen für die Inhaltsbereitstellung (z.B. Verteilungspunkte) zu erweitern. Da diese benutzerdefinierte Lösung nicht von BranchCache abhängig ist, funktioniert sie auch, wenn Sie Windows BranchCache nicht aktivieren oder verwenden.

### <a name="operations"></a>Vorgänge

Nachdem Sie Clienteinstellungen bereitgestellt haben, die den Peercache für eine Sammlung aktivieren, können Mitglieder dieser Sammlung als Peerinhaltsquelle für andere Clients in der gleichen Begrenzungsgruppe fungieren:
 -  Ein Client, der als Peerinhaltsquelle fungiert, übermittelt eine Liste der verfügbaren zwischengespeicherten Inhalte an seinen Verwaltungspunkt.
 -  Wenn der nächste Client in dieser Begrenzungsgruppe diese Inhalte anfordert, wird jede Peercachequelle, die die Inhalte enthält, als mögliche Inhaltsquelle zusammen mit den Verteilungspunkten und anderen Quellspeicherorten für Inhalt in dieser Begrenzungsgruppe zurückgegeben.
 -  Entsprechend dem normalen Verarbeitungsprozess wählt der nach den Inhalten suchende Client eine Inhaltsquelle aus dem Pool der bereitgestellten Quellen aus und versucht dann, die Inhalte abzurufen.

> [!NOTE]
> Wenn ein Fallback auf eine benachbarte Begrenzungsgruppe für Inhalte erfolgt, werden die Peercache-Quellspeicherorte für Inhalt aus den benachbarten Begrenzungsgruppen nicht dem Pool des Clients mit möglichen Quellspeicherorten für Inhalt hinzugefügt.  


Auch wenn Sie die Teilnahme aller Clients als Peercachequelle festlegen können, empfiehlt es sich, nur die Clients auszuwählen, die am besten als Peercachequellen geeignet sind.  Die Eignung von Clients kann anhand des Gehäusetyps, Speicherplatzes, der Netzwerkkonnektivität usw. eines Clients bewertet werden. Weitere Informationen zum Auswählen der am besten geeigneten Clients zur Verwendung für Peercache finden Sie in [diesem Blog eines Microsoft-Beraters](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Eingeschränkter Zugriff auf eine Peercachequelle**  
Ab Version 1702 lehnt ein Peercachequellcomputer eine Inhaltsanforderung ab, wenn der Peercachequellcomputer eine der folgenden Bedingungen erfüllt:  
  -  Niedriger Akkustand.
  -  Zum Zeitpunkt der Anforderungen des Inhalts liegt die CPU-Auslastung bei über 80 %.
  -  *AvgDiskQueueLength* der Datenträger-E/A überschreitet 10.
  -  Es gibt keine weiteren Verbindungen zum Computer.   

Sie können diese Einstellungen mithilfe der WMI-Klasse des Client Configuration-Servers für die Peerquellfunktion (*SMS_WinPEPeerCacheConfig*) konfigurieren, wenn Sie das Configuration Manager-SDK für System Center verwenden.

Wenn der Computer eine Anforderung von Inhalt ablehnt, sucht der anfordernde Computer bei alternativen Quellen seines Pools an verfügbaren Quellspeicherorten nach Inhalt.   



### <a name="monitoring"></a>Überwachung   
Um besser zu verstehen, wann der Peercache erfolgreich verwendet wird, sehen Sie sich das Dashboard „Clientdatenquellen“ an. Siehe dazu [Dashboard „Clientdatenquellen“](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

Ab Version 1702 können Sie drei Berichte verwenden, um die Peercacheauslastung anzuzeigen. Navigieren Sie in der Konsole zu **Überwachung** > **Berichterstellung** > **Berichte**. Die Berichte haben alle den Typ **Softwareverteilung – Inhalt**:
1.  **Ablehnen von Inhalt einer Peercachequelle**:  
Erfahren Sie mithilfe dieses Berichts, wie häufig die Peercachequellen in einer Begrenzungsgruppe eine Inhaltsanforderung abgelehnt haben.
 - **Bekanntes Problem:** Wenn Sie einen Drilldown für Ergebnisse wie *MaxCPULoad* und *MaxDiskIO* durchführen, erhalten Sie möglicherweise einen Fehler, der darauf hinweist, dass der Bericht oder Angaben nicht gefunden werden können. Verwenden Sie die folgenden beiden Berichte, die die Ergebnisse direkt anzeigen, um dies zum umgehen.

2. **Ablehnen von Inhalt einer Peercachequelle durch eine Bedingung**:  
Erfahren Sie mithilfe dieses Berichts, wie Sie Angaben zur Ablehnung einer angegebenen Begrenzungsgruppe oder eines Ablehnungstyps interpretieren können. Sie können Folgendes bestimmen:

  - **Bekannte Probleme:** Sie können nicht aus verfügbaren Parametern wählen, sondern müssen diese manuell eingeben. Geben Sie die Werte für *Name der Begrenzungsgruppe* und *Rejection Type* (Ablehnungstyp) ein, so wie im ersten Bericht dargestellt. Sie können z.B. für *Rejection Type* (Ablehnungstyp) *MaxCPULoad* oder *MaxDiskIO* eingeben.

3. **Angaben zur Ablehnung von Inhalt einer Peercachequelle**:   
  Erfahren Sie mithilfe dieses Berichts, welche Art von Inhalt angefordert und abgelehnt wurde.

 - **Bekannte Probleme:** Sie können nicht aus verfügbaren Parametern wählen, sondern müssen diese manuell eingeben. Geben Sie den Wert des *Rejection Type* (Ablehnungstyp) wie im ersten Bericht („Ablehnen von Inhalt einer Peercachequelle“) dargestellt ein, und geben Sie anschließend die *Resource ID* der Quelle des Inhalts ein, über die Sie mehr Informationen erhalten möchten.  So finden Sie die Resource ID der Quelle des Inhalts heraus:  

    1. Machen Sie den Namen des Computers ausfindig, der als *Peercachequelle* in den Ergebnissen des zweiten Berichts angezeigt wird („Ablehnen von Inhalt einer Peercachequelle durch eine Bedingung“).  
    2. Navigieren Sie anschließend zu **Bestand und Kompatibilität** > **Geräte**, und suchen Sie nach dem Namen des Computers. Verwenden Sie den Wert aus der Spalte „Resource ID“.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Anforderungen und Überlegungen für den Peercache
-   Der Peercache wird von jedem Windows-Betriebssystem unterstützt, das als Configuration Manager-Client unterstützt wird. Nicht-Windows-Betriebssysteme werden für den Peercache nicht unterstützt.

-   Clients können nur Inhalte von Peercacheclients übertragen, die sich in ihrer aktuellen Begrenzungsgruppe befinden.

-   Vor Version 1706 muss jeder Standort, an dem Clients Peer Cache verwenden, mit einem [Netzwerkzugriffskonto](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account) konfiguriert sein. Mit einer Ausnahme ist der Account ab Version 1706 nicht mehr erforderlich.  Die Ausnahme tritt ein, wenn Peercache von einem Client verwendet wird, um eine Tasksequenz aus dem Softwarecenter abzurufen und auszuführen, und diese Tasksequenz den Client über WinPE startet.  In diesem Szenario benötigt der Client in WinPE weiterhin das Netzwerkzugriffskonto, damit er zum Abrufen von Inhalten auf die Peercachequelle zugreifen kann.

    Bei Bedarf wird das Netzwerkzugriffskonto vom Peer Cache-Quellcomputer zum Authentifizieren von Downloadanforderungen von Peers verwendet und erfordert nur Domänenbenutzerberechtigungen für diesen Zweck.

-   Da die aktuelle Begrenzung einer Inhaltsquelle des Peercaches durch die letzte Hardwareinventurübermittlung des Clients bestimmt wird, gilt ein Client, der zu einem Netzwerkort in einer anderen Begrenzungsgruppe wechselt, für den Peercache weiterhin als Mitglied seiner früheren Begrenzungsgruppe. Dadurch kann ein Client als Inhaltsquelle des Peercaches angeboten werden, der sich nicht an seinem unmittelbaren Netzwerkort befindet. Es wird empfohlen, Clients, die für diese Konfiguration anfällig sind, von der Teilnahme als Peercachequelle auszuschließen.

## <a name="to-configure-client-peer-cache-client-settings"></a>So konfigurieren Sie Clienteinstellungen für Clientpeercache
1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clienteinstellungen**, und öffnen Sie dann das Objekt mit Geräteclienteinstellungen, das Sie verwenden möchten. Außerdem können Sie das Objekt „Clientstandardeinstellungen“ ändern.
2.  Wählen Sie in der Liste der verfügbaren Einstellungen **Clientcacheeinstellungen** aus.
3.  Legen Sie **Configuration Manager-Client in vollständigem Betriebssystem zur Freigabe von Inhalten aktivieren** auf **Ja** fest.
4.  Konfigurieren Sie die folgenden Einstellungen, um die Ports zu definieren, die für den Peercache verwendet werden sollen:  
  -  **Port für erste Netzwerkübertragung**
  -  **HTTPS für Client-Peer-Kommunikation aktivieren**
  -  **Port für Download der Inhalte vom Peer (HTTP/HTTPS)**

Wenn die Windows-Firewall verwendet wird, wird sie auf jedem für den Peercache aktivierten Computer von Configuration Manager so konfiguriert, dass die Verwendung der konfigurierten Ports zulässig ist.
