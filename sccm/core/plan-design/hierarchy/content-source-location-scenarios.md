---
title: "Quellspeicherort für Inhalt | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über die System Center Configuration Manager-Einstellungen, mit denen Clients Inhalte in einem langsamen Netzwerk finden können."
ms.custom: na
ms.date: 1/3/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a823458dc3b891b1c32d1cb44a96e8cafd376ed5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="content-source-location-scenarios-in-system-center-configuration-manager"></a>Szenarios für Quellspeicherorte für Inhalt in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager unterstützt vor Version 1610 mehrere Einstellungen, die festlegen, wie und wo Clients Inhalte finden, wenn sie sich in einem langsamen Netzwerk befinden. Die möglichen Kombinationen wirken sich auf die Inhaltsspeicherort-Clients und darauf aus, ob sie erfolgreich einen Fallbackpfad verwenden können, wenn eine bevorzugte Quelle für Inhalte nicht verfügbar ist.  

> [!IMPORTANT]  
> **Wenn an Ihren Standorten die Versionen 1511, 1602 oder 1606 laufen**, gelten die Informationen in diesem Thema für Ihre Infrastruktur. Siehe auch [Begrenzungsgruppen für die System Center Configuration Manager-Versionen 1511, 1602 und 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) für Informationen, die für Begrenzungsgruppen mit diesen Versionen von Configuration Manager spezifisch sind.
>
> **Wenn an Ihren Standorten die Version 1610 oder höher läuft**, verwenden Sie die Informationen in [Definieren von Standortgrenzen und Begrenzungsgruppen für Configuration Manager](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups), um zu verstehen, wie Ihre Clients Verteilungspunkte finden, die verfügbare Inhalte haben.





**Die folgenden drei Einstellungen definieren das Verhalten, wenn Clients Inhalte anfordern:**

-  **Fallbackquellpfad für Inhalt zulassen** (aktiviert oder deaktiviert): Diese Option können Sie auf der Registerkarte **Begrenzungsgruppen** eines Verteilungspunkts aktivieren. Dadurch kann der Client einen als Fallbackpfad konfigurierten Verteilungspunkt nutzen, wenn der Inhalt auf einem bevorzugten Verteilungspunkt nicht verfügbar ist.  

 - **Bereitstellungsverhalten für die Netzwerkverbindungsgeschwindigkeit**: Bei jeder Bereitstellung wird für den Fall von langsamen Verbindungen zum Verteilungspunkt eine der folgenden Verhaltensweisen konfiguriert:  

    -   **Inhalt vom Verteilungspunkt herunterladen und lokal ausführen**  

    -   **Inhalt nicht herunterladen**: Diese Option wird nur verwendet, wenn ein Client einen Fallbackpfad verwendet, um Inhalt abzurufen.  

    Die Verbindungsgeschwindigkeit für einen Verteilungspunkt wird auf der Registerkarte **Referenzen** der Begrenzungsgruppe konfiguriert und gilt nur für diese Begrenzungsgruppe.  

 -  **On-demand package distribution (Paketverteilung auf Anfrage)** (an bevorzugte Verteilungspunkte): Dieses Verhalten wird aktiviert, wenn Sie auf der Registerkarte **Verteilungseinstellungen** eines Pakets oder in den Anwendungseigenschaften die Option **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen** auswählen. Das Aktivieren dieser Option veranlasst Configuration Manager, nach einer auf einem Verteilungspunkt eingehenden Inhaltsanforderung durch einen Client den betreffenden Inhalt automatisch auf einen bevorzugten Verteilungspunkt zu kopieren, der den Inhalt noch nicht enthält.  


 **Die folgenden Anforderungen gelten für alle Szenarios:**


-   Der Inhalt ist an einem Fallbackverteilungspunkt verfügbar.  

-   Die Verteilungspunkte sind online und zugänglich.  


## <a name="scenario-1"></a>Szenario 1  
 Gilt, wenn folgende Konfigurationseinstellungen vorhanden sind:  

-   **Der Inhalt ist an einem bevorzugten Verteilungspunkt verfügbar.**  

-   **Fallback zulassen**: nicht aktiviert  

-   **Bereitstellungsverhalten für langsame Netzwerke**: beliebige Konfiguration  


**Details:** (Die Konfiguration für die bedarfsgesteuerte Paketverteilung ist in diesem Szenario nicht relevant.)  

1.  Vom Client wird eine Inhaltsanforderung an den Verwaltungspunkt gesendet.  

