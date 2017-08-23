---
title: "Beispielszenario – Bereitstellen von Windows Embedded-Clients | Microsoft-Dokumentation"
description: "Stellt ein Beispielszenario für die Bereitstellung und Verwaltung von System Center Configuration Manager-Clients auf Windows Embedded-Geräten dar."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: c535bc62497b5ff0b60ca266c28630d890af3604
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="example-scenario-for-deploying-and-managing-system-center-configuration-manager-clients-on-windows-embedded-devices"></a>Beispielszenario für die Bereitstellung und Verwaltung von System Center Configuration Manager-Clients auf Windows Embedded-Geräten

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Szenario wird gezeigt, wie Sie mithilfe von Configuration Manager Windows Embedded-Geräte mit aktivierten Schreibfiltern verwalten können. Wenn Ihre eingebetteten Geräte keine Schreibfilter unterstützen, entspricht ihr Verhalten dem Verhalten von Configuration Manager-Standardclients, und diese Verfahren werden nicht übernommen.  

Coho Vineyard & Winery eröffnet demnächst ein Besucherzentrum und benötigt Kioske, auf denen Windows Embedded-Geräte ausgeführt werden, um interaktive Präsentationen auszuführen. Das Gebäude, in dem das neue Besucherzentrum untergebracht ist, liegt nicht in unmittelbarer Nähe der IT-Abteilung. Es ist daher wichtig, dass die Kioske remote verwaltet werden können. Zusätzlich von der Software zur Ausführung der Präsentationen muss auf den Geräten den Sicherheitsrichtlinien des Unternehmens entsprechend eine aktuelle Antischadsoftware ausgeführt werden. Die Kioske müssen während der Öffnungszeiten des Besucherzentrums sieben Tage die Woche ohne Ausfallzeiten geöffnet haben.  

 Coho führt Configuration Manager bereits zur Verwaltung von Geräten in ihrem Netzwerk aus. Configuration Manager wird so konfiguriert, dass Endpoint Protection ausgeführt wird und Softwareupdates und Anwendungen installiert werden. Allerdings hat das IT-Team keinerlei Erfahrungen mit der Verwaltung von Windows Embedded-Geräten. Jane, die für Configuration Manager zuständige Administratorin, führt daher einen Pilotversuch mit zwei zu verwaltenden Kiosken im Eingangsbereich durch.   

 Zur Verwaltung dieser Windows Embedded-Geräte mit aktivierten Schreibfiltern führt Jane die nachstehenden Schritte aus, um den Configuration Manager-Client zu installieren, den Schutz des Clients mithilfe von Endpoint Protection zu gewährleisten und die Software für interaktive Präsentationen zu installieren.  

