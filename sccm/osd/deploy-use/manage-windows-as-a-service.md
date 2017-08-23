---
title: "Verwalten von Windows as a Service – Configuration Manager | Microsoft-Dokumentation"
description: "Lassen Sie sich mit Configuration Manager den Status von Windows as a Service anzeigen, erstellen Sie Wartungspläne, um Bereitstellungsringe zu bilden, und lassen Sie sich Warnungen anzeigen, wenn Windows 10-Clients das Supportende erreichen."
ms.custom: na
ms.date: 03/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
caps.latest.revision: "26"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2c2c0f81736c1b00ea487ae1261803a8105bb5e4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-windows-as-a-service-using-system-center-configuration-manager"></a>Verwalten von Windows als Dienst mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 In System Center Configuration Manager können Sie den Zustand von Windows as a Service in Ihrer Umgebung anzeigen, Wartungspläne zur Bildung von Bereitstellungsringen erstellen und sicherstellen, dass Windows 10 Current Branch-Systeme auf dem neuesten Stand gehalten werden, wenn neue Builds veröffentlicht werden. Außerdem können Sie Warnungen anzeigen, wenn sich Windows 10-Clients dem Ende des Supports für ihren Build von Current Branch oder von Current Branch for Business (CBB) nähern.  

 Weitere Informationen zu den Windows 10-Wartungsoptionen finden Sie unter  [Windows 10-Wartungsoptionen für Updates und Upgrades](https://technet.microsoft.com/library/mt598226\(v=vs.85\).aspx).  

 Gehen Sie wie in den folgenden Abschnitten beschrieben vor, um Windows als Dienst zu verwalten.

##  <a name="BKMK_Prerequisites"></a> Voraussetzungen  
 Um Daten im Windows 10-Wartungsdashboard anzuzeigen, gehen Sie wie folgt vor:  

-   Auf Windows 10-Computern müssen Configuration Manager-Softwareupdates mit Windows Server Update Services (WSUS) für die Verwaltung von Softwareupdates verwendet werden. Wenn auf Computern Windows Update für Unternehmen (oder Windows-Insider) für die Verwaltung von Softwareupdates verwendet wird, erfolgt in Windows 10-Wartungsplänen keine Auswertung des Computers. Weitere Informationen finden Sie unter [Integration with Windows Update for Business in Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   Auf den Softwareupdatepunkten und Standortservern muss WSUS 4.0 mit [Hotfix 3095113](https://support.microsoft.com/kb/3095113) installiert sein. Dadurch wird die Softwareupdateklassifizierung **Upgrades** hinzugefügt. Weitere Informationen finden Sie unter [Prerequisites for software updates (Voraussetzungen für Softwareupdates)](../../sum/plan-design/prerequisites-for-software-updates.md).  

-   WSUS 4.0 mit dem [Hotfix 3159706](https://support.microsoft.com/kb/3159706) muss auf Ihren Softwareupdatepunkten und Standortservern installiert sein, um ein Upgrade von Computern auf Windows 10 Anniversary Update sowie Unterversionen durchzuführen. Im Support-Artikel werden manuelle Schritte beschrieben, die Sie ausführen müssen, um diesen Hotfix zu installieren. Weitere Informationen finden Sie im Blog [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/05/update-your-configmgr-1606-sup-servers-to-deploy-the-windows-10-anniversary-update/).

-   Aktivieren Sie die Frequenzermittlung. Die im Windows 10-Wartungsdashboard angezeigten Daten werden mithilfe der Ermittlung gesammelt. Weitere Informationen finden Sie unter [Configure Heartbeat Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#a-namebkmkconfighbdisca-configure-heartbeat-discovery).  

     Die folgenden Branch- und Buildinformationen zu Windows 10 werden ermittelt und in den folgenden Attributen gespeichert:  

    -   **Bereitstellungsoption für Betriebssystem**: Gibt die Betriebssystem-Verzweigung an. Beispiel: **0** = CB (keine Upgrades zum Aufschieben), **1** = CBB (Upgrades aufschieben), **2** = Long Term Servicing Branch (LTSB)

    -   **Betriebssystembuild**: Gibt den Betriebssystembuild an. Beispiel: **10.0.10240** (RTM) oder **10.0.10586** (Version 1511)  

-   Der Dienstverbindungspunkt muss installiert und für den Modus **Online, dauerhafte Verbindung** konfiguriert werden, um Daten im Windows 10-Wartungsdashboard anzuzeigen. Wenn Sie im Offlinemodus arbeiten, werden Datenaktualisierungen erst dann im Dashboard angezeigt, wenn Sie Configuration Manager-Wartungsupdates erhalten.   
     Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](../../core/servers/deploy/configure/about-the-service-connection-point.md).  


-   Auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, muss Internet Explorer 9 installiert sein.  

-   Softwareupdates müssen konfiguriert und synchronisiert werden. Windows 10-Featureupgrades sind erst dann in der Configuration Manager-Konsole verfügbar, wenn Sie die Klassifizierung **Upgrades** ausgewählt und Softwareupdates synchronisiert haben. Weitere Informationen finden Sie unter [Prepare for software updates management (Vorbereiten der Softwareudateverwaltung)](../../sum/get-started/prepare-for-software-updates-management.md).  

##  <a name="BKMK_ServicingDashboard"></a> Windows 10-Wartungsdashboard  
 Das Windows 10-Wartungsdashboard stellt Informationen zu Windows 10-Computern in Ihrer Umgebung, aktive Wartungspläne, Informationen zu Kompatibilität usw. bereit. Damit Daten im Windows 10-Wartungsdashboard angezeigt werden, muss der Dienstverbindungspunkt installiert sein. Das Dashboard verfügt über die folgenden Kacheln:  

-   **Kachel „Windows 10-Verwendung“**: Enthält eine Aufschlüsselung der öffentlichen Builds von Windows 10. Windows Insider-Builds sind unter **Sonstige** aufgelistet, genau wie alle Builds, die Ihrem Standort noch nicht bekannt sind. Der Dienstverbindungspunkt lädt die Metadaten herunter, mit denen er über die Windows-Builds informiert wird. Anschließend werden diese Daten mit Ermittlungsdaten verglichen.  

-   **Kachel “Windows 10-Ringe“**: Enthält eine Aufschlüsselung von Windows 10 nach Branch und Bereitschaftsstatus. Das Segment „LTSB“ umfasst alle LTSB-Versionen (während auf der ersten Kachel eine Aufschlüsselung in die verschiedenen Versionen erfolgt. Beispiel: Windows 10 LTSB 2015. Das Segment **Release Ready** entspricht CB, und das Segment **Business Ready** entspricht CBB.  

-   **Kachel „Wartungsplan erstellen“**: Bietet eine schnelle Möglichkeit zum Erstellen eines Wartungsplans. Sie geben den Namen, die Sammlung (angezeigt werden nur die zehn kleinsten Sammlungen), das Bereitstellungspaket (angezeigt werden nur die zehn Pakete, die zuletzt geändert wurden) und den Bereitschaftsstatus an. Für die anderen Einstellungen werden Standardwerte verwendet. Klicken Sie auf **Erweiterte Einstellungen** , um den Assistenten zum Erstellen eines Wartungsplans zu starten, in dem Sie alle Einstellungen für den Wartungsplan konfigurieren können.  

-   **Kachel „Abgelaufen“**: Zeigt den Prozentsatz der Geräte mit einem abgelaufenen Build von Windows 10 an. Configuration Manager ermittelt den Prozentsatz anhand der Metadaten, die der Dienstverbindungspunkt herunterlädt, und vergleicht ihn mit Ermittlungsdaten. Ein Build, das nach Ablauf seiner Lebensdauer keine monatlichen kumulativen Updates, einschließlich Sicherheitsupdates, erhält. Die Computer in dieser Kategorie sollte auf die nächste Buildversion aktualisiert werden. Configuration Manager rundet auf die nächste ganze Zahl auf. Wenn Sie z. B. über rund 10.000 Computer verfügen, aber nur einen mit einem abgelaufenen Build, zeigt die Kachel 1 % an.  

-   **Kachel „Bald ablaufend“**: Zeigt, ähnlich wie die Kachel **Abgelaufen** , den Prozentsatz der Computer mit einem Build an, dessen Lebensdauer in Kürze abläuft (innerhalb von ca. vier Monaten). Configuration Manager rundet auf die nächste ganze Zahl auf.  

-   **Kachel „Warnungen“**: Zeigt aktive Warnungen an.  

-   **Kachel „Wartungsplanüberwachung“**: Zeigt die Wartungspläne, die Sie erstellt haben, zusammen mit einem entsprechenden Kompatibilitätsdiagramm an. Dadurch erhalten Sie einen schnellen Überblick über den aktuellen Zustand der Wartungsplanbereitstellungen. Wenn ein früherer Bereitstellungsring Ihre Erwartungen hinsichtlich der Kompatibilität erfüllt hat, können Sie einen späteren Wartungsplan (Bereitstellungsring) auswählen und auf **Jetzt bereitstellen** klicken, anstatt zu warten, bis die Wartungsplanregeln automatisch ausgelöst werden.  

-   **Kachel „Windows 10-Builds“**: Die Anzeige ist eine feste Imagezeitachse mit einer Übersicht der bisher veröffentlichten Windows 10-Builds. Sie bietet Ihnen einen allgemeinen Überblick darüber, wann Builds in die verschiedenen Zustände übergehen.  

> [!IMPORTANT]  
>  Die im Windows 10-Wartungsdashboard angezeigten Informationen (z. B. der Supportlebenszyklus für Windows 10-Versionen) dienen lediglich der Arbeitserleichterung und sind nur für die Verwendung innerhalb Ihres Unternehmens bestimmt. Sie sollten sich im Hinblick auf die Updatekompatibilität nicht ausschließlich auf diese Informationen verlassen. Überprüfen Sie stets die Richtigkeit der bereitgestellten Informationen.  

## <a name="servicing-plan-workflow"></a>Wartungsplanworkflow  
 Windows 10-Wartungspläne in Configuration Manager ähneln Regeln zur automatischen Bereitstellung von Softwareupdates. Sie erstellen einen Wartungsplan mit den folgenden Kriterien, die von Configuration Manager ausgewertet werden:  

-   **Klassifizierung „Upgrades“:**Nur Updates, die zur Klassifizierung **Upgrades** gehören, werden ausgewertet.  

-   **Bereitschaftsstatus**: Der im Wartungsplan definierte Bereitschaftsstatus wird mit dem Bereitschaftsstatus für das Upgrade verglichen. Die Metadaten für das Upgrade werden abgerufen, wenn der Dienstverbindungspunkt nach Updates sucht.  

-   **Zeitverzögerung**: Die Anzahl der Tage, die Sie im Wartungsplan für **Wie viele Tage möchten Sie nach der Veröffentlichung eines neuen Upgrades durch Microsoft warten, bevor Sie es in Ihrer Umgebung bereitstellen?** angegeben haben. Configuration Manager wird ausgewertet, ob ein Upgrade in die Bereitstellung eingeschlossen werden soll, und zwar, wenn das aktuelle Datum nach dem Veröffentlichungsdatum plus der konfigurierten Anzahl von Tagen liegt.  

 Wenn ein Upgrade die Kriterien erfüllt, fügt der Wartungsplan das Upgrade zum Bereitstellungspaket hinzu, verteilt das Paket an Verteilungspunkte und stellt der Sammlung das Upgrade basierend auf den im Wartungsplan konfigurierten Einstellungen bereit.  Sie können die Bereitstellungen über die Kachel „Wartungsplanüberwachung“ im Windows 10-Wartungsdashboard überwachen. Weitere Informationen finden Sie unter [Monitor software updates (Überwachen von Softwareupdates)](../../sum/deploy-use/monitor-software-updates.md).  

##  <a name="BKMK_ServicingPlan"></a> Windows 10-Wartungsplan  
 Bei der Bereitstellung von Windows 10 CB können Sie einen oder mehrere Wartungspläne erstellen, um die Bereitstellungsringe für Ihre Umgebung zu definieren, und sie dann im Windows 10-Wartungsdashboard überwachen.   
Wartungspläne verwenden nur die Softwareupdateklassifizierung **Upgrades** und keine kumulativen Updates für Windows 10. Für diese Updates müssen Sie Bereitstellungen weiterhin mit dem Softwareupdateworkflow vornehmen.  Die Endbenutzerumgebung mit einem Wartungsplan entspricht derjenigen mit Softwareupdates, einschließlich der Einstellungen, die Sie im Wartungsplan konfigurieren.  

> [!NOTE]  
>  Sie können eine Tasksequenz zum Bereitstellen eines Upgrades für jeden Windows 10-Build verwenden, dazu ist jedoch mehr manuelle Arbeit erforderlich. Sie müssten die aktualisierten Quelldateien als Upgradepaket für Betriebssysteme importieren, die Tasksequenz erstellen und dann in der entsprechenden Gruppe von Computern bereitstellen. Eine Tasksequenz bietet jedoch zusätzliche benutzerdefinierte Optionen, wie z. B. die Aktionen vor und nach der Bereitstellung.  

 Sie können einen grundlegenden Wartungsplan über das Windows 10-Wartungsdashboard erstellen. Nachdem Sie den Namen, die Sammlung (angezeigt werden nur die zehn kleinsten Sammlungen), das Bereitstellungspaket (angezeigt werden nur die zehn Pakete, die zuletzt geändert wurden) und den Bereitschaftsstatus an gegeben haben, erstellt Configuration Manager den Wartungsplan mit Standardwerten für die übrigen Einstellungen. Sie können auch den Assistenten zum Erstellen eines Wartungsplans starten, um alle Einstellungen zu konfigurieren. Verwenden Sie das folgende Verfahren zum Erstellen eines Wartungsplans mit dem Assistenten zum Erstellen eines Wartungsplans.  

> [!NOTE]  
>  Ab Version 1602 von Configuration Manager können Sie das Verhalten für Bereitstellungen mit hohem Risiko verwalten. Bei einer Bereitstellung mit hohem Risiko handelt es sich um eine Bereitstellung, die automatisch installiert wird und zu unerwünschten Ergebnissen führen kann. Beispielsweise wird eine Tasksequenz, die als Zweck **Erforderlich** aufweist und Windows 10 bereitstellt, als eine Bereitstellung mit hohem Risiko betrachtet. Weitere Informationen finden Sie unter [Settings to manage high-risk deployments (Einstellungen zum Verwalten risikoreicher Bereitstellungen)](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

#### <a name="to-create-a-windows-10-servicing-plan"></a>So erstellen Sie einen Windows 10-Wartungsplan  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie **Windows 10-Wartung**im Arbeitsbereich „Softwarebibliothek“, und klicken Sie dann auf **Wartungspläne**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Wartungsplan erstellen**. Der Assistent zum Erstellen eines Wartungsplans wird geöffnet.  

4.  Konfigurieren Sie auf der Seite **Allgemein** die folgenden Einstellungen:  

    -   **Name**: Geben Sie den Namen für den Wartungsplan an. Der Name muss eindeutig sein, das Ziel der Regel angeben und sich am Configuration Manager-Standort leicht von anderen Namen unterscheiden lassen.  

    -   **Beschreibung**: Geben Sie eine Beschreibung für den Wartungsplan an. Die Beschreibung muss einen Überblick über den Wartungsplan und alle anderen relevanten Informationen umfassen, die die Identifizierung und Unterscheidung des Plans am Configuration Manager-Standort erleichtern. Das Feld „Beschreibung“ ist optional, hat eine Begrenzung auf 256 Zeichen und ist standardmäßig leer.  

5.  Konfigurieren Sie auf der Seite „Wartungsplan“ die folgenden Einstellungen:  

    -   **Zielsammlung**: Gibt den für die Bereitstellung zu verwendenden Wartungsplan an. Mitglieder dieser Sammlung erhalten die im Wartungsplan definierten Windows 10-Upgrades.  

        > [!NOTE]  
        >  Ab Version 1602 von Configuration Manager werden bei einer Bereitstellung mit hohem Risiko, wie z.B. einem Wartungsplan, im Fenster **Sammlung auswählen** nur die benutzerdefinierten Sammlungen angezeigt, die den in den Eigenschaften des Standorts konfigurierten Einstellungen zur Bereitstellungsüberprüfung entsprechen.
        >    
        > Bereitstellungen mit hohem Risiko sind immer auf benutzerdefinierte Sammlungen, von Ihnen erstellte Sammlungen und die integrierte Sammlung **Unbekannte Computer** beschränkt. Beim Erstellen einer Bereitstellung mit hohem Risiko können Sie keine integrierte Sammlung auswählen, wie z. B. **Alle Systeme**. Deaktivieren Sie die Einstellung **Hide collections with a member count greater than the site's minimum size configuration** (Sammlungen mit einer Anzahl der Mitglieder ausblenden, die größer als die minimale Größenkonfiguration des Standorts ist), um alle benutzerdefinierten Sammlungen anzuzeigen, die weniger Clients als die konfigurierte maximale Größe enthalten. Weitere Informationen finden Sie unter [Einstellungen für die Verwaltung hochriskanter Bereitstellungen](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
        >  
        > Die Einstellungen zur Bereitstellungsüberprüfung basieren auf der aktuellen Mitgliedschaft der Sammlung. Nach der Bereitstellung des Wartungsplans wird die Sammlungsmitgliedschaft für die Einstellungen für eine Bereitstellung mit hohem Risiko nicht erneut bewertet.  
        >  
        > Angenommen, Sie legen **Standardgröße** auf 100 und **Maximale Größe** auf 1000 fest. Wenn Sie eine Bereitstellung mit hohem Risiko erstellen, werden im Fenster **Sammlung auswählen** nur die Sammlungen angezeigt, die weniger als 100 Clients enthalten. Wenn Sie die Einstellung **Hide collections with a member count greater than the site's minimum size configuration** (Sammlungen mit einer Anzahl der Mitglieder ausblenden, die größer als die minimale Größenkonfiguration des Standorts ist) deaktivieren, werden im Fenster Sammlungen angezeigt, die weniger als 1.000 Clients enthalten.  
        >
        > Wenn Sie eine Sammlung auswählen, die eine Standortrolle enthält, gilt Folgendes:    
        >   
        >    - Wenn die Sammlung einen Standortsystemserver enthält und Sie die Einstellungen zur Bereitstellungsüberprüfung so konfigurieren, dass Sammlungen mit Standortsystemservern blockiert werden, tritt ein Fehler auf, und Sie können nicht fortfahren.    
        >    - Wenn die Sammlung einen Standortsystemserver enthält und Sie die Einstellungen zur Bereitstellungsüberprüfung so konfigurieren, dass Sie im Fall von Sammlungen mit Standortsystemservern gewarnt werden, wird im Assistenten zum Bereitstellen von Software eine Warnung über ein hohes Risiko angezeigt, falls die Sammlung den Standardwert für die Größe überschreitet oder falls die Sammlung einen Server enthält. Sie müssen der Erstellung einer Bereitstellung mit hohem Risiko zustimmen, und eine Überwachungsstatusmeldung wird erstellt.  

6.  Konfigurieren Sie auf der Seite „Bereitstellungsring“ die folgenden Einstellungen:  

    -   **Geben Sie den Windows-Bereitschaftsstatus an, für den dieser Wartungsplan gelten soll**: Wählen Sie eine der folgenden Optionen aus:  

        -   **Sofortige Bereitstellung (Current Branch):** Beim CB Servicing-Modell sind Funktionsupdates verfügbar, sobald sie von Microsoft veröffentlicht werden.

        -   **Bereitstellung zum Testen (Current Branch for Business):** Der CBB Servicing Branch wird normalerweise für die umfassende Bereitstellung verwendet. Windows 10-Clients im CBB Servicing Branch erhalten denselben Build von Windows 10 wie Clients im CB Servicing Branch, allerdings zu einem späteren Zeitpunkt.

        Weitere Informationen zu Servicing Branches und die für Sie am besten geeignete Option finden Sie unter [Servicing Branches](https://technet.microsoft.com/itpro/windows/manage/waas-overview#servicing-branches).

    -   **Anzahl der Tage nach der Veröffentlichung eines neuen Updates durch Microsoft, nach der Sie die Bereitstellung in Ihrer Umgebung vornehmen möchten:** In Configuration Manager wird ausgewertet, ob ein Upgrade in die Bereitstellung eingeschlossen werden soll, und zwar, wenn das aktuelle Datum nach dem Veröffentlichungsdatum plus der Anzahl der für diese Einstellung konfigurierten Tage liegt.

    -   Klicken Sie in Configuration Manager vor Version 1602 auf **Vorschau**, um die Windows 10-Updates anzuzeigen, die dem Bereitschaftsstatus zugeordnet sind.  

    Weitere Informationen finden Sie unter [Servicing Branches](https://technet.microsoft.com/itpro/windows/manage/waas-overview#servicing-branches).
7.  Konfigurieren Sie ab Version 1602 von Configuration Manager auf der Seite „Upgrades“ die Suchkriterien zum Filtern der Upgrades, die dem Wartungsplan hinzugefügt werden. Nur Upgrades, die die angegebenen Kriterien erfüllen, werden der entsprechenden Bereitstellung hinzugefügt.  

     Klicken Sie auf **Vorschau** , um die Upgrades anzeigen, die die angegebenen Kriterien erfüllen.  

8.  Konfigurieren Sie auf der Seite Bereitstellungszeitplan die folgenden Einstellungen:  

    -   **Auswertung planen**: Geben Sie an, ob die verfügbare Zeit und die Installationsstichtage von Configuration Manager mit UTC oder der lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird, ausgewertet werden sollen.  

        > [!NOTE]  
        >  Wenn Sie die Ortszeit auswählen und dann **So bald wie möglich** für **Zeitpunkt der Verfügbarkeit der Software** oder **Installationsstichtag** auswählen, wird die aktuelle Uhrzeit auf dem Computer mit der Configuration Manager-Konsole verwendet, um zu bestimmen, wann Updates verfügbar sind, oder auf einem Client installiert werden. Wenn sich der Client in einer anderen Zeitzone befindet, erfolgen diese Aktionen, sobald die Evaluierungszeit des Clients erreicht ist.  

    -   **Zeitpunkt der Verfügbarkeit der Software**: Wählen Sie eine der folgenden Einstellungen aus, um anzugeben, wann die Softwareupdates den Clients zur Verfügung stehen:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung den Clientcomputern so bald wie möglich zur Verfügung gestellt werden. Wenn diese Einstellung beim Erstellen der Bereitstellung ausgewählt ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Die zur Installation verfügbaren Updates können dann abgerufen werden.  

        -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung den Clientcomputern zu einem bestimmten Termin (Datum und Uhrzeit) zur Verfügung gestellt werden. Wenn diese Einstellung beim Erstellen der Bereitstellung aktiviert ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Allerdings stehen die Softwareupdates in der Bereitstellung erst nach dem konfigurierten Termin (Datum und Uhrzeit) für die Installation zur Verfügung.  

    -   **Installationsstichtag**: Wählen Sie eine der folgenden Einstellungen aus, um den Installationsstichtag für die Softwareupdates in der Bereitstellung anzugeben:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung so bald wie möglich automatisch installiert werden.  

        -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung zu einem bestimmten Termin (Datum und Uhrzeit) automatisch installiert werden. Configuration Manager bestimmt den Stichtag zum Installieren von Softwareupdates durch Hinzufügen der konfigurierten Intervalle **Bestimmte Zeit** zu **Zeitpunkt der Verfügbarkeit der Software**.  

            > [!NOTE]  
            >  Der tatsächliche Installationsstichtag ergibt sich aus der Addition des angezeigten Stichtags und eines willkürlichen Zeitraums von bis zu 2 Stunden. Dadurch werden die potenziellen Auswirkungen reduziert, die mit der gleichzeitigen Installation der Updates in der Bereitstellung durch alle Clientcomputer in der Zielsammlung einhergehen.  
            >   
            >  Sie können die Clienteinstellung **Zufällige Stichtaganordnung deaktivieren** für **Computer-Agent** konfigurieren, um die zufällige Verzögerung der Installation für erforderliche Updates zu deaktivieren. Weitere Informationen finden Sie unter [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

9. Konfigurieren Sie auf der Seite Benutzerfreundlichkeit die folgenden Einstellungen:  

    -   **Benutzerbenachrichtigungen**: Geben Sie an, ob zum vorgegebenen **Zeitpunkt der Verfügbarkeit der Software** auf dem Clientcomputer eine Benachrichtigung zu den Updates im Softwarecenter angezeigt werden soll. Geben Sie auch an, ob Benutzerbenachrichtigungen auf den Clientcomputern angezeigt werden sollen.  

    -   **Verhalten am Stichtag**: Geben Sie das gewünschte Verhalten am Stichtag der Updatebereitstellung an. Geben Sie an, ob die Updates in der Bereitstellung installiert werden sollen. Geben Sie auch, ob nach einer Updateinstallation unabhängig von einem konfigurierten Wartungsfenster ein Systemneustart ausgeführt werden soll. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Verhalten beim Geräteneustart**: Geben Sie an, ob nach der Installation der Updates ein Systemneustart auf den Servern und Arbeitsstationen unterdrückt werden soll, wenn der Systemneustart zum Abschließen der Installation erforderlich ist.  

    -   **Schreibfilterverarbeitung für Windows Embedded-Geräte**: Beim Bereitstellen von Updates für Windows Embedded-Geräte mit aktiviertem Schreibfilter können Sie angeben, dass das Update auf dem temporären Overlay installiert wird und die Änderungen entweder später, am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden sollen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.  

        > [!NOTE]  
        >  Stellen Sie beim Bereitstellen eines Updates auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist.  

10. Wählen Sie auf der Seite Bereitstellungspaket ein vorhandenes Bereitstellungspaket aus, oder erstellen Sie anhand der nachfolgenden Einstellungen ein neues Bereitstellungspaket:  

    1.  **Name**: Geben Sie den Namen des Bereitstellungspakets an. Dies muss ein eindeutiger Name sein, der den Paketinhalt beschreibt. Er ist auf 50 Zeichen begrenzt.  

    2.  **Beschreibung**: Geben Sie eine Beschreibung mit Informationen zum Bereitstellungspaket an. Die Beschreibung ist auf 127 Zeichen begrenzt.  

    3.  **Paketquelle**: Gibt den Speicherort der Quelldateien der Softwareupdates an.  Geben Sie für den Quellspeicherort einen Netzwerkpfad wie **\\\Server\Freigabename\Pfad**ein. Alternativ können Sie auf **Durchsuchen** klicken, um den Netzwerkpfad zu suchen. Sie müssen den freigegebenen Ordner für die Quelldateien des Bereitstellungspakets erstellen, bevor Sie mit der nächsten Seite fortfahren.  

        > [!NOTE]  
        >  Der von Ihnen angegebene Quellspeicherort des Bereitstellungspakets kann von keinem anderen Softwarebereitstellungspaket verwendet werden.  

        > [!IMPORTANT]  
        >  Das Computerkonto für den SMS-Anbieter und der Benutzer, der den Assistenten zum Herunterladen der Softwareupdates ausführt, müssen über die NTFS-Berechtigung **Schreiben** für den Downloadort verfügen. Sie müssen den Zugriff auf den Downloadort beschränken, um das Risiko zu verringern, dass Angreifer die Quelldateien der Softwareupdates manipulieren.  

        > [!IMPORTANT]  
        >  Sie können den Paketquellspeicherort in den Eigenschaften des Bereitstellungspakets ändern, nachdem das Bereitstellungspaket von Configuration Manager erstellt wurde. In diesem Fall müssen Sie jedoch zuerst den Inhalt von der ursprünglichen Paketquelle an den neuen Paketquellspeicherort kopieren.  

    4.  **Sendepriorität**: Geben Sie die Sendepriorität für das Bereitstellungspaket an. Configuration Manager verwendet Sendepriorität für das Bereitstellungspaket beim Senden des Pakets an Verteilungspunkte. Bereitstellungspakete werden in der Reihenfolge ihrer Priorität gesendet: „Hoch“, „Mittel“ oder „Niedrig“. Pakete mit identischer Priorität werden in der Reihenfolge ihrer Erstellung gesendet. Wenn es keinen Rückstand gibt, wird das Paket unabhängig von seiner Priorität sofort verarbeitet.  

11. Geben Sie auf der Seite „Verteilungspunkte“ die Verteilungspunkte oder Verteilungspunktgruppen an, auf denen die Updatedateien gehostet werden sollen. Weitere Informationen zu Verteilungspunkten finden Sie unter [Konfigurieren eines Verteilungspunkts](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs).

    > [!NOTE]  
    >  Diese Seite ist nur verfügbar, wenn Sie ein neues Softwareupdate-Bereitstellungspaket erstellen.  

12. Geben Sie auf der Seite „Downloadpfad“ an, ob die Updatedateien vom Internet oder aus dem lokalen Netzwerk heruntergeladen werden sollen. Konfigurieren Sie die folgenden Einstellungen:  

    -   **Softwareupdates aus dem Internet herunterladen**: Wählen Sie diese Einstellung aus, um die Updates von einem bestimmten Speicherort im Internet herunterzuladen. Diese Einstellung ist standardmäßig aktiviert.  

    -   **Softwareupdates von einem Pfad im lokalen Netzwerk herunterladen**: Wählen Sie diese Einstellung aus, um die Updates aus einem lokalen Verzeichnis oder aus einem freigegebenen Ordner herunterzuladen. Diese Einstellung ist nützlich, wenn der Computer, auf dem der Assistent ausgeführt wird, keine Internetverbindung aufweist. Die Updates können von jedem Computer mit Internetzugriff vorläufig heruntergeladen und im lokalen Netzwerk an einem Speicherort abgelegt werden, der von dem Computer aus zugänglich ist, auf dem der Assistent ausgeführt wird.  

13. Wählen Sie auf der Seite „Sprachauswahl“ die Sprachen aus, für die die ausgewählten Updates heruntergeladen werden. Die Updates werden nur dann heruntergeladen, wenn sie in den ausgewählten Sprachen verfügbar sind. Updates, die nicht sprachspezifisch sind, werden immer heruntergeladen. Standardmäßig werden vom Assistenten die Sprachen ausgewählt, die Sie in den Eigenschaften des Softwareupdatepunkts konfiguriert haben. Es muss mindestens eine Sprache ausgewählt werden, bevor die nächste Seite angezeigt werden kann. Wenn Sie nur Sprachen auswählen, die von einem Update nicht unterstützt werden, kann das Update nicht heruntergeladen werden.  

14. Überprüfen Sie auf der Seite „Zusammenfassung“ die Einstellungen, und klicken Sie auf **Weiter** , um den Wartungsplan zu erstellen.  

 Nachdem Sie den Assistenten abgeschlossen haben, wird der Wartungs plan ausgeführt. Dabei werden die Updates, die die angegebenen Kriterien erfüllen, einer Softwareupdategruppe hinzugefügt. Dann werden die Updates in die Inhaltsbibliothek auf dem Standortserver heruntergeladen und an die konfigurierten Verteilungspunkte verteilt. Die Softwareupdategruppe wird schließlich den Clients in der Zielsammlung bereitgestellt.  

##  <a name="BKMK_ModifyServicingPlan"></a> Ändern eines Wartungsplans  
Nachdem Sie einen grundlegenden Wartungsplan über das Windows 10-Wartungsdashboard erstellt haben, oder wenn Sie die Einstellungen für einen vorhandenen Wartungsplan ändern müssen, können Sie zu den Eigenschaften für den Wartungsplan navigieren.

> [!NOTE]
> Sie können die Einstellungen in den Eigenschaften für den Wartungsplan konfigurieren, die bei der Erstellung des Wartungsplans im Assistenten nicht verfügbar sind. Im Assistenten werden für Downloadeinstellungen, Bereitstellungseinstellungen und Warnungen jeweils die Standardeinstellungen verwendet.  

Wenden Sie das folgende Verfahren an, um die Eigenschaften eines Wartungsplans zu ändern.  

#### <a name="to-modify-the-properties-of-a-servicing-plan"></a>So ändern Sie die Eigenschaften eines Wartungsplans  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie **Windows 10-Wartung**in der Softwarebibliothek, klicken Sie auf **Wartungspläne**, und wählen Sie dann den Wartungsplan aus, den Sie ändern möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** auf **Eigenschaften** , um Eigenschaften für den ausgewählten Wartungsplan zu öffnen.

    In den Eigenschaften für den Wartungsplan sind folgende Einstellungen verfügbar, die im Assistenten nicht konfiguriert wurden:

    **Bereitstellungseinstellungen**: Konfigurieren Sie auf der Registerkarte „Bereitstellungseinstellungen“ die folgenden Einstellungen:  

    -   **Bereitstellungstyp**: Geben Sie für die Softwareupdatebereitstellung den Bereitstellungstyp an. Wählen Sie **Erforderlich** aus, um eine obligatorische Softwareupdatebereitstellung zu erstellen, bei der Softwareupdates automatisch bis zu einem vorgegebenen Installationsstichtag auf Clients installiert werden. Wählen Sie **Verfügbar** aus, um eine optionale Softwareupdatebereitstellung zu erstellen, die im Softwarecenter zur Verfügung gestellt wird und von Benutzern installiert werden kann.  

        > [!IMPORTANT]  
        >  Nachdem Sie die Softwareupdatebereitstellung einmal erstellt haben, können Sie den Bereitstellungstyp nicht mehr ändern.  

        > [!NOTE]  
        >  Eine als **Erforderlich** bereitgestellte Softwareupdategruppe wird im Hintergrund heruntergeladen und berücksichtigt BITS-Einstellungen (sofern konfiguriert).  
        > Als **Verfügbar** bereitgestellte Softwareupdategruppen werden jedoch im Vordergrund heruntergeladen und ignorieren BITS-Einstellungen.  

    -   **Wake-on-LAN verwenden, um Clients für erforderliche Bereitstellungen zu aktivieren**: Geben Sie an, ob Wake-On-LAN am Stichtag aktiviert werden soll, damit Aktivierungspakete an Computer gesendet werden, für die mindestens eines der in der Bereitstellung enthaltenen Softwareupdates erforderlich ist. Alle Computer, die sich am Installationsstichtag im Energiesparmodus befinden, werden aktiviert, damit die Softwareupdateinstallation initiiert werden kann. Clients, die sich im Energiesparmodus befinden und für die keine der in der Bereitstellung enthaltenen Softwareupdates erforderlich sind, werden nicht gestartet. Diese Einstellung ist standardmäßig deaktiviert und nur verfügbar, wenn unter **Bereitstellungstyp** die Einstellung **Erforderlich**ausgewählt wurde.  

        > [!WARNING]  
        >  Sie können diese Option nur verwenden, wenn Computer und Netzwerke für Wake-On-LAN konfiguriert sind.  

    -   **Detailstufe**: Geben Sie die Detailstufe für die von den Clientcomputern zurückgegebenen Zustandsmeldungen an.  

    **Downloadeinstellungen**: Konfigurieren Sie auf der Registerkarte „Downloadeinstellungen“ die folgenden Einstellungen:  

    - Geben Sie an, ob die Softwareupdates vom Client heruntergeladen und installiert werden, wenn ein Client mit einer langsamen Netzwerkverbindung oder einer Fallbackinhaltsquelle vorliegt.  

    - Geben Sie an, ob die Softwareupdates vom Client von einem Fallbackverteilungspunkt heruntergeladen und installiert werden sollen, wenn der Inhalt für die Softwareupdates an einem bevorzugten Verteilungspunkt nicht verfügbar ist.  

    -   **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Geben Sie an, ob BranchCache beim Herunterladen von Inhalten verwendet werden soll. Weitere Informationen zu BranchCache finden Sie unter [Grundlegende Konzepte für die Inhaltsverwaltung](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Geben Sie an, ob von Clients Softwareupdates von Microsoft Update heruntergeladen werden sollen, wenn keine Softwareupdates an Verteilungspunkten verfügbar sind.
        > [!IMPORTANT]
        > Verwenden Sie diese Einstellung nicht für Windows 10-Wartungsupdates. Configuration Manager kann (zumindest bis Version 1610) keine Windows 10-Wartungsupdates von Microsoft Update herunterladen.

    -   Geben Sie an, ob es Clients mit einer getakteten Internetverbindung möglich sein soll, Inhalt nach dem Installationsstichtag herunterzuladen. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.   

    **Warnungen**: Geben Sie auf der Seite „Warnungen“ an, wie Configuration Manager und System Center Operations Manager Warnungen für diese Bereitstellung generieren sollen. Warnungen können nur konfiguriert werden, wenn auf der Seite „Bereitstellungseinstellungen“ unter **Bereitstellungstyp** die Option **Erforderlich** ausgewählt wurde.  

    > [!NOTE]  
    >  Sie können die letzten Warnungen zu Softwareupdates im Arbeitsbereich **Softwarebibliothek** im Knoten **Softwareupdates** prüfen.  
