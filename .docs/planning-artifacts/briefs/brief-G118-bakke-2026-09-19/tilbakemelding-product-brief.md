# Tilbakemelding på product brief

| | |
|---|---|
| **Gruppe** | G118 – G118-bakke |
| **Product brief** | `.docs/planning-artifacts/briefs/brief-G118-bakke-2026-09-19/product_brief.md` (commit 28396d0), lest sammen med `addendum.md`. Den engelske oversettelsen `product_brief.en.md` er ikke vurdert separat. |
| **Tilbakemelding fra** | Faglærer i IBE160 (utarbeidet med KI-støtte) |
| **Dato** | 2026-10-06 |

## Samlet vurdering

- **Godt utgangspunkt.** Gruppen kan gå videre som planlagt.

**Det som er bra:**

1. Barneloggen har en tydelig primærbruker med et ekte behov (forelder til et barn på ni måneder, ofte med én hånd og lite tid), og omfanget er delt i tre nivåer der nivå 1 er konkret og avgrenset. Det gir både en realistisk kjerne og en tydelig plan for hva som kommer hvis tiden strekker til.
2. KI-funksjonen er gjennomtenkt og trygg: KI fyller bare ut et utkast i et fast skjema som brukeren bekrefter, finner ikke på mengder, og gir aldri medisinske råd. Suksesskriteriene er testbare («overlappende søvn avvises i alle testtilfeller, også over midnatt», «8 av 10 testsetninger»), og personvernet er tenkt gjennom med adskilt demokonto og dataminimering mot KI-leverandøren.

**De viktigste endringene:**

1. Velg KI-leverandør og beskriv hvordan sensor kan kjøre appen uten din nøkkel, f.eks. med en mock-modus for KI-utkast. Demokontoen er et godt grep; sørg for at den også virker lokalt.
2. Briefen nevner en «publisert versjon». Sensor skal kunne kjøre appen lokalt etter README; sørg for at lokal kjøring er hovedsporet, og at publisering er et tillegg.
3. Kriteriet «designet er ryddig og behagelig» kan ikke sjekkes. Gjør det mer konkret, f.eks. med krav til kontrast, trykkflater og at registrering fungerer på 360 px bredde.

## Vanskelighetsgrad og gjennomførbarhet

### Vurdert vanskelighetsgrad

- **Middels**

**Sammenlignbart med:** 6) To-do-liste med smarte etiketter (enkel) i grunnstrukturen – registrering, oversikt og én avgrenset KI-funksjon – men løftet til middels av tidslogikken (søvn over midnatt, overlapp, tidssoner), ukekalenderen, innlogging med adskilte kontoer og kravene til trygg KI.

**Begrunnelse:**

| Faktor | Nivå (lav / middels / høy) | Kommentar |
|---|---|---|
| Domenelogikk – hvor mange og hvor kompliserte regler og beregninger må stemme? | Middels | Overlappende søvn, søvn over midnatt, UTC-lagring og visning, førstegangsmat og enkel statistikk. Få regler, men tidslogikk er en kjent feilkilde. |
| Datamodell – antall entiteter og relasjoner mellom dem | Middels | Bruker, barn, søvn, måltid, matvare (katalog), måltid–matvare og bleieskift. Oversiktlig, og `child_id` fra start er klokt. |
| Brukere, roller og innlogging | Middels | Innlogging med to adskilte kontoer (demo og ekte) og tilgangskontroll på serveren. Én rolle. |
| KI-funksjonalitet i appen, f.eks. kall til språkmodell, prompts i koden og håndtering av usikre svar | Middels | Én avgrenset funksjon: fritekst til strukturert måltidsutkast, med bekreftelse og testsett. KI-oppsummering ligger i nivå 2. |
| Integrasjoner og eksterne tjenester, f.eks. API-er, betaling og e-post | Middels | Språkmodell-API. Ingen betaling eller e-post. Leverandør ikke valgt ennå. |
| Sanntid, samtidighet eller flere brukere som påvirker hverandre | Lav | Én bruker per konto i nivå 1. Delt tilgang er riktig nok utsatt til nivå 3. |
| Filhåndtering, f.eks. opplasting, PDF-lesing og eksport | Lav | Ingen filhåndtering i nivå 1. Dataeksport er utsatt. |
| Sikkerhet og personvern | Middels | Opplysninger om et ekte barn. Godt håndtert i briefen med fiktive data i repo, adskilte kontoer og minimal deling med KI-leverandøren. |

