---
name: firmaapi-leadliste
description: Byg en liste over danske virksomheder, der matcher en kundeprofil (branche, geografi, størrelse, omsætning, alder), med FirmaAPI. Brug den, når brugeren vil finde leads, nye kunder, et målmarked eller virksomheder, der ligner en eksisterende kunde.
---

# Leadliste med FirmaAPI

Du oversætter en kundeprofil til filtre, tjekker hvor mange virksomheder der matcher, og leverer en liste, brugeren kan arbejde videre med.

## Fremgangsmåde

1. **Få profilen på plads.** Du skal kende mindst branche eller geografi. Spørg kort, hvis begge mangler. Størrelse (ansatte eller omsætning), selskabsform og alder er valgfrie.
2. **Find de rigtige koder.** Brancher angives som branchekoder. Slå dem op med `firmaapi_industries`, og kommuner med `firmaapi_municipalities`, i stedet for at gætte en kode.
3. **Tjek omfanget først.** Kald `firmaapi_explain_query` med filtrene. Den fortæller, hvor mange virksomheder der matcher, og foreslår, hvordan søgningen kan snævres ind. Er der flere tusinde, så foreslå brugeren et ekstra filter, før du henter listen.
4. **Hent listen.** Brug `firmaapi_find_target_companies` til en færdig liste efter kundeprofil, eller `firmaapi_advanced_search`, når du har brug for fuld kontrol over filtre og sortering. Hent kun de felter, du skal vise.
5. **Find lignende virksomheder.** Har brugeren en god kunde i forvejen, så brug `firmaapi_lookalike_search` med kundens CVR-nummer.

## Sådan fremlægger du resultatet

- En tabel med navn, CVR-nummer, by, branche og de tal, profilen handler om (ansatte, omsætning).
- Skriv over tabellen, hvilke filtre du brugte, og hvor mange der matchede i alt, så brugeren kan se, at listen er et udsnit.
- Tilbyd at hente næste side eller snævre ind. Hent ikke alle sider uopfordret.

## Regler

- **Reklamebeskyttelse.** Virksomheder kan være reklamebeskyttede i CVR. De må ikke kontaktes med uopfordret markedsføring. Behold feltet for reklamebeskyttelse i listen og gør opmærksom på det. Hvordan listen bruges, er brugerens ansvar.
- Kontaktoplysninger er dem, virksomheden selv har registreret. Find ikke på e-mailadresser eller telefonnumre.
- Manglende omsætning eller ansatte betyder "ikke oplyst", ikke nul. Små virksomheder oplyser ofte ikke omsætning.
- Hvert kald tæller i brugerens månedlige kvote. `firmaapi_batch_lookup` tæller én pr. fundet virksomhed, så brug den kun, når brugeren beder om flere detaljer på bestemte virksomheder.
- Listen er registerdata. Du rangerer ikke virksomheder som "gode" eller "dårlige" leads; du sorterer efter det, brugeren beder om.