2.  Vom Verwaltungspunkt wird eine Inhaltsortliste mit bevorzugten Verteilungspunkten, an denen der Inhalt verfügbar ist, an den Client zurückgegeben.  

3.  Der Inhalt wird von einem der bevorzugten Verteilungspunkte auf der Liste heruntergeladen.  

## <a name="scenario-2"></a>Szenario 2  
 Folgende Konfigurationseinstellungen sind vorhanden:  

-   **Der Inhalt ist an einem bevorzugten Verteilungspunkt verfügbar.**  

-   **Fallback zulassen**: aktiviert  

-   **Bereitstellungsverhalten für langsame Netzwerke**: Inhalt nicht herunterladen  


**Details:** (Die Konfiguration für die bedarfsgesteuerte Paketverteilung ist in diesem Szenario nicht relevant.)  

1.  Vom Client wird eine Inhaltsanforderung an den Verwaltungspunkt gesendet. Vom Client wird in die Anforderung ein Kennzeichen mit der Information eingeschlossen, dass Fallbackverteilungspunkte zulässig sind.  

2.  Vom Verwaltungspunkt wird eine Inhaltsortliste mit bevorzugten Verteilungspunkten sowie Fallbackverteilungspunkten, an denen der Inhalt verfügbar ist, an den Client zurückgegeben.  

3.  Der Inhalt wird von einem der bevorzugten Verteilungspunkte auf der Liste heruntergeladen.  

## <a name="scenario-3"></a>Szenario 3  
 Folgende Konfigurationseinstellungen sind vorhanden:  

-   **Der Inhalt ist an einem bevorzugten Verteilungspunkt verfügbar.**  

-   **Fallback zulassen**: aktiviert  

-   **Bereitstellungsverhalten für langsame Netzwerke**: Inhalt herunterladen und installieren  


**Details:** (Die Konfiguration für die bedarfsgesteuerte Paketverteilung ist in diesem Szenario nicht relevant.)  

1.  Vom Client wird eine Inhaltsanforderung an den Verwaltungspunkt gesendet. Vom Client wird in die Anforderung ein Kennzeichen mit der Information eingeschlossen, dass Fallbackverteilungspunkte zulässig sind.  

2.  Vom Verwaltungspunkt wird eine Inhaltsortliste mit bevorzugten Verteilungspunkten sowie Fallbackverteilungspunkten, an denen der Inhalt verfügbar ist, an den Client zurückgegeben.  

3.  Der Inhalt wird von einem der bevorzugten Verteilungspunkte auf der Liste heruntergeladen.  

## <a name="scenario-4"></a>Szenario 4  
 Folgende Konfigurationseinstellungen sind vorhanden:  

-   **Der Inhalt ist an keinem bevorzugten Verteilungspunkt verfügbar.**  

-   **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen** ist nicht aktiviert.  

-   **Fallback zulassen**: nicht aktiviert  

-   **Bereitstellungsverhalten für langsame Netzwerke**: beliebige Konfiguration  


**Details:**  

1.  Vom Client wird eine Inhaltsanforderung an den Verwaltungspunkt gesendet.  

2.  Vom Verwaltungspunkt wird eine Inhaltsortliste mit bevorzugten Verteilungspunkten, an denen der Inhalt verfügbar ist, an den Client zurückgegeben. Die Liste enthält keine bevorzugten Verteilungspunkte.  

3.  Es tritt ein Clientfehler auf, die Fehlermeldung **Inhalt ist nicht verfügbar** wird angezeigt, und vom Client wird in den Wiederholungsmodus gewechselt. Jede Stunde wird eine neue Inhaltsanforderung gesendet.  

## <a name="scenario-5"></a>Szenario 5  
 Folgende Konfigurationseinstellungen sind vorhanden:  

-   **Der Inhalt ist an keinem bevorzugten Verteilungspunkt verfügbar.**  

-   **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen** ist nicht aktiviert.  

-   **Fallback zulassen**: aktiviert  

-   **Bereitstellungsverhalten für langsame Netzwerke**: Inhalt nicht herunterladen  


**Details:**  

1.  Vom Client wird eine Inhaltsanforderung an den Verwaltungspunkt gesendet. Vom Client wird in die Anforderung ein Kennzeichen mit der Information eingeschlossen, dass Fallbackverteilungspunkte zulässig sind.  

