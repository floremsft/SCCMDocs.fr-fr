---
title: Barrierefreiheit | Microsoft-Dokumentation
description: "Enthält Informationen zu den Funktionen, die System Center Configuration Manager für Menschen mit Behinderung zugänglich machen."
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: ca518796477dda149a9f4c0ebd65f0a082eab806
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="accessibility-features-in-system-center-configuration-manager"></a>Barrierefreiheitsfunktionen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager enthält Funktionen, durch die es für Menschen mit Behinderungen zugänglich gemacht wird.


## <a name="bkmk_aconsole"></a> Barrierefreiheitsfunktionen für die Configuration Manager-Konsole  

**Tastenkombinationen und Verbesserungen ab Version 1706**

|Tastenkombination|  Zweck|
|--------|--------|  
|STRG+M|legt den Fokus auf den Hauptbereich in der Mitte fest|
|STRG+T|legt den Fokus auf den obersten Knoten im Navigationsbereich fest Wenn sich der Fokus bereits in diesem Bereich befand, wird er auf den letzten besuchten Knoten festgelegt.|
|STRG+I|legt den Fokus auf die Breadcrumb-Leiste unter dem Menüband fest|
|STRG+L|legt den Fokus auf das Feld **Suchen** fest, sofern verfügbar|
|STRG+D|legt den Fokus auf den Detailbereich fest, sofern verfügbar|
|ALT     |schaltet den Fokus auf das Menüband ein und aus|


- Verbesserte Navigation im Navigationsbereich, wenn Sie die Buchstaben eines Knotennamens eingeben.
- Die Tastaturnavigation durch die Hauptansicht und das Menüband erfolgt jetzt kreisförmig.
- Die Tastaturnavigation im Detailbereich erfolgt jetzt kreisförmig. Um zum vorherigen Objekt oder Bereich zurückzukehren, drücken Sie STRG+D und dann UMSCHALT+TAB.
- Nach der Aktualisierung einer Arbeitsbereichsansicht wird der Fokus auf den Hauptbereich des jeweiligen Arbeitsbereichs festgelegt.
- Ein Problem beim Aktivieren von Sprachausgaben zum Mitteilen der Namen von Listenelementen wurde behoben.
- Es wurden barrierefreie Namen für mehrere Steuerelemente auf der Seite hinzugefügt, die es Sprachausgaben ermöglichen, wichtige Informationen mitzuteilen.


**Die folgenden Tastenkombinationen sind für alle Versionen verfügbar**

- Verwenden Sie zum Zugriff auf einen Arbeitsbereich die folgenden Tastenkombinationen:  

|Tastenkombination| Arbeitsbereich|
|--------|--------|  
|STRG+1| Bestand und Kompatibilität|
|STRG+2|  Softwarebibliothek|
|STRG+3|  Überwachung|
|STRG+4|  Verwaltung|


-   Wählen Sie zum Zugriff auf ein Arbeitsbereichsmenü die TAB-TASTE, bis der Fokus auf dem Symbol „Erweitern/Reduzieren“ liegt. Wählen Sie die NACH-UNTEN-TASTE, um auf das Arbeitsbereichsmenü zuzugreifen.  

-   Verwenden Sie zum Navigieren durch ein Arbeitsbereichsmenü die Pfeiltasten.  

-   Verwenden Sie zum Zugriff auf die verschiedenen Bereiche im Arbeitsbereich die TAB-TASTE und die Tastenkombination UMSCHALT+TAB. Verwenden Sie zum Navigieren in einem Bereich des Arbeitsbereichs, z. B. im Menüband, die Pfeiltasten.  

-   Verwenden Sie dreimal UMSCHALT+TAB, um auf die Adressleiste zuzugreifen, wenn sich der Fokus auf dem Verzeichnisknoten befindet.  

-   Auf einer Assistenten- oder Eigenschaftenseite können Sie per Tastenkombination durch die Felder navigieren. Wählen Sie die ALT-TASTE plus das jeweils unterstrichene Zeichen (ALT+_), um ein bestimmtes Feld auszuwählen.     

-  Geben Sie den ersten Buchstaben des Namens eines Knotens ein, um zu den verschiedenen Knoten eines Arbeitsbereichs zu navigieren. Jeder Tastendruck verschiebt den Cursor auf den nächsten Knoten, der mit diesem Buchstaben beginnt. Wenn Sie eine Sprachausgabe verwenden, liest der Reader den Namen des Knotens.

