---
title: Definieren von Begrenzungsgruppen | Microsoft-Dokumentation
description: "Erfahren Sie mehr über Begrenzungsgruppen in System Center Configuration Manager, die Clients mit Standortsystemen verknüpfen."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 5debc6559f4b1c213e8ca513d685941c9e669063
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Begrenzungsgruppen für System Center Configuration Manager


*Gilt für: System Center Configuration Manager (Current Branch)*

Sie verwenden Begrenzungsgruppen in System Center Configuration Manager zum logischen Gruppieren zusammenhängender Netzwerkadressen ([Grenzen](/sccm/core/servers/deploy/configure/boundaries)), um die Verwaltung Ihrer Infrastruktur zu erleichtern. Bevor Sie eine Begrenzungsgruppe verwenden können, müssen ihr erst Grenzen zugewiesen werden.

Standardmäßig erstellt Configuration Manager eine Standard-Standortbegrenzungsgruppe an jedem Standort.

> [!IMPORTANT]  
>  **Die Informationen in diesem Begrenzungsgruppen-Abschnitt und seinen untergeordneten Abschnitten gelten für die Version 1610 oder höher.** Dieser Inhalt wurde überarbeitet, um für die Entwurfsänderungen spezifisch zu sein, die für Begrenzungsgruppen mit dieser Updateversion eingeführt werden.
>
> **Wenn Sie eine ältere Version als 1610 verwenden**, finden Sie unter [Boundary groups for System Center Configuration Manager versions 1606, and 1606 (Begrenzungsgruppen für die System Center Configuration Manager-Versionen 1511, 1602 und 1606)](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) Informationen zum Verwenden und Konfigurieren von Begrenzungsgruppen mit diesen Versionen.

Ordnen Sie der Begrenzungsgruppe Grenzen (Netzwerkspeicherorte) und Standortsystemrollen wie Verteilungspunkte zu, um Begrenzungsgruppen zu konfigurieren. Dadurch können Clients mit Standortsystemservern wie Verteilungspunkten verknüpft werden, die sich in der Nähe der Clients auf dem Netzwerk befinden.

Wenn sie mehreren Begrenzungsgruppen die gleiche Grenze und die gleichen Standortsystemserver, z.B. Verteilungspunkte, zuweisen, sind Standortsysteme für einen größeren Bereich von Netzwerkstandorten verfügbar.

Client verwenden eine Begrenzungsgruppe für Folgendes:  

