---
title: Bereitstellen von WLAN-, VPN-, E-Mail- und Zertifikatprofilen | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie WLAN-, VPN-, E-Mail- und Zertifikatprofile in System Center Configuration Manager bereitstellen.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
caps.latest.revision: "5"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 70372d5df13034b48f3e43b766776442f1be5823
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="deploy-profiles-in-system-center-configuration-manager"></a>Bereitstellen von Profilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Profile müssen in einer oder mehreren Sammlungen bereitgestellt werden, bevor sie verwendet werden können.  

 Verwenden Sie das Dialogfeld **WLAN-Profil bereitstellen**, **VPN-Profil bereitstellen**, **Exchange ActiveSync-Profil bereitstellen** oder **Zertifikatprofil bereitstellen**, um die Bereitstellung dieser Profile zu konfigurieren. Dabei definieren Sie die Sammlung, für die das Profil bereitgestellt wird, und geben an, wie häufig das Profil auf Kompatibilität ausgewertet wird.  

> [!NOTE]  
>  Wenn Sie für denselben Benutzer mehrere Zugriffsprofile für Unternehmensressourcen bereitstellen, tritt das folgende Verhalten auf:  
>   
>  -   Wenn eine in Konflikt stehende Einstellung einen optionalen Wert enthält, wird dieser nicht an das Gerät gesendet.  
> -   Wenn eine in Konflikt stehende Einstellung einen erforderlichen Wert enthält, wird der Standardwert an das Gerät gesendet. Wenn kein Standardwert vorhanden ist, tritt beim gesamten Zugriffsprofil für die Unternehmensressource ein Fehler auf. Wenn Sie z. B. zwei E-Mail-Profile für denselben Benutzer bereitstellen und die für **Exchange ActiveSync-Host** oder **E-Mail-Adresse** angegebenen Werte unterschiedlich sind, tritt bei beiden E-Mail-Profilen ein Fehler auf, da es sich um erforderliche Einstellungen handelt.  

> -   Bevor Sie Zertifikatprofile bereitstellen können, müssen Sie zunächst die Infrastruktur konfigurieren und Zertifikatprofile erstellen. Weitere Informationen finden Sie unter den folgenden Themen:  
>   
>  -   [Configuring certificate infrastructure in System Center Configuration Manager (Konfigurieren der Zertifikatinfrastruktur in System Center Configuration Manager)](certificate-infrastructure.md)  
> -   [How to create certificate profiles in System Center Configuration Manager (So erstellen Sie Zertifikatprofile in System Center Configuration Manager)](create-certificate-profiles.md)    

> [!IMPORTANT]  
>  Beim Entfernen einer VPN-Profilbereitstellung wird sie nicht von den Clientgeräten entfernt. Soll das Profil selbst von den Geräten entfernt werden, müssen Sie dies manuell erledigen.
>   

## <a name="deploying--profiles"></a>Bereitstellen von Profilen  


1.  Wählen Sie in der System Center Configuration Manager-Konsole **Bestand und Kompatibilität** aus.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, den **Zugriff auf Unternehmensressourcen**, und wählen sie dann den entsprechenden Profiltyp aus, z.B. **WLAN-Profile**.  

3.  Wählen Sie in der Liste der Profile das Profil aus, das Sie bereitstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

4.  Geben Sie im Dialogfeld „Profil bereitstellen“ die folgenden Informationen an:  

    -   **Sammlung**: Klicken Sie auf **Durchsuchen**, um die Sammlung auszuwählen, in der Sie das Profil bereitstellen möchten.  

    -   **Warnung generieren**: Aktivieren Sie diese Option zum Konfigurieren einer Warnung, die generiert wird, sobald die Kompatibilität eines Profils zu einem bestimmten Datum und einer bestimmten Uhrzeit unterhalb eines angegebenen Prozentsatzes liegt. Sie können außerdem angeben, ob eine Warnung an System Center Operations Manager gesendet werden soll.  

    -   -   **Zufällige Verzögerung (Stunden)**: (Nur für Zertifikatprofile, die Einstellungen für das Simple Certificate Enrollment-Protokoll enthalten) Geben Sie ein Verzögerungsfenster an, um übermäßige Verarbeitung im Registrierungsdienst für Netzwerkgeräte zu vermeiden. Der Standardwert beträgt **64** Stunden.  

    -   **Geben Sie den Zeitplan für die Kompatibilitätsauswertung dieses <type>Profils** an: Geben Sie den Zeitplan an, nach dem das bereitgestellte Profil auf Clientcomputern ausgewertet wird. Dabei kann es sich um einen einfachen oder benutzerdefinierten Zeitplan handeln.  

        > [!NOTE]  
        >  Das Profil wird von Clientcomputern ausgewertet, wenn sich der Benutzer anmeldet.  

5.  Klicken Sie auf **OK**, um das Dialogfeld zu schließen und die Bereitstellung zu erstellen.

### <a name="see-also"></a>Weitere Informationen:  

[Monitor Email, Wi-Fi and VPN profiles in System Center Configuration Manager (Überwachen von WLAN-, VPN- und E-Mail-Profilen in System Center Configuration Manager)](monitor-wifi-email-vpn-profiles.md)

[Überwachen von Zertifikatprofilen in System Center Configuration Manager](monitor-certificate-profiles.md)