2.  Vom Verwaltungspunkt wird eine Inhaltsortliste mit bevorzugten Verteilungspunkten sowie Fallbackverteilungspunkten, an denen der Inhalt verfügbar ist, an den Client zurückgegeben. Der Inhalt ist an keinem bevorzugten Verteilungspunkt, jedoch an mindestens einem Fallbackverteilungspunkt verfügbar.  

3.  Der Inhalt wird nicht heruntergeladen, weil die Bereitstellungseigenschaft für den Fall der Verwendung eines Fallbackverteilungspunkts auf **Inhalt nicht herunterladen** festgelegt ist (diese Einstellung wird verwendet, wenn Clients zum Abrufen des Inhalts auf den Fallback ausweichen). Es tritt ein Clientfehler auf, die Fehlermeldung **Inhalt ist nicht verfügbar** wird angezeigt, und vom Client wird in den Wiederholungsmodus gewechselt. Jede Stunde wird eine neue Inhaltsanforderung gesendet.  

## <a name="scenario-6"></a>Szenario 6  
 Folgende Konfigurationseinstellungen sind vorhanden:  

-   **Der Inhalt ist an keinem bevorzugten Verteilungspunkt verfügbar.**  

-   **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen** ist nicht aktiviert.  

-   **Fallback zulassen**: aktiviert  

-   **Bereitstellungsverhalten für langsame Netzwerke**: Inhalt herunterladen und installieren  


**Details:**  

1.  Vom Client wird eine Inhaltsanforderung an den Verwaltungspunkt gesendet. Vom Client wird in die Anforderung ein Kennzeichen mit der Information eingeschlossen, dass Fallbackverteilungspunkte aktiviert sind.  

2.  Vom Verwaltungspunkt wird eine Inhaltsortliste mit bevorzugten Verteilungspunkten sowie Fallbackverteilungspunkten, an denen der Inhalt verfügbar ist, an den Client zurückgegeben. Der Inhalt ist an keinem bevorzugten Verteilungspunkt, jedoch an mindestens einem Fallbackverteilungspunkt verfügbar.  

3.  Der Inhalt wird von einem Fallbackverteilungspunkt aus der Liste heruntergeladen, da die Bereitstellungseigenschaft für das Verwenden eines Fallbackverteilungspunkts auf den Wert **Inhalt herunterladen und installieren**festgelegt ist.  

## <a name="scenario-7"></a>Szenario 7  
 Folgende Konfigurationseinstellungen sind vorhanden:  

-   **Der Inhalt ist an keinem bevorzugten Verteilungspunkt verfügbar.**  

-   **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen** ist aktiviert.  

-   **Fallback zulassen**: nicht aktiviert  

-   **Bereitstellungsverhalten für langsame Netzwerke**: beliebige Konfiguration  


**Details:**  

1.  Vom Client wird eine Inhaltsanforderung an den Verwaltungspunkt gesendet.  

2.  Vom Verwaltungspunkt wird eine Inhaltsortliste mit bevorzugten Verteilungspunkten, an denen der Inhalt verfügbar ist, an den Client zurückgegeben. Der Inhalt ist an keinem bevorzugten Verteilungspunkt verfügbar.  

3.  Es tritt ein Clientfehler auf, die Fehlermeldung **Inhalt ist nicht verfügbar** wird angezeigt, und vom Client wird in den Wiederholungsmodus gewechselt. Jede Stunde wird eine neue Inhaltsanforderung gesendet.  

4.  Vom Verwaltungspunkt wird ein Trigger erstellt, mit dem der Verteilungs-Manager zur Verteilung des Inhalts an alle bevorzugten Verteilungspunkte des Clients, von dem die Inhaltsanforderung erfolgt ist, aufgefordert wird.  

5.  Der Inhalt wird vom Verteilungs-Manager an alle bevorzugten Verteilungspunkte verteilt. In den meisten Fällen wird der Inhalt innerhalb einer Stunde erfolgreich an die bevorzugten Verteilungspunkte verteilt.  

6.  Vom Client wird eine neue Inhaltsanforderung an den Verwaltungspunkt gesendet.  

7.  Vom Verwaltungspunkt wird eine Inhaltsortliste mit bevorzugten Verteilungspunkten, an denen der Inhalt verfügbar ist, an den Client zurückgegeben. Der Inhalt wird von einem der bevorzugten Verteilungspunkte auf der Liste heruntergeladen.  

## <a name="scenario-8"></a>Szenario 8  
 Folgende Konfigurationseinstellungen sind vorhanden:  

