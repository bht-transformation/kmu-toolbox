# Agenda Wolke · Version 2

Teil der Netzwerk Toolbox für KMU Meetings (Projektmodul III, Netzwerk Großbeerenstraße).

Eine kostenlose Web-App zur gemeinsamen Erstellung einer Meeting-Agenda. Das ursprüngliche Corporate Design bleibt erhalten.

## Ablauf

1. **Runde 1 – Eigene Begriffe:** QR-Code scannen und genau drei eigene Begriffe eingeben. Optional eine Notiz (maximal 500 Zeichen) je Begriff ergänzen. Auf dem Beamer erscheint nur der Fortschritt, nicht der Inhalt. Die eigenen Eingaben sind auf dem jeweiligen Handy sichtbar. Wenn alle Teilnehmenden fertig sind, öffnet die Moderation die zweite Runde. Eine vorzeitige Freigabe erfordert eine Bestätigung; später hinzukommende oder noch nicht fertige Teilnehmende müssen ihre drei eigenen Begriffe zuerst einreichen, bevor sie die gemeinsame Liste auf dem Handy sehen.
2. **Runde 2 – Gemeinsame Wortwolke:** Die Begriffe werden am Beamer und als Liste auf dem Handy sichtbar. Die Moderation kann die Anzahl zusätzlicher Begriffe pro Person einstellen (Standard: drei weitere). Ähnliche Schreibweisen werden automatisch anhand normalisierter Schreibweisen und einer konservativen Editierdistanz zusammengefasst. Die häufigste Schreibweise (bei Gleichstand die zuerst eingereichte) wird angezeigt. Häufigkeit, ursprüngliche Varianten und Notizen bleiben erhalten. Die grüne Schrift ist dunkler und besser lesbar.
3. **Themen wählen:** Die Moderation wählt Themen für das Ranking aus und kann eigene Themen ergänzen. Offene Themen aus früheren Meetings erscheinen im Themenspeicher und sind erneut auswählbar. Durch Klick auf ein Wort in der Wolke öffnet sich ein Dialog mit den Notizen und Varianten; ein fälschlich gebildetes Cluster kann getrennt werden. Absichtlich ausgeblendete aktuelle Begriffe werden nicht neu archiviert.
4. **Ranking:** Alle bringen die ausgewählten Themen auf dem Handy in ihre Reihenfolge. Notizen und Varianten lassen sich unter den Themen aufklappen.
5. **Agenda:** Alle oder nur die wichtigsten N Themen übernehmen. Die übrigen Themen werden automatisch einschließlich Notizen im Themenspeicher abgelegt. Bei einer späteren Übernahme in eine Agenda verschwinden sie aus dem offenen Speicher. Agenda und zurückgestellte Themen können als Text kopiert werden.

## Timer

Oben in der Moderationsansicht erscheint ein gemeinsamer Countdown (Standard: 5 Minuten). Durch Klick auf die Zeitanzeige kann die Dauer in Minuten und Sekunden eingestellt oder eine Voreinstellung gewählt werden. Start/Pause, +1 Minute und Zurücksetzen stehen direkt daneben. Der Timer ist auf den Handys lesbar und läuft über Phasenwechsel und das Neuladen der Moderationsseite hinweg weiter. Beim Ablauf erscheint „Zeit um“; die nächste Phase startet nicht automatisch.

## Installation und Benutzung

- Die ZIP-Datei entpacken. `index.html` und den Ordner `lib` gemeinsam auf dem Webserver bzw. in GitHub Pages ablegen. `README.md` dient als Anleitung.
- Laptop/Beamer: Seite öffnen, „Neue Runde starten“ anklicken, anschließend durch die fünf Schritte wechseln.
- Handys: QR-Code scannen; kein Konto und keine Installation nötig. Beide Ansichten müssen die gleiche Version der App verwenden.
- Einstellungen: Frage, zusätzliche Begriffe in Runde 2, Vollbild bzw. Steuerleiste. „Neue Runde mit neuem Code“ speichert offene Themen und startet ein neues Meeting.
- Der Themenspeicher liegt lokal im Browser der Moderation (`localStorage`). Er bleibt bei neuen Codes und Neuladen erhalten, solange dieselbe Website und dasselbe Browserprofil verwendet werden. Er wird nicht geräteübergreifend synchronisiert. Beim Löschen von Website-Daten oder bei privatem Surfen kann er verloren gehen. Die Moderationsansicht sollte nicht gleichzeitig für mehrere unabhängige Meetings im selben Profil genutzt werden.

## Technik und Datenschutz

Eine HTML-Datei mit den beiden mitgelieferten JavaScript-Bibliotheken, ohne eigenen Anwendungsserver. Die Live-Verbindung läuft über einen öffentlichen MQTT-Broker (HiveMQ; bei Störung versucht die Moderationsansicht auf EMQX oder Mosquitto zu wechseln). Der Nachrichtenkanal der Version 2 ist von Version 1 getrennt. Frühere lokal gespeicherte Moderationsrunden können migriert werden; eine bereits freigegebene Wortwolke kann nicht nachträglich geheim werden.

Runde 1 unterdrückt fremde Begriffe und Notizen in der Oberfläche und im veröffentlichten Rundenzustand. Die einzelnen Eingaben werden dennoch über den öffentlichen Broker übertragen. Der Rundencode ist kein Zugriffsschutz. Es werden keine Namen abgefragt; bitte keine vertraulichen oder personenbezogenen Inhalte eingeben.

Testmodus ohne Live-Broker: `?local=1` an die Adresse hängen, dann funktioniert die App zwischen Tabs desselben Browsers. Für die geräteübergreifende Verwendung die App über eine normale Webadresse aufrufen.

Bibliotheken: [MQTT.js](https://github.com/mqttjs/MQTT.js) 5.10.1 und [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 1.4.4, beide MIT-Lizenz.
