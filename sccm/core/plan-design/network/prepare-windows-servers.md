---
title: Vorbereiten von Computern mit Windows Server | Microsoft-Dokumentation
description: "Stellen Sie sicher, dass ein Computer die Voraussetzungen für die Verwendung als Standortserver oder Standortsystemserver für System Center Configuration Manager erfüllt."
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9b97dedb5d2be0bd2e47260033e6e4361467dc4e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-windows-servers-to-support-system-center-configuration-manager"></a>Vorbereiten von Computern mit Windows Server zur Unterstützung von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ehe Sie einen Windows-Computer als Standortsystemserver für System Center Configuration Manager nutzen können, muss der Computer die Voraussetzung für die vorgesehene Verwendung als Standortserver oder Standortsystemserver erfüllen.  

-   Zu diesen Voraussetzungen gehören häufig ein(e) oder mehrere Windows-Features oder -Rollen, die mithilfe von Server-Manager auf dem Computer aktiviert werden.  

-   Da sich die Methode zum Aktivieren von Windows-Features und -Rollen je nach Betriebssystem unterscheidet, konsultieren Sie die Dokumentation Ihres Betriebssystems hinsichtlich detaillierter Informationen zur entsprechenden Einrichtung.  

Die Informationen in diesem Artikel bieten einen Überblick über die verschiedenen Windows-Konfigurationstypen, die zur Unterstützung von Configuration Manager-Standortsystemen erforderlich sind. Konfigurationsdetails für bestimmte Standortsystemrollen finden Sie unter [Voraussetzungen für Standorte und Standortsysteme](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

##  <a name="BKMK_WinFeatures"></a> Windows-Features und -Rollen  
 Wenn Sie Windows-Features und -Rollen auf einem Computer einrichten, müssen Sie möglicherweise den Computer neu starten, um die Konfiguration abzuschließen. Daher ist es eine gute Idee, die Computer zu identifizieren, die bestimmte Standortsystemrollen hosten, bevor Sie einen Configuration Manager-Standort oder Standortsystemserver installieren.
### <a name="features"></a>Features  
 Die folgenden Windows-Features sind auf bestimmten Standortsystemservern erforderlich und müssen eingerichtet werden, bevor Sie eine Standortsystemrolle auf dem jeweiligen Computer installieren.  

-   **.NET Framework:** einschließlich  

    -   ASP.NET  
    -   HTTP-Aktivierung  
    -   Nicht-HTTP-Aktivierung  
    -   Windows Communication Foundation (WCF)  

    Verschiedene Versionen von .NET Framework sind je nach Standortsystemrolle erforderlich.  

    Da .NET Framework 4.0 und höher nicht so abwärtskompatibel ist, dass 3.5 oder ältere Versionen ersetzt werden, müssen Sie entsprechende Versionen auf demselben Computer aktivieren, sofern diese als erforderlich angegeben sind.  

-   **Background Intelligent Transfer Service (BITS)**: Verwaltungspunkte erfordern BITS (und automatisch ausgewählte Optionen), damit die Kommunikation mit verwalteten Geräten unterstützt wird.  

-   **BranchCache:** Verteilungspunkte können mit BranchCache so eingerichtet werden, dass Sie Clients unterstützen, die BranchCache verwenden.  

-   **Datendeduplizierung:** Verteilungspunkte können mit Datendeduplizierung eingerichtet werden und davon profitieren.  

-   **Remotedifferenzialkomprimierung (Remote Differential Compression, RDC)**: Jeder Computer, der einen Standortserver oder Verteilungspunkt hostet, benötigt RDC.   
    RDC wird zum Erstellen von Paketsignaturen und Durchführen von Signaturvergleichen verwendet.  

### <a name="roles"></a>Rollen  
 Die folgenden Windows-Rollen sind erforderlich, um bestimmte Funktionen zu unterstützen, z. B. Softwareupdates und Betriebssystembereitstellungen, während IIS von den meisten gängigen Standortsystemrollen benötigt wird.  

 -   **Registrierungsdienst für Netzwerkgeräte** (unter Active Directory-Zertifikatdienste): Diese Windows-Rolle ist eine Voraussetzung für die Verwendung von Zertifikatprofilen in Configuration Manager.  

 -   **Webserver (IIS)**: Einschließlich:  
    -   Allgemeine HTTP-Features >  
        -   HTTP-Umleitung  
    -   Anwendungsentwicklung >  
        -   .NET-Erweiterbarkeit  
        -   ASP.NET  
        -   ISAPI-Erweiterungen  
        -   ISAPI-Filter  
    -   Verwaltungstools >  
        -   IIS 6-Verwaltungskompatibilität  
        -   IIS 6-Metabasiskompatibilität  
        -   IIS 6-WMI-Kompatibilität  
    -   Sicherheit >  
        -   Anforderungsfilterung  
        -   Windows-Authentifizierung  

 Die folgenden Standortsystemrollen verwenden eine oder mehrere der aufgelisteten IIS-Konfigurationen:  
    -   Anwendungskatalog-Webdienstpunkt  
    -   Anwendungskatalog-Websitepunkt  
    -   Verteilungspunkt  
    -   Anmeldungspunkt  
    -   Anmeldungsproxypunkt  
    -   Fallbackstatuspunkt  
    -   Verwaltungspunkt  
    -   Softwareupdatepunkt  
    -   Zustandsmigrationspunkt     

    Die erforderliche Mindestversion von IIS ist die Version, die zum Betriebssystem des Standortservers gehört.  

    Zusätzlich zu diesen IIS-Konfigurationen müssen Sie möglicherweise [IIS-Anforderungsfilterung für Verteilungspunkte](#BKMK_IISFiltering) einrichten.  

-   **Windows-Bereitstellungsdienste:** Diese Rolle wird mit der Betriebssystembereitstellung verwendet.  
-   **Windows Server Update Services:** Diese Rolle ist erforderlich, wenn Sie Softwareupdates bereitstellen.  

##  <a name="BKMK_IISFiltering"></a> IIS-Anforderungsfilterung für Verteilungspunkte  
 IIS verwendet standardmäßig die Filterung von Benutzeranforderungen, um Dateierweiterungen und Ordnerpfade für den Zugriff über HTTP- oder HTTPS-Verbindungen zu blockieren. Auf einem Verteilungspunkt verhindert dies, dass Clients Pakete mit blockierten Erweiterungen oder Ordnerpfaden herunterladen.  

 Wenn Ihre Paketquelldateien Erweiterungen aufweisen, die in IIS durch Ihre Konfiguration der Anforderungsfilterung blockiert werden, müssen Sie die Anforderungsfilterung so einrichten, dass sie diese zulässt. Dies erfolgt durch [Bearbeiten des Anforderungsfilterfeatures](https://technet.microsoft.com/library/hh831621.aspx) im IIS-Manager auf Ihren Verteilungspunktcomputern.  

 Die folgenden Dateinamenerweiterungen werden außerdem von Configuration Manager für Pakete und Anwendungen verwendet. Stellen Sie sicher, dass Ihre Konfigurationen der Anforderungsfilterung diese Erweiterungen nicht blockieren:  

-   .PCK  
-   .PKG  
-   .STA  
-   .TAR  

Beispiel: Sie verfügen über Quelldateien für eine Softwarebereitstellung, die möglicherweise einen Ordner mit der Bezeichnung **bin** oder eine Datei mit der Dateierweiterung **.mdb** aufweisen.  

-   Standardmäßig blockiert die IIS-Anforderungsfilterung den Zugriff auf diese Elemente (**bin** wird als ausgeblendetes Segment und **.mdb** als Dateierweiterung blockiert).  

-   Wenn Sie die IIS-Standardkonfiguration auf einem Verteilungspunkt verwenden, treten beim Herunterladen dieser Softwarebereitstellung vom Verteilungspunkt Fehler auf, wenn die Clients BITS verwenden. Außerdem geben die Clients an, dass sie auf Inhalte warten.  

-   Damit die Clients diese Inhalte herunterladen können, bearbeiten Sie auf jedem betreffenden Verteilungspunkt im IIS-Manager das Feature **Anforderungsfilterung**, um den Zugriff auf die Dateierweiterungen und Ordner in den Paketen und Anwendungen zuzulassen, die Sie bereitstellen.  

> [!IMPORTANT]  
>  Durch Bearbeitung des Anforderungsfilters kann sich die Angriffsfläche des Computers erhöhen.  
>   
>  -   Auf Serverebene vorgenommene Änderungen gelten für alle Websites auf dem Server.  
> -   Änderungen an einzelnen Websites gelten nur für die jeweilige Website.  
>   
>  Eine bewährte Sicherheitsmethode besteht darin, Configuration Manager auf einem dedizierten Webserver auszuführen. Wenn das Ausführen anderer Webanwendungen auf dem Webserver erforderlich ist, verwenden Sie für Configuration Manager eine benutzerdefinierte Website. Weitere Informationen finden Sie unter [Websites für Standortsystemserver in System Center Configuration Manager](../../../core/plan-design/network/websites-for-site-system-servers.md).  

## <a name="http-verbs"></a>HTTP-Verben
**Verwaltungspunkte:** Damit die Clients erfolgreich mit einem Verwaltungspunkt kommunizieren können, müssen auf dem Verwaltungspunktserver die folgenden HTTP-Verben zulässig sein:  
 - GET
 - POST
 - CCM_POST
 - HEAD
 - PROPFIND

**Verteilungspunkte:** Für Verteilungspunkte müssen die folgenden HTTP-Verben zulässig sein:
 - GET
 - HEAD
 - PROPFIND

Informationen zum Konfigurieren der Anforderungsfilterung finden Sie unter [Konfigurieren der Anforderungsfilterung in IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs) auf TechNet oder in einer ähnlichen Dokumentation, die sich auf die Version von Windows Server bezieht, die den Verwaltungspunkt hostet.
