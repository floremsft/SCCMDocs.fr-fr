---
title: "Einführung in Zertifikatprofile | Microsoft-Dokumentation"
description: Erfahren Sie, wie Zertifikatprofile in System Center Configuration Manager mit den Active Directory-Zertifikatdiensten funktionieren.
ms.custom: na
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: "7"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 7b1c0e449f3d1ef42e279e8707df6bf1df163b3f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Einführung in Zertifikatprofile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Zertifikatprofile arbeiten mit Active Directory-Zertifikatdiensten und der Rolle „Registrierungsdienst für Netzwerkgeräte“, um Authentifizierungszertifikate für verwaltete Geräte bereitzustellen, damit Benutzer nahtlos auf Unternehmensressourcen zugreifen können. Sie können z. B. Zertifikatprofile erstellen und bereitstellen, um Benutzern die erforderlichen Zertifikate zum Initiieren von VPN- und Drahtlosverbindungen bereitzustellen. 

Mit Zertifikatprofilen können Benutzergeräte automatisch so konfiguriert werden, dass auf Unternehmensressourcen wie WLAN-Netzwerke und VPN-Server ohne manuelle Installation von Zertifikaten bzw. ohne Verwendung eines Out-of-Band-Prozesses zugegriffen werden kann. Mit Zertifikatprofilen können auch Unternehmensressourcen geschützt werden, da Sie sicherere Einstellungen verwenden können, die von der Public Key-Infrastruktur (PKI) Ihres Unternehmens unterstützt werden. Sie können z. B. eine Serverauthentifizierung für alle WLAN- und VPN-Verbindungen erforderlich machen, da Sie die erforderlichen Zertifikate auf den verwalteten Geräten bereitgestellt haben.   

Zertifikatprofile bieten die folgenden Verwaltungsfunktionen:  

-   Zertifikatregistrierung und -erneuerung von einer Unternehmenszertifizierungsstelle für Geräte unter iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop und Mobile sowie Android. Diese Zertifikate können dann für WLAN- und VPN-Verbindungen verwendet werden.  

-   Bereitstellung von Stammzertifizierungsstellen- und Zwischenzertifizierungsstellen-Zertifikaten zur Konfiguration einer Vertrauenskette auf Geräten für VPN- und WLAN-Verbindungen, wenn die Serverauthentifizierung erforderlich ist.  

-   Überwachen und Melden der installierten Zertifikate.  

**Beispiel:** Alle Mitarbeiter müssen Verbindungen mit WLAN-Hotspots an verschiedenen Unternehmensstandorten herstellen können. Stellen Sie die für die WLAN-Verbindung erforderlichen Zertifikate bereit, und stellen Sie anschließend auf das Zertifikat verweisende WLAN-Profile bereit, um eine nahtlose Benutzerverbindung zu ermöglichen.  

**Beispiel:** Sie haben eine PKI eingerichtet und möchten Zertifikate auf eine flexiblere, sicherere Art und Weise bereitstellen, die Benutzern ohne Beeinträchtigung der Sicherheit den Zugriff auf Unternehmensressourcen über ihre persönlichen Geräten ermöglicht. Konfigurieren Sie Zertifikatprofile mit Einstellungen und Protokollen, die von der jeweiligen Geräteplattform unterstützt werden. Die Geräte können diese Zertifikate dann automatisch von einem mit dem Internet verbundenen Registrierungsserver anfordern. Anschließend konfigurieren Sie VPN-Profile, die diese Zertifikate verwenden, damit das Gerät auf Unternehmensressourcen zugreifen kann.  

## <a name="types-of-certificate-profiles"></a>Arten von Zertifikatprofilen  
 Es gibt drei Arten von Zertifikatprofilen:  

-   **Vertrauenswürdiges Zertifikat der Zertifizierungsstelle** : Ermöglicht Ihnen die Bereitstellung eines Zertifikats einer vertrauenswürdigen Stammzertifizierungsstelle oder einer Zwischenzertifizierungsstelle, um eine Zertifikatkette zu bilden, wenn das Gerät einen Server authentifizieren muss.  

-   **Simple Certificate Enrollment-Protokoll (SCEP)**: Ermöglicht Ihnen das Anfordern eines Zertifikats für ein Gerät oder einen Benutzer mithilfe des Protokolls SCEP und des Registrierungsdiensts für Netzwerkgeräte auf einem Server mit Windows Server 2012 R2.

    Sie müssen ein **Zertifikatprofil für ein vertrauenswürdiges Zertifikat der Zertifizierungsstelle** erstellen, um ein Zertifikatprofil des Typs **Simple Certificate Enrollment Protocol (SCEP)** erstellen zu können.

