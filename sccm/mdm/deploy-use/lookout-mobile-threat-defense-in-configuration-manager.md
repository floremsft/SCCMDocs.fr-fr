---
title: "Einschränken des Zugriffs basierend auf dem Risiko | Microsoft-Dokumentation"
description: "Schränken Sie den Zugriff auf Unternehmensressourcen basierend auf Gerät, Netzwerk und Anwendungsrisiko ein."
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 21841d97387f07f53993d957641f9ad892d723c2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Verwalten des Zugriffs auf Unternehmensressourcen basierend auf Gerät, Netzwerk und Anwendungsrisiko

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können den Zugriff von mobilen Geräten auf Unternehmensressourcen mithilfe einer Risikobewertung durch Lookout steuern. Lookout ist eine Lösung zum Schutz vor Gerätebedrohungen, die in Microsoft Intune integriert ist. Das Risiko basiert auf Telemetrie, die der Lookout-Dienst auf Geräten sammelt, um Sicherheitsrisiken beim Betriebssystem, installierte schädliche Apps und schädliche Netzwerkprofile zu erkennen. 

Basierend auf der Risikobewertung von Lookout, die durch die Konformitätsrichtlinien von System Center Configuration Manager (SCCM) aktiviert ist, können Sie bedingte Zugriffsrichtlinien konfigurieren und Geräte zulassen oder blockieren, die als nicht konform eingestuft wurden, da auf diesen Geräten Bedrohungen festgestellt wurden.

