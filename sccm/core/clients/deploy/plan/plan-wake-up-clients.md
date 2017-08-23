---
title: Aufwecken von Clients | Microsoft-Dokumentation
description: Planen Sie das Aufwecken von Clients in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 20f595a5b0634a627dff9ba6feeb848754615f2c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="plan-how-to-wake-up-clients-in-system-center-configuration-manager"></a>Planen des Aufweckens von Clients in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

 Configuration Manager unterstützt zwei Wake-On-LAN-Technologien (Local Area Network), über die Computer im Energiesparmodus aktiviert werden, wenn Sie erforderliche Software wie Softwareupdates und Anwendungen installieren möchten. Dabei handelt es sich um herkömmliche Aktivierungspakete und um AMT-Einschaltbefehle.  

Sie können die auf herkömmlichen Aktivierungspaketen beruhende Methode durch die Clienteinstellungen für den Aktivierungsproxy ergänzen. Vom Aktivierungsproxy wird mithilfe eines Peer-zu-Peer-Protokolls und ausgewählten Computern überprüft, ob andere Computer im Subnetz aktiv sind. Diese werden bei Bedarf dann aktiviert. Wenn der Standort für Wake-On-LAN konfiguriert ist und gleichzeitig Clients für den Aktivierungsproxy konfiguriert sind, gilt Folgendes:  

1.  Von Computern, auf denen der Configuration Manager-Client installiert ist und die im Subnetz aktiv sind, wird geprüft, ob andere Computer im Subnetz aktiv sind. Hierzu wird von den Computern alle 5  Sekunden ein TCP/IP-Pingbefehl gesendet.  

2.  Wenn keine Antwort von anderen Computern eingeht, wird davon ausgegangen, dass sie inaktiv sind. Die aktiven Computer werden als *Manager-Computer* des Subnetzes eingesetzt.  

     Nicht alle Computer, von denen keine Antwort eingeht, sind inaktiv. Manche wurden möglicherweise ausgeschaltet, aus dem Netzwerk entfernt oder die Clienteinstellung für den Aktivierungsproxy wird nicht mehr angewendet. Aus diesem Grund wird täglich ein Aktivierungspaket an die Computer gesendet, und zwar um 14:00 Uhr lokale Zeit. Computer, von denen keine Antwort eingeht, werden nicht mehr als inaktiv eingestuft und nicht durch den Aktivierungsproxy aktiviert.  

     Zur Unterstützung des Aktivierungsproxys müssen in jedem Subnetz mindestens drei Computer aktiv sein. Hierzu werden drei Computer auf nicht deterministische Weise als *Wächter-Computer* für das Subnetz ausgewählt. Dies bedeutet, dass sie unabhängig von einer konfigurierten Energierichtlinie aktiv bleiben und nicht nach einer gewissen Zeit der Inaktivität in den Energiespar- oder Ruhemodus umgeschaltet werden. Befehle zum Herunterfahren oder Neustarten, die mit Wartungstasks zusammenhängen, werden von Wächter-Computern beachtet. In einem solchen Fall wird von den verbleibenden Wächter-Computern ein weiterer Computer im Subnetz aktiviert, damit das Subnetz weiterhin drei Wächter-Computer aufweist.  

3.  Der Netzwerkswitch wird von den Manager-Computern angewiesen, den für die inaktiven Computer vorgesehenen Netzwerkverkehr zu den Manager-Computern umzuleiten.  

     Die Umleitung erfolgt durch den Manager-Computer, von dem ein Ethernet-Frame übertragen wird. Von diesem wird die MAC-Adresse des Computers, der sich im Ruhezustand befindet, als Quelladresse verwendet. Dadurch reagiert der Netzwerkswitch so, als ob der inaktive Computer auf den Port verschoben wurde, auf dem sich auch der Manager-Computer befindet. Vom Manager-Computer werden außerdem ARP-Pakete für die inaktiven Computer gesendet, damit der Eintrag im ARP-Cache aktuell bleibt. Darüber hinaus werden vom Manager-Computer im Auftrag des inaktiven Computers Antworten auf ARP-Anfragen gesendet. Die Antwort erfolgt mit der MAC-Adresse des inaktiven Computers.  

    > [!WARNING]  
    >  Während dieses Vorgangs bleibt die IP-zu-MAC-Zuordnung für den inaktiven Computer bestehen. Der Netzwerkswitch wird über einen Aktivierungsproxy darüber informiert, dass der von einer Netzwerkkarte registrierte Port von einer anderen Netzwerkkarte verwendet wird. Dieses Verhalten wird als MAC-Flapping bezeichnet und ist bei Standardnetzwerkvorgängen nicht üblich. Von einigen Netzwerküberwachungstools wird geprüft, ob dieses Verhalten auftritt. Falls ja, werden Fehler angenommen. Durch diese Überwachungstools können also Warnungen generiert oder Ports heruntergefahren werden, wenn Sie einen Aktivierungsproxy verwenden.  
    >   
    >  Verwenden Sie keinen Aktivierungsproxy, wenn Ihre Netzwerküberwachungstools und -dienste kein MAC-Flapping zulassen.  

