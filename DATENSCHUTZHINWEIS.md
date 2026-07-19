# Datenschutzhinweis — JAS Pseudonymisierungs-Werkzeug

Stand: 2026-07-17. Version: Fertigstellung 1.0.

## 1. Zweck

JAS ersetzt in einem eingegebenen Text erkannte personenbezogene Daten
(Namen, Adressen, Geburtsdaten, Geburtsorte, Aktenzeichen, Kunden-/Kennungs-
nummern, Kfz-Kennzeichen, IBAN, E-Mail, Telefon u. a.) durch nummerierte
Platzhalter. Das ist **Pseudonymisierung im Sinne von Art. 4 Nr. 5 DSGVO**,
keine Anonymisierung: eine Zuordnungstabelle erlaubt die Rückübersetzung.

## 2. Rechtliche Einordnung

- Der **Nutzer ist Verantwortlicher** im Sinne von Art. 4 Nr. 7 DSGVO für
  die Verarbeitung seiner Texte. Der Anbieter (AETHON DYNAMICS) erhält keine
  Daten und ist kein Auftragsverarbeiter — das Werkzeug läuft ausschließlich
  lokal und sendet nichts.
- Weil eine Zuordnungstabelle existiert, bleibt der pseudonymisierte Text
  **personenbezogen** im Sinne von Erwägungsgrund 26. Er ist nicht anonym.

## 3. Was das Werkzeug tut / nicht tut

- **Tut:** erkennt regelbasiert personenbezogene Daten, ersetzt sie durch
  Platzhalter, hält die Rückzuordnung lokal im Arbeitsspeicher vor, führt ein
  Verarbeitungsprotokoll ohne Klartext (Abschnitt 5).
- **Tut nicht:** es garantiert keine Vollständigkeit der Erkennung. Bleibt
  nach der Ersetzung noch etwas Erkennbares stehen, wird **nichts
  ausgeliefert** (Fail-Closed). Es verarbeitet nur Fließtext (`.txt`), keine
  Bilder, keine PDF-/Tabellenstruktur.

## 4. Datenflüsse

Die Verarbeitung geschieht vollständig lokal auf dem Rechner des Nutzers. Es
werden keine Netzwerkverbindungen aufgebaut, keine Telemetrie gesendet, keine
Temporärdateien mit Klartext angelegt. Belege: `BEFUND_art32_netzwerk_2026-07-17.md`,
`BEFUND_art32_temp_2026-07-17.md`.

## 5. Speicherung

- **Zuordnungstabelle:** nur im Arbeitsspeicher, wird nie in eine Datei
  geschrieben und verschwindet beim Schließen des Fensters
  (`BEFUND_dsgvo_tabelle_weg_2026-07-17.md`).
- **Verarbeitungsprotokoll:** `~/.jas/protokoll.db` — enthält je Vorgang nur
  Zeitstempel, Anzahl und Kategorien der Ersetzungen sowie das Fail-Closed-
  Flag. **Kein Klartext, keine Zuordnung, kein Dokumentinhalt, kein
  Dateiname** (`BEFUND_dsgvo_protokoll_klartext_2026-07-17.md`). Vom Nutzer
  einsehbar und löschbar.

## 6. Rechte Betroffener

Die Rechte betroffener Personen (Auskunft, Berichtigung, Löschung usw.)
richten sich an den **Verantwortlichen (den Nutzer)**, nicht an AETHON
DYNAMICS, da dieser keine Daten erhält.

## 7. Grenzen

Die Restliste (bekannte Durchrutscher, Übereifer, strukturelle
Grenzen) steht in `GRENZEN.md`. Wer das Werkzeug einsetzt, sollte sie kennen.