**Hva vanskelighetsgraden betyr for dere:**

- _Middels:_ Et godt balansert valg. Pass på at kjerneflyten blir ferdig og stabil før dere legger til mer. Nivåinndelingen din gjør akkurat dette, og «reservetrappen» for kalenderen (ukerutenett → dagsvisning → liste) er et godt eksempel på risikostyring.

### Gjennomførbarhet med BMAD og Claude Code

Dere skal planlegge med BMAD (product brief → PRD → arkitektur → epics og stories) og implementere med Claude Code. Vurderingen under tar hensyn til at det må være tid til hele denne flyten, og til testing, retting og README til slutt.

| Spørsmål | Vurdering (OK / risiko / stor risiko) | Kommentar |
|---|---|---|
| **Tid og omfang** – kan v1 realistisk bli ferdig og stabil i løpet av semesteret, med tid til flere iterasjoner? | OK | Nivå 1 er realistisk for én person. Funksjonsstopp rundt 1. november gir tid til testing og README. Nivå 1 er likevel ganske bredt (tre registreringstyper, kalender, dashboard, historikk, statistikk, KI og designsystem); hold fast på prioriteringen. |
| **BMAD-flyten** – er briefen konkret nok til at PRD, arkitektur og stories kan lages uten store hull, og blir det overkommelig mange stories? | OK | Svært konkret, med idédugnad, beslutninger og forkastede alternativer dokumentert. Et godt grunnlag for PRD og stories. |
| **Egnet for Claude Code** – bruker løsningen en vanlig, godt dokumentert teknologistakk som Claude Code håndterer godt, eller krever den nisjeteknologi, spesialmaskinvare eller mye manuell konfigurasjon? | OK | En responsiv webapp med CRUD, kalenderbibliotek og ett LLM-kall passer Claude Code godt. |
| **Kontroll på KI-ens arbeid** – kan gruppen selv avgjøre om koden gjør det riktige? Krever domenet kunnskap gruppen ikke har, f.eks. avanserte beregninger eller fagregler, så er det vanskelig å kvalitetssikre. | OK | Du kjenner domenet og bruker appen daglig, og kan dermed raskt se om registreringer og oversikter stemmer. |
| **Testbarhet** – finnes det tydelige regler og forventede resultater som tester kan skrives mot? | OK | Tydelige regler (overlapp, midnatt) og faste testsett for KI-utkast og «er dette normalt?»-spørsmål. Svært godt utgangspunkt. |
| **Kjørbar for sensor** – kan appen kjøres lokalt etter README, uten gruppens nøkler, betalte kontoer eller egen infrastruktur? | Risiko | Demo-innlogging er bra, men KI-delen krever nøkkel, og hosting er ikke avklart. Planlegg lokal kjøring med `.env.example` og mock-modus for KI. |
| **Avhengigheter og kostnader** – krever løsningen betalte API-er, f.eks. språkmodeller, og finnes det en plan for kostnad, testmodus eller mock-data? | Risiko | KI-leverandør er et åpent spørsmål. Velg leverandør tidlig ut fra vilkår og kostnad, og bruk mock-svar i automatiske tester. |

**Konklusjon om gjennomførbarhet:**

- **Gjennomførbart som beskrevet.**

**Forslag til justering av omfang eller vanskelighetsgrad:**

1. Legg inn en mock-modus for KI-utkastet som et eget punkt i nivå 1, slik at både tester og sensor kan kjøre hele kjerneflyten uten nøkkel.
2. Hvis nivå 1 blir ferdig tidlig, er KI-oppsummering av søvn (første punkt i nivå 2) en god utvidelse som løfter KI-delen uten å åpne for frie spørsmål.

## Hvorfor product brief er viktig for mappen

Product brief er utgangspunktet for PRD, arkitektur, stories og til slutt koden. Del 1 av mappen vurderes blant annet på om sensor kan følge en sporbar vei fra plan til ferdig app. Den vurderes også på om appen gjør det dere har beskrevet, om den er testet, om den er godt designet, og om den kan kjøres etter README. Et uklart, for stort eller for lite brief gjør alt dette vanskeligere senere. Det er mye enklere å rette nå enn sent i semesteret.

## 1. Gjennomgang av briefens deler

