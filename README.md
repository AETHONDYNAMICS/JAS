# JAS — Janus-Aethon Security Layer

JAS ist ein **lokales Werkzeug**, das personenbezogene Daten in anwaltlichen
Schriftsätzen durch Platzhalter ersetzt, bevor der Text an eine KI weitergegeben
wird. Das ist **Pseudonymisierung nach Art. 4 Nr. 5 DSGVO**, keine
Anonymisierung: eine Zuordnungstabelle bleibt lokal und erlaubt die
Rückübersetzung der Antwort.

## Wie es arbeitet

- **Läuft ausschließlich lokal.** Keine Netzwerkverbindung, keine Cloud, kein
  Auftragsverarbeitungsvertrag nötig — der Anbieter erhält keine Daten. Belegt
  in [TOM.md](TOM.md) (Art. 32 DSGVO).
- **Fail-Closed:** Bleibt nach der Ersetzung etwas Erkennbares im Text stehen,
  wird **nichts** ausgeliefert. Das Werkzeug liefert lieber gar nichts als
  etwas Unsicheres.
- Die Zuordnungstabelle liegt nur im Arbeitsspeicher und verschwindet mit dem
  Programm.

## Erkennungsrate

Belastbar ist nur ein Wert, der an Dokumenten gemessen wird, die der Code nicht
kennt (Blindtest). Zwei solche unabhängigen Werte liegen vor:

- **94,1 %** — 450 von 478 Datenposten in 30 fremden Dokumenten.
- **94,6 %** — 279 von 295 Datenposten in 30 anderen fremden Dokumenten.

Beide **blind** gemessen: der Code kannte die Dokumente nicht.

Ein dritter Korpus wurde später zum Verbessern des Codes benutzt; der Wert
dort (98,3 %) ist deshalb **kein Blindwert** und wird hier nicht als
Erkennungsrate genannt.

Was das Werkzeug nicht kann, steht offen in [GRENZEN.md](GRENZEN.md).

## Dokumente

- [GRENZEN.md](GRENZEN.md) — was das Werkzeug nicht kann, die Restliste
- [TOM.md](TOM.md) — technische und organisatorische Maßnahmen (Art. 32 DSGVO)
- [DATENSCHUTZHINWEIS.md](DATENSCHUTZHINWEIS.md) — Datenschutzhinweis

## Quellcode

Der Quellcode (die Erkennungslogik) ist **nicht Teil dieses Repositoriums**.
Dieses Repository enthält ausschließlich die Dokumentation.

## Kontakt / Bezug

AETHON DYNAMICS.

<!-- TODO: Domain der Verkaufsseite eintragen -->
<!-- TODO: Lemon-Squeezy-Kauflink eintragen -->
