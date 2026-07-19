# Technische und organisatorische Maßnahmen (Art. 32 DSGVO)

Stand: 2026-07-17. Jede Maßnahme ist durch eine Prüfung belegt, nicht
behauptet. Die Prüfskripte liegen unter `pruefstand2/werkzeuge/`, die
Ergebnisse als Befund-Dateien neben dieser Datei.

## 1. Lokale Verarbeitung, keine Netzwerkverbindung

Das Werkzeug importiert die Erkennungs-/Ersetzungslogik im selben Prozess und
öffnet keinen Server, keinen Port, keinen Browser. AST-Scan aller vier
ausgelieferten Module (`jas_bruecke.py`, `jas_gui.py`, `jas_protokoll.py`,
`jas_start.py`): **0** Netzwerk- oder Dynamik-Importe, **0** Telemetrie-
Schlagwörter. Beleg: `BEFUND_art32_netzwerk_2026-07-17.md`.

## 2. Keine Temporärdateien mit Klartext

Vor/nach einem Pseudonymisierungs-Durchlauf entstehen **0** neue
Temporärdateien. Beleg: `BEFUND_art32_temp_2026-07-17.md`.

## 3. Zuordnungstabelle nur im Arbeitsspeicher

Die Tabelle (Platzhalter ↔ Klartext) lebt ausschließlich als Objekt im
Prozessspeicher, wird nie in eine Datei geschrieben und beim Schließen des
Fensters freigegeben. Nach Prozessende ist der Klartext an keinem Ablageort
auffindbar. Beleg: `BEFUND_dsgvo_tabelle_weg_2026-07-17.md`.
Datenschutzfreundliche Voreinstellung (Art. 25 Abs. 2): es gibt keine
Sitzungsspeicherung und keinen Export der Tabelle.

## 4. Protokollierung ohne Klartext

Das Verarbeitungsprotokoll (`~/.jas/protokoll.db`, im Benutzerprofil, damit es
Neustarts/Updates übersteht) enthält je Vorgang nur: Zeitstempel, Anzahl und
Kategorien der Ersetzungen, Fail-Closed-Flag. Geprüft gegen alle echten
PII-Werte beider Prüfstände: **0** Klartext-Treffer im Protokoll. Beleg:
`BEFUND_dsgvo_protokoll_klartext_2026-07-17.md`. Der Nutzer kann das Protokoll
im Fenster einsehen und löschen.

## 5. Fail-Closed als technische Maßnahme

Nach der Ersetzung prüft ein Rescan-Wächter den Text erneut. Bleibt etwas
Erkennbares stehen, wird **nichts** ausgeliefert und stattdessen die
betroffenen Kategorien (nie die Werte) gemeldet. Die Schärfe des Wächters ist
gegengeprüft: eine testweise unterdrückte Kategorie löst weiterhin den Abbruch
aus. Beleg: `pruefstand2/werkzeuge/BEFUND_waechter_gegenprobe_2026-07-17.md`.

## 6. Bekannte Grenzen

Technische und organisatorische Maßnahmen ersetzen keine vollständige
Erkennung. Die Restliste steht in `GRENZEN.md` und ist Teil der
Risikobewertung des Verantwortlichen.