| Del av brief | Status | Kommentar |
|---|---|---|
| Executive Summary – er det klart hva appen er, og hvilket problem den løser? | OK | Klart og konsist: rask registrering av søvn, måltider og bleier, ukekalender og KI som hjelper uten å gi råd. |
| The Problem – er problemet konkret, med reelle situasjoner og brukere? | OK | Konkret, med overgangen til fast føde som en god, spesifikk situasjon. |
| The Solution – beskriver løsningen brukeropplevelsen, ikke bare teknologi? | OK | Beskriver hva brukeren gjør og ser, med et godt eksempel på KI-registrering. |
| What Makes This Different – er vurderingen ærlig og realistisk? | Juster | Ærlig om at det ikke finnes noen teknisk vollgrav. Nevn gjerne et par eksisterende babylogg-apper og hva Barneloggen gjør annerledes enn dem. |
| Who This Serves – er primærbrukerne tydelige, og vet vi hva de trenger? | OK | Svært tydelig primærbruker med konkrete behov (én hånd, lite tid, mønstre over uker). |
| Success Criteria – kan kriteriene faktisk sjekkes eller testes? | Juster | De fleste er gode og testbare. «Designet er ryddig og behagelig» bør gjøres sjekkbart, og «publisert versjon» bør suppleres med «kjører lokalt etter README». |
| Scope – er det klart hva som er med i første versjon, og hva som ikke er det? | OK | Tydelige nivåer med prioritert rekkefølge og en klar grense mot medisinske vurderinger. |
| Vision – henger visjonen sammen med resten uten å blåse opp omfanget? | OK | Realistisk og tydelig holdt utenfor prosjektet, med bevissthet om regelverk før lansering. |

## 2. Utgangspunkt for del 1 av mappen

Punktene følger kriteriene i sensorveiledningen for del 1. Vektene i parentes viser hvor mye hvert kriterium teller i del 1.

| Kriterium i del 1 | Hva briefen bør legge til rette for | Status | Kommentar |
|---|---|---|---|
| **1. Prosess og KI-styring** (30 %) | Brief som er presis nok til at PRD og stories kan bygges direkte på den, slik at krav kan spores fra brief til kode. | OK | Idédugnad, brief og addendum med beslutninger og forkastede alternativer gir god sporbarhet. Fortsett med små commits og lagrede KI-økter gjennom PRD og implementering. |
| **2. Funksjonalitet og omfang** (20 %) | Realistisk omfang for gruppen og semesteret: en tydelig kjerneflyt som kan bli ferdig og stabil, og nok innhold til å vise reell funksjonalitet. | OK | Nivå 1 gir nok reell funksjonalitet og er realistisk. |
| **3. Kvalitetssikring og testing** (15 %) | Suksesskriterier og funksjoner som er konkrete nok til å bli testtilfeller. | OK | Konkrete testtilfeller for tidslogikk og KI-sikkerhet er allerede beskrevet. |
| **4. Design og brukeropplevelse** (10 %) | Tydelige brukere og brukssituasjoner som designet kan bygges rundt, gjerne med de viktigste skjermbildene eller flytene skissert. | OK | Enhåndsbruk på mobil og eget designsystem gir tydelig retning. Gjør designkriteriet sjekkbart og ta med grunnleggende universell utforming. |
| **5. Kodekvalitet og arkitektur** (10 %) | Teknologivalg som er begrunnet og ikke mer komplekse enn appen trenger. | OK | Teknologi er riktig nok utsatt til arkitekturen, og addendumet har gode prinsipper (felles mønster for registreringer, ett spørringslag, UTC). |
| **6. README og kjørbarhet** (10 %) | Løsning som andre kan kjøre lokalt uten betalte kontoer, og uten tilgang til gruppens egne tjenester og nøkler. | Juster | Demo-innlogging er bra. Legg til plan for lokal kjøring, `.env.example` og mock-modus for KI. |
| **7. Ryddighet i repoet** (5 %) | En plan for hvor hemmeligheter, testdata og dokumentasjon skal ligge. | OK | Ekte data holdes utenfor kode og seed-data, og API-nøkler eksponeres ikke. Planleggingsdokumentene ligger ryddig i `.docs/`. |

## 3. Neste steg for gruppen

1. Velg KI-leverandør, og beskriv mock-modus og lokal kjøring for sensor.
2. Gjør designkriteriet sjekkbart, og legg til «kjører lokalt etter README» som suksesskriterium.
3. Gå videre til PRD med nivå 1 som grunnlag for epics og stories.

Oppdater product brief i repoet når dere har gjort endringene, slik at historikken viser hvordan planen utviklet seg. Det er en del av prosessen sensor ser etter.
