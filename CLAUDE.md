# Bierkaart Biercafé Pallieter

Interactieve bierkaart van Biercafé Pallieter, Groenstraat 23, Prinsenbeek.
Live op https://mchielsen.github.io/bierkaart_pallieter/ via GitHub Pages (branch `main`, map `/`).
Gasten openen de kaart via een geprinte QR-code die naar dat adres wijst.

## Vaste regels

- Antwoord en schrijf altijd in het Nederlands.
- Het adres mag nooit veranderen: niet hernoemen, niet verplaatsen, `index.html` blijft in de hoofdmap. Anders werkt de geprinte QR-code niet meer.
- Wijzigingen gaan direct naar `main`. GitHub Pages zet ze binnen een paar minuten live.
- Geen bestel-, reken- of "lat"-functie toevoegen. De kaart is alleen om te bekijken.
- De letterborden in het café zijn de bron. Prijzen en bieren komen van het bord of van de eigenaar.
- Niets verzinnen. Alcoholpercentage, brouwerij en plaats alleen invullen als het via een bron is te controleren. Is iets niet te vinden, laat het veld leeg (`abv:null`, `br:""`, `pl:null`, `lc:null`, `ll:null`). De kaart toont lege velden dan niet.
- Is een prijs onbekend of twijfelachtig, gebruik `p:null`. De kaart toont dan "aan de bar".
- Geen interne notities in teksten die gasten zien (dus niet "kon ik niet vinden" of "op het bord als ...").

## Hoe de kaart in elkaar zit

Alles staat in één bestand: `index.html`. De bieren staan in de lijst `const B=[ ... ]` in het script. Eén regel per bier:

```
{id:"duvel",n:"Duvel",c:"blond",p:[P(5.5)],abv:8.5,st:"Sterk blond",br:"Duvel Moortgat",pl:"Breendonk",lc:"BE",ll:[51.05,4.33],col:"#f3c24c",g:"tulip",pr:[3,1,3,2,0,0],m:["hop"],note:"..."},
```

| Veld | Betekenis |
| - | - |
| `id` | unieke korte naam, kleine letters, geen spaties |
| `n` | naam zoals gasten hem zien |
| `c` | bord: `tap`, `wissel` (wisselkrat), `donker`, `blond`, `tripel`, `fruit`, `gluten`, `nul` (alcoholvrij) |
| `p` | prijs(zen): `[P(5.5)]`, of met maten `[P(4.5,"33 cl"),P(6.75,"50 cl")]`, of `null` |
| `abv` | alcoholpercentage als getal, of `null` |
| `st` | stijl, bijvoorbeeld `Tripel`, `Weizen`, `Double IPA` |
| `br`, `pl`, `lc` | brouwerij, plaats, land (`NL`, `BE`, `IE`) |
| `ll` | coördinaten van de brouwerij `[breedte, lengte]` voor de afstand, of `null` |
| `col` | kleur van het bier (hex) |
| `foam` | optioneel: kleur van het schuim |
| `cloudy` | optioneel `1` bij troebel bier |
| `g` | glas: `vaas`, `tulip`, `chalice`, `weizen`, `pint`, `tumbler`, `teku`, `flute`, `ballon`, `kwak` |
| `pr` | smaakprofiel 0–5: `[bitter, zoet, vol, fruit, zuur, geroosterd]` |
| `m` | stemmingen: `fris`, `donker`, `fruit`, `hop` |
| `tr` | optioneel `1` bij een erkende trappist |
| `note` | korte beschrijving voor gasten, 1–3 zinnen |

Snacks staan in `const SNACKS=[ ... ]` (`n` naam, `q` aantal, `v` prijs).

## Backups en terugzetten

- Elke wijziging blijft bewaard in de geschiedenis van `main`. Gebruik nooit `git push --force` op `main` en herschrijf de geschiedenis niet.
- Elke nacht maakt de GitHub Action `Dagelijkse backup` een kopie: de tag `backup-JJJJ-MM-DD` en de branch `backup-gisteren`.
- Terugzetten naar gisteren: `git checkout backup-gisteren -- index.html`, controleren, committen ("Kaart teruggezet naar backup van ...") en pushen naar `main`.
- Terugzetten naar een bepaalde dag: hetzelfde met de tag, bijvoorbeeld `git checkout backup-2026-10-06 -- index.html`.
- Maak bij twijfel over een grote wijziging eerst een extra tag, bijvoorbeeld `voor-wijziging-JJJJ-MM-DD`.

## Na elke wijziging

1. Controleer dat het script nog werkt (bijvoorbeeld `node --check` op de inhoud van de `<script>`).
2. Commit met een duidelijke Nederlandse omschrijving en push naar `main`.
3. Meld wat er is veranderd en dat het binnen een paar minuten live staat.
