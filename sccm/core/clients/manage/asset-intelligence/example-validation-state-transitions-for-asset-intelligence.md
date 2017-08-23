---
title: "Beispiel-Überprüfungszustandsübergänge für Asset Intelligence | Microsoft-Dokumentation"
description: "Beispiele für Überprüfungsstatusübergänge für Asset Intelligence in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: f280e06f34c0ed355b7c2652c571e36eb6684c59
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="example-validation-state-transitions-for-asset-intelligence-in-system-center-configuration-manager"></a>Beispiel-Überprüfungszustandsübergänge für Asset Intelligence in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Überprüfungszustände für Asset Intelligence in System Center Configuration Manager sind nicht statisch und können sich durch Verwaltungsaktionen, die die im Asset Intelligence-Katalog gespeicherten Daten beeinflussen, ändern. Dieses Thema enthält Beispiele für mögliche Überprüfungsstatusübergänge.

##  <a name="BKMK_UncategorizedIsCategorized"></a> Nicht kategorisiertes Katalogelement wird vom Administrator kategorisiert  

|**Zustandsübergang**|**Beschreibung des Zustandsübergangs**|  
|--------------------------|--------------------------------------|  
|**Nicht kategorisiert**|Ein inventarisierter Softwaretitel, der noch nicht von System Center Online kategorisiert wurde oder vom Administrator in den Asset Intelligence-Katalog eingetragen wurde.|  
|**Nicht kategorisierte** auf **Benutzerdefinierten**|Das nicht kategorisierte Element wird vom Administrator kategorisiert.|  

##  <a name="BKMK_CategorizedIsReCategorized"></a> Kategorisiertes Katalogelement wird vom Administrator neu kategorisiert  

|**Zustandsübergang**|**Beschreibung des Zustandsübergangs**|  
|--------------------------|--------------------------------------|  
|**Überprüft**|Der Katalogeintrag wurde von System Center Online-Entwicklern definiert und ist im Asset Intelligence-Katalog vorhanden.|  
|**Überprüft** zu **Benutzerdefiniert**|Das kategorisierte Katalogelement wird vom Administrator neu kategorisiert.|  

> [!NOTE]  
>  Da die von System Center Online erhaltenen Kategorisierungsinformationen in der Datenbank gespeichert werden und nicht gelöscht werden können, kann der Administrator zu einem späteren Zeitpunkt wieder auf die System Center Online-Kategorisierung zurückgreifen.  

##  <a name="BKMK_UserDefinedIsRecategorized"></a> Benutzerdefiniertes Katalogelement wird von System Center Online neu kategorisiert  

|**Zustandsübergang**|**Beschreibung des Zustandsübergangs**|  
|--------------------------|--------------------------------------|  
|**Nicht kategorisiert**|Ein inventarisierter Softwaretitel, der noch nicht von System Center Online oder vom Administrator kategorisiert wurde, wird in den Asset Intelligence-Katalog eingegeben.|  
|**Benutzerdefiniert**|Das nicht kategorisierte Element wird vom Administrator kategorisiert.|  
|**Benutzerdefiniert** zu **Aktualisierbar**|Ein benutzerdefiniertes Katalogelement wurde von System Center Online bei den darauffolgenden manuellen Massenaktualisierungen des Asset Intelligence-Katalogs anders kategorisiert.<br /><br /> Mittels des Dialogfelds **Auflösung des Konflikts zwischen Softwaredetails** kann der Administrator festlegen, ob die neuen Kategorisierungsinformationen oder der vorherige benutzerdefinierte Wert verwendet werden sollen.|  
|**Aktualisierbar** zu **Überprüft**|Mittels des Dialogfelds **Auflösung des Konflikts zwischen Softwaredetails** kann der Administrator die neuen Kategorisierungsinformationen verwenden, die bei der vorherigen Katalogaktualisierung von System Center Online übermittelt wurden.|  
|oder||  
|**Aktualisierbar** zu **Benutzerdefiniert**|Mittels des Dialogfelds **Auflösung des Konflikts zwischen Softwaredetails** kann der Administrator den vorherigen benutzerdefinierten Wert verwenden.|  

