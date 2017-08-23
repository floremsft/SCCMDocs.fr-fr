---
title: "Unicode- und ASCII-Unterstützung | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über die Unterstützung für Unicode- und ASCII-Zeichen in System Center Configuration Manager-Objekten."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 18f1c64c1f27001a0fdfbab4236d09a5bc279272
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="unicode-and-ascii-support-in-system-center-configuration-manager"></a>Unicode- und ASCII-Unterstützung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager erstellt die meisten Objekte mithilfe von Unicode-Zeichen. Allerdings werden von mehreren Objekten nur ASCII-Zeichen unterstützt, oder sie weisen andere Einschränkungen auf.  

 In den folgenden Abschnitten werden die Objekte aufgelistet, bei denen nur Zeichen aus dem ASCII-Zeichensatz verwendet werden dürfen oder die zusätzliche Einschränkungen aufweisen.  

-   [Objekte, die ASCII-Zeichen verwenden](#BKMK_ASCIIchar)  

-   [Zusätzliche Einschränkungen](#BKMK_OtherCharLimitations)  

-   [Nicht lokalisierte Configuration Manager-Objekte](#BKMK_LangNonLocalize)  

##  <a name="BKMK_ASCIIchar"></a> Objekte, die ASCII-Zeichen verwenden  
 Von Configuration Manager wird beim Erstellen der folgenden Objekte nur der ASCII-Zeichensatz unterstützt:  

-   Standortcode  

-   Alle Computernamen von Standortsystemservern  

-   Folgende Configuration Manager-Konten:  

    > [!NOTE]  
    >  Bei diesen Konten werden an Standorten in russischer Sprache sowohl ASCII-Zeichen als auch kyrillische Zeichen (RUS) unterstützt.  

    -   Clientpushinstallations-Konto  

    -   Konto zum Veröffentlichen der Integritätszustandsreferenz  

    -   Konto zum Abfragen der Integritätszustandsreferenz  

    -   Verbindungskonto für Verwaltungspunktdatenbank  

    -   Netzwerkzugriffskonto  

    -   Paketzugriffskonto  

    -   Standard-Sendekonto  

    -   Standortsystem-Installationskonto  

    -   Verbindungskonto des Softwareupdatepunkts  

    -   Proxyserverkonto für Softwareupdatepunkt  

    > [!NOTE]  
    >  Bei den Konten, die Sie für die rollenbasierte Verwaltung angeben, wird Unicode unterstützt.  
    >   
    >  Vom Konto des Reporting Services-Punkts wird Unicode mit Ausnahme kyrillischer Zeichen (RUS) unterstützt.  

-   Vollständig qualifizierter Domänenname (FQDN) für Standortserver und Standortsysteme  

-   Installationspfad für Configuration Manager  

-   SQL Server-Instanznamen  

-   Pfadnamen der folgenden Standortsystemrollen:  

    -   Anwendungskatalog-Webdienstpunkt  

    -   Anwendungskatalog-Websitepunkt  

    -   Anmeldungspunkt  

    -   Anmeldungsproxypunkt  

    -   Reporting Services-Punkt  

    -   Zustandsmigrationspunkt  

-   Pfadnamen der folgenden Ordner:  

    -   Der Ordner, in dem Clientzustandsmigrationsdaten gespeichert werden  

    -   Der Ordner mit den Configuration Manager-Berichten  

    -   Der Ordner mit der Configuration Manager-Sicherung  

    -   Der Ordner, in dem die Installationsquelldateien für die Standorteinrichtung gespeichert werden  

    -   Der Ordner, in dem die für Setup erforderlichen Downloads gespeichert werden  

-   Pfadnamen der folgenden Objekte:  

    -   IIS-Website  

    -   Installationspfad der virtuellen Anwendung  

    -   Name der virtuellen Anwendung  

-   Die folgenden Objekte für AMT und Out-of-Band-Verwaltung:  

    -   Der FQDN des AMT-basierten Computers  

    -   Der Computername des AMT-basierten Computers  

    -   Der NetBIOS-Domänenname  

    -   Der Funkprofilname und die SSID  

    -   Name der vertrauenswürdigen Zertifizierungsstelle  

    -   Der Name der Zertifizierungsstelle (CA) und Vorlagennamen  

    -   Der Dateiname und -pfad der Bilddatei für die IDE-Umleitung  

    -   Der Inhalt des AMT-Datenspeichers  

-   ISO-Dateinamen für Startmedien  

##  <a name="BKMK_OtherCharLimitations"></a> Zusätzliche Einschränkungen  
 Nachfolgend sind weitere Einschränkungen für unterstützte Zeichensätze und Sprachversionen aufgelistet:  

-   In Configuration Manager wird eine Änderung des Gebietsschemas für den Standortservercomputer nicht unterstützt.  

-   Von einer Unternehmenszertifizierungsstelle (CA) werden keine Clientcomputernamen mit Doppelbyte-Zeichensätzen (DBCS) unterstützt. Welche Clientcomputernamen verwendet werden können, ist durch die PKI-Einschränkung des IA5-Zeichensatzes eingeschränkt. Außerdem werden von Configuration Manager keine Zertifizierungsstellennamen oder Werte für Antragstellernamen unterstützt, in denen Doppelbyte-Zeichensätze (DBCS) verwendet werden.  

##  <a name="BKMK_LangNonLocalize"></a> Nicht lokalisierte Configuration Manager-Objekte  
 Bei den meisten in der Configuration Manager-Datenbank gespeicherten Objekten wird Unicode unterstützt. Sofern möglich, werden diese Informationen in der Betriebssystemsprache angezeigt, die dem Gebietsschema eines Computers entspricht. Damit Informationen von der Clientschnittstelle oder der Configuration Manager-Konsole in der Betriebssystemsprache des Computers angezeigt werden, muss das Gebietsschema des Computers mit einer am Standort installierten Client- oder Serversprache übereinstimmen.  

 Allerdings wird Unicode nicht von allen Configuration Manager-Objekten unterstützt. Diese Objekte werden in der Datenbank in ASCII gespeichert. Es gibt auch Objekte mit zusätzlichen Einschränkungen hinsichtlich der Sprache. Diese Informationen werden immer im ASCII-Zeichensatz oder in der Sprache, in der das betreffende Objekt ursprünglich erstellt wurde, angezeigt.  
