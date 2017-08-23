---
title: "Konfigurieren von iOS-Apps mit Konfigurationsrichtlinien für Apps | Microsoft-Dokumentation"
description: "Vermeidung von Konfigurationsproblemen auf Geräten, die iOS 8 oder höher ausführen, durch Bereitstellung von Richtlinien zur Konfiguration von Apps an Benutzer vor dem Ausführen von Apps."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0a78038-ea22-4826-9c07-1771b7dd2e8d
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 50aea2afaf34974ca92ac58b6569bff56403a9ab
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="apply-settings-to-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Einstellungen anwenden für iOS-Apps mit Konfigurationsrichtlinien in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Sie können Konfigurationsrichtlinien für Apps in System Center Configuration Manager verwenden, um Einstellungen bereitzustellen, die beim Ausführen einer App durch den Benutzer erforderlich sein können. Beispielsweise kann eine App vom Benutzer Folgendes anfordern:
- Eine benutzerdefinierte Portnummer
- Spracheinstellungen
- Sicherheitseinstellungen
- Brandingeinstellungen wie z.B. ein Unternehmenslogo

Wenn der Benutzer die Einstellungen falsch eingibt, liegt die Last, sie zu beheben, auf Ihrem Help Desk, und die App-Bereitstellung ist langsam.
Zur Vermeidung dieser Probleme können Sie App-Konfigurationsrichtlinien verwenden, um erforderliche Einstellungen für Benutzer bereitzustellen, bevor sie die App ausführen. Die Einstellungen werden automatisch einem Benutzer zugeordnet. Der Benutzer muss keine Maßnahmen ergreifen.
Zur Verwendung einer App-Konfigurationsrichtlinie in Configuration Manager, verknüpfen Sie eine Richtlinie mit einem Bereitstellungstyp, wenn Sie die App bereitstellen, anstatt die Konfigurationsrichtlinien direkt für Benutzer und Geräte bereitzustellen. Die Richtlinieneinstellungen werden immer dann verwendet, wenn die App danach sucht (in der Regel beim ersten Ausführen der App).

Konfigurationsrichtlinien für Apps sind derzeit nur auf Geräten mit iOS 8 und höher verfügbar, und für die folgenden Anwendungstypen:

- **App-Paket für iOS (*IPA-Datei)**
- **App-Paket für iOS aus App Store**