-   **Der Inhalt ist an keinem bevorzugten Verteilungspunkt verfügbar.**  

-   **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen** ist aktiviert.  

-   **Fallback zulassen**: aktiviert  

-   **Bereitstellungsverhalten für langsame Netzwerke**: Inhalt nicht herunterladen  


**Details:**  

1.  Vom Client wird eine Inhaltsanforderung an den Verwaltungspunkt gesendet. Vom Client wird in die Anforderung ein Kennzeichen mit der Information eingeschlossen, dass Fallbackverteilungspunkte zulässig sind.  

2.  Vom Verwaltungspunkt wird eine Inhaltsortliste mit bevorzugten Verteilungspunkten sowie Fallbackverteilungspunkten, an denen der Inhalt verfügbar ist, an den Client zurückgegeben. Der Inhalt ist an keinem bevorzugten Verteilungspunkt, jedoch an mindestens einem Fallbackverteilungspunkt verfügbar.  

3.  Der Inhalt wird nicht heruntergeladen, weil die Bereitstellungseigenschaft bei Verwendung eines Fallbackverteilungspunkts mit dem Wert **Nicht herunterladen**festgelegt ist. Es tritt ein Clientfehler auf, die Fehlermeldung **Inhalt ist nicht verfügbar** wird angezeigt, und vom Client wird in den Wiederholungsmodus gewechselt. Jede Stunde wird eine neue Inhaltsanforderung gesendet.  

4.  Vom Verwaltungspunkt wird ein Trigger erstellt, mit dem der Verteilungs-Manager zur Verteilung des Inhalts an alle bevorzugten Verteilungspunkte des Clients, von dem die Inhaltsanforderung erfolgt ist, aufgefordert wird.  

5.  Der Inhalt wird vom Verteilungs-Manager an alle bevorzugten Verteilungspunkte verteilt. In den meisten Fällen wird der Inhalt innerhalb einer Stunde erfolgreich an die bevorzugten Verteilungspunkte verteilt.  

6.  Vom Client wird eine neue Inhaltsanforderung an den Verwaltungspunkt gesendet.  

7.  Vom Verwaltungspunkt wird eine Inhaltsortliste mit bevorzugten Verteilungspunkten, an denen der Inhalt verfügbar ist, an den Client zurückgegeben.  

8.  Der Inhalt wird von einem der bevorzugten Verteilungspunkte auf der Liste heruntergeladen.  

## <a name="scenario-9"></a>Szenario 9  
 Folgende Konfigurationseinstellungen sind vorhanden:  

-   **Der Inhalt ist an keinem bevorzugten Verteilungspunkt verfügbar.**  

-   **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen** ist aktiviert.  

-   **Fallback zulassen**: aktiviert  

-   **Bereitstellungsverhalten für langsame Netzwerke**: Inhalt herunterladen und installieren  


**Details:**  

1.  Vom Client wird eine Inhaltsanforderung an den Verwaltungspunkt gesendet. Vom Client wird in die Anforderung ein Kennzeichen mit der Information eingeschlossen, dass Fallbackverteilungspunkte zulässig sind.  

2.  Vom Verwaltungspunkt wird eine Inhaltsortliste mit bevorzugten Verteilungspunkten sowie Fallbackverteilungspunkten, an denen der Inhalt verfügbar ist, an den Client zurückgegeben. Der Inhalt ist an keinem bevorzugten Verteilungspunkt, jedoch an mindestens einem Fallbackverteilungspunkt verfügbar.  

3.  Der Inhalt wird von einem Fallbackverteilungspunkt aus der Liste heruntergeladen, da die Bereitstellungseigenschaft für das Verwenden eines Fallbackverteilungspunkts auf den Wert **Inhalt herunterladen und installieren**festgelegt ist. Diese Bereitstellungseinstellung ermöglicht es einem Client, der eine Fallbackinhaltsquelle verwenden muss, den Inhalt von diesem Ort abzurufen.  

4.  Vom Verwaltungspunkt wird ein Trigger erstellt, mit dem der Verteilungs-Manager zur Verteilung des Inhalts an alle bevorzugten Verteilungspunkte des Clients aufgefordert wird, von dem die Inhaltsanforderung erfolgt ist.  

5.  Der Verteilungs-Manager verteilt den Inhalt an alle bevorzugten Verteilungspunkte. Dadurch können weitere Clients den Inhalt ohne Verwendung eines Fallbackverteilungspunkts abrufen.  