> [!NOTE]  
>  Da die von System Center Online erhaltenen Kategorisierungsinformationen in der Datenbank gespeichert werden und nicht gelöscht werden können, kann der Administrator zu einem späteren Zeitpunkt wieder auf die System Center Online-Kategorisierung zurückgreifen.  

##  <a name="BKMK_UncategorizedIsSubmitted"></a> Nicht kategorisiertes Katalogelement wird zur Kategorisierung an System Center Online übermittelt  

|**Zustandsübergang**|**Beschreibung des Zustandsübergangs**|  
|--------------------------|--------------------------------------|  
|**Nicht kategorisiert**|Ein inventarisierter Softwaretitel, der noch nicht von System Center Online oder vom Administrator kategorisiert wurde, wird in die Asset Intelligence-Datenbank eingegeben.|  
|**Nicht kategorisiert** zu **Ausstehend**|Das nicht kategorisierte Element wird zur Kategorisierung vom Administrator an System Center Online übermittelt.|  
|**Ausstehend** zu **Überprüft**|Das Element wird von System Center Online kategorisiert. Vom Administrator wird das Element mithilfe einer Massenkatalogaktualisierung oder einer Asset Intelligence-Katalogsynchronisierung in den Asset Intelligence-Katalog importiert. Beide sind durch Verwendung der Standortsystemrolle für den Asset Intelligence-Synchronisierungspunkt verfügbar.|  

##  <a name="BKMK_UserDefinedIsSubmitted"></a> Benutzerdefiniertes Katalogelement wird zur Kategorisierung an System Center Online übermittelt  

|**Zustandsübergang**|**Beschreibung des Zustandsübergangs**|  
|--------------------------|--------------------------------------|  
|**Nicht kategorisiert**|Ein inventarisierter Softwaretitel, der noch nicht von einem Administrator oder von System Center Online kategorisiert wurde, wird in die Asset Intelligence-Datenbank eingegeben.|  
|**Benutzerdefiniert**|Das nicht kategorisierte Element wurde kategorisiert.|  
|**Benutzerdefiniert** zu **Ausstehend**|Das benutzerdefinierte Element wird zur Kategorisierung an System Center Online übermittelt.|  
|**Ausstehend** zu **Aktualisierbar**|Ein benutzerdefiniertes Katalogelement wurde von System Center Online während einer nachfolgenden Katalogsynchronisierung anders kategorisiert. Sie können mithilfe der Aktion **Konflikt beheben** entscheiden, ob die neuen Kategorisierungsinformationen oder der vorherige benutzerdefinierte Wert verwendet werden sollen. Weitere Informationen zum Lösen von Konflikten finden Sie unter [Softwaredetailkonflikte lösen](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|**Aktualisierbar** zu **Überprüft**|Verwenden Sie die Aktion **Konflikt beheben** , und wählen Sie die neuen Kategorisierungsinformationen aus, die bei der vorherigen Katalogaktualisierung von System Center Online übermittelt wurden. Weitere Informationen zum Lösen von Konflikten finden Sie unter [Softwaredetailkonflikte lösen](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|oder||  
|**Aktualisierbar** zu **Benutzerdefiniert**|Verwenden Sie die Aktion **Konflikt beheben** , und verwenden Sie den vorherigen benutzerdefinierten Wert. Weitere Informationen zum Lösen von Konflikten finden Sie unter [Softwaredetailkonflikte lösen](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  

> [!NOTE]  
>  Da die von System Center Online erhaltenen Kategorisierungsinformationen in der Datenbank gespeichert werden und nicht gelöscht werden können, können Sie zu einem späteren Zeitpunkt wieder auf die System Center Online-Kategorisierung zurückgreifen.  
