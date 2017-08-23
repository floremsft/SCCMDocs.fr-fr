---
title: Asset Intelligence Sicherheit und Datenschutz | Microsoft-Dokumentation
description: "Abrufen von Sicherheits- und Datenschutzinformationen für Asset Intelligence in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: b12054cce52e2b83715a083d78a62e06b5127a2f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-asset-intelligence-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz für Asset Intelligence in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält Sicherheits- und Datenschutzinformationen für Asset Intelligence in System Center Configuration Manager.  

##  <a name="BKMK_Security_AI"></a> Bewährte Sicherheitsmethoden für Asset Intelligence  
 Wenden Sie die folgenden bewährten Sicherheitsmethoden beim Verwenden von Asset Intelligence an.  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Sichern Sie beim Importieren einer Lizenzdatei die Datei und den Kommunikationskanal (Microsoft-Volumenlizenzierungsdatei oder allgemeine Lizenzübersichtsdatei).|Verwenden Sie NTFS-Dateisystemberechtigungen, um sicherzustellen, dass nur berechtigte Benutzer auf die Lizenzdateien zugreifen können. Verwenden Sie außerdem SMB-Signaturen (Server Message Block), um die Integrität der Daten bei der Übertragung an den Standortserver während des Importvorgangs sicherzustellen.|  
|Wenden Sie beim Importieren der Lizenzdateien das Prinzip der geringsten Berechtigungen an.|Wählen Sie eine rollenbasierte Verwaltung, um die Berechtigung "Asset Intelligence verwalten" dem Administrator zu gewähren, der die Lizenzdateien importiert. Die integrierte Rolle "Asset-Manager" umfasst diese Berechtigung.|  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Datenschutzinformationen für Asset Intelligence  
 Asset Intelligence erweitert die Inventurfähigkeiten von Configuration Manager und ermöglicht eine höhere Sichtbarkeit der Anlagewerte im Unternehmen. Die Sammlung von Asset Intelligence-Informationen ist nicht automatisch aktiviert. Sie können die Art der gesammelten Informationen ändern, indem Sie Hardwareinventur-Berichtsklassen aktivieren. Weitere Informationen finden Sie unter [Konfigurieren von Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Die Asset Intelligence-Informationen werden in der Configuration Manager-Datenbank auf die gleiche Weise gespeichert wie Inventurinformationen. Wenn von Clients per HTTPS eine Verbindung zu Verwaltungspunkten hergestellt wird, sind die Daten während des Transfers zum Verwaltungspunkt jederzeit verschlüsselt. Wenn von Clients per HTTP eine Verbindung hergestellt wird, können Sie die Inventurdatenübertragung so konfigurieren, dass sie signiert und verschlüsselt wird. Die Inventurdaten werden in der Datenbank nicht in einem verschlüsselten Format gespeichert. Die Informationen werden in der Datenbank gespeichert, bis sie vom Standortwartungstask **Veralteten Inventurverlauf löschen** in Intervallen von 90 Tagen gelöscht werden. Sie können das Löschintervall konfigurieren.  

 Von Asset Intelligence werden keine Benutzer-, Computer oder Lizenzverwendungsinformationen an Microsoft gesendet. Sie können System Center Online-Kategorisierungsanforderungen senden. Das bedeutet, dass Sie einen oder mehrere nicht kategorisierte Softwaretitel kennzeichnen und zur Recherche und Kategorisierung an System Center Online senden können. Nachdem ein Softwaretitel hochgeladen wurde, können die Recherchemitarbeiter bei Microsoft diesen identifizieren und kategorisieren und danach dieses Wissen für alle Kunden verfügbar machen, die den Onlinedienst nutzen. Sie sollten sich bei der Übermittlung von Informationen an System Center Online immer der Implikationen im Hinblick auf den Datenschutz bewusst sein:  

-   Der Upload gilt nur für generische Softwaretitelinformationen (Name, Herausgeber usw.), die Sie an System Center Online senden. Beim Upload werden keine Inventurinformationen gesendet.  

-   Dateien werden nie automatisch hochgeladen. Im System kann dieser Task auch nicht automatisiert werden. Sie müssen den Upload jedes Softwaretitels manuell auswählen und genehmigen.  

-   Über ein Dialogfeld wird vor dem Start des Uploadvorgangs genau angezeigt, welche Daten hochgeladen werden.  

-   Die Lizenzinformationen werden nicht an Microsoft gesendet. Die Lizenzinformationen werden in einem separaten Bereich der Configuration Manager-Datenbank gespeichert. Es gibt keine Möglichkeit, diese an Microsoft zu senden.  

-   Jeder Softwaretitel, der hochgeladen wird, wird öffentlich in dem Sinn, dass die Kenntnis dieser gegebenen Anwendung und ihre Kategorisierung Teil des System Center Online Asset Intelligence-Katalogs werden und dann für andere Kunden des Katalogs heruntergeladen werden.  

-   Die Quelle des Softwaretitels wird im Asset Intelligence-Katalog nicht aufgezeichnet und anderen Kunden nicht zur Verfügung gestellt. Sie müssen jedoch trotzdem sicherstellen, dass Sie keine Anwendungstitel laden, die private Informationen enthalten.  

-   Hochgeladene Daten können nicht zurückgerufen werden.  

 Berücksichtigen Sie die Datenschutzanforderungen Ihrer Organisation, bevor Sie die Asset Intelligence-Datensammlung konfigurieren und entscheiden, ob Sie Informationen an System Center Online übermitteln möchten.  
