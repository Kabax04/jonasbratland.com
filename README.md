# jonasbratland.com

Personlig nettside skrevet i Markdown og publisert med GitHub Pages.
Alt du pusher til `main` blir automatisk publisert på [jonasbratland.com](https://jonasbratland.com) etter et minutt eller to.

## Hvor ligger hva?

```
_config.yml           Innstillinger: tittel, e-post, slagord osv.
_data/navigation.yml  Menyen øverst på siden
_layouts/default.html Grunnmalen alle sider bygger på (header, meny, footer)
_layouts/post.html    Mal for blogginnlegg (tittel, dato, «tilbake»-lenke)
_layouts/tool.html    Mal for verktøy (tittel, beskrivelse, «tilbake»-lenke)
_includes/post-list.html  Listen over blogginnlegg
_includes/tool-list.html  Listen over verktøy
assets/css/style.css  All styling. Fargene står øverst.

index.md              Forsiden
blogg.md              Oversikt over alle blogginnlegg (lages automatisk)
verktoy.md            Oversikt over verktøy (lages automatisk)
prosjekter.md         Oversikt over prosjekter
om.md                 Om meg + kontakt
wmstjenester.md       Liste over WMS-tjenester
startpage.md          Startsiden min i nettleseren (ikke i menyen)

blog/                 Blogginnlegg, én .md-fil per innlegg
tools/                Verktøy, én .html-fil per verktøy
tromso/               Kartprosjekt eksportert fra QGIS
img/                  Bilder
```

Mapper som starter med `_` er «maskineriet». Til vanlig trenger du bare å endre `.md`-filene.

## Lage en ny side

1. Lag en fil, f.eks. `kart.md`, med dette øverst:

   ```markdown
   ---
   title: Kart
   ---

   # Kart

   Skriv innholdet her i vanlig Markdown.
   ```

2. Siden blir tilgjengelig på `jonasbratland.com/kart.html`.
3. Vil du ha den i menyen? Legg til to linjer i `_data/navigation.yml`:

   ```yaml
   - title: Kart
     url: /kart.html
   ```

## Skrive et nytt blogginnlegg

Lag en ny fil i `blog/`, f.eks. `blog/lasagne.md`:

```markdown
---
title: "Verdens beste lasagne"
date: 2026-11-09
description: "Én setning som vises i listen over innlegg."
---

Selve innlegget skrives her. Tittel og dato legges til automatisk,
så du trenger ikke skrive dem en gang til.
```

`date` må være med (format `ÅÅÅÅ-MM-DD`), ellers havner innlegget feil i listen.
Innlegget dukker automatisk opp på forsiden og under **Blogg**.

## Lenker mellom sider

Du kan lenke til `.md`-filer akkurat som før, og GitHub Pages gjør dem om til riktige lenker:

```markdown
[Les oppskriften](blog/onepotspaghetti.md)
```

## Endre utseendet

- **Farger:** endre variablene øverst i `assets/css/style.css` (`--accent` er den grønne fargen).
- **Tittel, slagord, e-post:** `_config.yml`.
- **Header og footer:** `_layouts/default.html`.

## Lage et nytt verktøy

Et verktøy er én `.html`-fil i `tools/` med HTML, litt CSS og JavaScript.
Øverst står den samme typen `---`-blokk som på vanlige sider:

```html
---
title: Mitt verktøy
description: Én setning som vises i verktøylisten og under tittelen.
---

<div class="dropzone">...</div>
<button class="btn">Kjør</button>

<script>
  // JavaScript her
</script>
```

Menyen, tittelen og «← Alle verktøy» kommer automatisk, og verktøyet dukker opp
på forsiden og under **Verktøy**. Se på de som finnes for eksempler.

Ferdige byggeklosser i `assets/css/style.css`, så verktøyene ser like ut:

| Klasse | Hva |
| --- | --- |
| `btn`, `btn secondary` | Knapp (grønn / omriss) |
| `actions` | Rad med knapper |
| `dropzone` | Felt for å slippe eller velge en fil |
| `form`, `field`, `choices` | Skjema med etikett + felt, radioknapper |
| `result` | Stort, grønt resultat |
| `stats` | Rad med nøkkeltall |
| `note`, `error`, `small` | Infoboks, feilmelding, dempet tekst |
| `table-scroll` | Tabell som kan scrolles |

Har du flyttet en side, kan du legge til `redirect_from: /gammel-adresse.html`
i `---`-blokken, så sendes gamle lenker videre.

## Frittstående HTML-sider

Alt i `tromso/` har ingen `---`-blokk øverst. Da lar GitHub Pages filene være helt i fred,
så de får ikke menyen eller stilen fra resten av siden. Det er med vilje, siden kartet har sin egen design.

## Forhåndsvise på egen PC (valgfritt)

Krever [Ruby](https://rubyinstaller.org/) (velg versjonen «with Devkit»). Første gang:

```bash
bundle install
```

Deretter, hver gang:

```bash
bundle exec jekyll serve
```

Åpne <http://localhost:4000>. Siden oppdateres når du lagrer en fil.