> [!NOTE]  
>  Die in diesem Abschnitt enthaltenen Informationen gelten ggf. nur für Benutzer, die Microsoft-Produkte in den USA lizenzieren lassen. Wenn Sie dieses Produkt außerhalb der USA erworben haben, enthält das Softwarepaket eine Karte mit zusätzlichen Informationen, der die Kontaktinformationen für den Microsoft-Support zu entnehmen sind. Diese Informationen finden Sie auch auf der [Microsoft-Website zur Barrierefreiheit](http://go.microsoft.com/fwlink/?LinkId=8431). Setzen Sie sich mit der Niederlassung in Ihrer Nähe in Verbindung, um herauszufinden, ob die in diesem Abschnitt aufgeführten Produkte und Dienste in Ihrem Land bzw. Ihrer Region verfügbar sind. Informationen zur Barrierefreiheit stehen auch in anderen Sprachen (einschl. Japanisch und Französisch) zur Verfügung.  

##  <a name="bkmk_ahelp"></a> Barrierefreiheitsfunktionen für die Configuration Manager-Hilfe  
 Die Configuration Manager-Hilfe ist dank Barrierefreiheitsfunktionen einer größeren Zahl von Benutzern zugänglich. Dazu zählen u.a. Benutzer mit eingeschränkter Beweglichkeit der Hände, Sehbehinderungen oder anderen Behinderungen.  

|Zweck|Tastenkombination|  
|----------------|--------------------------------|  
|Anzeigen von Hilfe|F1|  
|Verschieben des Cursors zwischen Hilfethemen- und Navigationsbereich (Registerkarten **Inhalt**, **Suchen**und **Index** )|F6|  
|Wechsel zwischen Registerkarten (z.B. **Inhalt**, **Suchen** und **Index**) im Navigationsbereich|ALT + auf der Registerkarte unterstrichener Buchstabe|  
|Auswählen des nächsten ausgeblendeten Texts oder Hyperlinks|Registerkarte|  
|Auswählen des vorherigen ausgeblendeten Texts oder Hyperlinks|UMSCHALT+TAB|  
|Ausführen der Aktion für die ausgewählte Option Alle einblenden oder Alle ausblenden, für ausgeblendeten Text oder Hyperlink|EINGABETASTE|  
|Anzeigen des Menüs **Optionen** für den Zugriff auf die Befehle der Hilfesymbolleiste|ALT+O|  
|Ein- oder Ausblenden des Bereichs mit den Registerkarten **Inhalt**, **Suchen** und **Index**|ALT+O und dann T wählen|  
|Anzeigen des zuvor angezeigten Themas|ALT+O und dann B wählen|  
|Anzeigen des nächsten Themas in einer Serie nacheinander angezeigter Themen|ALT+O und dann F wählen|  
|Zurück zur angegebenen Startseite|ALT+O und dann H wählen|  
|Abbrechen des Öffnens eines Hilfethemas im Hilfefenster, z.B. um das Herunterladen einer Webseite zu verhindern|ALT+O und dann S wählen|  
|Öffnen des Dialogfelds **Internetoptionen** für Windows Internet Explorer, in dem Sie die Barrierefreiheiteinstellungen ändern können|ALT+O und dann I wählen|  
|Aktualisieren des Themas, z. B. einer verlinkten Webseite|ALT+O und dann R wählen|  
|Drucken aller Themen in einem Buch bzw. des ausgewählten Themas|ALT+O und dann P wählen|  
|Schließen des Hilfefensters|ALT+F4|  

#### <a name="to-change-the-appearance-of-a-help-topic"></a>So ändern Sie die Darstellung eines Hilfethemas  

1.  Öffnen Sie das Hilfefenster, um die in der Hilfe verwendeten Farben, Schriftschnitte und Schriftgrade anzupassen.  

2.  Wählen Sie **Optionen** und dann **Internetoptionen**.  

3.  Auf der Registerkarte **Allgemein** wählen Sie **Eingabehilfen**. Aktivieren Sie die Optionen **Farbangaben auf Webseiten ignorieren**, **Schriftartangaben auf Webseiten ignorieren** und **Schriftgradangaben auf Webseiten ignorieren**. Sie können auch die Einstellungen aus einem eigenen Stylesheet verwenden.  

#### <a name="to-change-the-color-of-the-background-or-text-in-help"></a>So ändern Sie die Hintergrund- oder Textfarbe in der Hilfe  

1.  Öffnen Sie das Hilfefenster.  

2.  Wählen Sie **Optionen** und dann **Internetoptionen**.  

3.  Auf der Registerkarte **Allgemein** wählen Sie **Eingabehilfen**. Aktivieren Sie das Kontrollkästchen **Farbangaben auf Webseiten ignorieren**. Sie können auch die Einstellungen aus einem eigenen Stylesheet verwenden.  

4.  Wählen Sie zum Anpassen der Farben, die in der Hilfe verwendet werden, auf der Registerkarte **Allgemein** die Option **Farben**. Deaktivieren Sie das Kontrollkästchen **Windows-Farben verwenden**, und wählen Sie dann die gewünschten Farben für Text und Hintergrund aus.  

    > [!NOTE]  
    >  Wenn Sie die Hintergrundfarbe der Hilfethemen im Hilfefenster ändern, wirkt sich die Änderung auch auf die Hintergrundfarbe für Webseiten in Windows Internet Explorer aus.  

#### <a name="to-change-the-font-in-help"></a>So ändern Sie die Schriftart in der Hilfe  

1.  Öffnen Sie das Hilfefenster.  

2.  Wählen Sie **Optionen** und dann **Internetoptionen**.  

3.  Auf der Registerkarte **Allgemein** wählen Sie **Eingabehilfen**. Wenn Sie dieselben Einstellungen verwenden möchten wie in Ihrer Windows Internet Explorer-Instanz, aktivieren Sie die Kontrollkästchen **Schriftartangaben auf Webseiten ignorieren** und **Schriftgradangaben auf Webseiten ignorieren**. Sie können auch die Einstellungen aus einem eigenen Stylesheet verwenden.  

4.  Wählen Sie auf der Registerkarte **Allgemein** die Option **Schriftarten** und anschließend die gewünschte Schriftart, um die in der Hilfe verwendete Schriftart anzupassen.  

    > [!NOTE]  
    >  Wenn Sie die Farbe der Hilfethemen im Hilfefenster ändern, wirkt sich die Änderung auch auf die Farbe für Webseiten in Windows Internet Explorer aus.  
