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
ms.openlocfilehash: 250671660c1c6da0ca9b593b06b8f344dfe17ad6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Verwalten des Zugriffs auf Unternehmensressourcen basierend auf Gerät, Netzwerk und Anwendungsrisiko

*Gilt für: System Center Configuration Manager (Current Branch)*

Mobile Threat Defense-Connectors geben Ihnen die Möglichkeit, einen Mobile Threat Defense-Hersteller Ihrer Wahl als Informationsquelle für Ihre Kompatibilitätsrichtlinien und bedingte Zugriffsregeln zu nutzen. So haben IT-Administratoren die Möglichkeit, eine Schutzschicht um ihre Unternehmensressourcen zu schaffen, wie etwa Exchange oder Sharepoint, besonders für gefährdete mobile Geräte.

## <a name="what-problem-does-this-solve"></a>Welches Problem wird dadurch gelöst?

Unternehmen müssen sensible Daten vor potenziellen Gefahren schützen. Darunter fallen physische, App-basierte und Netzwerk-basierte Bedrohungen, sowie Sicherheitsrisiken beim Betriebssystem.
In der Vergangenheit waren Unternehmen beim Schutz ihrer PCs vor Angriffen proaktiv, während mobile Geräte unüberwacht und ungeschützt blieben. Mobile Plattformen verfügen über einen integrierten Schutz des Betriebssystems durch Techniken wie die Isolierung von Apps oder überprüfte App Stores für Heimanwender, aber diese Plattformen sind trotzdem noch anfällig für komplexe Angriffe. Heute verwenden Angestellte Geräte für die Arbeit und benötigen Zugriff auf vertrauliche Informationen. Deshalb müssen Geräte vor immer komplexeren Angriffen geschützt werden.

Die [Bereitstellung der hybriden Verwaltung mobiler Geräte (System Center Configuration Manager mit Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) bietet Ihnen die Möglichkeit, den Zugriff auf Unternehmensressourcen und -daten zu steuern. Dies basiert auf der Risikobewertung, die Lösungen zur Verfügung stellen, die Mobile Threat Defense-Partner bieten.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>So funktionieren die Intune Threat Defense-Connectors

Der Connector schützt Unternehmensressourcen mithilfe eines Kommunikationskanals zwischen Intune und Ihrem ausgewählten Mobile Threat Defense-Hersteller. Partner von Intune Mobile Threat Defense bieten intuitive, leicht bereitzustellende Anwendungen für mobile Geräte, die aktiv Bedrohungsinformationen scannen und analysieren, um diese in Intune freizugeben, entweder für Berichte oder für Erzwingungen. Wenn beispielsweise eine verbundene Mobile Threat Defense-Anwendung dem Mobile Threat Defense-Hersteller meldet, dass ein Telefon in Ihrem Netzwerk aktuell mit einem Netzwerk verbunden ist, das nicht gegen „Man-in-the-Middle“-Angriffe geschützt ist, werden diese Informationen freigegeben und einer angemessenen Risikostufe zugeordnet (niedrig/mittel/hoch). Dies kann wiederum mit Ihren konfigurierten Einstellungen für berücksichtigte Risikostufen in Intune abgeglichen werden, um festzustellen, ob bestimmte Ressourcen Ihrer Wahl gesperrt werden sollten, während das Gerät gefährdet ist.

## <a name="sample-scenarios"></a>Beispielszenarios

Wenn ein Gerät von der Mobile Threat Defense-Lösung als infiziert eingestuft wird:

![Mobile Threat Defense: Infiziertes Gerät](../media/mtp/MTD-image-1.png)

Der Zugriff wird ermöglicht, wenn das Gerät wiederhergestellt ist:

![Mobile Threat Defense: Zugriff gewährt](../media/mtp/MTD-image-2.png)

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie den Zugriff auf Unternehmensressourcen basierend auf Gerät, Netzwerk und Anwendungsrisiko schützen können mithilfe von:

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)