# DMJU – modeljernbaner

Statisk hjemmeside bygget i semantisk HTML5 og almindelig CSS efter Figma-filen
"Mockups", siden "DMJU · Nour".

## Åbn projektet lokalt

Åbn `index.html` i en browser, eller vælg **Open in Browser** for filen i PhpStorm.
Ret indholdet i den relevante HTML-fil og designet i `css/styles.css`.
Der kræves hverken installation, npm, Sass eller JavaScript.

Om DMJU bruger efter aftale en lokal kopi af Bootstraps grid-CSS til bestyrelseskortene.
De øvrige sider bruger almindelig CSS. Ingen sider kræver Bootstrap-JavaScript.
Kør ikke det gamle `npm run sass`, da det overskriver den almindelige CSS-fil.
`mads.html` er den oprindelige tomme skabelon; forsiden ligger i `index.html`.

## Struktur

- `index.html`: header, navigation, forsidens indhold og footer.
- `klubber.html`: klubkort, kluboversigt og vejledning til første klubbesøg.
- `arrangementer.html`: udstilling, toganimation og andre oplevelser.
- `modeltog-for-alle.html`: besøgsinformation, oplevelser og praktiske links.
- `viden.html`: begynderguide og links til skalaer, normer og jernbaneepoker.
- `om-dmju.html`: unionen, medlemskab, bestyrelse og dokumentlinks.
- `aarets-model.html`: årets model 2026 og årskort for 2025, 2024 og 2023.
- `css/styles.css`: lokale skrifttyper, designværdier, fælles elementer og sidernes layout.
- `css/vendor/`: Bootstrap Grid 5.3.8 og MIT-licens; indlæses kun på Om DMJU.
- `assets/images/`: originale billeder eksporteret fra Figma.
- `assets/fonts/`: Inter og Roboto Mono i WOFF2-format samt deres OFL-licenser.

Farver og afstande er samlet øverst i CSS-filen. Menuen har den godkendte ekstra
genvej "Årets model" mellem "Arrangementer" og "Info". Info fører til `viden.html`.
Copyrightteksten er bevaret fra Figma, selvom denne implementering ikke bruger WordPress.

## Mobil, tablet og desktop

Desktoplayoutet fra Figma bevares fra 1200 px. Tilpasningerne er samlet nederst i
CSS-filen og følger den godkendte plan:

- 768–1199 px: 32 px sidemargin, to kort pr. række og tekst/billeder under hinanden.
- Under 768 px: 20 px sidemargin, ét kort pr. række og mindre overskrifter.
- Under 1200 px: headeren følger siden ved scrolling. Menuen står synligt under logoet og kan ombrydes uden JavaScript.
- Sektionerne vokser med indholdet. Billeder beholder deres proportioner.
- Sidefoden har to linkkolonner på tablet og én kolonne på mobil.

## Toganimationen på Arrangementer

Det originale Figma-lag "Tog news - slide" er eksporteret som
`assets/images/tog-vognraekke.png` (2344 × 224 px).

I CSS-afsnittet "Toganimation" gentages billedet vandret langs `.train-track`.
Sporet er én billedbredde bredere end containeren og flyttes mod højre med
`@keyframes`, `translateX()` og konstant hastighed (`linear`).
Det sikrer, at der også er vogne i venstre side, mens andre forlader højre side.
Nulstillingen flytter præcis én gentagelse, så billedmønstret fortsætter uden spring.
Alle vognene i originalbilledet passerer skærmen under hvert gennemløb.

- Ret `--train-duration: 35s` for at ændre hastigheden. Flere sekunder giver langsommere kørsel.
- `--train-height: 170px` følger det godkendte animationsbånd. `--train-width: 1779px` følger originalens proportioner, afrundet til hele pixels for at undgå et lille rasterhop ved gentagelsen.
- `overflow: hidden` begrænser toget til animationsbåndet.
- Ved `prefers-reduced-motion: reduce` står toget stille.
- Båndet har en tilgængelig billedbeskrivelse; de gentagne vogne læses ikke op flere gange.

