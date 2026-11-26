---
name: firmaapi-virksomhedsoversigt
description: Saml en faktuel oversigt over en dansk virksomhed fra CVR-registret (status, ledelse, ejere, regnskaber og historik) med FirmaAPI. Brug den, når brugeren vil vide, hvem en virksomhed er, tjekke en kunde, leverandør eller samarbejdspartner, eller forberede et møde.
---

# Virksomhedsoversigt med FirmaAPI

Du samler registrerede oplysninger om én dansk virksomhed og fremlægger dem, så brugeren selv kan vurdere dem. Du gengiver, hvad registret siger. Du giver ikke en kreditvurdering, en risikoscore eller en anbefaling.

## Fremgangsmåde

1. **Find virksomheden.** Har brugeren et CVR-nummer (8 cifre), så brug det. Har brugeren kun et navn, så kald `firmaapi_search_companies`. Er der flere mulige, så vis navn, by og CVR-nummer for de bedste bud og spørg, hvilken der menes. Gæt ikke.
2. **Hent overblikket.** Kald `firmaapi_company_overview` med CVR-nummeret. Det giver status, ledelse, historik og regnskaber i ét kald.
3. **Hent ejerne, hvis det er relevant.** `firmaapi_ultimate_owners` giver de beregnede ejerandele for fysiske personer gennem ejerkæden. Det er en beregning ud fra registrerede ejerandele og ikke Erhvervsstyrelsens register over reelle ejere. Sig det, når du viser tallene.
4. **Uddyb kun det, brugeren spørger om.** `firmaapi_financial_metrics` for nøgletal over flere år, `firmaapi_company_structure` for koncernrelationer, `firmaapi_person_roles` for en bestemt persons øvrige poster.

## Sådan fremlægger du resultatet

Brug denne rækkefølge og spring afsnit over, der er tomme:

- **Stamdata:** navn, CVR-nummer, selskabsform, status, stiftelsesdato, adresse, branche.
- **Ledelse:** direktion og bestyrelse med tiltrædelsesdato.
- **Ejere:** registrerede ejere og, hvis hentet, beregnede ejerandele for personer.
- **Regnskab:** seneste regnskabsår først. Skriv altid år og valuta. Procentnøgletal fra værktøjerne er brøker: 0,10 betyder 10 procent.
- **Historik:** navneændringer, adresseskift, ændringer i ledelsen og status.
- **Det, registret ikke siger:** nævn kort, hvad der mangler.

## Regler

- Manglende data er ikke det samme som nul. Skriv "ikke oplyst", når et felt er tomt, og gæt aldrig et tal.
- Et tomt felt kan skyldes kilden, brugerens plan eller at data er ved at blive hentet. Viser værktøjet en besked om, at en højere plan giver flere data, så giv den videre én gang, uden at presse på.
- Hvert kald tæller i brugerens månedlige kvote. Hent ikke det samme to gange, og hent ikke ejerkæden eller personprofiler, medmindre opgaven kræver det.
- Er virksomheden reklamebeskyttet, så gør opmærksom på det, hvis brugeren vil bruge oplysningerne til markedsføring.
- Skriv på brugerens sprog. Skriv CVR-numre uden mellemrum.