1.  Jane informiert sich darüber, wie Schreibfilter von Windows Embedded-Geräten eingesetzt werden, und wie dieser Vorgang mithilfe von Configuration Manager erleichtert werden kann, indem die Schreibfilter automatisch deaktiviert und erneut aktiviert werden, um eine Softwareinstallation beizubehalten.  

     Weitere Informationen finden Sie unter [Planen der Clientbereitstellung auf Windows Embedded-Geräten in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2.  Jane erstellt zunächst eine neue abfragebasierte Gerätesammlung für die Windows Embedded-Geräte, bevor sie den Configuration Manager-Client installiert. Da für die Computer des Unternehmens ein Standardbenennungsformat verwendet wird, kann Andrea die Windows Embedded-Geräte anhand der ersten sechs Buchstaben des jeweiligen Computernamens eindeutig identifizieren: **WEMDVC** Anhand der folgenden WQL-Abfrage erstellt sie diese Sammlung: **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

     Mithilfe dieser Sammlung kann sie die Windows Embedded-Geräte mit anderen Konfigurationsoptionen als die anderen Geräte verwalten. Mit dieser Sammlung kann sie Neustarts steuern, Endpoint Protection mit Clienteinstellungen bereitstellen und die Anwendung für interaktive Präsentationen bereitstellen.  

     Siehe [Erstellen von Sammlungen in System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

3.  Andrea konfiguriert die Sammlung für ein Wartungsfenster, um sicherzustellen, dass keine der Neustarts, die möglicherweise bei der Installation der Präsentationsanwendung und von Upgrades erforderlich sind, während der Öffnungszeiten des Besucherzentrums ausgeführt werden. Die Öffnungszeiten sind täglich von 09:00 bis 18:00 Uhr. Sie konfiguriert das Wartungsfenster für 18:30 bis 06:00 Uhr täglich.  

4.  Weitere Informationen finden Sie unter [Verwenden von Wartungsfenstern in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5.  Anschließend konfiguriert Andrea eine benutzerdefinierte Geräteclienteinstellung zur Installation des Endpoint Protection-Clients. Dazu wählt sie für die nachfolgenden Einstellungen **Ja** aus und stellt dann diese Clienteinstellung der Windows Embedded-Gerätesammlung bereit:  

    -   **Installieren des Endpoint Protection-Clients auf Clientcomputern**  

    -   **Für Windows Embedded-Geräte mit Schreibfiltern Commit für Endpoint Protection-Clientinstallation ausführen (hierdurch werden Neustarts erforderlich)**  

    -   **Endpoint Protection-Clientinstallation und Neustarts außerhalb der Wartungsfenster zulassen**  

     Wenn der Configuration Manager-Client installiert ist, wird mit diesen Einstellungen der Endpoint Protection-Client installiert und sichergestellt, dass er nicht lediglich in die Überlagerung geschrieben, sondern im Betriebssystem als Teil der Installation beibehalten wird. Den Sicherheitsrichtlinien des Unternehmens entsprechend muss die Antischadsoftware stets installiert sein. Andrea möchte zudem nicht das Risiko eingehen, die Kioske bei einem Neustart auch nur für kurze Zeit ungeschützt zu lassen.  

    > [!NOTE]  
    >  Die bei der Installation des Endpoint Protection-Clients erforderlichen Neustarts finden lediglich während der Setupphase für die Geräte statt und bevor das Besucherzentrum eröffnet wird. Im Gegensatz zur periodischen Bereitstellung von Anwendungen oder Softwaredefinitionsupdates wird der Endpoint Protection-Client wahrscheinlich erst wieder auf dem gleichen Gerät installiert, wenn das Unternehmen das Upgrade auf die nächste Version von Configuration Manager durchführt.  

     Weitere Informationen finden Sie unter [Konfigurieren von Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md).  

6.  Da die Konfigurationseinstellungen für den Client nun festliegen, bereitet Jane die Installation der Configuration Manager-Clients vor. Sie muss den Schreibfilter auf den Windows Embedded-Geräten manuell deaktivieren, bevor sie die Clients installieren kann. Sie liest die den Kiosken beiliegende OEM-Dokumentation und befolgt die dort beschriebenen Anweisungen zur Deaktivierung der Schreibfilter.  

     Andrea benennt das Gerät so um, dass es dem im Unternehmen geltenden Standardbenennungsformat entspricht. Dann installiert sie den Client manuell. Dazu führt sie CCMSetup mit folgendem Befehl von einem zugeordneten Laufwerk aus, auf dem sich die Clientquelldateien befinden: **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

     Mit diesem Befehl wird der Client installiert und dem Verwaltungspunkt mit dem Intranet-FQDN **mpserver.cohovineyardandwinery.com**sowie dem primären Standort **CO1**zugewiesen.  

     Andrea weiß, dass es immer eine Weile dauert, bis die Installation von Clients abgeschlossen ist und der Clientstatus an den entsprechenden Standort gesendet wird. Darum prüft sie erst nach einer gewissen Wartezeit, ob die Clients installiert und dem Standort zugewiesen wurden und ob sie in der Sammlung, die sie für die Windows Embedded-Geräte erstellt hat, als Clients erscheinen.  

     Zusätzlich prüft sie Eigenschaften von Configuration Manager in der Systemteuerung der Geräte und vergleicht diese mit Windows-Standardcomputern, die vom Standort verwaltet werden. Beispielsweise wird auf der Registerkarte **Komponenten** unter **Hardwareinventur-Agent** die Einstellung **Aktiviert**angezeigt. Auf der Registerkarte **Aktionen** sind 11 Aktionen verfügbar, darunter **Evaluationszyklus für die Anwendungsbereitstellung** und **Ermittlungsdaten-Sammlungszyklus**.  

     Andrea ist sich nun sicher, dass die Clients erfolgreich installiert und zugewiesen wurden und dass bei ihnen Clientrichtlinien vom Verwaltungspunkt eingehen. Als Nächstes aktiviert sie die Schreibfilter anhand der OEM-Anweisungen manuell.  

     Weitere Informationen finden Sie in folgenden Quellen:  

    -   [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

    -   [Zuweisen von Clients zu einem Standort in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7.  Der Configuration Manager-Client ist jetzt auf den Windows Embedded-Geräten installiert. Jane vergewissert sich nun, dass sie die Geräte genau wie Windows-Standardclients verwalten kann. Beispielsweise ist es ihr möglich, die Geräte über die Configuration Manager-Konsole mithilfe der Remotesteuerung remote zu verwalten, Clientrichtlinien für sie zu starten sowie Clienteigenschaften und eine Hardwareinventur anzuzeigen.  

     Da diese Geräte einer Active Directory-Domäne hinzugefügt werden, muss sie sie nicht manuell als vertrauenswürdige Clients genehmigen, und bestätigt über die Configuration Manager-Konsole, dass die Geräte genehmigt sind.  

     Weitere Informationen finden Sie unter [How to manage clients in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

8.  Andrea führt den **Assistenten zum Bereitstellen von Software** aus und konfiguriert eine erforderliche Anwendung, um die Software für interaktive Präsentationen zu installieren. Auf der Seite **Benutzerfreundlichkeit** des Assistenten akzeptiert sie im Bereich **Schreibfilterverarbeitung für Windows Embedded-Geräte** die Standardoption **Änderungen zum Stichtag oder während eines Wartungsfensters ausführen (erfordert Neustart)**.  

     Andrea behält diese Standardoption für Schreibfilter bei, um sicherzustellen, dass die Anwendung nach einem Neustart beibehalten wird und somit den Besuchern, die die Kioske benutzen, stets zur Verfügung steht. Mit dem täglichen Wartungsfenster wird ein sicherer Zeitraum bereitgestellt, in dem die bei Installationen und Updates erforderlichen Neustarts stattfinden können.  

     Andrea stellt die Anwendung der Windows Embedded-Gerätesammlung bereit.  

     Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen mit System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. Andrea verwendet Softwareupdates und führt den Assistenten zum Erstellen automatischer Bereitstellungsregeln aus, um Definitionsupdates für Endpoint Protection zu konfigurieren. Sie wählt die Vorlage **Definitionsupdates** aus, um den Assistenten mit Einstellungen aufzufüllen, die für Endpoint Protection geeignet sind.  

     Dazu gehören die folgenden Einstellungen auf der Seite **Benutzerfreundlichkeit** des Assistenten:  

    -   **Verhalten am Stichtag**: Das Kontrollkästchen **Softwareinstallation** ist nicht aktiviert.  

    -   **Schreibfilterverarbeitung für Windows Embedded-Geräte**: Das Kontrollkästchen **Änderungen zum Stichtag oder während eines Wartungsfensters ausführen (erfordert Neustart)** ist nicht aktiviert.  

     Andrea behält diese Standardeinstellungen bei. Wenn diese beiden Optionen diese Konfiguration aufweisen, können alle Softwaredefinitionsupdates für Endpoint Protection tagsüber im Overlay installiert werden. Es ist nicht notwendig, mit Installation und Commit bis zum Wartungsfenster zu warten. Mit dieser Konfiguration wird die Sicherheitsrichtlinie des Unternehmens, laut der auf Computern aktuelle Antischadsoftware ausgeführt werden muss, am besten erfüllt.  

    > [!NOTE]  
    >  Anders als Softwareinstallationen für Anwendungen können Softwaredefinitionsupdates für Endpoint Protection sehr häufig und sogar mehrmals täglich auftreten. Dabei handelt es sich oft um kleine Dateien. Für diese Arten sicherheitsbezogener Bereitstellungen ist es oft von Vorteil, immer im Overlay zu installieren, anstatt bis zum Wartungsfenster zu warten. Die Softwaredefinitionsupdates werden bei einem Geräteneustart schnell vom Configuration Manager-Client erneut installiert, da mit dieser Aktion eine Auswertungsüberprüfung gestartet und nicht auf die nächste geplante Auswertung gewartet wird.  

     Andrea wählt die Windows Embedded-Gerätesammlung für die automatische Bereitstellungsregel aus.  

     Weitere Informationen finden Sie unter  
                  Schritt 3: Konfigurieren von Configuration Manager-Softwareupdates zum Bereitstellen von Definitionsupdates für Clientcomputer unter [Konfigurieren von Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md)  

10. Andrea entscheidet sich dazu, einen Wartungstask zu konfigurieren, von dem für alle Änderungen im Overlay regelmäßig ein Commit ausgeführt wird. Mit diesem Task soll nicht nur die Bereitstellung von Softwaredefinitionsupdates unterstützt, sondern auch die Anzahl der Updates reduziert werden, die sich ansammeln und bei jedem Geräteneustart erneut installiert werden müssen. Nach ihrer Erfahrung trägt dies zu einer effizienteren Ausführung der Antischadsoftware bei.  

    > [!NOTE]  
    >  Für diese Softwaredefinitionsupdates würde automatisch ein Commit auf das Abbild ausgeführt, falls auf den eingebetteten Geräten ein anderer Verwaltungstask ausgeführt wird, von dem die Ausführung eines Commits für Änderungen unterstützt wird. Beispielsweise würde bei der Installation einer neuen Version der Software für interaktive Präsentationen auch ein Commit für die Änderungen an Softwaredefinitionsupdates ausgeführt. Ein Commit für die Änderungen an Softwaredefinitionsupdates könnte auch bei der monatlichen, während des Wartungsfensters stattfindenden Installation von Standardsoftwareupdates ausgeführt werden. In diesem Szenario jedoch werden keine Standardsoftwareupdates ausgeführt, und Updates für die Software für interaktive Präsentationen dürften eher selten vorkommen. Es könnte daher einige Monate dauern, bis für die Softwaredefinitionsupdates ein automatischer Commit auf das Abbild ausgeführt wird.  

     Andrea erstellt zuerst eine benutzerdefinierte Tasksequenz, die außer dem Namen keinerlei Einstellungen aufweist. Sie führt den Tasksequenzerstellungs-Assistenten aus:  

    1.  Auf der Seite **Neue Tasksequenz erstellen** wählt sie die Option **Neue benutzerdefinierte Tasksequenz erstellen**aus und klickt dann auf **Weiter**.  

    2.  Auf der Seite **Informationen zur Tasksequenz** gibt sie den Tasksequenznamen **Maintenance task to commit changes on embedded devices** ein und klickt dann auf **Weiter**.  

    3.  Auf der Seite **Zusammenfassung** klickt sie auf **Weiter**und schließt den Assistenten ab.  

     Dann stellt Andrea diese benutzerdefinierte Tasksequenz der Windows Embedded-Gerätesammlung bereit und legt im Zeitplan fest, dass die Tasksequenz jeden Monat ausgeführt werden soll. Im Rahmen der Bereitstellungseinstellungen aktiviert sie das Kontrollkästchen **Änderungen zum Stichtag oder während eines Wartungsfensters ausführen (erfordert Neustart)** , damit die Änderungen nach einem Neustart beibehalten werden. Zum Konfigurieren dieser Bereitstellung wählt sie die von ihr erstellte benutzerdefinierte Tasksequenz aus. Dann klickt sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen** , um den Assistenten zum Bereitstellen von Software zu starten:  

    1.  Auf der Seite **Allgemein** wählt sie die Windows Embedded-Gerätesammlung aus und klickt dann auf **Weiter**.  

    2.  Auf der Seite **Bereitstellungseinstellungen** wählt sie für **Erforderlich** den **Zweck**aus und klickt dann auf **Weiter**.  

    3.  Auf der Seite **Zeitplanung** klickt sie auf **Neu** , um einen wöchentlichen Zeitplan während des Wartungsfensters anzugeben, und klickt dann auf **Weiter**.  

    4.  Sie schließt den Assistenten ohne weitere Änderungen ab.  

     Weitere Informationen finden Sie unter  
                  [Verwalten von Tasksequenzen zum Automatisieren von Tasks in System Center Configuration Manager](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. Die Kioske sollen automatisch ausgeführt werden. Andrea schreibt daher ein Skript, um die Geräte für die folgenden Einstellungen zu konfigurieren:  

    -   Verwenden der automatischen Anmeldung mithilfe eines Gastkontos ohne Kennwort  

    -   Automatisches Ausführen der Software für interaktive Präsentationen beim Start  

     Andrea verwendet Pakete und Programme, um dieses Skript für die Windows Embedded-Gerätesammlung bereitzustellen. Beim Ausführen des Assistenten zum Bereitstellen von Software aktiviert sie das Kontrollkästchen **Änderungen zum Stichtag oder während eines Wartungsfensters ausführen (erfordert Neustart)** wieder, damit die Änderungen nach einem Neustart beibehalten werden.  

     Weitere Informationen finden Sie unter [Pakete und Programme in System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

12. Am nächsten Morgen überprüft Andrea die Windows Embedded-Geräte. Sie stellt Folgendes sicher:  

    -   Der Kiosk wurde mithilfe des Gastkontos automatisch angemeldet.  

    -   Die Software für interaktive Präsentationen wird ausgeführt.  

    -   Der Endpoint Protection-Client wurde installiert und verfügt über die aktuellen Softwaredefinitionsupdates.  

    -   Das Gerät wurde während des Wartungsfensters neu gestartet.  

     Weitere Informationen finden Sie in folgenden Quellen:  

    -   [Überwachen von Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    -   [Überwachen von Anwendungen mit System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

13. Andrea überwacht die Kioske und meldet deren erfolgreiche Verwaltung ihrem Manager. Das Ergebnis ist, dass 20 Kioske für das Besucherzentrum bestellt werden.  

     Zum Vermeiden der manuellen Installation des Configuration Manager-Clients, das manuelles Deaktivieren und Aktivieren der Schreibfilter erfordert, stellt Jane sicher, dass die Bestellung ein benutzerdefiniertes Image mit den Installationsdaten und der Standortzuweisung des Configuration Manager-Clients enthält. Darüber hinaus werden die Geräte gemäß dem Benennungsformat des Unternehmens benannt.  

     Die Kioske werden eine Woche vor der Eröffnung an das Besucherzentrum geliefert. Während dieses Zeitraums sind die Kioske mit dem Netzwerk verbunden, und die gesamte Geräteverwaltung erfolgt automatisch, sodass kein lokaler Administrator erforderlich ist. Andrea vergewissert sich, dass die Kioske wie gewünscht funktionieren:  

    -   Von den Clients auf den Kiosken wird die Standortzuweisung durchgeführt, und die vertrauenswürdigen Stammschlüssel werden aus den Active Directory-Domänendiensten heruntergeladen.  

    -   Die Clients auf den Kiosken werden automatisch der Windows Embedded-Gerätesammlung hinzugefügt und per Wartungsfenster konfiguriert.  

    -   Der Endpoint Protection-Client wurde installiert und verfügt über die aktuellen Softwaredefinitionsupdates für den Antischadsoftware-Schutz.  

    -   Die Software für interaktive Präsentationen wurde installiert, wird automatisch ausgeführt und ist für Besucher bereit.  

14. Nach diesem ersten Setup werden Neustarts, die für Updates ggf. erforderlich sind, nur bei geschlossenem Besucherzentrum ausgeführt.  
