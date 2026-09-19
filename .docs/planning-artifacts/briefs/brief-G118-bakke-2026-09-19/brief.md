---
title: "Produktbrief: Barneloggen"
status: final
created: 2026-09-19
updated: 2026-09-19
language: nb
---

# Produktbrief: Barneloggen

## Sammendrag

Barneloggen er en responsiv webapplikasjon der foreldre raskt registrerer barnets søvn, måltider og bleieskift, ser dem samlet i en ukekalender og får hjelp av KI til å registrere og oppsummere. KI gir aldri medisinske råd. Prosjektet er et soloprosjekt i IBE160 (Programmering med KI), utvikles med KI som kodeassistent og skal være ferdig til midten av november 2026.

Bakgrunnen er personlig. Forfatteren er forelder til et barn på ni måneder og registrerer oftest søvn og måltider. Barneloggen testes daglig på forfatterens eget barn.

Briefen er grunnlag for videre arbeid (PRD, arkitektur, epics). På lengre sikt, utenfor dette prosjektet, er ambisjonen en fullverdig applikasjon for tracking av barns oppvekst og utvikling.

## Problemet

Foreldre til små barn må huske og sammenligne mye: når barnet sov, hvor lenge, hva det har spist og når nye matvarer ble introdusert. Uten et enkelt verktøy blir dette notater og gjetning, og det er vanskelig å se mønstre fra dag til dag og uke til uke.

Ved ni måneder er barnet i overgangen til fast føde, og da blir det viktig å vite hvilke matvarer barnet har fått, hvor ofte og når de først ble introdusert.

## Løsningen

En webapplikasjon for mobil, nettbrett og PC, bygget rundt rask registrering og tydelig oversikt.

- **Registrering:** søvn (med kvalitet og regler mot overlappende søvn, også over midnatt), måltider (med egen matvarekatalog og flere matvarer per måltid) og bleieskift (med farge og konsistens).
- **Oversikt:** ukekalender med sju dager side om side, dashboard, historikk og enkel statistikk.
- **KI som hjelper, ikke rådgiver:** brukeren skriver en setning som «Emma spiste en halv banan og litt havregrøt klokken 10», og KI foreslår strukturerte felter i et utkast som brukeren bekrefter. KI lagrer aldri noe selv og finner ikke på mengder eller matvarer.
- **Ingen medisinske råd:** KI beskriver kun registrerte observasjoner. Begrensningen bygges inn i funksjonsdesign og svarhåndtering, ikke bare i en ansvarsfraskrivelse.

## Hva gjør dette annerledes

Det finnes ingen teknisk vollgrav. Styrken ligger i:

- **Fokus der bruken er:** søvn og måltider får mest kvalitet. Bleier er med for at appen skal være komplett for foreldre flest.
- **Matvarekatalog og førstegangsmat:** man ser hvilke matvarer barnet har fått, hvor ofte og når de først ble registrert.
- **Trygg KI av konstruksjon:** KI fyller kun ut et fast skjema som brukeren bekrefter, uten vei for fritekstsvar som kan gli over i råd.
- **Testet på et ekte barn** i den faktiske hverdagen, ikke bare mot en kravliste.

## Hvem dette er for

**Primær bruker og testbruker:** forfatteren, forelder til et barn på ni måneder, som registrerer flere ganger daglig, ofte med én hånd og lite tid, og vil se mønstre over uker.

**Bredere målgruppe:** foreldre og foresatte med små barn. Datamodellen støtter flere barneprofiler per bruker fra start, mens bytte mellom barn i grensesnittet kommer i nivå 2. Delt tilgang for flere foresatte er en senere utvidelse.

## Omfang

Tre nivåer, uten harde kutt:

- **Nivå 1, kjerne (ferdig og polert):** innlogging (også Demo-innlogging) og barneprofil, søvn, måltider med matvarekatalog, bleier, ukekalender, dashboard, historikk med redigering og sletting, enkel statistikk, KI-assistert måltidsregistrering og eget designsystem.
- **Nivå 2, ønskelig, i prioritert rekkefølge:** vekstregistrering; KI-oppsummering og trendanalyse (først søvn, så per område, så helhetsbilde med uke-mot-uke); KI-registrering for alle typer; KI-forslag for matvarer; bytte mellom barn; matvarekatalog-side; flere grafer; nattmodus, PWA og stemmeinput.
- **Nivå 3, planlagt senere:** pumping, temperatur, medisinlogg, milepæler, notater; flere foresatte; dataeksport; frie spørsmål til KI (krever egen sikkerhetsvurdering); vurdering av regelverk for medisinsk utstyr og personvern før offentlig lansering.

Utenfor omfanget: alt som gir medisinske vurderinger, diagnoser eller doseringsråd.

## Suksesskriterier

**For brukeren (testet på eget barn):**
- Brukeren kan registrere søvn eller et måltid på under 10 sekunder, med én hånd, på mobil.
- Brukeren ser forrige ukes søvn og måltider i ukekalenderen med ett blikk.

**For prosjektet:**
- Nivå 1 er ferdig og polert i en publisert versjon ved funksjonsstopp rundt 1. november, og en demo på ca. tre minutter går feilfritt på fiktive data.
- Overlappende søvn avvises i alle testtilfeller, også over midnatt.
- KI-utkast for måltider er riktige eller trenger høyst én rettelse i minst 8 av 10 testsetninger.
- Et fast testsett («er dette normalt?») gir alltid svar uten vurdering eller råd.
- Designet er ryddig og behagelig, også på mobil.

## Personvern og data

Utvikling og demo bruker fiktive data. Forfatteren bruker i tillegg eget barns faktiske registreringer til testing. Derfor:

- Én applikasjon med to adskilte kontoer: en demokonto fylt med fiktive data (Demo-innlogging) og forfatterens egen konto med ekte data. Tilgangskontroll på serveren holder dem adskilt, og demoinnloggingen gir aldri tilgang til den andre kontoen.
- Ekte data holdes utenfor kildekode og seed-data.
- API-nøkler eksponeres ikke i frontend.
- KI-kall sender kun det som trengs (ikke navn, bilder eller fødselsdato), og leverandørens vilkår for datalagring og trening sjekkes.

## Åpne spørsmål

- Teknologivalg og hosting avklares i arkitekturfasen.
- Valg av KI-leverandør, ut fra vilkår for datalagring og trening.

## Visjon

Hvis prosjektet lykkes, blir Barneloggen grunnlaget for en fullverdig applikasjon for tracking av barns oppvekst og utvikling: alle registreringstyper, delt tilgang, dataeksport og trygge, beskrivende KI-oppsummeringer over tid. Det krever egen vurdering av personvern og regelverk før offentlig lansering og ligger utenfor dette prosjektet.
