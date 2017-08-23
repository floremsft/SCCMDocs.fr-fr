---
title: "Bewährte Methoden für Sammlungen | Microsoft-Dokumentation"
description: "Erhalten Sie bewährte Methoden für Sammlungen in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
caps.latest.revision: "4"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: fd62af3910c0745e0f1105417701b894e10cbbac
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>Bewährte Methoden für Sammlungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die folgenden bewährten Methoden für Sammlungen in System Center Configuration Manager.  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>Verwenden Sie keine inkrementellen Updates bei einer größeren Anzahl von Sammlungen  
 Wenn Sie die Option **Inkrementelle Updates für diese Sammlung verwenden** für zahlreiche Sammlungen aktivieren, können durch diese Konfiguration Bewertungsverzögerungen bewirkt werden. Dies gilt ab einem Schwellenwert von etwa 200 Sammlungen in Ihrer Hierarchie. Die genaue Anzahl hängt von folgenden Faktoren ab:  

-   Gesamtzahl der Sammlungen  

-   Häufigkeit, mit der neue Ressourcen der Hierarchie hinzugefügt und darin geändert werden  

-   Anzahl der Clients in Ihrer Hierarchie  

-   Komplexität der Sammlungsmitgliedschaftsregeln in Ihrer Hierarchie  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Achten Sie darauf, dass die Wartungsfenster für die Bereitstellung wichtiger Softwareupdates groß genug sind.  
 Durch Wartungsfenster für Gerätesammlungen können Sie festlegen, dass Software nur zu bestimmten Zeiten von Configuration Manager auf diesen Geräten installiert werden kann. Wenn das Wartungsfenster zu klein ist, können wichtige Softwareupdates möglicherweise nicht vom Client installiert werden. Dies erhöht das Risiko eines Angriffs, der von diesem Softwareupdate verhindert würde.  