4.  Wird von einem Manager-Computer eine neue TCP-Verbindungsanforderung für einen Computer erkannt, der sich im Ruhezustand befindet, und die Anforderung erfolgt an einem Port, der vom Computer vor den Wechsel in den Ruhezustand abgehört wurde, wird vom Manager-Computer ein Aktivierungspaket an den inaktiven Computer gesendet. Außerdem wird das Umleiten von Datenverkehr für diesen Computer beendet.  

5.  Der inaktive Computer erhält das Aktivierungspaket und wird dadurch aktiviert. Vom sendenden Computer wird automatisch versucht, die Verbindung wiederherzustellen. Der Computer ist nun aktiv und kann antworten.  

 Für Aktivierungsproxys gelten die folgenden Voraussetzungen und Einschränkungen:  

> [!IMPORTANT]  
>  Wenn in Ihrem Unternehmen ein eigenes Team für die Netzwerkstruktur und die Netzwerkdienste verantwortlich ist, sollten Sie dieses Team informieren und während des Testzeitraums einbeziehen. Beispiel: In einem Netzwerk, von dem eine 802.1X-Zugriffssteuerung verwendet wird, funktioniert der Aktivierungsproxy nicht. Der Netzwerkdienst wird möglicherweise unterbrochen. Außerdem kann es durch den Aktivierungsproxy dazu kommen, dass von einigen Netzwerküberwachungstools Warnungen generiert werden, wenn Datenverkehr zur Aktivierung anderer Computer erkannt wird.  

-   Unterstützte Clients sind Windows 7, Windows 8, Windows Server 2008 R2, Windows Server 2012.  

-   Es werden keine Gastbetriebssysteme unterstützt, die auf einem virtuellen Computer ausgeführt werden.  

-   Die Clients müssen durch die Verwendung von Clienteinstellungen für den Aktivierungsproxy aktiviert sein. Zwar hängt der Vorgang des Aktivierungsproxys nicht von der Hardwareinventur ab, aber die Installation des Aktivierungsproxydiensts wird von Clients erst dann gemeldet, wenn sie für die Hardwareinventur aktiviert sind und von ihnen mindestens eine Hardwareinventur gesendet wurde.  

-   Für Aktivierungspakete müssen Netzwerkkarten (und möglichst das BIOS) aktiviert und konfiguriert sein. Ist die Netzwerkkarte nicht für Aktivierungspakete konfiguriert bzw. wurde diese Einstellung deaktiviert, wird sie von Configuration Manager automatisch konfiguriert und für einen Computer aktiviert, wenn die Clienteinstellung zum Aktivieren des Aktivierungsproxys empfangen wird.  

-   Verfügt ein Computer über mehrere Netzwerkkarten, können Sie nicht auswählen, welche Karte für den Aktivierungsproxy verwendet werden soll. Die Auswahl ist nicht deterministisch. Die ausgewählte Karte wird in der Datei „SleepAgent_<DOMÄNE\>@SYSTEM_0.log“ aufgezeichnet.  

-   Vom Netzwerk müssen ICMP-Echoanforderungen zugelassen werden, zumindest innerhalb des Subnetzes. Es ist nicht möglich, das 5-Minuten-Intervall zum Senden der ICMP-Ping-Befehle zu konfigurieren.  

-   Die Kommunikation ist unverschlüsselt und nicht authentifiziert, und IPsec wird nicht unterstützt.  

-   Die folgenden Netzwerkkonfigurationen werden nicht unterstützt:  

    -   802.1 X mit Portauthentifizierung  

    -   Drahtlosnetzwerke  

    -   Netzwerkswitches, von denen MAC-Adressen an bestimmte Ports gebunden werden  

    -   Netzwerke, die nur IPv6 unterstützen  

    -   DHCP-Lease-Dauer von weniger als 24 Stunden  

Falls Sie Computer für eine geplante Softwareinstallation aktivieren möchten, müssen Sie jeden primären Standort für die Verwendung von Aktivierungspaketen konfigurieren.  

 Zur Verwendung eines Aktivierungsproxys müssen Sie in der Energieverwaltung die Clienteinstellungen für den Aktivierungsproxy bereitstellen und den primären Standort konfigurieren.  