Die [Bereitstellung der hybriden Verwaltung mobiler Geräte (System Center Configuration Manager mit Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) bietet Ihnen die Möglichkeit, den Zugriff auf Unternehmensressourcen und -daten zu steuern. Dies basiert auf der Risikobewertung, die Lösungen zum Schutz vor Gerätebedrohungen wie Lookout zur Verfügung stellen.

## <a name="how-do-the-hybrid-mdm-deployment-and-lookout-device-threat-protection-help-protect-company-resources"></a>Wie unterstützen die Bereitstellung der hybriden Verwaltung mobiler Geräte und der Schutz vor Gerätebedrohungen mit Lookout den Schutz von Unternehmensressourcen?
Die mobile App von Lookout (Lookout for Work), die auf mobilen Geräten ausgeführt wird, erfasst Dateisysteme, Netzwerkstapel, Geräte- und Anwendungstelemetrie (sofern verfügbar), und sendet diese an den Clouddienst von Lookout zum Schutz vor Gerätebedrohungen, um die zusammengefassten Risiken mobiler Bedrohungen für Geräte zu berechnen. Sie können auch die Klassifizierung der Risikostufe der Bedrohungen in der Lookout-Konsole ändern, um sie Ihren Anforderungen anzupassen.  

Die Konformitätsrichtlinie in System Center Configuration Manager enthält nun eine neue Regel für Lookout Mobile Threat Protection, die auf Risikobewertung von Bedrohungen für Geräte von Lookout basiert. Wenn diese Regel aktiviert ist, wird das Gerät auf Konformität ausgewertet.

Wenn das Gerät als nicht konform mit der Konformitätsrichtlinie eingestuft wird, kann der Zugriff auf Ressourcen wie Exchange Online und SharePoint Online mithilfe bedingter Zugriffsrichtlinien blockiert werden. Wenn der Zugriff blockiert ist, wird den Endbenutzern eine exemplarische Vorgehensweise zur Verfügung gestellt, wie sie das Problem lösen und Zugriff auf Unternehmensressourcen erhalten. Diese exemplarische Vorgehensweise wird durch die App „Lookout for Work“ gestartet.

## <a name="supported-platforms"></a>Unterstützte Plattformen:
* **Android 4.1 und höher**, und bei Microsoft Intune registriert.
* **iOS 8 und höher**, und bei Microsoft Intune registriert.
Informationen über die Plattformen und Sprachen, die von Lookout unterstützt werden, finden Sie in diesem [Artikel](https://personal.support.lookout.com/hc/en-us/articles/114094140253).

## <a name="prerequisites"></a>Voraussetzungen:
* [Bereitstellung der hybriden Verwaltung mobiler Geräte](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)
* Ein Abonnement für Microsoft Intune und Azure Active Directory.
* Ein Konzern-Abonnement für Lookout Mobile EndPoint Security.  Weitere Informationen finden Sie unter [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="example-scenarios"></a>Beispielszenarien
Hier finden Sie einige häufige Szenarios:
### <a name="control-access-based-on-threat-from-malicious-apps"></a>Steuern des Zugriffs basierend auf Bedrohungen durch böswillige Apps:
Wenn böswillige Apps wie Schadsoftware auf dem Gerät entdeckt werden, können Sie folgende Vorgänge für diese Geräte blockieren:
* Herstellen einer Verbindung zur geschäftlichen E-Mail-Adresse, bevor die Bedrohung beseitigt ist.
* Synchronisieren von Unternehmensdateien mithilfe der App „OneDrive für die Arbeit“.
* Zugreifen auf wichtige App für das Unternehmen.

**So wird der Zugriff blockiert, wenn böswillige Apps entdeckt werden:**

![Diagramm das zeigt, wie die Richtlinie für bedingten Zugriff den Zugriff blockiert, wenn das Gerät aufgrund von böswilligen Apps auf dem Gerät als nicht konform eingestuft wird](media/config-mgr-maliciousapps_blocked.png)

**So wird die Blockierung des Geräts aufgehoben, und der Zugriff auf Unternehmensressourcen zugelassen, wenn die Bedrohung beseitigt wurde:**

![Diagramm, das zeigt, wie die Richtlinie für bedingten Zugriff den Zugriff erlaubt, wenn das Gerät nach der Beseitigung als konform eingestuft wird](media/config-mgr-maliciousapps-unblocked.png)
### <a name="control-access-based-on-threat-to-network"></a>Steuern des Zugriffs basierend auf Bedrohung für das Netzwerk:
Erkennen Sie Bedrohungen für Ihr Netzwerk wie Man-in-the-Middle-Angriffe, und schränken Sie den Zugriff auf WLAN-Netzwerke basierend auf den Risiken für Geräte ein.

**Zugriff auf Netzwerk über WLAN ist blockiert:**

![Diagramm das zeigt, wie bedingter Zugriff den Zugriff auf WLAN basierend auf Netzwerkbedrohungen blockiert](media/config-mgr-network-wifi-blocked.png)

**Zugriff nach Beseitigung gewährt:**

![Diagramm, das zeigt, wie bedingter Zugriff den Zugriff nach Beseitigung der Bedrohung erlaubt](media/config-mgr-network-wifi-unblocked.png)
### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Steuern des Zugriffs auf SharePoint Online basierend auf Netzwerkbedrohungen:

Erkennen Sie Bedrohungen für Ihr Netzwerk wie Man-in-the-Middle-Angriffe, und verhindern Sie die Synchronisierung von Unternehmensdateien basierend auf den Risiken für Geräte.

**Zugriff auf SharePoint Online basierend auf Netzwerkbedrohungen, die auf dem Gerät gefunden wurden, blockiert:**

![Diagramm, das zeigt, wie bedingter Zugriff den Zugriff des Geräts auf SharePoint Online basierend auf der Bedrohungserkennung blockiert](media/config-mgr-network-spo-blocked.png)


**Zugriff nach Beseitigung gewährt:**

![Diagramm, das zeigt, wie bedingter Zugriff den Zugriff nach Beseitigung der Netzwerkbedrohung erlaubt](media/config-mgr-network-spo-unblocked.png)

## <a name="next-steps"></a>Nächste Schritte
Hier sind die wichtigsten Schritte, die Sie ausführen müssen, um diese Lösung zu implementieren:
1.  [Set up your subscription with Lookout mobile threat protection (Einrichten Ihres Abonnements mit Lookout Mobile Threat Protection)](set-up-your-subscription-with-lookout.md)
2.  [Enable Lookout MTP connection in Intune (Aktivieren einer Lookout MTP-Verbindung in Intune)](enable-lookout-connection-in-intune.md)
3.  [Configure and deploy Lookout for work application (Konfigurieren und Bereitstellen von Lookout for Work-Anwendungen)](configure-and-deploy-lookout-for-work-apps.md)
4.  [Configure compliance policy (Konfigurieren von Konformitätsrichtlinien)](enable-device-threat-protection-rule-compliance-policy.md)
5.  [Behandeln von Problemen bei der Lookout-Integration](troubleshoot-lookout-integration.md)