## Den lille Bootstrap-del på Om DMJU

Søg efter `<!-- Bootstrap: START` i `om-dmju.html` for at finde bestyrelseskortene.
`row` laver en række. `col-12` giver én kolonne på mobil, `col-md-6` giver to fra
768 px, og `col-xl-4` giver tre fra 1200 px. Selve kortenes farver, kanter og
typografi følger Figma via den fælles `styles.css`.

Kun den lokale `css/vendor/bootstrap-grid.min.css` er indlæst på denne side.
Den fulde Bootstrap-CSS og Bootstrap-JavaScript bruges ikke.

## Årets model

Efter aftale er "Se vinderne" og årskortene almindeligt indhold uden links,
klikhandlinger eller tastaturfokus. De oprindelige linkmål i Figma er fravalgt.
Kommentarer i `aarets-model.html` markerer dette. Sidens navigation og brødkrummer
fungerer som på de øvrige sider. Layoutregler genbruges med Viden-siden.

## Kvalitetssikring

Alle syv sider er kontrolleret i Chromium ved 320, 360, 390, 767, 768, 1024,
1199, 1200, 1280, 1440 og 1920 px uden vandret scrolling eller tekstoverløb.
Skærmbilleder af mobil- og tabletvisninger er gennemgået. Desktopmålingerne ved
1440 px er identiske med før de responsive ændringer.

Alle syv HTML-filer validerer uden fejl eller advarsler hos W3C. Lokal
PhpStorm-inspektion finder ingen HTML- eller CSS-fejl; den påpeger kun bevidst
billedskalering og decimaler ved breakpoints. Den afsluttende eksterne
CSS-validering blev afvist af automatisk godkendelseskontrol, fordi filen skulle
sendes til W3C. Den tidligere CSS-validering bestod; den seneste fil er kontrolleret
lokalt og i browseren.

Der er kontrolleret én h1 pr. side, overskriftshierarki, dansk dokumentsprog,
alt-tekster, synligt tastaturfokus og springlink til hovedindholdet. Alle lokale
links og assets er testet under en undermappe som på GitHub Pages.
Tastaturnavigation er gennemgået på alle sider ved 390 og 1440 px. Togets retning,
loop, dækning af animationsbåndet og reduceret bevægelse er kontrolleret ved
360, 1024 og 1440 px.

Kendte forhold:

- Figmas link til Kalundborg Model Jernbane Klub (`https://kmjk.dk/`) kunne ikke DNS-opslås, heller ikke med `www`. Adressen er bevaret og bør kontrolleres før udgivelse.
- Figmas vedtægtslink gav HTTP 404 og er rettet til [DMJU's officielle vedtægter](https://dmju.dk/0-vedtaegter/).
- Besøgsområdet på Modeltog for alle er efter aftale 4 px højere på desktop, så hele besøgsboksen vises. Sidehøjden ved 1440 px er 1882 px i stedet for Figmas 1878 px.

## GitHub Pages

1. Upload projektets filer til dit GitHub-repository med `index.html` i roden.
2. Åbn repositoryets **Settings → Pages**.
3. Vælg **Deploy from a branch**, din udgivelsesbranch og mappen **/(root)**.
4. Gem, og åbn adressen, som GitHub viser, når udgivelsen er færdig.

Alle interne filstier er relative, så siden kan ligge i et GitHub Pages-undermappeprojekt.
Projektet er ikke udgivet automatisk.

## Design og assets

Design: https://www.figma.com/design/N3L0Jcn2ACyI1Yu8A9ScnA/Mockups?node-id=61-317

Logo, Facebook-ikon og udstillingsplakat kommer fra Figma. Skrifttyperne er hentet
fra Google Fonts og ligger lokalt, så siden ikke afhænger af eksterne font- eller billedservere.
