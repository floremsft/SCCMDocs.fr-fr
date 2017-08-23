---
title: "Sicherheit und Datenschutz für Zertifikatprofile | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über bewährte Sicherheitsmethoden für die Verwaltung von Zertifikatprofilen für Benutzer und Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: c51787ad3fa0bdb285017cfab1ca6931afba9ea6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-certificate-profiles-in-system-center-configuration-manager"></a>Sicherheit und Datenschutz für Zertifikatprofile in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


##  <a name="security-best-practices-for-certificate-profiles"></a>Bewährte Sicherheitsmethoden für Zertifikatprofile  
 Verwenden Sie bei der Verwaltung von Zertifikatprofilen für Benutzer und Geräte die folgenden bewährten Sicherheitsmethoden.  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Bestimmen und beachten Sie die bewährten Sicherheitsmethoden für den Registrierungsdienst für Netzwerkgeräte. Dazu zählt die Konfiguration der NDES-Website in Internetinformationsdienste (IIS), um SSL zu erfordern und Clientzertifikate zu ignorieren.|Weitere Informationen finden Sie unter [Network Device Enrollment Service Guidance (Anleitung zum Registrierungsdienst für Netzwerkgeräte)](http://go.microsoft.com/fwlink/p/?LinkId=309016) in der Bibliothek zu Active Directory-Zertifikatdiensten auf der TechNet-Website.|  
|Wählen Sie bei der Konfiguration von SCEP-Zertifikatprofilen die sichersten Optionen aus, die von den Geräten und Ihrer Infrastruktur unterstützt werden können.|Bestimmen, implementieren und beachten Sie die bewährten Sicherheitsmethoden, die für Ihre Geräte und die Infrastruktur empfohlen wurden.|  
|Geben Sie manuell die Affinität zwischen Benutzer und Gerät an, statt zuzulassen, dass die Benutzer das primäre Gerät selbst bestimmen. Aktivieren Sie darüber hinaus die verwendungsbasierte Konfiguration nicht.|Wenn Sie die Option **Zertifikatregistrierung nur auf dem primären Gerät des Benutzers zulassen** in einem SCEP-Zertifikatprofil anklicken, betrachten Sie die von Benutzern oder vom Gerät gesammelten Informationen nicht als autoritativ. Wenn Sie SCEP-Zertifikatprofile mit dieser Konfiguration bereitstellen und die Affinität zwischen Benutzer und Gerät nicht von einem vertrauenswürdigen Administrator angegeben wurde, kann dies zu Rechteerweiterungen führen, und nicht autorisierten Benutzern werden möglicherweise Zertifikate zur Authentifizierung erteilt.<br /><br /> **Hinweis:** Wenn Sie die verwendungsbasierte Konfiguration zulassen, werden diese Informationen mithilfe von Statusmeldungen erfasst, die nicht von System Center Configuration Manager geschützt werden. Sie können diese Bedrohung durch SMB-Signaturen oder IPsec zwischen Clientcomputern und dem Verwaltungspunkt verringern.|  
|Fügen Sie den Zertifikatvorlagen nicht die Berechtigungen Lesen und Anmelden für Benutzer hinzu, oder konfigurieren Sie den Zertifikatregistrierungspunkt so, dass die Überprüfung von Zertifikatvorlagen übersprungen wird.|Obwohl Configuration Manager die zusätzliche Überprüfung unterstützt, wenn Sie die Sicherheitsberechtigungen zum Lesen und Registrieren für Benutzer hinzufügen, und Sie den Zertifikatregistrierungspunkt so konfigurieren können, dass die Überprüfung übersprungen wird, wenn keine Authentifizierung möglich ist, ist keine dieser Konfigurationen eine bewährte Sicherheitsmethode. Weitere Informationen finden Sie unter [Planen der Berechtigungen von Zertifikatvorlagen für Zertifikatprofile in System Center Configuration Manager](../../protect/plan-design/planning-for-certificate-template-permissions.md).|  

## <a name="privacy-information-for-certificate-profiles"></a>Informationen zum Datenschutz für Zertifikatprofile  
 Sie können Zertifikatprofile verwenden, um Zertifikate der Stammzertifizierungsstelle und Clientzertifikate bereitzustellen, und dann auswerten, ob die Geräte nach der Anwendung der Profile Kompatibilität erreichen. Der Verwaltungspunkt sendet Kompatibilitätsinformationen an den Standortserver, die dann von System Center Configuration Manager in der Standortdatenbank gespeichert werden. Zu den Kompatibilitätsinformationen zählen Zertifikateigenschaften wie Antragstellername und Fingerabdruck. Die Informationen werden verschlüsselt, wenn sie von Geräten an den Verwaltungspunkt gesendet werden, sie werden aber nicht in einem verschlüsselten Format in der Standortdatenbank gespeichert. Die Informationen verbleiben in der Datenbank, bis sie mit dem Standortwartungstask **Veraltete Konfigurationsverwaltungsdaten löschen** nach dem Standardintervall von 90 Tagen gelöscht werden. Sie können das Löschintervall konfigurieren. Die Kompatibilitätsinformationen werden nicht an Microsoft gesendet.  

 In Zertifikatprofilen werden Informationen verwendet, die von Configuration Manager mithilfe der Ermittlung gesammelt werden. Weitere Informationen zu Datenschutzinformationen zur Ermittlung finden Sie im Abschnitt **Datenschutzinformationen zur Ermittlung** unter [Security and privacy for System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

> [!NOTE]  
>  Für Benutzer oder Geräte ausgestellte Zertifikate lassen möglicherweise Zugriff auf vertrauliche Informationen zu.  

 Standardmäßig werden Zertifikatprofile von Geräten nicht ausgewertet. Darüber hinaus müssen Sie die Zertifikatprofile konfigurieren und sie dann Benutzern oder Geräten bereitstellen.  

 Berücksichtigen Sie beim Konfigurieren der Zertifikatprofile Ihre Datenschutzanforderungen.  