-   **Privater Informationsaustausch (.pfx)**: Erlaubt es Ihnen, für ein Gerät oder einen Benutzer ein PFX-Zertifikat (auch als PKCS #12-Zertifikat bezeichnet) anzufordern.

    Sie können PFX-Zertifikatprofile erstellen, indem Sie n entweder aus bestehenden Zertifikaten [Anmeldeinformationen importieren](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md) oder für die Bearbeitung von Anfragen [eine Zertifizierungsstelle definieren](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md).

    Ab Version 1706 können Sie Microsoft oder Entrust als Zertifizierungsstelle für **PFX-Zertifikate (Personal information exchange)** nutzen.


## <a name="requirements-and-supported-platforms"></a>Anforderungen und unterstützte Plattformen  
Zum Bereitstellen von Zertifikatprofilen, die SCEP verwenden, müssen Sie den Zertifikatregistrierungspunkt auf einem Standortsystemserver am Standort der zentralen Verwaltung oder an einem primären Standort installieren. Zudem müssen Sie ein Richtlinienmodul für NDES – das Configuration Manager-Richtlinienmodul – auf einem Server unter Windows Server 2012 R2 mit der Rolle „Active Directory-Zertifikatdienste“ und einem funktionsfähigen NDES installieren, der für die Geräte verfügbar ist, welche die Zertifikate benötigen. Bei Geräten, die von Microsoft Intune registriert werden, muss der NDES über das Internet verfügbar sein, z.B. in einem Umkreisnetzwerk (auch als DMZ bezeichnet).  

Für PFX-Zertifikate benötigen Sie zusätzlich einen Zertifikatregistrierungspunkt auf einem Standortsystemserver am zentralen Verwaltungsstandort oder einem primären Standort.  Sie müssen auch die Zertifizierungsstelle (Certificate Authority – CA) für das Zertifikat und die notwendigen Anmeldeinformationen angeben.  Ab Version 1706 können Sie entweder Microsoft oder Entrust als Zertifizierungsstelle angeben.  

Weitere Informationen zur Unterstützung eines Richtlinienmoduls durch den Registrierungsdienst für Netzwerkgeräte, damit Configuration Manager Zertifikate bereitstellen kann, finden Sie unter [Verwenden eines Richtlinienmoduls mit dem Registrierungsdienst für Netzwerkgeräte](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

Configuration Manager unterstützt die anforderungs-, gerätetyp- und betriebssystemabhängige Bereitstellung von Zertifikaten für unterschiedliche Zertifikatspeicher. Folgende Geräte und Betriebssysteme werden unterstützt:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop und Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Um Profile für Android-, iOS-, Windows Phone- und registrierte Windows 8.1-Geräte (und höher) bereitzustellen, müssen diese Geräte [bei Microsoft Intune registriert](https://technet.microsoft.com/en-us/library/dn646962.aspx) werden.   

In einem typischen Szenario für System Center Configuration Manager werden vertrauenswürdige Stammzertifizierungsstellenzertifikate zum Authentifizieren von WLAN- und VPN-Servern installiert, wenn für die Kommunikation die Authentifizierungsprotokolle EAP-TLS, EAP-TTLS und PEAP sowie die VPN-Tunnelprotokolle IKEv2, L2TP/IPsec und Cisco IPsec verwendet werden.  

Sie müssen sicherstellen, dass auf dem Gerät ein Stammzertifizierungsstellen-Zertifikat des Unternehmens installiert ist. Nur dann können vom Gerät mithilfe eines SCEP-Zertifikatprofils Zertifikate angefordert werden.  

Sie können eine Reihe von Einstellungen in einem SCEP-Zertifikatprofil angeben, um benutzerdefinierte Zertifikate für unterschiedliche Umgebungen oder Verbindungsanforderungen anzufordern. Der **Assistent zum Erstellen von Zertifikatprofilen** enthält zwei Seiten für Parameter für die Anmeldung. Die erste Seite **SCEP-Anmeldung**enthält Einstellungen für die Anmeldeanforderung sowie zum Installationsort des Zertifikats. Auf der zweiten Seite **Zertifikateigenschaften**wird das angeforderte Zertifikat beschrieben.  

## <a name="deploying-certificate-profiles"></a>Bereitstellen von Zertifikatprofilen  
 Beim Bereitstellen eines Zertifikatprofils werden die Zertifikatdateien im Profil auf Clientgeräten installiert. Zudem werden SCEP-Parameter bereitgestellt, und die SCEP-Anforderungen werden auf dem Clientgerät verarbeitet. Sie können Zertifikatprofile für Benutzer- oder Gerätesammlungen bereitstellen und den Zielspeicher für die einzelnen Zertifikate angeben. Durch Anwendbarkeitsregeln wird bestimmt, ob die Zertifikate auf dem Gerät installiert werden können. Beim Bereitstellen von Zertifikatprofilen für Benutzersammlungen wird durch die Affinität zwischen Benutzer und Gerät bestimmt, auf welchen Geräten der Benutzer die Zertifikate installiert werden. Wenn Zertifikatprofile, die Benutzerzertifikate enthalten, für Gerätesammlungen bereitgestellt werden, werden die Zertifikate standardmäßig auf allen primären Geräten der Benutzer installiert. Das Verhalten, dass das Zertifikat auf allen Geräten der Benutzer bereitgestellt wird, können Sie auf der Seite **SCEP-Anmeldung** des **Assistenten zum Erstellen von Zertifikatprofilen** ändern. Zudem werden Benutzerzertifikate auf Geräten, bei denen es sich um Arbeitsgruppencomputer handelt, nicht installiert.  

## <a name="monitoring-certificate-profiles"></a>Überwachen von Zertifikatprofilen  

Sie können Zertifikatprofilbereitstellungen überwachen, indem Sie Konformitätsergebnisse oder -berichte anzeigen. Diese Ansätze werden unter [Überwachen von Zertifikatprofilen in System Center Configuration Manager](/sccm/protect/deploy-use/monitor-certificate-profiles) beschrieben.


## <a name="automatic-revocation-of-certificates"></a>Automatisches Sperren von Zertifikaten  
 System Center Configuration Manager widerruft automatisch Benutzer- und Computerzertifikate, die unter den folgenden Umständen mithilfe von Zertifikatprofilen erstellt wurden:  

-   Die Verwaltung in System Center Configuration Manager wurde für dieses Gerät außer Kraft gesetzt.  

-   Das Gerät wird selektiv zurückgesetzt.  

-   Das Gerät wurde in der System Center Configuration Manager-Hierarchie gesperrt.  

 Zum Sperren der Zertifikate wird vom Standortserver ein Sperrbefehl an die ausstellende Zertifizierungsstelle gesendet. Der Grund für die Sperre ist **Vorgangsende**.  