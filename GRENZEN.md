# Grenzen von JAS — die Restliste

Stand: 2026-07-18. Kein Verkaufston. Wer JAS einsetzt, muss wissen, woran er
ist. Dieses Werkzeug ist ein Hilfsmittel, kein Ersatz für die Prüfung durch
den Verantwortlichen.

## Messmethodik

Prüfstände mit je einer vor jedem Lauf gehashten Liste aller enthaltenen
personenbezogenen Daten (Goldstandard):

- **Prüfstand 1:** 12 selbst erstellte Anwaltsschreiben.
  Goldstandard-SHA-256 `2474442208b8a458cb19d772dff2f06fe7e632c4fb847f2e33e71b2433eb8035`.
- **Prüfstand 2:** 30 Briefe von einer fremden Instanz (Erkennungscode nicht
  bekannt). Goldstandard-SHA-256 `092198db14f77df2e1dd65063872234806c448d6fe0307564aab71bbe8f74437`.
- **Prüfstand 3:** 30 weitere fremde Briefe („Satz 3"), 478 Datenposten.
  Goldstandard-SHA-256 `220c7bb38020494c015f9c402666e71981c30499f39eed9b944ac694991d911e`.
- **Prüfstand 4:** 30 komplette Streitvorgänge („Satz 4"), mehrere Absender,
  Behördendeutsch mit direkter Anrede, 1568 Datenposten.
  Goldstandard-SHA-256 `4d30b25b57771d2bab744d30b2e6c72bcb6fb24b615350dc5e5b381b1599fff4`.

Messgrößen je Dokument: **Treffer** (Gold-Wert verschwindet aus der Ausgabe),
**Durchrutscher** (Gold-Wert bleibt stehen), **Übereifer** (etwas wird
ersetzt, das nicht im Goldstandard steht).

## Erkennungsrate — der blinde Wert

Belastbar ist nur ein Wert, der an Dokumenten gemessen wird, die der Code
nicht kennt. Drei solche unabhängigen Blindwerte liegen vor:

- **Prüfstand 4 (Blindlauf 4): 1504 von 1568 = 95,9 %** — kein Fail-Closed.
- **Prüfstand 3 (Blindlauf 3): 450 von 478 = 94,1 %** — kein Fail-Closed.
- **Prüfstand 2, als er noch blind war: 279 von 295 = 94,6 %.**

Drei fremde Korpora, nah beieinander.

**Vorbehalt zur 95,9 % (Satz 4), wörtlich aus der Messung:** Ein erheblicher
Teil der Treffer entsteht durch Kopf-/Fuß-Entfernung, nicht durch kategorische
Erkennung. Kategorien ohne eigenen Anker zeigen 0 Durchrutscher, weil ihre
Werte im entfernten Kopf stehen. Im Rumpf würden sie durchrutschen. Beleg:
`pruefstand4/BEFUND_blindlauf4_2026-07-17.md`, Abschnitt 1. Die 95,9 % sind
darum kein reiner Erkennungswert.

**Was NICHT als Erkennungsrate gilt:** Prüfstand 2 wurde nach der ersten
Messung zum Verbessern des Codes benutzt. Der spätere Wert dort (290 von 295 =
98,3 %) ist deshalb **kein Blindwert** — der Code wurde gegen genau diese 30
Dokumente gebaut. Er wird hier nicht als Erkennungsrate genannt.

**Ebenso der BIC-Anker (2026-07-18):** Nachdem in Satz 4 die BIC-Lücke sichtbar
wurde, wurde ein gezielter BIC-Erkennungsanker gebaut. Er senkt die
verbleibenden Satz-4-Durchrutscher von 64 auf **46** (gemessen; Treffer 1504 →
1522). Weil er an genau diesen Dokumenten gemessen ist, ist dieser Zuwachs —
wie die 98,3 % bei Prüfstand 2 — **kein reiner Blindwert**. Der oben genannte
Satz-4-Blindwert von 95,9 % bleibt deshalb als der unabhängige Wert
stehen.

## Bekannte Durchrutscher (Blindlauf 3, 28 Stück) nach Klasse

Beispiele sind **erfunden** (keine echten Mandantendaten); die Klasse des
Problems ist das Bleibende.

- **AKTENZEICHEN — 8:** unbekannte Aktenzeichen-Formate, die keine der
  eingebauten Regeln trifft (erfundenes Beispiel „XY/2099/1234").
- **NAME — 7:** meist Namen mit vorangestelltem Titel, der nicht mit-erfasst
  wird (erfundenes Beispiel „Dr. Erika Beispiel", „Dipl.-Ing. Max Muster",
  „Dipl.-Kfm. Lena Vorbild").
- **RECHNUNGSNUMMER — 6 (alle sechs):** das Etikett „Rechnungsnummer" ist zwar
  bekannt, die konkreten Werte in Satz 3 wurden dennoch nicht erfasst
  (erfundenes Beispiel „2099-0000").
- **VORGANGSNUMMER — 3:** Vorgangs-/Geschäftsnummern in unerfassten Formen
  (erfundenes Beispiel „XX-2099-0000000").
- **GEBURTSORT — 2:** Geburtsort, der nicht direkt an „geboren am DATUM in ORT"
  hängt (erfundenes Beispiel „Musterstadt").
- **ADRESSE — 2:** Straßenadresse, die der Erkennungs-Kern nicht als Adresse
  fasst (erfundenes Beispiel „Beispielweg 1").

## Bekannte Durchrutscher (Satz 4, 46 Stück — nach Einbau des BIC-Ankers) nach Klasse

Beispiele **erfunden**, keine echten Mandantendaten. (Vor dem BIC-Anker waren es
64; die 18 BIC-Durchrutscher — vormals größte Gruppe — entfallen, siehe oben.)

- **RECHNUNGSNUMMER — 9, STEUERNUMMER — 7:** Nummern in unerfassten Formaten
  (erfundene Beispiele „2099-0000", „099/1234/5678").
- **NAME — 6:** meist mit Titel (erfundenes Beispiel „Dr. Erika Beispiel").
- **BUCHUNGSNUMMER — 5, AKTENZEICHEN — 5:** unbekannte Formate (erfundene
  Beispiele „9999999-XYZ", „61 IN 999/99").
- **GEBURTSORT — 4:** Ort ohne direkte Bindung an „geboren am DATUM in ORT".
- **OBJEKTNUMMER — 3, GERAETENUMMER — 2, und je 1:** KASSENZEICHEN, UST-IdNr.,
  BETRIEBSNUMMER, FÜHRERSCHEINNUMMER, KONTONUMMER — Fach-/Behördennummern ohne
  eigenen Anker.

## Strukturelle Grenzen (was das Werkzeug nicht kann)

- **Kopf-/Fußzeilen-Entfernung hängt an einer erkannten Anrede.** Der Absender-
  Briefkopf wird nur entfernt, wenn eine Anrede-Floskel („Sehr geehrte…",
  „Guten Tag", „Hallo") erkannt wird. In **18 von 30** Dokumenten aus Satz 3
  gibt es keine — Schriftsätze, die mit „Namens und in Vollmacht…" öffnen, und
  interne Vermerke/Notizen. Dort bleibt der Absender-Briefkopf im Text und
  wird geschwärzt (Übereifer). Beleg:
  `pruefstand3/BEFUND_blindlauf3_2026-07-17.md`, Abschnitt 1.
- **Nur Fließtext (`.txt`).** Kein PDF, kein Word, keine Bilder, keine
  Tabellen-/Layoutstruktur.
- **Ein Name, der nur informell im Fließtext steht** und nie formell (Kopf,
  Anrede, Rolle, Namenszeile, „geborene …") auftaucht, bleibt Restrisiko.
- **Freie Formulierungen** ohne klares Etikett oder Zahlenformat werden nicht
  zuverlässig erfasst.
- **Die Erkennung ist regelbasiert**, nicht lernend. Sie kennt die Muster,
  die ihr eingebaut wurden — nicht mehr.

## Übereifer — die sichere Richtung, aber nicht immer harmlos

Übereifer schwärzt zu viel, nie zu wenig. Ganz überwiegend ist er harmlos:
meist Absenderdaten (Kanzleiname, Anschrift, Telefon, E-Mail) und Rollen-/
Briefkopf-Wörter, die syntaktisch wie ein Name oder eine Adresse aussehen. In
Prüfstand 1–3 war **kein einziger** Übereifer „teuer" (Norm, Frist oder
Fristdatum geschwärzt).

**In Blindlauf 4 traten erstmals zwei „teure" Übereifer auf** (von 36 gesamt).
Beide mit **erfundenem** Beispiel, keine echte PII:

- **Ein Datum, das kein Geburtsdatum war.** Steht ein Datum nahe dem Wort
  „Geburtstag", bindet die Geburtsdatum-Erkennung es fälschlich (erfundenes
  Beispiel: „Am 01.01.2099 hatte ich Geburtstag." → das Datum wird geschwärzt,
  obwohl es kein Geburtsdatum ist). Als „teuer" gewertet, weil ein Datum
  betroffen ist. Beleg: `pruefstand4/BEFUND_datum21_2026-07-18.md`.
- **Ein Formular-/Checklistenblock mit dem Wort „Frist".** Die
  Kennung-Erkennung fasst mitunter einen ganzen mehrzeiligen Vorlagenblock
  (erfundenes Beispiel: „[ ] Frist notiert? [ ] Frist gelöscht?") — als
  „teuer" gewertet, weil das Wort „Frist" darin steht. Es ist eine leere
  Vorlage, keine Mandatsfrist.

Wer JAS einsetzt, prüft die Ampel/Zuordnungstabelle vor der Weitergabe — auch
darauf, ob ein Datum oder ein Fristfeld unnötig geschwärzt wurde.

## Der eine Schutz, auf den Verlass ist

Bleibt nach der Ersetzung etwas Erkennbares stehen, wird **nichts**
ausgeliefert (Fail-Closed). Das Werkzeug liefert lieber gar nichts als etwas
Unsicheres. Die Schärfe dieses Wächters ist gegengeprüft
(`pruefstand2/werkzeuge/BEFUND_waechter_gegenprobe_2026-07-17.md`). In
Blindlauf 3 und Blindlauf 4 hat kein Dokument den Wächter ausgelöst.