-   Automatische Standortzuweisung  
-   um einen Standortsystemserver zu finden, der einen Dienst bereitstellen kann, darunter z.B.:
    - Verteilungspunkte für Inhaltsstandorte
    -   Softwareupdatepunkte (ab Version 1702)
    - Zustandsmigrationspunkte
    - Bevorzugte Verwaltungspunkte (wenn Sie bevorzugte Verwaltungspunkte verwenden, müssen Sie diese Option für die Hierarchie und nicht über die Konfiguration der Begrenzungsgruppe aktivieren. Weitere Informationen finden Sie unter [So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte](#to-enable-use-of-preferred-management-points) in diesem Thema.)

##  <a name="boundary-groups-and-relationships"></a>Begrenzungsgruppen und Beziehungen
Für jede Begrenzungsgruppe in Ihrer Hierarchie können Sie folgende Zuweisungen vornehmen:

-  Eine oder mehrere Grenzen. Wenn sich ein Client an einem Netzwerkspeicherort befindet, der als Grenze definiert ist, die einer bestimmten Begrenzungsgruppe zugewiesen ist, ist diese die **aktuelle** Begrenzungsgruppe. Ein Client kann mehr als eine aktuelle Begrenzungsgruppe aufweisen.
- Eine oder mehrere Standortsystemrollen.  Clients können immer Standortsystemrollen verwenden, die mit der aktuellen Begrenzungsgruppe verknüpft sind. Je nach zusätzlichen Konfigurationen haben sie möglicherweise die Möglichkeit, Standortsystemrollen in zusätzlichen Begrenzungsgruppen zu verwenden.  

Für jede von Ihnen erstellte Begrenzungsgruppe können Sie einen unidirektionalen Link zu einer anderen Begrenzungsgruppe konfigurieren. Dieser Link wird als **Beziehung** bezeichnet. Die Begrenzungsgruppen, mit denen Sie verknüpfen, heißen **Nachbarbegrenzungsgruppen**. Eine Begrenzungsgruppe kann mehrere Beziehungen mit unterschiedlichen Nachbarbegrenzungsgruppen haben.

Mit der Konfiguration jeder Beziehung wird festgelegt, ab wann ein Client, der keinen verfügbaren Standortsystemserver in seiner aktuellen Begrenzungsgruppe ausfindig machen kann, mit der Suche nach einem verfügbaren Standortsystem in einer Nachbarbegrenzungsgruppe beginnen kann. Diese Suche in zusätzlichen Gruppen wird als **Fallback** bezeichnet.

## <a name="fallback"></a>Fallback
Um zu verhindern, dass bei Clients Probleme auftreten, wenn ein verfügbares Standortsystem nicht in der aktuellen Begrenzungsgruppe gefunden werden kann, definieren Sie Beziehungen zwischen Begrenzungsgruppen, die das Verhalten bei einem Fallback beeinflussen. Durch Fallback kann ein Client seine Suche auf zusätzliche Begrenzungsgruppen erweitern, um ein verfügbares Standortsystem zu finden.

Beziehungen werden auf der Registerkarte **Beziehungen** in den Eigenschaften der Begrenzungsgruppe. Wenn Sie eine Beziehung konfigurieren, definieren Sie eine Verknüpfung mit einer Nachbarbegrenzungsgruppe. Für jeden unterstützten Typ von Standortsystemrollen können Sie unabhängige Fallbackeinstellungen für die jeweilige Nachbarbegrenzungsgruppe konfigurieren. Wenn Sie beispielsweise eine Beziehung mit einer bestimmten Begrenzungsgruppe konfigurieren, können Sie festlegen, dass das Fallback für Verteilungspunkte schon nach 20 Minuten und nicht erst, wie es der Standard ist, nach 120 Minuten auftritt. Ein ausführlicheres Beispiel finden Sie unter [Beispiel für das Verwenden von Begrenzungsgruppen](#example-of-using-boundary-groups).

Wenn ein Client keine verfügbare Standortsystemrolle in seiner aktuellen Begrenzungsgruppe finden kann, verwendet der Client die Fallbackzeit (in Minuten) dafür, festzustellen, wann er mit der Suche nach einem verfügbaren Standortsystem, das mit dieser Nachbarbegrenzungsgruppe verknüpft ist, beginnen kann.  

Wenn ein Client kein verfügbares Standortsystem finden kann und mit dem Durchsuchen von Speicherorten anderer Nachbarbegrenzungsgruppen beginnt, wird der Pool der verfügbaren Standortsysteme, die er verwenden kann, so erweitert, wie Sie es mit Ihrer Konfiguration von Begrenzungsgruppen und deren Beziehungen definiert haben.

- Eine Begrenzungsgruppe kann mehr als eine Beziehung haben. Dadurch können Sie die verschiedenen Arten von Standortsystemen festlegen, dass nach unterschiedlich langen Zeitspannen ein Fallback auf unterschiedliche Nachbarn erfolgen soll.    
- Das Ziel des Fallbacks eines Clients kann nur eine Begrenzungsgruppe sein, die ein direkter Nachbar der aktuellen Begrenzungsgruppe ist.
- Wenn ein Client Mitglied mehrerer Begrenzungsgruppen ist, wird die aktuelle Begrenzungsgruppe als die Gesamtheit aller Begrenzungsgruppen dieses Clients definiert. Anschließend kann ein Fallback dieses Clients auf eine Nachbargruppe jeder dieser ursprünglichen Begrenzungsgruppen erfolgen.

### <a name="the-default-site-boundary-group"></a>Die standardmäßige Standortbegrenzungsgruppe
Zusätzlich zu den von Ihnen erstellten Begrenzungsgruppen hat jeder Standort eine Standard-Standortbegrenzungsgruppe, die von Configuration Manager erstellt wird. Diese Gruppe heißt ***Default-Site-Boundary-Group&lt;sitecode>***. Die Gruppe des Standorts ABC hieße z.B. *Default-Site-Boundary-Group&lt;ABC>*.

Für jede von Ihnen erstellte Begrenzungsgruppe erstellt Configuration Manager automatisch einen implizierten Link zu jeder Standard-Standortbegrenzungsgruppe in der Hierarchie.
-   Der implizierte Link ist eine Standardoption für ein Fallback von der aktuellen Begrenzungsgruppe auf die Standardbegrenzungsgruppe der Standorte, die eine Standardfallbackzeit von 120 Minuten hat.
-   Clients, die sich nicht in einer Begrenzungsgruppe befinden, die einer anderen Begrenzungsgruppe in Ihrer Hierarchie zugeordnet ist, verwenden die Standardbegrenzungsgruppe des zugewiesenen Standorts, um gültige Quellspeicherorte für Inhalt zu ermitteln.

So verwalten Sie das Fallback auf die Standard-Standortbegrenzungsgruppe:
- Sie können zu den Einstellungen der Standardbegrenzungsgruppe navigieren und die Werte auf der Registerkarte **Standardverhalten** anpassen. Die Änderungen, die Sie hier vornehmen, gelten für *alle* implizierten Links zu dieser Begrenzungsgruppe. Diese Einstellungen können außer Kraft gesetzt werden, indem Sie den expliziten Link zu dieser Standard-Standortbegrenzungsgruppe einer anderen Begrenzungsgruppe konfigurieren.
- Sie können zu den Einstellungen einer von Ihnen erstellten Begrenzungsgruppe navigieren und die Werte für den expliziten Link zu einer Standard-Standortbegrenzungsgruppe anpassen. Wenn Sie eine neue Zeit (in Minuten) für das Fallback oder das Blockieren des Fallbacks festlegen, wirkt sich diese Änderung nur auf den von Ihnen konfigurierten Link aus. Konfigurierungen des expliziten Links überschreiben diejenigen auf der Registerkarte **Standardverhalten** der Standard-Standortbegrenzungsgruppe.


## <a name="site-assignment"></a>Standortzuweisung  
 Sie können jede Begrenzungsgruppe mit einem zugewiesenen Standort für Clients konfigurieren.  

-   Ein neu installierter Client, der die automatische Standortzuweisung verwendet, tritt dem zugewiesenen Standort einer Begrenzungsgruppe bei, die die aktuelle Netzwerkadresse des Clients enthält.  
-   Nach Zuweisung zu einem Standort ändert sich die Standortzuweisung eines Clients nicht, wenn sich seine Netzwerkadresse ändert. Beim Wechsel des Clients zu einer neuen Netzwerkadresse, die von einer Grenze in einer Begrenzungsgruppe mit abweichender Standortzuweisung repräsentiert wird, bleibt der dem Client zugewiesene Standort unverändert.  
-   Wenn mithilfe von Active Directory-Systemermittlung eine neue Ressource ermittelt wird, werden die Netzwerkinformationen für diese Ressource anhand der Grenzen in Begrenzungsgruppen bewertet. Dabei wird die neue Ressource einem zugewiesenen Standort zur Verwendung bei einer Clientpushinstallation zugeordnet.  
-   Wenn eine Grenze zu mehreren Begrenzungsgruppen gehört, denen verschiedene Standorte zugewiesen sind, wählen die Clients einen dieser Standorte nach dem Zufallsprinzip aus.  
-   Änderungen an dem zugewiesenen Standort einer Begrenzungsgruppe betreffen nur neue Standortzuweisungsaktionen. Clients, die bereits einem Standort zugewiesen sind, bewerten ihre Standortzuweisung nicht basierend auf Änderungen an der Konfiguration einer Begrenzungsgruppe (oder ihrer eigenen Netzwerkadresse) neu.  

Weitere Informationen zur automatischen Standortzuweisung finden Sie unter [Verwenden von automatischen Standortzuweisungen für Computer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [Zuweisen von Clients zu einem Standort in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## <a name="distribution-points"></a>Verteilungspunkte

Wenn ein Client den Speicherort eines Verteilungspunkts anfordert, sendet Configuration Manager eine Liste mit den Standortsystemen des entsprechenden Typs, die mit jeder Begrenzungsgruppe verknüpft sind, die den aktuellen Netzwerkspeicherort des Clients enthält:

-   **Während der Softwareverteilung** fordern Clients einen Speicherort für Bereitstellungsinformationen an, die auf einem Verteilungspunkt oder einer anderen gültigen Inhaltsquelle zur Verfügung stehen (wie z.B. ein Client, der für Peer Cache konfiguriert wurde).

-   **Während der Bereitstellung des Betriebssystems** fordern Clients einen Speicherort zum Senden oder Empfangen ihrer Zustandsmigrationsinformationen an.  

Wenn ein Client während der Informationsbereitstellung Informationen anfordert, die in einer Quelle in seiner aktuellen Begrenzungsgruppe nicht verfügbar sind, fordert der Client solange diese Informationen an, indem er unterschiedliche Inhaltsquellen in seiner aktuellen Begrenzungsgruppe ausprobiert, bis die Fallbackzeit der Nachbarbegrenzungsgruppe oder der Standard-Standortbegrenzungsgruppe verstrichen ist. Wenn der Client noch keinen Inhalt gefunden hat, erweitert er seine Suche nach Inhaltsquellen auf die Nachbarbegrenzungsgruppen.

Wenn der Inhalt allerdings nach Bedarf verteilt wird und zum Zeitpunkt der Anforderung durch einen Client auf einem Verteilungspunkt nicht zur Verfügung steht, beginnt der Übertragungsprozess des Inhalts auf diesen Verteilungspunkt. Es ist möglich, dass der Client diesen Server als Inhaltsquelle findet, bevor er damit beginnt, eine Nachbarbegrenzungsgruppe zu verwenden.

## <a name="software-update-points"></a>Softwareupdatepunkte
Ab Version 1702 können Client Begrenzungsgruppen verwenden, um neue Softwareupdatepunkte zu finden. Sie können verschiedenen Begrenzungsgruppen einzelne Softwareupdatepunkte hinzufügen, um zu steuern, welchen Server ein Client finden kann.

Wenn Sie ein Update von einer früheren Version als Version 1702 durchführen, werden alle vorhandenen Softwareupdatepunkte in die Standard-Standortbegrenzungsgruppe an jedem Standort eingefügt. So wird das Verhalten von vor dem Update beibehalten, bei dem Clients einen Softwareupdatepunkt aus dem Pool der verfügbaren Softwareupdatepunkte auswählen, den Sie für Ihre Hierarchie konfiguriert haben.  Dieses Verhalten wird so lange beibehalten, bis Sie einzelne Softwareupdatepunkte in unterschiedliche Begrenzungsgruppen einfügen, um ein gesteuertes Auswahl- und Fallbackverhalten zu erzielen.

Wenn Sie einen neuen Standort installieren, auf dem Version 1702 oder neuer ausgeführt wird, weder der Standard-Standortbegrenzungsgruppe keine Softwareupdatepunkte hinzugefügt. Weisen Sie Softwarepudatepunkte zu einer Begrenzungsgruppe hinzu, damit Clients sie suchen und nutzen können.

### <a name="fallback-for-software-update-points"></a>Fallback für Softwareupdatepunkte
Das Fallback für Softwareupdatepunkte wird genauso wie für andere Standortsystemrollen konfiguriert, hat aber folgende Probleme:
- **Neue Clients verwenden Begrenzungsgruppen zur Auswahl von Softwareupdatepunkten.** Nach der Installation von Version 1702 wählen von Ihnen installierte Client einen Softwareupdatepunkt aus denjenigen aus, die mit der von Ihnen konfigurierten Begrenzungsgruppe verknüpft sind. Dies ersetzt das vorherige Verhalten, bei dem die Clients zufällig einen Softwareupdatepunkt aus der Liste derer auswählten, die sich die Gesamtstruktur der Clients teilen.

- **Clients verwenden so lange den bisher funktionierenden Softwareupdatepunkt, bis sie ein Fallback ausführen, um einen neuen zu finden.** Clients, die bereits über einen Softwareupdatepunkt verfügen, werden diesen solange verwenden, bis der Server nicht mehr erreicht werden kann.  Dies betrifft auch das weitere Verwenden eines Softwareupdatepunkts, der nicht der aktuellen Begrenzungsgruppe des Clients zugeordnet ist.

  Das weitere Verwenden eines vorhandenen Softwareupdatepunkts ist beabsichtigt, auch wenn sich dieser Server nicht in der aktuellen Begrenzungsgruppe eines Client befindet. Dies liegt daran, dass der Wechsel eines Softwareupdatepunkts einen großen Teil der Netzwerkbandbreite in Anspruch nimmt, da der Client Daten mit dem neuen Softwareupdatepunkt synchronisiert. Die Verzögerung beim Übergang vermeidet eine Komplettauslastung Ihres Netzwerk, da nicht all Ihre Clients gleichzeitig zu einem neuen Softwareupdatepunkt wechseln.

- **Ein Client versucht immer 120 Minuten lang, den bisher funktionierenden Softwareupdatepunkt zu erreichen, bevor ein Fallback initialisiert wird.** Wenn der Client 120 Minuten lang keinen Kontakt herstellen konnte, kommt es zu einem Fallback. Die Einleitung des Fallback führt dazu, dass der Client von seiner aktuellen Begrenzungsgruppe eine Liste der Softwareupdatepunkte erhält. Abhängig von den Fallbackkonfigurationen können auch zusätzliche Softwareupdatepunkte von benachbarten und standardmäßigen Standortbegrenzungsgruppen verfügbar sein.

### <a name="fallback-configurations-for-software-update-points"></a>Fallbackkonfigurationen für Softwareupdatepunkte
#### <a name="beginning-with-version-1706"></a>Ab Version 1706   
Sie können die **Fallbackzeit (in Minuten)** für Softwareupdatepunkte auch auf unter 120 Minuten einstellen. Ein Client muss dennoch für 120 Minuten versuchen, den bisher genutzten Softwareupdatepunkt zu erreichen, bevor die Suche auf weitere Server ausgedehnt wird. Da die Fallbackzeit für Begrenzungsgruppen erst zu laufen beginnt, wenn der Client seinen ursprünglichen Server nicht erreicht, werden einem Client, dem dies nicht innerhalb von 120 Minuten gelingt und für den die Suche ausgedehnt wird, alle Begrenzungsgruppen bereitgestellt, für die eine Fallbackzeit von weniger als 120 Minuten festgelegt ist.

Mit der Option **Nie ein Fallback durchführen** können Sie das Fallback eines Softwareupdatepunkts auf eine benachbarte Begrenzungsgruppe blockieren.

Nachdem er zwei Stunden erfolglos den Kontakt zu seinem ursprünglichen Server gesucht hat, sucht der Client nun mit einer kürzeren Zeitspanne nach einem neuen Softwareupdatepunkt. So kann er die erweiterte Liste potenzieller Softwareupdatepunkte schneller durchgehen.

 -  **Beispiel eines Fallback**  
    Für die aktuelle Begrenzungsgruppe eines Clients ist ein Fallback für Softwareupdatepunkte konfiguriert, *10* Minuten für die Begrenzungsgruppe *A* und *130* Minuten für die Begrenzungsgruppe *B*. Wenn der Client den bisher funktionierenden Softwareupdatepunkt nicht erreichen kann, geschieht Folgendes:
    -   Der Client versucht 120 Minuten lang den ursprünglichen Server zu erreichen.  Nach 10 Minuten werden die Softwareupdatepunkte aus der Begrenzungsgruppe A in den Pool der verfügbaren Server aufgenommen. Der Client kann jedoch erst zu ihnen oder einem anderen Server Kontakt aufnehmen, wenn die Zeitspanne (120 Minuten) für den Verbindungsversuch mit dem ursprünglichen Server abgelaufen ist.
    -   Nachdem 120 Minuten lang versucht wurde, den usprünglichen Softwareupdatepunkt zu finden, kann der Client seine Suche ausdehnen. Dazu werden Server aus der aktuellen Begrenzungsgruppe des Clients und aus benachbarten Begrenzungsgruppen, deren Fallbackzeit auf 120 Minuten oder weniger festgelegt wurde, dem Pool der verfügbaren Softwareupdatepunkte hinzugefügt. Darin sind die Server der Begrenzungsgruppe A enthalten, die bereits vorher dem Pool der verfügbaren Server hinzugefügt wurden.
    -       Nach weiteren 10 Minuten (insgesamt 130 Minuten nach der ersten fehlgeschlagenen Kontaktaufnahme zwischen Client und Softwareupdatepunkt) dehnt der Client seine Suche auf die Softwareupdatepunkte der Begrenzungsgruppe B aus.  

#### <a name="prior-to-version-1706"></a>Vor Version 1706
Vor Version 1706 kann bei Fallbackkonfigurationen für Softwareupdatepunkte keine Zeit in Minuten angegeben werden. Stattdessen ist das Fallbackverhalten auf Folgendes beschränkt:

  - **Fallbackzeit (in Minuten):** Diese Option ist für Softwareupdatepunkte abgeblendet und kann auch nicht konfiguriert werden. Sie ist auf 120 Minuten festgelegt.
  -     **Kein Fallback:** Mit dieser Konfiguration können Sie das Fallback für einen Softwareupdatepunkt auf eine Nachbarbegrenzungsgruppe blockieren.

Wenn ein Client, der bereits über einen Softwareupdatepunkt verfügt, diesen nicht erreiche kann, kann der Client dann ein Fallback ausführen, um einen anderen zu finden. Beim Verwenden von Fallback erhält der Client eine Liste von Softwareupdatepunkten von seiner aktuellen Begrenzungsgruppe. Wenn er 120 Minuten lang keinen Server finden kann, fällt er auf seine Nachbarbegrenzungsgruppe und die Standard-Standortbegrenzungsgruppe zurück. Das Fallback für beide Begrenzungsgruppen wird gleichzeitig durchgeführt, da die Fallbackzeit für Softwareupdatepunkte auf Nachbargruppen auf 120 Minuten festgelegt ist und nicht angepasst werden kann. Das Standardzeitintervall für Fallback auf die Standard-Standortbegrenzungsgruppe ist ebenfalls auf 120 Minuten festgelegt. Wenn ein Client sowohl auf die Nachbar- als auch auf die Standard-Standortbegrenzungsgruppe zurückfällt, versucht er, mit den Softwareupdatepunkten von der Nachbarbegrenzungsgruppe Kontakt aufzunehmen, bevor er einen Punkt aus der Standard-Standortbegrenzungsgruppe verwendet.

### <a name="manually-switch-to-a-new-software-update-point"></a>Manuell auf einen neuen Softwareupdatepunkt wechseln
Zusätzlich zur Verwendung des Fallback, können Sie die Option *Clientbenachrichtigung* nutzen, um ein Gerät manuell zu einem Wechsel auf einen neuen Softwareupdatepunkt zu zwingen.

Beim Wechseln auf einen neuen Server wird das Fallback verwendet, um diesen zu finden. Deshalb sollten Sie vor diesem Wechsel die Konfigurationen Ihrer Begrenzungsgruppen überprüfen und sicherstellen, dass sich Ihre Softwareupdatepunkte in den korrekten Begrenzungsgruppen befinden.

Weitere Informationen finden Sie unter [Manuelles Wechseln von Clients auf einen neuen Softwareupdatepunkt](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).


## <a name="preferred-management-points"></a>Bevorzugte Verwaltungspunkte

 Bevorzugte Verwaltungspunkte ermöglichen einem Client die Identifikation eines Verwaltungspunkts, der seiner aktuellen Netzwerkadresse (oder Begrenzung) zugeordnet ist.  

-   Ein Client versucht zunächst, einen bevorzugten Verwaltungspunkt seines zugewiesenen Standorts zu verwenden, bevor er einen Verwaltungspunkt seines zugewiesenen Standorts verwendet, der nicht als bevorzugt konfiguriert wurde.  
-   Für diese Option müssen Sie sie für die Hierarchie aktivieren und anschließend Begrenzungsgruppen an den einzelnen primären Standorten konfigurieren, die die Verwaltungspunkte enthalten, die den Grenzen dieser Begrenzungsgruppe zugeordnet sein sollen.  
-   Wenn bevorzugte Verwaltungspunkte konfiguriert werden und ein Client seine Liste der Verwaltungspunkte organisiert, platziert er die bevorzugten Verwaltungspunkte ganz oben in der Liste der zugewiesenen Verwaltungspunkte (die alle Verwaltungspunkte des zugewiesenen Standorts des Clients enthält).  

> [!NOTE]  
>  Wenn ein Client seinen Standort wechselt (d. h. sich seine Netzwerkadresse ändert, wenn beispielsweise ein Laptop an einem Remotestandort mit dem Netzwerk verbunden wird), kann er einen Verwaltungspunkt (bzw. Proxyverwaltungspunkt) des lokalen Standorts verwenden, bevor versucht wird, einen Verwaltungspunkt seines zugewiesenen Standorts zu verwenden (was die bevorzugten Verwaltungspunkte einschließt).  Weitere Informationen finden Sie unter [Understand how clients find site resources and services for System Center Configuration Manager (Verstehen, wie Clients Standortressourcen und -dienste für System Center Configuration Manager suchen)](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

### <a name="overlapping-boundaries"></a>Überlappende Grenzen  
 Bei der Abfrage von Inhaltsorten werden überlappende Grenzkonfigurationen von Configuration Manager unterstützt:  

-   **Wenn ein Client Inhalt anfordert**und die Netzwerkadresse des Clients zu mehreren Begrenzungsgruppen gehört, erhält der Client von Configuration Manager eine Liste mit allen Verteilungspunkten, die über diesen Inhalt verfügen.  
-   **Wenn von einem Client Zustandsmigrationsinformationen bei einem Server angefordert bzw. an diesen gesendet werden**und das Netzwerk des Clients Mitglied mehrerer Begrenzungsgruppen ist, erhält der Client von Configuration Manager eine Liste mit allen Zustandsmigrationspunkten, die einer Begrenzungsgruppe mit der aktuellen Netzwerkadresse des Clients zugeordnet sind.  

So kann von den Clients der am nächsten liegende Server zur Übertragung der Inhalts- oder Zustandsmigrationsinformationen ausgewählt werden.  



## <a name="example-of-using-boundary-groups"></a>Beispiel für das Verwenden von Begrenzungsgruppen
In folgendem Beispiel wird ein Client verwendet, der in einem Verteilungspunkt nach Inhalt sucht. Dieses Beispiel kann auch auf andere Standortsystemrollen angewendet werden, die Begrenzungsgruppen verwenden. Beachten Sie, dass Softwareupdatepunkte die Konfiguration der Fallbackzeit (in Minuten) auf eine Nachbargruppe nicht unterstützen und immer ein Intervall von 120 Minuten verwenden.

Sie erstellen drei Begrenzungsgruppen, die keine Grenzen oder Standortsystemserver teilen:
-   Gruppe BG_A mit den Verteilungspunkten DP_A1 und DP_A2, die der Gruppe zugeordnet sind
-   Gruppe BG_B mit den Verteilungspunkten DP_B1 und DP_B2, die der Gruppe zugeordnet sind
-   Gruppe BG_C mit den Verteilungspunkten DP_C1 und DP_C2, die der Gruppe zugeordnet sind

Fügen Sie die Netzwerkspeicherorte Ihres Clients nur der Begrenzungsgruppe BG_A als Grenze hinzu, und konfigurieren Sie anschließend Beziehungen von dieser Begrenzungsgruppe zu den anderen beiden Begrenzungsgruppen:
-   Konfigurieren Sie Verteilungspunkte für die erste *Nachbargruppe* (BG_B), die nach 10 Minuten verwendet wird. Diese Gruppe enthält die Verteilungspunkte DP_B1 und DP_B2. Beide verfügen über eine gute Verbindung mit den Grenzspeicherorten der ersten Gruppe.
-   Konfigurieren Sie die zweite *Nachbargruppe* (BG_C), die nach 20 Minuten verwendet wird. Diese Gruppe enthält die Verteilungspunkte DP_C1 und DP_C2. Beide sind über ein WAN von den anderen Begrenzungsgruppen aus zugänglich.
-   Fügen Sie auch einen zusätzlichen Verteilungspunkt hinzu, der sich auf dem Standortserver der Standard-Standortbegrenzungsgruppe der Standorte befindet. Dies ist der am wenigsten bevorzugte Quellspeicherort für Inhalt, der sich jedoch zu all Ihren Begrenzungsgruppen zentral befindet.

    Beispiel für Begrenzungsgruppen und Fallbackzeiten:

     ![BG_Fallback](media/BG_Fallback.png)


Mit dieser Konfiguration:
-   Beginnt der Client die Suche nach Inhalt aus Verteilungspunkten in seiner *aktuellen* Begrenzungsgruppe (BG_A), wobei er jeden Verteilungspunkt 2 Minuten lang durchsucht, bevor er zum nächsten Verteilungspunkt in der Begrenzungsgruppe wechselt. Der Pool des Clients mit gültigen Quellspeicherorten für Inhalt umfasst DP_A1 und DP_A2.
-   Wenn der Client 10 Minuten lang keinen Inhalt aus der *aktuellen* Begrenzungsgruppe findet, fügt er die Verteilungspunkte aus der Begrenzungsgruppe BG_B zur Suche hinzu. Anschließend setzt er die Suche nach Inhalt von einem Verteilungspunkt in seinem kombinierten Pool von Verteilungspunkten fort, der nun die Verteilungspunkte der Begrenzungsgruppen BG_A und BG_B enthält. Der Client kontaktiert weiterhin jeden Verteilungspunkt zwei Minuten lang, bevor er zum nächsten Verteilungspunkt seines Pools wechselt. Der Pool des Clients mit gültigen Quellspeicherorten für Inhalt umfasst DP_A1, DP_A2, DP_B1 und DP_B2.
-   Nach weiteren 10 Minuten (insgesamt 20 Minuten), in denen der Client immer noch keinen Verteilungspunkt mit Inhalt gefunden hat, erweitert er seinen Pool mit verfügbaren Verteilungspunkten um die Verteilungspunkte der zweiten *Nachbargruppe*, also der Begrenzungsgruppe BG_C. Der Client verfügt nun über 6 Verteilungspunkte, die er durchsuchen kann (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 und DP_C2), und wechselt weiterhin alle zwei Minuten zu einem neuen Verteilungspunkt, bis er Inhalt gefunden hat.
-   Wenn der Client nach maximal 120 Minuten keinen Inhalt gefunden hat, greift er darauf zurück, die *Standard-Standortbegrenzungsgruppe* als Teil der kontinuierlichen Suche einzuschließen. In den Pool mit Verteilungspunkten werden nun alle Verteilungspunkte aus den drei konfigurierten Begrenzungsgruppen sowie der letzte Verteilungspunkt eingeschlossen, der sich auf dem Standortservercomputer befindet.  Der Client setzt die Suche nach Inhalt anschließend fort und wechselt alle zwei Minuten den Verteilungspunkt, bis er Inhalt gefunden hat.

Indem Sie die verschiedenen Nachbargruppen so konfigurieren, dass diese zu verschiedenen Zeiten verfügbar sind, steuern Sie, wann bestimmte Verteilungspunkte als Quellspeicherort für Inhalt hinzugefügt werden, sowie wann bzw. ob der Client ein Fallback auf die Standard-Standortbegrenzungsgruppe als Sicherheitsnetz für Inhalt verwendet, der von einem anderen Speicherort nicht verfügbar ist.






### <a name="update-existing-boundary-groups-to-the-new-model"></a>Aktualisieren vorhandener Begrenzungsgruppen auf das neue Modell
Wenn Sie auf eine Version vor Version 1610 aktualisieren, werden die folgenden Konfigurationen automatisch vorgenommen. Diese sollen sicherstellen, dass Ihr aktuelles Fallbackverhalten verfügbar bleibt, bis Sie neue Begrenzungsgruppen und Beziehungen konfigurieren.

-   Eine standardmäßige Standort-Begrenzungsgruppe für jeden primären Standort wird erstellt, der Name ist ***Standard-Standort-Begrenzungsgruppe&lt;Standortcode>.***
  - Verteilungspunkte mit aktiviertem *Fallbackquellpfad für Inhalt zulassen* und Zustandsmigrationspunkten an primären Standorten werden der *Standard-Standort-Begrenzungsgruppe&lt;Standortcode>* Begrenzungsgruppe dieses Standorts hinzugefügt.
  - Ab Version 1702 werden Softwareupdatepunkte in *Default-Site-Boundary-Group&lt;sitecode>* an jedem Standort hinzugefügt.
-   Von jeder vorhandenen Begrenzungsgruppe, die einen Standortserver umfasst, der mit einer langsamen Verbindung konfiguriert wurde, wird eine Kopie erstellt. Der Name der neuen Gruppe lautet ***&lt;ursprünglicher Name der Begrenzungsgruppe>-&lt;ursprüngliche ID der Begrenzungsgruppe>***:  
    -   Standortsysteme, die über eine schnelle Verbindung verfügen, bleiben in der ursprünglichen Begrenzungsgruppe.
    -   Eine Kopie der Standortsysteme (Verteilungspunkte, Verwaltungspunkte) mit einer langsamen Verbindung wird der Kopie der Begrenzungsgruppe hinzugefügt. Die ursprünglichen Standortsysteme, die als langsam konfiguriert wurden, bleiben zur Abwärtskompatibilität in den ursprünglichen Begrenzungsgruppen, werden von diesen Begrenzungsgruppen jedoch nicht verwendet.
    - Dieser Begrenzungsgruppenkopie sind keine Grenzen zugeordnet. Jedoch wird ein Fallbacklink zwischen der ursprünglichen Gruppe und der neuen Begrenzungsgruppe erstellt, deren Fallbackzeit auf 0 festgelegt ist.  


- **Für sekundäre Standorte gilt:**
  - Eine Begrenzungsgruppe wird erstellt, wenn ein sekundärer Standort mindestens einen Verteilungspunkt mit aktiviertem *Fallbackquellpfad für Inhalt zulassen* oder Zustandsmigrationspunkt aufweist. Der Name der Begrenzungsgruppe ist ***Sekundärer-Standort-Nachbar--Tmp&lt;Standortcode>.***
  - Alle Verteilungspunkte mit aktiviertem *Fallbackquellpfad für Inhalt zulassen* und Zustandsmigrationspunkten werden dieser neu erstellten sekundären Standortbegrenzungsgruppe hinzugefügt.
  - Ein Fallbacklink wird zwischen der ursprünglichen Begrenzungsgruppe und der neu erstellten Nachbarbegrenzungsgruppe erstellt, deren Fallbackzeit auf 0 festgelegt ist.


 Die folgende Tabelle ermittelt das neue Fallbackverhalten, das Sie von der Kombination aus den ursprünglichen Bereitstellungseinstellungen und den Verteilungspunktkonfigurationen erwarten können:

Ursprüngliche Bereitstellungskonfiguration für „Programm nicht ausführen“ im langsamen Netzwerk  |Ursprüngliche Verteilungspunktkonfiguration für „Allow client to use a fallback source location for content“ (Zulassen, dass der Client einen Fallbackquellspeicherort für Inhalt verwendet)  |Neues Fallbackverhalten  
---------|---------|---------
Ausgewählt     |  Ausgewählt    |  **Kein Fallback** – Verwenden Sie nur die Verteilungspunkte in der aktuellen Begrenzungsgruppe.       
Ausgewählt     |  Nicht ausgewählt|  **Kein Fallback** – Verwenden Sie nur die Verteilungspunkte in der aktuellen Begrenzungsgruppe.       
Nicht ausgewählt |  Nicht ausgewählt|  **Fallback auf Nachbar** – Verwenden Sie die Verteilungspunkte in der aktuellen Begrenzungsgruppe, und fügen Sie anschließend die Verteilungspunkte aus der Nachbarbegrenzungsgruppe hinzu. Sofern kein expliziter Link zur Standard-Standortbegrenzungsgruppe konfiguriert wurde, erfolgt kein Fallback der Clients auf diese Gruppe.    
Nicht ausgewählt | Ausgewählt     |   **Normales Fallback** – Verwenden Sie die Verteilungspunkte in der aktuellen Begrenzungsgruppe und anschließend die der Nachbar- und der Standard-Standortbegrenzungsgruppen.

 Alle anderen Bereitstellungskonfigurationen führen zum **Normalen Fallback**.  




## <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Änderungen gegenüber früheren Versionen für Benutzeroberfläche und Verhalten für Speicherorte für Inhalt
Beim Folgenden handelt es sich um die wichtigsten Änderungen von Begrenzungsgruppen und dem Suchen von Inhalt durch Clients. Diese Änderungen wurden mit Version 1610 eingeführt. Viele dieser Änderungen und Konzepte arbeiten zusammen.


-   **Konfigurationen für „schnell“ oder „langsam“ werden entfernt:** Sie konfigurieren einzelne Verteilungspunkte nicht mehr so, dass diese schnell oder langsam sind.  Stattdessen wird jedes Standortsystem, das einer Begrenzungsgruppe zugeordnet ist, auf die gleiche Weise behandelt. Aufgrund dieser Änderung unterstützt die Registerkarte **Referenz** der Begrenzungsgruppeneigenschaften die Konfiguration von „schnell“ und „langsam“ nicht mehr.
-   **Neue Standardbegrenzungsgruppen an jedem Standort:** Jeder primäre Standort verfügt über eine neue Standardbegrenzungsgruppe mit dem Namen ***Default-Site-Boundary-Group&lt;sitecode>***.  Wenn sich ein Client nicht an einem Netzwerkstandort befindet, der einer Begrenzungsgruppe zugewiesen ist, verwendet dieser Client die Standortsysteme, die der Standardgruppe seines zugewiesenen Standorts zugeordnet sind. Planen Sie, diese Begrenzungsgruppe als Ersatz für das Konzept der Fallbackinhaltsquelle zu verwenden.      
 -  **Allow fallback source locations for content** (Fallbackquellspeicherorte für Inhalt zulassen) wird entfernt: Sie konfigurieren nicht mehr explizit einen Verteilungspunkt, der für das Fallback verwendet wird, und die Optionen, um dies festzulegen, werden von der Benutzeroberfläche entfernt.

    Darüber hinaus hat sich das Ergebnis geändert, das auftritt, wenn die Einstellung **Die Verwendung eines Fallbackquellpfads für den Inhalt durch Clients zulassen** auf einem Bereitstellungstyp für Anwendungen festgelegt wird. Diese Einstellung auf einem Bereitstellungstyp ermöglicht es einem Client nun, die Standard-Standortbegrenzungsgruppe als Quellspeicherort für Inhalt zu verwenden.

 -  **Begrenzungsgruppenbeziehungen:** Jede Begrenzungsgruppe kann mit einer oder mehreren zusätzlichen Begrenzungsgruppen verknüpft werden. Diese Links bilden Beziehungen, die auf der neuen Registerkarte der Begrenzungsgruppeneigenschaften mit dem Namen **Beziehungen** konfiguriert sind:
    -   Jede Begrenzungsgruppe, der ein Client direkt zugewiesen ist, wird **aktuelle** Begrenzungsgruppe genannt.  
    -   Jede Begrenzungsgruppe, die ein Client aufgrund einer Zuweisung zwischen der *aktuellen* Begrenzungsgruppe des Clients und einer anderen Gruppe verwenden kann, wird **Nachbarbegrenzungsgruppe** genannt.
    -  Auf der Registerkarte **Beziehungen** können Sie Begrenzungsgruppen hinzufügen, die als *Nachbarbegrenzungsgruppe* verwendet werden können. Sie können auch eine Zeit in Minuten konfigurieren, die bestimmt, wann ein Client, der keinen Inhalt von einem Verteilungspunkt in der *aktuellen* Gruppe findet, beginnt, Speicherorte für Inhalt von diesen *Nachbarbegrenzungsgruppen* zu suchen.

        Beim Hinzufügen oder Ändern einer Begrenzungsgruppenkonfiguration verfügen Sie über die Option, das Fallback auf diese bestimmte Begrenzungsgruppe von der aktuellen Gruppe zu blockieren, die Sie konfigurieren.

    Um die neue Konfiguration zu verwenden, definieren Sie explizite Zuordnungen (Links) von einer Begrenzungsgruppe zu einer anderen, und konfigurieren Sie alle Verteilungspunkte in dieser zugeordneten Gruppe mit der gleichen Zeit in Minuten. Die Zeit, die Sie konfigurieren, bestimmt, wann ein Client, der keine Inhaltsquelle von seiner *aktuellen* Begrenzungsgruppe findet, beginnt, Inhaltsquellen von dieser Nachbarbegrenzungsgruppe zu suchen.

    Zusätzlich zu Begrenzungsgruppen, die Sie explizit konfigurieren, verfügt jede Begrenzungsgruppe über einen implizierten Link zur Standard-Standortbegrenzungsgruppe. Dieser Link wird nach 120 Minuten aktiv, wenn die Standard-Standortbegrenzungsgruppe zu einer Nachbarbegrenzungsgruppe wird, was den Clients ermöglicht, die Verteilungspunkte zu verwenden, die dieser Begrenzungsgruppe als Quellspeicherort für Inhalt zugeordnet sind.

    Dieses Verhalten ersetzt, was zuvor als Fallback für den Inhalt bezeichnet wurde.  Sie können dieses Standardverhalten von 120 Minuten außer Kraft setzen, indem Sie die Standardbegrenzungsgruppe einer *aktuellen* Gruppe zuordnen und eine bestimmte Zeit in Minuten festlegen oder das Fallback vollständig blockieren, um dessen Verwendung zu verhindern.


-   **Clients versuchen bis zu 2 Minuten lang, Inhalt aus jedem Verteilungspunkt zu erhalten:** Wenn ein Client nach einem Quellspeicherort für Inhalt sucht, versucht er 2 Minuten lang auf jeden Verteilungspunkt zuzugreifen, bevor er anschließend einen anderen Verteilungspunkt versucht. Dabei handelt es sich um eine Änderung gegenüber früheren Versionen, bei denen Clients bis zu 2 Stunden lang versucht haben, eine Verbindung zu einem Verteilungspunkt herzustellen.

    - Der erste Verteilungspunkt, den ein Client versucht zu verwenden, wird zufällig aus dem Pool verfügbarer Punkte in der *aktuellen* Begrenzungsgruppe (bzw. den aktuellen Begrenzungsgruppen) ausgewählt.

    - Wenn der Client den Inhalt nach zwei Minuten nicht gefunden hat, wechselt er zu einem neuen Verteilungspunkt und versucht, Inhalt von diesem Server zu erhalten. Dieser Vorgang wird alle zwei Minuten wiederholt, bis der Client den Inhalt findet oder den letzten Server im Pool erreicht.

    - Wenn ein Client in seinem *aktuellen* Pool keinen gültigen Quellspeicherort für Inhalt findet, bevor der Zeitraum für ein Fallback auf eine *Nachbarbegrenzungsgruppe* erreicht ist, fügt der Client die Verteilungspunkte aus dieser *Nachbarbegrenzungsgruppe* am Ende seiner aktuellen Liste hinzu und durchsucht anschließend die erweiterte Gruppe von Quellspeicherorten, die die Verteilungspunkte aus beiden Begrenzungsgruppen umfasst.

        > [!TIP]  
        > Wenn Sie einen expliziten Link von der aktuellen Begrenzungsgruppe zu der Standard-Standortbegrenzungsgruppe erstellen und eine Fallbackzeit festlegen, die kürzer ist als die Fallbackzeit für einen Link zu einer Nachbarbegrenzungsgruppe, beginnen Clients, Quellspeicherorte aus der Standard-Standortbegrenzungsgruppe zu durchsuchen, bevor sie die Nachbargruppe einschließen.

    - Wenn der Client vom letzten Server im Pool keinen Inhalt abrufen kann, beginnt er den Prozess erneut.


## <a name="procedures-for-boundary-groups"></a>Prozeduren für Begrenzungsgruppen
Die folgenden Prozeduren gelten ab Version 1610. Wenn Sie eine Version älter als Version 1610 verwenden, finden Sie die Prozeduren in [Boundary groups for System Center Configuration Manager version 1606, and 1606 (Begrenzungsgruppen für die System Center Configuration Manager-Versionen 1511, 1602 und 1606)](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).


### <a name="to-create-a-boundary-group"></a>So erstellen Sie eine Begrenzungsgruppe  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Begrenzungsgruppe erstellen**.  

3.  Wählen Sie im Dialogfeld **Begrenzungsgruppe erstellen** die Registerkarte **Allgemein** aus, und geben Sie unter **Name** einen Namen für diese Begrenzungsgruppe an.  

4.  Klicken Sie auf **OK** , um die neue Begrenzungsgruppe zu speichern.  


### <a name="to-configure-a-boundary-group"></a>So konfigurieren Sie eine Begrenzungsgruppe  
 1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

 2.  Wählen Sie die Begrenzungsgruppe aus, die Sie ändern möchten.  

 3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

 4.  Wählen Sie im Dialogfeld **Eigenschaften** für die Begrenzungsgruppe die Registerkarte **Allgemein** aus, um die Grenzen zu ändern, die Mitglieder dieser Begrenzungsgruppe sind.  

     -   Wenn Sie Grenzen hinzufügen möchten, klicken Sie auf **Hinzufügen**, aktivieren Sie das Kontrollkästchen für eine oder mehrere Grenzen, und klicken Sie dann auf **OK**.  

     -   Wenn Sie Grenzen entfernen möchten, wählen Sie die Grenze aus, und klicken Sie auf **Entfernen**.  

 5.  Wählen Sie die Registerkarte **Referenzen** aus, um die Konfiguration für Standortzuweisung und zugeordnete Standortsystemserver zu ändern:  

     -   Aktivieren Sie das Kontrollkästchen **Diese Begrenzungsgruppe für die Standortzuweisung verwenden**, und wählen Sie dann aus der Dropdownliste **Zugewiesener Standort** einen Standort aus, damit Clients diese Begrenzungsgruppe für die Standortzuweisung verwenden können.  

     -   Um zu konfigurieren, welche verfügbaren Standortsystemserver dieser Begrenzungsgruppe zugeordnet sind, gehen Sie wie folgt vor:  

     1.  Klicken Sie auf **Hinzufügen**, und aktivieren Sie dann das Kontrollkästchen für einen oder mehrere Server. Die Server werden als zugeordnete Standortsystemserver für diese Begrenzungsgruppe hinzugefügt. Nur Server, auf denen die unterstützte Standortsystemrolle installiert ist, sind verfügbar.  

         > [!NOTE]  
         >  Sie können eine beliebige Kombination verfügbarer Standortsysteme von einem beliebigen Standort in der Hierarchie auswählen. Ausgewählte Standortsysteme werden in den Eigenschaften jeder Grenze, die dieser Begrenzungsgruppe angehört, auf der Registerkarte **Standortsysteme** aufgelistet.  

     2.  Wenn Sie einen Server aus dieser Begrenzungsgruppe entfernen möchten, wählen Sie den Server aus, und klicken Sie dann auf **Entfernen**.  

         > [!NOTE]  
         >  Wenn diese Begrenzungsgruppe nicht mehr zum Zuordnen von Standortsystemen verwendet werden soll, müssen Sie alle Server entfernen, die als zugeordnete Standortsystemserver aufgelistet sind.  

 6.  Wählen Sie die Registerkarte **Beziehungen** aus, um das Fallbackverhalten zu konfigurieren:  

     - Klicken Sie auf **Hinzufügen**, und wählen Sie anschließend die Begrenzungsgruppe aus, die Sie konfigurieren möchten.

     - Legen Sie eine Fallbackzeit für Verteilungspunkte fest. Nach dieser Zeitspanne können Clients in der Begrenzungsgruppe, für die Sie die Beziehungen konfigurieren, die Suche nach Inhalten aus den Verteilungspunkten der von Ihnen hinzugefügten Begrenzungsgruppe starten.

     - Zur Verhinderung von Fallback auf eine bestimmte Begrenzungsgruppe einschließlich der *Standard-Standortbegrenzungsgruppe*, die standardmäßig konfiguriert ist, wählen Sie die Begrenzungsgruppe aus, und aktivieren Sie das Kontrollkästchen **Never Fallback** (Kein Fallback).   

 7.  Klicken Sie auf **OK** , um die Eigenschaften der Begrenzungsgruppe zu schließen und die Konfiguration zu speichern.  

#### <a name="to-associate-a-site-systme-server-with-a-boundary-group"></a>So ordnen Sie ein Standortsystem einer Begrenzungsgruppe zu  
 1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

 2.  Wählen Sie die Begrenzungsgruppe aus, die Sie ändern möchten.  

 3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

 4.  Wählen Sie im Dialogfeld **Eigenschaften** für die Begrenzungsgruppe die Registerkarte **Referenzen** aus.  

 5.  Klicken Sie unter **Standortsystemserver auswählen**auf **Hinzufügen**, aktivieren Sie das Kontrollkästchen für die Standortsystemserver, die dieser Begrenzungsgruppe zugeordnet werden sollen, und klicken Sie dann auf **OK**.  

 6.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen und die Konfiguration der Begrenzungsgruppe zu speichern.  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>So konfigurieren Sie einen Fallbackstandort für die automatische Standortzuweisung  

  1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** >  **Standorte**.  

  2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.  

  3.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen **Fallbackstandort verwenden**, und wählen Sie dann in der Dropdownliste **Fallbackstandort** einen Standort aus.  

  4.  Klicken Sie auf **OK** , um die Konfiguration zu speichern.  

#### <a name="to-enable-use-of-preferred-management-points"></a>So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte  

 1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie anschließend **Hierarchieeinstellungen**auf der Registerkarte **Start** aus.  

 2.  Wählen Sie im Dialogfeld „Hierarchieeinstellungen“ auf der Registerkarte **Allgemein** die Option **Clients bevorzugen die in Begrenzungsgruppen angegebenen Verwaltungspunkte**.  

 3.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen und die Konfiguration zu speichern.  
