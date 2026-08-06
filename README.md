# ZOLEX Live 2027 – Mailing Aussteller-Akquise

HTML-E-Mail-Template auf Basis der Vorlage
`Mailing_Aussteller_Akquise_ArT_ZOLEX_LIVE_2027.pdf`, aufgebaut für **Optimizely
Campaign / CMP**.

## Dateien

| Datei | Beschreibung |
|---|---|
| `zolex-live-2027-aussteller-akquise.html` | Das fertige E-Mail-Template (600 px, Tabellen-Layout, Inline-CSS) |
| `assets/zolex-live-2027-banner.jpg` | Briefkopf / Banner – Anzeige 600 × 159 px (Datei 1200 × 318 px für Retina) |
| `assets/zolex-live-2027-konfigurator.jpg` | Konfigurator-Visual – Anzeige 560 × 560 px (Datei 1120 × 1120 px) |
| `assets/haken-pink.png` | Häkchen-Icon der Vorteilsliste – Anzeige 22 × 22 px (Datei 66 × 66 px) |

## Betreff & Preheader

**Betreff**
> Treffen Sie über 100 Entscheider aus Zoll, Export und Einkauf – das große Branchenevent!

**Preheader (Vorschautext)**
> Werden Sie Aussteller auf der ZOLEX Live 2027 im Historischen Wasserturm Köln.

Der Betreff steht zusätzlich im `<title>`-Tag. Der Preheader ist als versteckter
Block direkt am Anfang von `<body>` eingebaut (inkl. Auffüll-Zeichen), damit in
Gmail, Outlook & Co. genau dieser Text neben der Betreffzeile erscheint und nicht
der Beginn des Fließtextes. Sichtbar beginnt die E-Mail mit dem Banner/Briefkopf.

## Platzhalter (doppelte geschweifte Klammern)

| Platzhalter | Verwendung |
|---|---|
| `{{ Name }}` | Anrede: „Guten Tag {{ Name }}," |
| `{{ Beratungstermin_URL }}` | Ziel des Buttons „Jetzt kostenlosen Beratungstermin buchen!" |
| `{{ Firma }}` | Footer – Absendername |
| `{{ Strasse }}` | Footer – Straße |
| `{{ PLZ_Ort }}` | Footer – PLZ und Ort |
| `{{ Telefon }}` | Footer – Telefonnummer |
| `{{ Email }}` | Footer – E-Mail-Adresse (Text + `mailto:`) |
| `{{ Website_URL }}` | Footer – Website |
| `{{ Impressum_URL }}` | Footer – Impressum |
| `{{ Datenschutz_URL }}` | Footer – Datenschutz |
| `{{ Webversion_URL }}` | Kopfzeile „Im Browser ansehen" + Footer „Webversion" |
| `{{ Abmelde_URL }}` | Footer – Abmeldelink |

Alternativ kann der komplette Footer-Block (`<td style="background-color:#0B4359">`)
durch einen einzelnen Optimizely-Baustein `{{ Footer }}` ersetzt werden – siehe
Kommentar im HTML.

## Links (CTAs)

| Button | Ziel |
|---|---|
| Banner (Briefkopf) | `https://lp.zoll-export-wissen.de/zolex-live/` |
| „Jetzt Aussteller in unter 40 Sekunden werden!" | `https://lp.zoll-export-wissen.de/zolex-live/` |
| Konfigurator-Bild | `https://lp.zoll-export-wissen.de/zolex-live/` |
| „Jetzt Ausstellerpaket konfigurieren!" | `https://lp.zoll-export-wissen.de/zolex-live/` |
| „Jetzt kostenlosen Beratungstermin buchen!" | `{{ Beratungstermin_URL }}` – in der Vorlage war **kein** Link angegeben |

## Bild-URLs vor dem Versand setzen

Die Bilder aus `assets/` in die Optimizely-Medienbibliothek hochladen und im HTML
die Basis-URL per Suchen & Ersetzen austauschen:

```
https://lp.zoll-export-wissen.de/email/zolex-live-2027/   →   <Ihre Optimizely-Medien-URL>
```

E-Mails benötigen absolute `https://`-URLs; relative Pfade oder Data-URIs werden von
Gmail und Outlook blockiert.

## Farben (exakt aus der Vorlage übernommen)

| Element | Hex |
|---|---|
| CTA-Buttons (Pink) | `#E72E89` |
| Paket **Basic** – Rahmen & Überschrift | `#00A3C4` |
| Paket **Plus** – Rahmen & Überschrift | `#E5007D` |
| Paket **Premium** – Rahmen & Überschrift | `#B7D134` |
| Überschriften / Textblau | `#0B4359` |
| Fließtext | `#333333` |
| Seitenhintergrund | `#EFEFEF` |

## Technische Umsetzung (Optimizely-tauglich)

- XHTML 1.0 Transitional, `<table>`-Layout, komplett Inline-CSS
- 600 px feste Breite, responsiv ab 620 px Viewport (`@media`, Bilder `width:100%`)
- Outlook (Word-Engine): `mso`-Conditionals, `<o:OfficeDocumentSettings>` mit
  `AllowPNG`, VML-`roundrect`-Buttons, `mso-line-height-rule:exactly`
- Alle Bilder mit `width`/`height`-Attribut, `display:block` und Alt-Text
  (Häkchen fallen auf „✓" zurück, wenn Bilder blockiert werden)
- `role="presentation"` auf allen Layout-Tabellen
- Gmail-/iOS-Fixes gegen automatische Link-Erkennung und Zitat-Abschneidung
- `color-scheme: light` gegen ungewollte Dark-Mode-Invertierung

## Vorschau lokal ansehen

```bash
python3 - <<'PY'
s = open('zolex-live-2027-aussteller-akquise.html', encoding='utf-8').read()
open('.preview.html', 'w', encoding='utf-8').write(
    s.replace('https://lp.zoll-export-wissen.de/email/zolex-live-2027/', 'assets/'))
PY
# .preview.html im Browser öffnen
```
