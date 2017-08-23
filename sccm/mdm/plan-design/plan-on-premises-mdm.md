---
title: "Planen der lokalen Verwaltung mobiler Geräte | Microsoft-Dokumentation"
description: "Planen Sie die lokale Verwaltung mobiler Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 544c3bea0c7df96887ee1717f061c39c64b82d01
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Planen der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Berücksichtigen Sie die folgenden Anforderungen vor der Vorbereitung der Configuration Manager\-Infrastruktur für die lokale Verwaltung mobiler Geräte.

##  <a name="bkmk_devices"></a> Unterstützte Geräte  
 Die lokale Verwaltung mobiler Geräte ermöglicht das Verwalten mobiler Geräte mithilfe der in die Gerätebetriebssysteme integrierten Verwaltungsfunktionen.  Die Verwaltungsfunktionen basieren auf dem Geräteverwaltungsstandard von Open Mobile Alliance (OMA), und viele Geräteplattformen nutzen diesen Standard für die Geräteverwaltung.  In der Dokumentation und der Benutzeroberfläche der Configuration Manager-Konsole werden diese Geräte als **moderne Geräte** bezeichnet, um sie von anderen Geräten zu unterscheiden, für deren Verwaltung der Configuration Manager-Client erforderlich ist.  

 > [!NOTE]  
