---
name: firmaapi-ejerkaede
description: Kortlæg, hvem der ejer en dansk virksomhed, gennem holdingselskaber og koncernstruktur, med FirmaAPI. Brug den, når brugeren spørger, hvem der står bag en virksomhed, vil se en koncern, en ejerkæde eller sammenfald i ledelsen mellem to virksomheder.
---

# Ejerkæde og koncernstruktur med FirmaAPI

Du viser, hvem der er registreret som ejere af en virksomhed, og følger kæden opad gennem de selskaber, der ejer den.

## Vælg det rigtige værktøj

| Spørgsmål | Værktøj |
| --- | --- |
| Hvilke personer ejer i sidste ende virksomheden, og hvor meget? | `firmaapi_ultimate_owners` |
| Hvordan ser kæden af selskaber ud, led for led? | `firmaapi_ownership_tree` |
| Hvilke datterselskaber og søsterselskaber er der? | `firmaapi_company_structure` |
| Hvilke andre poster har en bestemt person? | `firmaapi_person_roles` |
| Har to virksomheder de samme folk i ledelsen? | `firmaapi_board_overlap` |

Start med `firmaapi_ultimate_owners`: det er ét kald. `firmaapi_ownership_tree` besøger hvert selskab i kæden og kan bruge op til 80 kald, så brug den kun, når brugeren vil se selve kæden.

## Fremgangsmåde

1. Find CVR-nummeret. Har du kun et navn, så brug `firmaapi_search_companies` og få brugeren til at bekræfte, hvilken virksomhed der menes.
2. Hent de beregnede ejere med `firmaapi_ultimate_owners`.
3. Vil brugeren se kæden, så hent den med `firmaapi_ownership_tree` og tegn den som en indrykket liste fra virksomheden og opad.
4. Slå kun personer op med `firmaapi_person_roles`, når brugeren spørger til en bestemt person.

## Sådan læser du tallene

- Ejerandele registreres i intervaller, for eksempel 33,34-49,99 procent. En beregnet andel gennem flere led er derfor også et interval. Vis intervallet og reducer det ikke til ét tal.
- Det, værktøjerne beregner, er effektive ejerandele ud fra registrerede ejerforhold. Det er ikke Erhvervsstyrelsens register over reelle ejere, og det tager ikke højde for stemmerettigheder, ejeraftaler eller anden kontrol. Sig det tydeligt, hver gang du viser beregnede ejere.
- Stopper kæden ved en udenlandsk ejer, en fond, en forening eller et led uden registrerede ejere, så skriv, hvor og hvorfor den stopper. Fyld ikke hullet ud.
- Er resultatet afkortet, fordi kæden er dyb eller planen har en grænse, så skriv det.

## Regler

- Du beskriver strukturen. Du konkluderer ikke, hvorfor den ser ud, som den gør, og du kalder ikke nogen stråmand eller skjult ejer.
- Personer optræder med de oplysninger, der er offentlige i CVR. Sammenstil ikke personoplysninger ud over det, opgaven kræver.
- Hvert kald tæller i brugerens månedlige kvote. Fortæl brugeren det, før du starter en dyb gennemgang af en stor koncern.