Sie müssen außerdem entschieden, welche subnetzgesteuerten Broadcastpakete oder Unicastpakete verwendet und welche UDP-Portnummer angegeben werden soll. Herkömmliche Aktivierungspakete werden standardmäßig über UDP-Port 9 übertragen. Zur Steigerung der Sicherheit können Sie aber für den Standort einen anderen Port auswählen, sofern dieser Port von beteiligten Routern und Firewalls unterstützt wird.  

### <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Auswahl zwischen Unicast und subnetzgesteuerten Broadcasts für Wake-On-LAN  
 Falls Sie sich für die Aktivierung von Computern mit herkömmlichen Aktivierungspaketen entscheiden, müssen Sie angeben, ob Unicastpakete oder subnetzgesteuerte Broadcastpakete übertragen werden sollen. Wenn Sie einen Aktivierungsproxy nutzen, müssen Sie Unicastpakete verwenden. Orientieren Sie sich andernfalls bei der Auswahl der Übertragungsmethode an der folgenden Tabelle.  

|Übertragungsmethode|Vorteil|Nachteil|  
|-------------------------|---------------|------------------|  
|Unicast|Diese Lösung ist sicherer als subnetzgesteuerte Broadcasts, weil das Paket nicht an alle Computer in einem Subnetz, sondern direkt an einen Computer gesendet wird.<br /><br /> Eine Neukonfiguration der Router ist möglicherweise nicht erforderlich (Sie müssen eventuell den ARP-Cache konfigurieren).<br /><br /> Belegt weniger Netzwerkbandbreite als subnetzgesteuerte Broadcasts.<br /><br /> Unterstützt mit IPv4 und IPv6.|Zielcomputer, deren Subnetzadresse seit der letzten geplanten Hardwareinventur geändert wurde, werden von Aktivierungspaketen nicht gefunden.<br /><br /> Es müssen möglicherweise Switches zum Weiterleiten der UDP-Pakete konfiguriert werden.<br /><br /> Bei manchen Netzwerkadapter ist die Aktivierung durch Aktivierungspakete möglicherweise nicht in allen Ruhezuständen möglich, wenn als Übertragungsmethode Unicast verwendet wird.|  
|Subnetzgesteuerte Broadcasts|Höhere Erfolgsrate als Unicast, wenn die IP-Adressen einiger Computer innerhalb des gleichen Subnetzes sich oft ändern<br /><br /> Keine Switchneukonfiguration erforderlich<br /><br /> Hohe Kompatibilitätsrate mit Computernetzwerkkarten in allen Ruhezuständen, weil subnetzgesteuerte Broadcasts die Originalübertragungsmethode zum Senden von Reaktivierungspaketen sind|Diese Lösung ist weniger sicher als Unicast, da von einem Angreifer kontinuierlich ICMP-Echoanforderungen von einer gefälschten Quelladresse an die gesteuerte Broadcastadresse gesendet werden könnten. Dies führt dazu, dass von allen Hosts Antworten an diese Quelladresse gesendet werden. Wenn Router für die Verwendung subnetzgesteuerter Broadcasts konfiguriert sind, wird die folgende zusätzliche Konfiguration aus Sicherheitsgründen empfohlen:<br /><br /> - Konfigurieren Sie Router so, dass sie nur IP-gesteuerte Broadcasts vom Configuration Manager-Standortserver zulassen. Verwenden Sie hierzu die angegebene UDP-Portnummer.<br />- Konfigurieren Sie Configuration Manager so, dass die angegebene, nicht standardmäßige Portnummer verwendet wird.<br /><br /> Erfordert möglicherweise die Neukonfiguration aller beteiligten Router, damit subnetzgesteuerte Broadcasts möglich werden.<br /><br /> Belegt mehr Netzwerkbandbreite als Unicast-Übertragungen.<br /><br /> Nur mit IPv4 unterstützt, keine Unterstützung für IPv6.|  

> [!WARNING]  
>  Subnetzgesteuerte Broadcasts sind mit Sicherheitsrisiken verbunden: Von einem Angreifer könnten kontinuierlich ICMP-Echoanforderungen (Internet Control Message Protocol) von einer gefälschten Quelladresse an die gesteuerte Broadcastadresse gesendet werden. Dies würde dazu führen, dass von allen Hosts Antworten an diese Quelladresse gesendet werden. Diese Art von DoS-Angriff wird allgemein als „Smurf Attack“ bezeichnet und üblicherweise dadurch verhindert, dass keine subnetzgesteuerten Broadcasts zugelassen werden.
