# Agenda Wolke

Teil der Netzwerk Toolbox für KMU Meetings (Projektmodul III, Netzwerk Großbeerenstraße).

Eine kostenlose Web App, um die Agenda eines Meetings gemeinsam zu gestalten:

1. **Begriffe sammeln:** Alle scannen am Beamer den QR Code und geben auf dem Handy Begriffe ein. Die Wortwolke am Beamer aktualisiert sich live, häufig genannte Begriffe werden größer.
2. **Themen wählen:** Die Moderation übernimmt die wichtigsten Begriffe als Themen und kann eigene ergänzen.
3. **Ranking:** Alle bringen die Themen auf dem Handy in ihre Reihenfolge. Daraus ergibt sich die gemeinsame Reihenfolge.
4. **Agenda:** Der Beamer zeigt die gemeinsame Reihenfolge.

## Benutzung

* Laptop am Beamer: Seite öffnen, „Neue Runde starten“, dann unten durch die Schritte 1 bis 4 klicken.
* Teilnehmende: QR Code scannen. Kein Konto und keine Installation nötig.
* Einen Begriff ausblenden: in der Wortwolke auf den Begriff klicken.
* Einstellungen: Frage ändern, Begriffe pro Person.

## Technik

Eine einzelne HTML Datei ohne Server. Die Live Verbindung läuft über einen öffentlichen MQTT Broker (HiveMQ, bei Störung automatisch EMQX oder Mosquitto). Es werden keine Namen gespeichert. Die Inhalte sind für alle sichtbar, die den Code der Runde kennen, deshalb bitte keine vertraulichen Inhalte eingeben.

Testmodus ohne Internet: `?local=1` an die Adresse hängen, dann funktioniert die App zwischen Tabs im selben Browser.

Bibliotheken: [MQTT.js](https://github.com/mqttjs/MQTT.js) 5.10.1 und [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 1.4.4, beide MIT Lizenz.
