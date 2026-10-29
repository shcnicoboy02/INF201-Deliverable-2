# GenAI-logg – Task 1 (Deliverable 2, INF201)

**Verktøy:** Claude (Anthropic) i Cowork-appen, brukt som sparringspartner. Den fikk beskjed om å veilede med spørsmål og små eksempler, ikke å gi ferdige løsninger.
**Dato:** 28.–29. oktober 2026

## 1. Oppsett før Task 1
- Claude leste oppgaveteksten, notebooken og datageneratoren, og kjørte generatoren for å sjekke dataene. Funn:
  - `BASE_DIR` i generatoren pekte til veilederens Windows-sti. Jeg endret den til `Path("data")`.
  - Generatoren bruker ingen seed og lager nye data hver gang den kjøres. Vi genererte derfor data én gang og la `data/` i git, så begge i gruppa jobber med de samme dataene.
  - Alle loggfilene er ren ASCII, også de som lagres som ISO-8859-1.
- Hjelp med oppsett i VS Code: klone GitHub-repoet, lage nytt venv (Python 3.14), `.gitignore` for `.venv/`, `requirements.txt` med `pip freeze`, velge kernel, commit og push.

## 2. Task 1 del 1 – fil-leser
**Problem:** Hvordan lese en fil uten å vite encodingen på forhånd?

**Hvordan AI hjalp:**
- Forklarte forskjellen på modul (`pathlib`), klasse (`Path`) og metode (`read_text()`), og at encoding er en parameter til metoden.
- Ga et lite eksperiment: `"Café"` kodet med UTF-8 og Latin-1, og så dekodet med feil regel, for å vise hva som skjer.
- Forklarte `try`/`except` med et eksempel som ikke var fra oppgaven.
- Skrev `try`-delen (plan A, UTF-8) som eksempel. Jeg skrev `except`-delen (plan B, Latin-1) selv ut fra et skjelett med tomme felt, og rettet innrykket.

**Hva jeg lærte:**
- UTF-8 må prøves først. Latin-1 klarer å dekode alle bytes og gir aldri feil. Prøves Latin-1 først, blir UTF-8-filer lest feil uten noen feilmelding.
- `except` tar en feiltype (`UnicodeDecodeError`), ikke en encoding.
- Innrykket bestemmer hvilken blokk en linje hører til (`try` og `except` på samme nivå).

**Testing:** De ekte loggfilene er ren ASCII og leses derfor alltid som UTF-8, så dataene tester aldri plan B. AI foreslo en egen testfil med `"Café"` lagret som Latin-1. Resultat: `('Café', 'latin-1')`, altså virker plan B.

## 3. Task 1 del 2 – log-parser (pågår)
- AI ga en oversikt over regex-tegn (`\d`, `\d{4}`, `\[`, grupper med `( )`) og et eksempel på en annen tekst enn oppgavens.
- Jeg bygger mønsteret bit for bit og tester etter hver bit. AI ga en mal med tomme felt der det første feltet var fylt inn, og jeg fylte inn resten. Første del (tidspunktet) fungerer:
  `\[(\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2})\]` → `2026-10-15 08:30:00`

## 4. Refleksjon
- Mest nyttig: forklaringer med små eksempler utenfor oppgaven, og å bygge koden én linje om gangen.
- AI fant problemer jeg ikke hadde lagt merke til selv (Windows-stien, manglende seed, at dataene er ren ASCII).
- All kode er kjørt og testet i notebooken.
