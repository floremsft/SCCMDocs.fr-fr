---
title: "Registrieren von Geräten | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über Geräteregistrierungsmethoden für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
caps.latest.revision: "6"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4abaef35969ef1a5340ae8ca8aa5699cd3942642
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Registrieren von Geräten für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zum Verwalten von Computern und Geräten mit der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager müssen die Geräte registriert werden, damit Configuration Manager für Verwaltungstasks mit den Geräten kommunizieren kann. Configuration Manager bietet zwei Methoden zum Registrieren von Geräten:  

-   **Benutzerregistrierung** : Bei dieser Methode initiieren Benutzer den Registrierungsvorgang auf ihren Geräten. Damit die Benutzerregistrierung erfolgreich ist, muss auf dem Gerät ein vertrauenswürdiges Stammzertifikat installiert sein, und der Benutzer muss für die Registrierung von Configuration Manager bereitgestellt sein.  Zum Registrieren eines Geräts braucht der Benutzer lediglich seine Unternehmensanmeldeinformationen anzugeben, und das Gerät wird für die Verwaltung registriert.  

     Weitere Informationen finden Sie unter [Informationen zur Registrierung von Geräten mit der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

-   **Massenregistrierung** : Bei dieser Methode braucht der Benutzer des Geräts die Registrierung nicht zu initiieren. Stattdessen wird ein Massenregistrierungspaket in Configuration Manager erstellt, auf dem Gerät abgelegt und geöffnet. Das Paket stellt nach dem Öffnen die erforderlichen Informationen zum Registrieren des Geräts bereit.  

     Weitere Informationen finden Sie unter [Massenregistrierung von Geräten mit der lokalen Verwaltung von Geräten in System Center Configuration Manager](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md).  

 > [!NOTE]  
>  Configuration Manager Current Branch unterstützt die Registrierung bei der lokalen Verwaltung mobiler Geräte für Geräte, auf denen folgende Betriebssysteme ausgeführt werden:  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team 
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise   