Weitere Informationen zu App-Installationstypen finden Sie unter [Einführung in die Anwendungsverwaltung](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Erstellen einer Konfigurationsrichtlinie für Apps

1. Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **App-Konfigurationsrichtlinien** aus.
2. Wählen Sie auf der Registerkarte **Start** in der Gruppe **App-Konfigurationsrichtlinien** **Neue App-Konfigurationsrichtlinie erstellen** aus.
3. Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen einer App-Konfigurationsrichtlinie die folgenden Richtlinieninformationen an:
  - **Name**. Geben Sie einen eindeutigen Namen für die Richtlinie ein.
  - **Beschreibung**. Zur leichteren Identifizierung der Richtlinie können Sie optional eine Beschreibung hinzufügen.
  - **Zugewiesene Kategorien zum leichteren Suchen und Filtern**. Wählen Sie optional zum Erstellen und Zuweisen von Kategorien für die Richtlinie **Kategorien** aus. Kategorien machen es einfacher für Sie, Elemente in der Configuration Manager-Konsole zu sortieren und zu finden.
4. Wählen Sie auf der Seite **iOS-Richtlinie** aus, wie Sie die Informationen zur Konfigurationsrichtlinie angeben wollen:
  - **Name und Wert-Paare angeben**. Sie können diese Option für Daten der Eigenschaftsliste verwenden, die keine Schachtelung verwenden.

      *Name und Wert-Paare angeben*
        1. Wählen Sie **Neu** aus, um ein neues Paar hinzuzufügen.
        2. Geben Sie im Dialogfeld **Name/Wert-Paar hinzufügen** folgendes an:
            - **Typ**. Wählen Sie aus der Liste den Typ des Werts aus, den Sie angeben möchten.
            - **Name**. Geben Sie den Namen des Eigenschaftslistenschlüssels an, für den Sie einen Wert angeben möchten.
            - **Wert**. Geben Sie den Wert an, der für den eingegebenen Schlüssel festgelegt wird.

  - **Wechseln Sie zu einer Eigenschaftslistendatei**. Verwenden Sie diese Option, wenn Sie bereits über eine XML-Datei zum Konfigurieren einer App verfügen, oder für komplexere Dateien, die Schachtelung verwenden.

    *Zu einer Eigenschaftslistendatei navigieren*

      1.  Geben Sie im Feld **App-Konfigurationsrichtlinie** die Informationen zur Eigenschaftsliste im richtigen XML-Format an.

      Weitere Informationen zu XML-Eigenschaftenlisten finden Sie unter [Understanding XML Property Lists (XML-Eigenschaftslisten verstehen)](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) in der iOS Developer Library.

Das Format der XML-Eigenschaftenliste variiert je nach der App, die Sie konfigurieren. Wenden Sie sich an den Hersteller der App, um ausführliche Informationen über das zu verwendende Format zu erhalten.
Intune unterstützt die folgenden Datentypen in einer Eigenschaftenliste:
            
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
Weitere Informationen zu Datentypen finden Sie unter [About Property Lists (Über Eigenschaftslisten)](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) in der iOS Developer Library.
Intune unterstützt auch die folgenden Tokentypen in der Eigenschaftsliste:
            
            ```
            {{userprincipalname}} - (Example: John@contoso.com)
            {{mail}} - (Example: John@contoso.com)
            {{partialupn}} - (Example: John)
            {{accountid}} - (Example: fc0dc142-71d8-4b12-bbea-bae2a8514c81)
            {{deviceid}} - (Example: b9841cd9-9843-405f-be28-b2265c59ef97)
            {{userid}} - (Example: 3ec2c00f-b125-4519-acf0-302ac3761822)
            {{username}} - (Example: John Doe)
            {{serialnumber}} - (Example: F4KN99ZUG5V2) for iOS devices
            {{serialnumberlast4digits}} - (Example: G5V2) for iOS devices
            ```

Die Zeichen {{ und }} werden nur von Tokentypen verwendet und dürfen nicht für andere Zwecke verwendet werden.
            
5. Zum Importieren einer zuvor erstellten XML-Datei wählen Sie **Datei auswählen** aus.
6. Wählen Sie **Weiter** aus. Falls Sie Fehler im XML-Code feststellen, müssen Sie diese korrigieren, bevor Sie fortfahren.
7. Schließen Sie die im Assistenten gezeigten Schritte ab.

Die neue App-Konfigurationsrichtlinie wird im Knoten **App-Konfigurationsrichtlinien** des Arbeitsbereichs **Softwarebibliothek** angezeigt.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Zuordnen einer Konfigurationsrichtlinie für Apps zu einer Configuration Manager-Anwendung

Um eine App-Konfigurationsrichtlinie mit der Bereitstellung einer iOS-App zuzuordnen, stellen Sie die Anwendung wie gewohnt bereit, indem Sie die Vorgehensweise im Thema [Bereitstellen von Anwendungen](/sccm/apps/deploy-use/deploy-applications) durchführen.

Wählen Sie im Assistenten zum Bereitstellen von Software auf der Seite **App-Konfigurationsrichtlinien** **Neu**. Wählen Sie anschließend im Dialogfeld **App-Konfigurationsrichtlinie auswählen** einen Bereitstellungstyp und die App-Konfigurationsrichtlinie aus, die Sie zuordnen möchten.
Bei der Installation des Bereitstellungstyps werden die Einstellungen der App-Konfigurationsrichtlinie automatisch angewendet.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Beispiel für das Format für die XML-Konfigurationsdatei für mobile Apps

Wenn Sie eine Konfigurationsdatei für mobile Apps erstellen, können Sie mithilfe dieses Formats einen oder mehrere der folgenden Werte angeben:

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>
```
