# Tillegg til produktbrief: Barneloggen

Detaljer som hører hjemme i PRD og arkitektur, ikke i selve briefen. Kilder: `Barneloggen_prosjektforslag.txt` og `.docs/brainstorming/brainstorm-barneloggen-scope-2026-09-19/brainstorm-intent.md` (fullstendig nivåinndeling, risikotabell og leveranseopplegg).

## Prioritering på brukerens egne ord
- Søvn og måltider er det som brukes daglig og må være best.
- Bleier er nødvendig for at appen skal føles komplett og nyttig for foreldre. Forfatteren hadde sluttet å registrere bleier, men tar det opp igjen for å teste appen, så funksjonen får ekte testing.
- Suksess måles både på hastighet og enhåndsbruk ved registrering og på oversikt over forrige uke.

## Beslutninger og forkastede alternativer fra idédugnaden
- Valgt: kjerne med KI-registrering, bibliotek-basert ukekalender og eget designsystem, fremfor «bredde» (alle typer, dårlig design) eller «trygg minimum» (uten KI, ville droppet kursets hovedtema).
- Kalenderen har en reservetrapp: ukerutenett, så dagsvisning, så gruppert liste. Den mest stabile varianten leveres ved funksjonsstopp.
- Kun tre reelle risikoer: kalenderlayout med overlapp og over midnatt, KI-sikkerhet og at KI-tjenesten er tilgjengelig (oppetid), tidssone- og midnattslogikk.
- Fritekstspørsmål til KI er flyttet til nivå 3 på grunn av sikkerhetsrisiko.

## Konstruksjoner som holder nivå 3 billig
Felles mønster for registreringstyper, `child_id` på alle registreringer, eierskap som senere kan bli delt tilgang, ett felles spørringslag for kalender, historikk og statistikk, KI kun mot en strukturert statistikkpakke med fast skjema, UTC-lagring med én datohjelper.

## Personvern og KI
Ekte data om barnet i test betyr at KI-leverandør og dataminimering må avklares i arkitekturfasen. Demo og ekte data skilles med to kontoer i samme applikasjon (ikke to miljøer), der demokontoen er den eneste Demo-innloggingen kan nå.

## Åpne spørsmål
- Hva vurderes ut fra kursets rubrikk eller forventninger til briefen? (rundt 15 minutter å sjekke)
- Hvordan søvnkvalitet «ikke vurdert» håndteres i statistikk og oppsummeringer.
- (Løst) Engelsk versjon: product_brief.en.md.