>  Configuration Manager Current Branch unterstützt die Registrierung bei der lokalen Verwaltung mobiler Geräte für Geräte, auf denen folgende Betriebssysteme ausgeführt werden:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Microsoft 10 Team \(ab Configuration Manager Version 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

##  <a name="bkmk_intune"></a> Verwenden des Microsoft Intune-Abonnements  
 Für den Einstieg in die lokale Verwaltung mobiler Geräte benötigen Sie ein Microsoft Intune\-Abonnement. Das Abonnement ist nur erforderlich, um die Lizenzierung der Geräten zu verfolgen und dient nicht zum Verwalten oder Speichern von Geräteverwaltungsinformationen. Die gesamte Verwaltung erfolgt mithilfe der lokalen Configuration Manager-Infrastruktur in Ihrem Unternehmen.  

 > [!NOTE]  
 > Ab Version 1610 unterstützt Configuration Manager für die Verwaltung mobiler Geräte die gleichzeitige Verwendung von Microsoft Intune und der lokalen Configuration Manager-Infrastruktur.   

 Wenn an Ihrem Standort Geräte mit Internetverbindung vorhanden sind, können Geräte über Intune benachrichtigt werden, dass sie den Geräteverwaltungspunkt nach Richtlinienupdates überprüfen sollen. Diese Verwendung von Intune dient ausschließlich zur Benachrichtigung von mit dem Internet verbundenen Geräten. Geräte ohne Internetverbindung (die nicht von Intune kontaktiert werden können) überprüfen im konfigurierten Abrufintervall die Standortsystemrollen auf Verwaltungsfunktionen.  

> [!TIP]  
>  Es wird empfohlen, Intune einzurichten, bevor Sie die erforderlichen Standortsystemrollen einrichten, um die erforderliche Zeit zu minimieren, bis die Standortsystemrollen funktionsfähig sind.  

 Weitere Informationen zum Einrichten des Intune-Abonnements finden Sie unter [Einrichten eines Microsoft Intune-Abonnements in System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md).  

##  <a name="bkmk_roles"></a> Erforderliche Standortsystemrollen  
 Die lokale Verwaltung mobiler Geräte erfordert mindestens jeweils eine der folgenden Standortsystemrollen:  

-   **Anmeldungsproxypunkt** zur Unterstützung von Anmeldungsanforderungen.  

-   **Anmeldungspunkt** zur Unterstützung der Geräteanmeldung.  

-   **Geräteverwaltungspunkt** für die Bereitstellung von Richtlinien. Diese Standortsystemrolle ist eine Variante der Verwaltungspunktrolle, die konfiguriert wurde, um die Verwaltung mobiler Geräte zu ermöglichen.  

-   **Verteilungspunkt** für die Inhaltsübermittlung.  

-   **Dienstverbindungspunkt** für die Verbindung mit Intune, um Geräte außerhalb der Firewall zu benachrichtigen.  

 Diese Standortsystemrollen können auf dem einzigen Standortsystemserver installiert oder separat auf verschiedenen Servern ausgeführt werden, je nach den Bedürfnissen Ihrer Organisation. Jeder für die lokale Verwaltung mobiler Geräte verwendete Standortsystemserver muss als HTTPS\-Endpunkt für die Kommunikation mit vertrauenswürdigen Geräten konfiguriert werden. Weitere Informationen finden Sie unter [Erforderliche vertrauenswürdige Kommunikation](#bkmk_trustedComs).  

 Weitere Informationen zur Planung der Standortsystemrollen finden Sie unter [Planen von Standortsystemservern und Standortsystemrollen für System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Weitere Informationen zum Hinzufügen der erforderlichen Standortsystemrollen finden Sie unter [Installieren von Standortsystemrollen für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).  

##  <a name="bkmk_trustedComs"></a> Erforderliche vertrauenswürdige Kommunikation  
 Die lokale Verwaltung mobiler Geräte erfordert, dass die Standortsystemrollen für die HTTPS\-Kommunikation aktiviert sind. Je nach Ihren Anforderungen können Sie die Zertifizierungsstelle Ihres Unternehmens zum Herstellen der vertrauenswürdigen Verbindungen zwischen Servern und Geräten oder eine öffentlich verfügbare Zertifizierungsstelle als vertrauenswürdige Zertifizierungsstelle verwenden.  In beiden Fällen benötigen Sie ein mit IIS konfiguriertes Webserverzertifikat auf den Standortsystemservern, auf denen die erforderlichen Standortsystemrollen gehostet werden. Außerdem muss auf den Geräten, die eine Verbindung mit diesen Servern herstellen müssen, das Stammzertifikat dieser Zertifizierungsstelle installiert sein.  

 Wenn Sie die Zertifizierungsstelle Ihres Unternehmens für die vertrauenswürdige Kommunikation verwenden, müssen Sie die folgenden Aufgaben ausführen:  

-   Generieren Sie die Webserver-Zertifikatvorlage bei der Zertifizierungsstelle und stellen Sie sie aus.  

-   Fordern Sie ein Webserverzertifikat für jeden Standortsystemserver an, auf dem eine erforderliche Standortsystemrolle gehostet wird.  

-   Konfigurieren Sie IIS auf dem Standortsystemserver für die Verwendung des angeforderten Webserverzertifikats.  

 Auf Geräten, die mit der Active Directory-Unternehmensdomäne verknüpft sind, ist das Stammzertifikat der Unternehmenszertifizierungsstelle bereits für vertrauenswürdige Verbindungen verfügbar. Dies bedeutet, dass Geräte, die einer Domäne angehören, (z. B. Desktopcomputer) automatisch für HTTPS-Verbindungen mit den Standortsystemservern als vertrauenswürdig eingestuft werden. Auf Geräten, die der Domäne nicht angehören, (in der Regel mobile Geräte) ist das erforderliche erforderliche Stammzertifikat jedoch nicht installiert. Auf diesen Geräten muss das Stammzertifikat manuell installiert werden, um erfolgreich mit Standortsystemservern zu kommunizieren, die die lokale Verwaltung mobiler Geräte unterstützen.  

 Sie müssen das Stammzertifikat der ausstellenden Zertifizierungsstelle für die Verwendung durch einzelne Geräte exportieren. Die Stammzertifikatdatei erhalten Sie, indem Sie es über die Zertifizierungsstelle exportieren. Eine einfachere Methode ist es, mit dem von der Zertifizierungsstelle ausgestellten Webserverzertifikat das Stammzertifikat zu extrahieren und eine Stammzertifikatdatei zu erstellen.   Anschließend muss das Stammzertifikat an das Gerät übermittelt werden.  Einige Beispiele für Übermittlungsmethoden:  

-   Dateisystem  

-   E-Mail-Anlage  

-   Speicherkarte  

-   Verbundenes Gerät  

-   Cloudspeicher (z. B. OneDrive)  

-   NFC-Verbindung (Near Field Communication)  

-   Barcodescanner  

-   Out-of-Box-Experience (OOBE) des bereitstellenden Pakets  

 Weitere Informationen finden Sie unter [Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

##  <a name="bkmk_enrollment"></a> Überlegungen zur Registrierung  
 Zum Aktivieren der Geräteregistrierung für die lokale Verwaltung mobiler Geräte müssen Benutzer über Registrierungsberechtigungen verfügen, und ihre Geräte müssen zur vertrauenswürdigen Kommunikation mit den Standortsystemservern in der Lage sein, auf denen die erforderlichen Standortsystemrollen gehostet werden.  

 Richten Sie zum Erteilen von Registrierungsberechtigungen an Benutzer in den Configuration Manager-Clienteinstellungen ein Anmeldungsprofil ein. Sie können die Clientstandardeinstellungen verwenden, um das Anmeldungsprofil per Push an alle ermittelten Benutzer zu übertragen, oder Sie können das Anmeldungsprofil in benutzerdefinierten Clienteinstellungen einrichten und die Einstellungen per Push an eine oder mehrere Benutzersammlungen senden.  

 Benutzer, die über Benutzeranmeldeberechtigungen verfügen, können ihre eigenen Geräte registrieren. Damit das Gerät des Benutzers registriert werden kann, muss darauf das Stammzertifikat der Zertifizierungsstelle installiert sein, die das Webserverzertifikat ausgestellt hat, das auf den Standortsystemservern verwendet wird, auf denen die erforderlichen Standortsystemrollen gehostet werden.  

 Als Alternative zur benutzerinitiierten Registrierung können Sie ein Massenregistrierungspaket einrichten, mit dem das Gerät ohne Eingreifen des Benutzers registriert werden kann. Dieses Paket kann an dem Gerät übermittelt werden, bevor es erstmalig für die Verwendung bereitgestellt wird oder nachdem das Gerät den OOBE-Prozess durchlaufen hat.  

 Weitere Informationen zum Einrichten und Registrieren von Geräten finden Sie unter  

-   [Einrichten der Geräteregistrierung für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

-   [Registrieren von Geräten für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)  
