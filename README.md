# Website-Template: Verein der Griechen aus Pontos e.V.

Statisches Website-Template im **Neubrutalismus-Stil** mit **daisyUI 5 (Tailwind CSS)**.
Sprache: Deutsch. Kein Build-Step nötig – Dateien direkt im Browser öffnen oder per
statischem Server ausliefern.

## Seiten

| Datei | Inhalt |
|---|---|
| `index.html` | Startseite: Hero, News-Teaser, Termine, CTA |
| `vereinsgeschichte.html` | Zeitleiste des Vereins, Auftrag, Vorstand (Platzhalter) |
| `pontos-geschichte.html` | Geschichte der Pontosgriechen von der Antike bis zur Diaspora |
| `aktuelles.html` | News-Karten mit aufklappbarem Volltext |
| `kontakt.html` | Adresse, Öffnungszeiten, Kontaktformular, Beitrag |
| `impressum.html` | Impressum + Datenschutz-Kurzfassung (Platzhalter, `noindex`) |

## Struktur

```
pontos-verein/
├── index.html
├── vereinsgeschichte.html
├── pontos-geschichte.html
├── aktuelles.html
├── kontakt.html
├── impressum.html
├── css/brutal.css      Brutalismus-Layer über daisyUI (Farben, Schatten, Komponenten)
├── js/main.js          Fußzeilen-Jahr (einziger JS-Zweck)
├── favicon.svg
├── robots.txt          Suchbots erlaubt, Trainings-Crawler ausgeschlossen
├── sitemap.xml
└── README.md
```

## Lokal ansehen

```sh
cd pontos-verein
python3 -m http.server 8000
# http://localhost:8000
```

## Design-System (Neubrutalismus)

- **Farbtokens** in `css/brutal.css` unter `:root` (Papier, Tinte, Gelb, Blau, Rot).
  Dunkelmodus folgt automatisch `prefers-color-scheme`.
- **Harte Schatten**: Klassen `.brutal`, `.brutal-sm`, `.brutal-lg`; Hover-Effekt `.brutal-hover`.
- **Keine Abrundungen**: daisyUI-Radien werden auf `0` gesetzt.
- **Marquee-Laufband**, **Ionisch-Voluten-Trenner** (`.ionik`), **Eierstab-Kyma** (`.kyma`), **Zeitleiste** (`.timeline-brutal`),
  **Textmarker** (`.mark`), **Sticker-Rotation** (`.sticker-l/r`).

## Vor Veröffentlichung ersetzen

1. Bei Umzug auf eine eigene Domain: Adresse in allen `<link rel="canonical">`,
   `og:url`, JSON-LD, `sitemap.xml` und `robots.txt`.
2. Vereinsname, Adresse, Kontakt, Beitragshöhe, Vorstand, Impressumsangaben.
3. Platzhalter-Jahreszahlen in `vereinsgeschichte.html` durch die echte Chronik ersetzen.
4. Kontaktformular: Das Template nutzt `mailto:` als Übergangslösung. Für echten Versand
   ein Formular-Backend anbinden (z. B. Formspree, Netlify Forms, eigener Endpoint).

## Produktionsempfehlung (CDN → Build)

Das Template lädt daisyUI + Tailwind über CDN (schneller Einstieg). Für Produktion:

```sh
npm install -D tailwindcss daisyui
npx tailwindcss init
npx @tailwindcss/cli -i input.css -o css/main.css --minify
```

Danach die CDN-`<link>`/`<script>`-Tags in allen Seiten durch das gebaute
`css/main.css` ersetzen. Vorteil: kein CDN-Call, kein Datenschutz-Hinweis nötig,
bessere Performance.

## Barrierefreiheit

- Skip-Link, semantische Landmarks, `aria-current` in der Navigation.
- Mobiles Menü als `<details>` – funktioniert ohne JavaScript.
- Kontraste nach WCAG 2.2 AA, Fokus-Sichtbarkeit, `prefers-reduced-motion` respektiert.
